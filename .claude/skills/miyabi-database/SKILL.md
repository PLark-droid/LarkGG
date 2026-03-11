---
name: miyabi-database
description: "Database Foundation - データベース接続テスト・テーブル一覧・スキーマ確認・クエリ実行・実行計画・ヘルスチェック。トリガー: DB接続、テーブル確認、スキーマ確認、SQLクエリ、SQL実行、テーブル一覧、EXPLAIN、実行計画、データベースヘルスチェック"
allowed-tools: mcp__miyabi-mcp-bundle__db_connect, mcp__miyabi-mcp-bundle__db_tables, mcp__miyabi-mcp-bundle__db_schema, mcp__miyabi-mcp-bundle__db_query, mcp__miyabi-mcp-bundle__db_explain, mcp__miyabi-mcp-bundle__db_health, Read
---

# Miyabi Database Foundation

miyabi-mcp-bundleのDatabase Foundation カテゴリ（6ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `db_connect` | データベース接続テスト |
| `db_tables` | データベース内の全テーブル一覧 |
| `db_schema` | テーブルスキーマ取得 |
| `db_query` | 読み取り専用SELECTクエリ実行 |
| `db_explain` | クエリ実行計画取得 |
| `db_health` | データベースヘルスチェック |

## 典型的なワークフロー

### データベース調査
1. `db_connect` で接続確認
2. `db_tables` でテーブル一覧取得
3. `db_schema` で対象テーブルの構造確認
4. `db_query` でデータ確認

### パフォーマンス調査
1. `db_health` でDB全体のヘルスチェック
2. `db_explain` で遅いクエリの実行計画確認

## 注意事項

- `db_query` は読み取り専用（SELECT）のみ対応
- 接続情報は環境変数（DATABASE_URL等）で設定してください
