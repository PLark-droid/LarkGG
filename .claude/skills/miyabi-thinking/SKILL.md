---
name: miyabi-thinking
description: "Sequential Thinking - 段階的推論の記録・分岐・要約。複雑な問題を構造化して思考するためのツール。トリガー: 段階的思考、推論プロセス、問題整理、仮説検証、選択肢比較、設計判断、思考の分岐"
allowed-tools: mcp__miyabi-mcp-bundle__think_step, mcp__miyabi-mcp-bundle__think_branch, mcp__miyabi-mcp-bundle__think_summarize, Read, Write
---

# Miyabi Sequential Thinking

miyabi-mcp-bundleのSequential Thinking カテゴリ（3ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `think_step` | 推論ステップを記録 |
| `think_branch` | 代替思考ブランチを作成 |
| `think_summarize` | 思考セッションを要約 |

## 使い方

複雑な問題を段階的に分解して考える際に使用します。思考結果はファイルに保存して後から参照可能です。

### ワークフロー
1. `think_step` で各推論ステップを記録
2. `think_branch` で「もし〜だったら」の代替案を検討
3. `think_summarize` で思考プロセス全体を要約

### 活用シーン
- アーキテクチャ設計の選択肢比較
- バグの原因特定（仮説→検証の記録）
- 複雑なリファクタリング計画の策定
