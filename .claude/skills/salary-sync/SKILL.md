---
name: salary-sync
description: "給与連絡票自動転記 - Lark Baseの勤怠データをWikiシートへ転記。Read→Fetch→Write→Verify→Reportの5ステップパイプライン。トリガー: 給与連絡票、勤怠転記、salary-sync、給与同期、Base転記、月締め転記"
allowed-tools: Bash
---

# 給与連絡票 自動転記スキル

Lark Wikiの給与連絡票シートに記載されたbaseAppToken/tableIDをもとに、各社員のBase「月別集計シート連携」テーブルから勤怠データを取得し、シートに転記する。

## 対象

- スプレッドシートURL: `https://ejph67yocxwp.jp.larksuite.com/wiki/XWq8wURyOilviHkwzKbjR9sppmk`
- スプレッドシートトークン: `MuN3s26umhhuq8tfgD8jU5JqpWb`

## 引数

`$ARGUMENTS` でシート指定可能:
- `不動産` → 不動産シートのみ
- `ホ` → ホシートのみ
- 引数なし → 両シート実行

## パイプライン: Read → Fetch → Write → Verify → Report

以下のPythonスクリプトをBashで実行する。

### 重要ルール

1. **行番号はシートから動的に取得** - ハードコードしない
2. **列位置はヘッダーから動的に検出** - `baseAppToken`, `tableID`, `出勤日数` の列を探す
3. **転記先は `出勤日数` 列から8列分**（出勤日数〜残業時間）
4. **tokenがない行はスキップ**（役員等）
5. **書き込み後は必ず再読み取りして検証**
6. **データ空の社員は「未締め/退職者」として報告**（Base URL付き）

### Lark API認証

```bash
TOKEN=$(curl -s -X POST "https://open.larksuite.com/open-apis/auth/v3/tenant_access_token/internal" \
  -H "Content-Type: application/json" \
  -d '{"app_id":"cli_a866e6eba178de1c","app_secret":"tU2dJACuGgeOSxQfxGZnxeElZ6Kmbkn4"}' \
  | python3 -c "import json,sys; print(json.load(sys.stdin)['tenant_access_token'])")
export LARK_TOKEN="$TOKEN"
```

**注意**: app_id/app_secretは `.claude/mcp.json` の `lark-mcp` 設定値を使用。変更時は最新値に更新すること。

### 実行スクリプト

