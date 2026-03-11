---
name: miyabi-health
description: "System Health Check - miyabi-mcp-bundle全体の包括的ヘルスチェック。全ツールカテゴリの動作状態を一括確認。トリガー: ヘルスチェック、システム診断、動作確認、miyabi状態確認、MCPサーバー動作テスト"
allowed-tools: mcp__miyabi-mcp-bundle__health_check
---

# Miyabi System Health Check

miyabi-mcp-bundleのSystem Health カテゴリ（1ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `health_check` | 包括的なヘルスチェック実行 |

## 使い方

miyabi-mcp-bundle全体の動作状態を確認する際に `health_check` を実行します。

### チェック内容
- 全21カテゴリのツール動作状態
- MCP接続状態
- 環境変数の設定状況
- 依存サービスの可用性

### いつ使うか
- miyabi-mcp-bundleを初めて設定した後の動作確認
- MCPツールが応答しない場合のトラブルシューティング
- 定期的なシステムヘルスチェック
