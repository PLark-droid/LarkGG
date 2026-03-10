---
name: miyabi-file
description: "File Watcher - ファイル監視・検索・比較・重複検出・チェックサム計算。10ツールでファイルシステムを分析。トリガー: ファイル検索、最近の変更ファイル、ファイル比較、ディレクトリサイズ、重複ファイル検出、ファイルツリー"
allowed-tools: mcp__miyabi-mcp-bundle__file_stats, mcp__miyabi-mcp-bundle__file_recent_changes, mcp__miyabi-mcp-bundle__file_search, mcp__miyabi-mcp-bundle__file_tree, mcp__miyabi-mcp-bundle__file_compare, mcp__miyabi-mcp-bundle__file_changes_since, mcp__miyabi-mcp-bundle__file_read, mcp__miyabi-mcp-bundle__file_checksum, mcp__miyabi-mcp-bundle__file_size_summary, mcp__miyabi-mcp-bundle__file_duplicates, Read, Grep, Glob
---

# Miyabi File Watcher

miyabi-mcp-bundleのFile Watcher カテゴリ（10ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `file_stats` | ファイルメタデータ（サイズ・権限・更新日時） |
| `file_recent_changes` | 最近変更されたファイル検索 |
| `file_search` | globパターンによるファイル検索 |
| `file_tree` | ディレクトリツリー構造生成 |
| `file_compare` | 2ファイルの比較 |
| `file_changes_since` | 指定タイムスタンプ以降に変更されたファイル |
| `file_read` | テキストファイルの安全な読み取り（MCP経由） |
| `file_checksum` | ファイルハッシュ計算 |
| `file_size_summary` | ディレクトリサイズ分析 |
| `file_duplicates` | コンテンツハッシュによる重複ファイル検出 |

## 典型的なワークフロー

### プロジェクト構造把握
1. `file_tree` でディレクトリ構造確認
2. `file_size_summary` でサイズ分布確認
3. `file_search` で特定パターンのファイル検索

### 変更追跡
1. `file_recent_changes` で最近変更されたファイル確認
2. `file_changes_since` で特定時点以降の変更確認
3. `file_compare` で2ファイル間の差分確認

### クリーンアップ
1. `file_duplicates` で重複ファイル検出
2. `file_size_summary` で大きなディレクトリ特定
3. `file_stats` で個別ファイルの詳細確認

## 注意事項

- `file_read`（MCP経由）とClaude Code組み込みの`Read`は別物。MCPツール経由では追加のセキュリティ検証が行われます
