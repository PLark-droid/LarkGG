---
name: miyabi-claude-monitor
description: "Claude Code Monitor - Claude Desktop/Code の設定・MCP接続状態・セッション情報・ログの監視・診断。トリガー: Claude設定確認、MCP接続確認、MCPサーバー状態、Claude Codeログ、セッション情報、Claude Code診断、バックグラウンドシェル確認"
allowed-tools: mcp__miyabi-mcp-bundle__claude_config, mcp__miyabi-mcp-bundle__claude_mcp_status, mcp__miyabi-mcp-bundle__claude_session_info, mcp__miyabi-mcp-bundle__claude_logs, mcp__miyabi-mcp-bundle__claude_log_search, mcp__miyabi-mcp-bundle__claude_log_files, mcp__miyabi-mcp-bundle__claude_background_shells, mcp__miyabi-mcp-bundle__claude_status, Read, Grep, Glob
---

# Miyabi Claude Code Monitor

miyabi-mcp-bundleのClaude Code Monitor カテゴリ（8ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `claude_config` | Claude Desktop設定取得 |
| `claude_mcp_status` | MCPサーバー接続状態チェック |
| `claude_session_info` | Claude Codeセッション詳細 |
| `claude_logs` | 最近のClaude Codeログ取得 |
| `claude_log_search` | Claudeログの特定パターン検索 |
| `claude_log_files` | 全Claude Codeログファイル一覧 |
| `claude_background_shells` | Claude Codeから起動されたバックグラウンドシェル一覧 |
| `claude_status` | Claude完全ステータス取得 |

## 典型的なワークフロー

### 環境診断
1. `claude_status` で全体状態確認
2. `claude_mcp_status` でMCPサーバー接続確認
3. `claude_config` で設定内容確認

### トラブルシューティング
1. `claude_logs` で最新ログ確認
2. `claude_log_search` でエラーパターン検索
3. `claude_background_shells` でバックグラウンドプロセス確認
4. `claude_session_info` でセッション詳細確認

### MCP接続復旧
1. `claude_mcp_status` で接続状態確認
2. `claude_config` で設定の正当性確認
3. `claude_log_search` でMCP関連エラー検索
