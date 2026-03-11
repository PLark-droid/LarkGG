---
name: miyabi-generator
description: "Generator Tools - UUID生成・乱数生成・ハッシュ計算・セキュアパスワード生成。トリガー: UUID生成、ランダム値、ハッシュ、パスワード生成"
allowed-tools: mcp__miyabi-mcp-bundle__gen_uuid, mcp__miyabi-mcp-bundle__gen_random, mcp__miyabi-mcp-bundle__gen_hash, mcp__miyabi-mcp-bundle__gen_password
---

# Miyabi Generator Tools

miyabi-mcp-bundleのGenerator Tools カテゴリ（4ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `gen_uuid` | UUID生成 |
| `gen_random` | ランダム整数・浮動小数点数生成 |
| `gen_hash` | 文字列のハッシュ化 |
| `gen_password` | セキュアパスワード生成 |

## 使い方の例

- 「新しいUUIDを生成して」→ `gen_uuid`
- 「1〜100のランダムな数値を5つ」→ `gen_random`
- 「"hello world"のSHA256ハッシュ」→ `gen_hash`
- 「16文字のセキュアなパスワードを生成」→ `gen_password`

### 複合例: APIキー生成
1. `gen_uuid` でベースとなるUUID生成
2. `gen_hash` でUUIDをハッシュ化してAPIキー生成
