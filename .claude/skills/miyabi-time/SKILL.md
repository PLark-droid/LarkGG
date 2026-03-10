---
name: miyabi-time
description: "Time Tools - 現在時刻取得・タイムゾーン変換・日時フォーマット・時間差計算。トリガー: 現在時刻、タイムゾーン変換、日時計算、時差計算、日付フォーマット、日付変換"
allowed-tools: mcp__miyabi-mcp-bundle__time_current, mcp__miyabi-mcp-bundle__time_convert, mcp__miyabi-mcp-bundle__time_format, mcp__miyabi-mcp-bundle__time_diff
---

# Miyabi Time Tools

miyabi-mcp-bundleのTime Tools カテゴリ（4ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `time_current` | 任意のタイムゾーンで現在時刻取得 |
| `time_convert` | タイムゾーン間の時刻変換 |
| `time_format` | カスタムパターンで日時フォーマット |
| `time_diff` | 2つの日時間の差分計算 |

## 使い方の例

- 「東京とニューヨークの現在時刻は？」→ `time_current`
- 「日本時間15:00はロンドン時間で？」→ `time_convert`
- 「2026-01-01から今日までの日数は？」→ `time_diff`
- 「今日の日付をYYYY/MM/DD形式で」→ `time_format`

### 複合例: 国際会議の時間調整
1. `time_current` で各地の現在時刻確認
2. `time_convert` で候補時間を各タイムゾーンに変換
3. `time_format` で参加者向けフォーマットに整形
