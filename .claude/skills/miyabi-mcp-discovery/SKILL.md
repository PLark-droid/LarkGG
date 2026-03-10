---
name: miyabi-mcp-discovery
description: "MCP Tool Discovery - 利用可能なMCPツールの検索・カテゴリ一覧・ツール詳細情報取得。172+ツールから必要なツールを素早く発見。トリガー: ツール検索、MCPツール一覧、ツール情報、利用可能なツール確認、どのツールを使えばいい"
allowed-tools: mcp__miyabi-mcp-bundle__mcp_search_tools, mcp__miyabi-mcp-bundle__mcp_list_categories, mcp__miyabi-mcp-bundle__mcp_get_tool_info
---

# Miyabi MCP Tool Discovery

miyabi-mcp-bundleのMCP Tool Discovery カテゴリ（3ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `mcp_search_tools` | 名前・説明によるMCPツール検索 |
| `mcp_list_categories` | 全ツールカテゴリ一覧 |
| `mcp_get_tool_info` | ツールの詳細情報取得（パラメータ等） |

## 使い方

### ツールを見つける
1. `mcp_list_categories` で全カテゴリ確認
2. `mcp_search_tools` でキーワード検索（例: "docker", "git", "network"）
3. `mcp_get_tool_info` で特定ツールの詳細（パラメータ等）確認

### 活用シーン
- 「こういうことをしたいんだけど、どのツールを使えばいい？」
- 「dockerに関連するツールは何がある？」
- 「git_blameツールの使い方を教えて」
