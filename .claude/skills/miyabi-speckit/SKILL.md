---
name: miyabi-speckit
description: "Spec-Kit - 仕様駆動開発ツール。プロジェクト初期化、仕様書作成、実装計画生成、タスクリスト・チェックリスト生成、整合性分析。トリガー: 仕様書作成、実装計画、タスク生成、Spec-Kit、仕様駆動開発、チェックリスト、整合性分析"
allowed-tools: mcp__miyabi-mcp-bundle__speckit_init, mcp__miyabi-mcp-bundle__speckit_status, mcp__miyabi-mcp-bundle__speckit_constitution, mcp__miyabi-mcp-bundle__speckit_specify, mcp__miyabi-mcp-bundle__speckit_plan, mcp__miyabi-mcp-bundle__speckit_tasks, mcp__miyabi-mcp-bundle__speckit_checklist, mcp__miyabi-mcp-bundle__speckit_analyze, mcp__miyabi-mcp-bundle__speckit_list_features, Read, Write
---

# Miyabi Spec-Kit

miyabi-mcp-bundleのSpec-Kit カテゴリ（9ツール）をClaude Codeから活用するスキルです。
仕様駆動開発（Spec-Driven Development）を支援します。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `speckit_init` | プロジェクトにSpec-Kitを初期化 |
| `speckit_status` | Spec-Kitプロジェクトの状態取得 |
| `speckit_constitution` | プロジェクト憲法の読み取り・更新 |
| `speckit_specify` | 機能説明から正式な仕様書を作成 |
| `speckit_plan` | 実装計画の生成 |
| `speckit_tasks` | アクション可能なタスクリスト生成 |
| `speckit_checklist` | 実装前チェックリスト作成 |
| `speckit_analyze` | プロジェクトの整合性分析 |
| `speckit_list_features` | 定義済み全機能の一覧 |

## 典型的なワークフロー

### 新機能の仕様策定
1. `speckit_init` でSpec-Kit初期化（初回のみ）
2. `speckit_constitution` でプロジェクト憲法確認
3. `speckit_specify` で機能仕様書作成
4. `speckit_plan` で実装計画生成
5. `speckit_tasks` でタスクリスト生成
6. `speckit_checklist` で実装前チェックリスト作成

### プロジェクト整合性チェック
1. `speckit_status` で全体状態確認
2. `speckit_list_features` で定義済み機能一覧確認
3. `speckit_analyze` で整合性分析実行
