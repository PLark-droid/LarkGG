---
name: miyabi-log
description: "Log Aggregator - ログファイルの検索・フィルタリング・統計分析。エラー・警告の抽出、パターン検索、ログ統計。トリガー: ログ確認、エラーログ、警告ログ、ログ検索、ログ統計、ログ分析、ログ集約"
allowed-tools: mcp__miyabi-mcp-bundle__log_sources, mcp__miyabi-mcp-bundle__log_get_recent, mcp__miyabi-mcp-bundle__log_search, mcp__miyabi-mcp-bundle__log_get_errors, mcp__miyabi-mcp-bundle__log_get_warnings, mcp__miyabi-mcp-bundle__log_tail, mcp__miyabi-mcp-bundle__log_stats, Read, Grep, Glob
---

# Miyabi Log Aggregator

miyabi-mcp-bundleのLog Aggregator カテゴリ（7ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `log_sources` | 利用可能なログファイル一覧 |
| `log_get_recent` | 最新ログエントリ取得（フィルタリング可） |
| `log_search` | パターンによるログ検索 |
| `log_get_errors` | エラーレベルのログエントリ取得 |
| `log_get_warnings` | 警告レベルのログエントリ取得 |
| `log_tail` | ログファイルの末尾N行取得 |
| `log_stats` | ログファイルの統計情報 |

## 典型的なワークフロー

### エラー調査
1. `log_sources` で利用可能なログ確認
2. `log_get_errors` でエラー一覧取得
3. `log_search` でエラー関連パターン検索
4. `log_tail` で最新ログの文脈確認

### ログ監視
1. `log_stats` でログ全体の統計確認
2. `log_get_warnings` で警告確認
3. `log_get_recent` で最新エントリ確認

### 時間帯絞り込み
1. `log_sources` でログファイル特定
2. `log_search` でタイムスタンプパターンで絞り込み
3. `log_get_errors` でその時間帯のエラー確認