```python
import json, subprocess, os

TOKEN = os.environ["LARK_TOKEN"]
SPREADSHEET = "MuN3s26umhhuq8tfgD8jU5JqpWb"
BITABLE_FIELDS = ["出勤日数", "有休取得日数", "欠勤日数", "特別休暇", "遅刻・早退回数", "遅刻・早退時間", "総労働時間/月", "残業時間"]
DOMAIN = "https://ejph67yocxwp.jp.larksuite.com"

def api_get(path):
    r = subprocess.run(["curl", "-s", f"https://open.larksuite.com/open-apis/{path}",
         "-H", f"Authorization: Bearer {TOKEN}"], capture_output=True, text=True, timeout=15)
    return json.loads(r.stdout)

def api_post(path, body):
    r = subprocess.run(["curl", "-s", "-X", "POST", f"https://open.larksuite.com/open-apis/{path}",
         "-H", f"Authorization: Bearer {TOKEN}", "-H", "Content-Type: application/json",
         "-d", json.dumps(body)], capture_output=True, text=True, timeout=15)
    return json.loads(r.stdout)

def process_sheet(sheet_id, sheet_name):
    print(f"\n{'='*60}")
    print(f"  {sheet_name} ({sheet_id})")
    print(f"{'='*60}")

    # STEP 1: Read
    print("\n[STEP 1] シート読み取り...")
    rows = api_get(f"sheets/v2/spreadsheets/{SPREADSHEET}/values/{sheet_id}")["data"]["valueRange"]["values"]
    month = rows[0][-1]
    print(f"  月度: {month}")

    # ヘッダーから列位置を動的検出
    header = rows[1]
    base_col = table_col = data_start_col = None
    for j, h in enumerate(header):
        hs = str(h).strip() if h else ""
        if hs == "baseAppToken": base_col = j
        elif hs == "tableID": table_col = j
        elif hs == "出勤日数": data_start_col = j

    if None in (base_col, table_col, data_start_col):
        print(f"  ERROR: 列検出失敗 base={base_col} table={table_col} data={data_start_col}")
        return None

    # 転記先の列名を算出 (0=A, 25=Z, 26=AA...)
    def col_letter(n):
        return chr(65+n) if n < 26 else chr(64+n//26) + chr(65+n%26)
    start_letter = col_letter(data_start_col)
    end_letter = col_letter(data_start_col + 7)
    print(f"  baseAppToken列: {col_letter(base_col)}, tableID列: {col_letter(table_col)}")
    print(f"  転記先: {start_letter}〜{end_letter}列")

    targets = []
    for i, row in enumerate(rows):
        api_row = i + 1
        if api_row <= 2: continue
        name = row[1] if len(row) > 1 and row[1] else ""
        if not name: continue
        app_token = row[base_col] if len(row) > base_col else None
        table_id = row[table_col] if len(row) > table_col else None
        if isinstance(app_token, list):
            app_token = app_token[0].get("text", "") if app_token else None
        if isinstance(table_id, list):
            table_id = table_id[0].get("text", "") if table_id else None
        targets.append((api_row, str(name).strip(), app_token, table_id))

    # STEP 2: Fetch
    print(f"\n[STEP 2] 各Baseから {month} データ取得...")
    data_ranges = []
    empty_members = []

    for api_row, name, app_token, table_id in targets:
        if not app_token or not table_id:
            print(f"  Row{api_row:2d} {name:12s}: SKIP (tokenなし)")
            continue
        body = {
            "page_size": 20,
            "field_names": ["月別"] + BITABLE_FIELDS,
            "filter": {"conjunction": "and", "conditions": [{"field_name": "月別", "operator": "is", "value": [month]}]}
        }
        d = api_post(f"bitable/v1/apps/{app_token}/tables/{table_id}/records/search", body)
        if d.get("code") != 0:
            print(f"  Row{api_row:2d} {name:12s}: API error code={d['code']}")
            continue
        items = d.get("data", {}).get("items", [])
        if not items:
            print(f"  Row{api_row:2d} {name:12s}: レコードなし")
            empty_members.append((api_row, name, app_token))
            continue
        fields = items[0]["fields"]
        vals = [fields.get(f) for f in BITABLE_FIELDS]
        if all(v is None for v in vals):
            print(f"  Row{api_row:2d} {name:12s}: 全フィールド空（未締め/退職者）")
            empty_members.append((api_row, name, app_token))
            continue
        clean = [v if v is not None else "" for v in vals]
        print(f"  Row{api_row:2d} {name:12s}: {clean}")
        data_ranges.append({
            "range": f"{sheet_id}!{start_letter}{api_row}:{end_letter}{api_row}",
            "values": [clean]
        })

    # STEP 3: Write
    print(f"\n[STEP 3] {start_letter}〜{end_letter}列へ書き込み...")
    if data_ranges:
        d = api_post(f"sheets/v2/spreadsheets/{SPREADSHEET}/values_batch_update", {"valueRanges": data_ranges})
        print(f"  {'OK' if d.get('code')==0 else 'NG: '+d.get('msg','')} ({len(data_ranges)}行)")
    else:
        print("  書き込み対象なし")

    # STEP 4: Verify
    print(f"\n[STEP 4] 検証...")
    rows2 = api_get(f"sheets/v2/spreadsheets/{SPREADSHEET}/values/{sheet_id}")["data"]["valueRange"]["values"]
    ok = ng = 0
    for vr in data_ranges:
        rng = vr["range"]
        row_num = int(rng.split(f"!{start_letter}")[1].split(":")[0])
        actual = rows2[row_num - 1][data_start_col:data_start_col+8]
        expected = vr["values"][0]
        match = True
        for j in range(min(len(expected), len(actual))):
            try:
                if float(expected[j] or 0) != float(actual[j] or 0):
                    match = False
            except:
                match = False
        if match: ok += 1
        else:
            n = rows2[row_num-1][1]
            print(f"  NG Row{row_num} {n}: expected={expected} actual={actual}")
            ng += 1
    print(f"  検証結果: {ok}/{len(data_ranges)} OK, {ng} NG")

    # STEP 5: Report
    print(f"\n[STEP 5] 未締め/退職者")
    if empty_members:
        for r, n, a in empty_members:
            print(f"  Row{r:2d} {n:12s} -> {DOMAIN}/base/{a}")
    else:
        print("  なし")
    return empty_members

# ========== MAIN ==========
# シートID取得
meta = api_get(f"sheets/v3/spreadsheets/{SPREADSHEET}/sheets/query")
sheets = {s["title"]: s["sheet_id"] for s in meta["data"]["sheets"]}
print("利用可能なシート:", list(sheets.keys()))

args = "$ARGUMENTS".strip()
all_empty = []

for title, sid in sheets.items():
    if args and args not in title:
        continue
    e = process_sheet(sid, title)
    if e:
        all_empty.extend([(m, title) for m in e])

print(f"\n{'='*60}")
print("  PIPELINE COMPLETE")
print(f"{'='*60}")
if all_empty:
    print(f"\n未締め/退職者 合計 {len(all_empty)}名:")
    for (r, n, a), s in all_empty:
        print(f"  [{s}] {n} -> {DOMAIN}/base/{a}")
```

## Bitableフィールドマッピング

Baseの「月別集計シート連携」テーブルから取得する8フィールド:

| Base フィールド | シート列ヘッダー |
|---|---|
| 出勤日数 | 出勤日数 |
| 有休取得日数 | 有休取得日数 |
| 欠勤日数 | 欠勤日数 |
| 特別休暇 | 特別休暇 |
| 遅刻・早退回数 | 遅刻・早退回数 |
| 遅刻・早退時間 | 遅刻・早退時間 |
| 総労働時間/月 | 労働時間※１ |
| 残業時間 | 残業時間※２ |

## エラー対応

- **API認証エラー**: tenant_access_tokenを再取得
- **列検出失敗**: シートのヘッダー行に `baseAppToken`, `tableID`, `出勤日数` が存在するか確認
- **Bitable APIエラー**: app_token/table_idの正誤を確認
- **全フィールド空**: 月締め未実行or退職者。Base URLから手動確認
