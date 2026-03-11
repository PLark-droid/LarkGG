---
name: miyabi-git
description: "Git Inspector - Gitリポジトリの状態確認・履歴分析・ブランチ管理。git status, diff, log, blame, stash, worktree, conflicts, contributors等の19ツールを提供。トリガー: git操作、ブランチ確認、差分確認、コミット履歴、コンフリクト検出、stash管理、blame調査、タグ確認、worktree管理"
allowed-tools: mcp__miyabi-mcp-bundle__git_status, mcp__miyabi-mcp-bundle__git_branch_list, mcp__miyabi-mcp-bundle__git_current_branch, mcp__miyabi-mcp-bundle__git_log, mcp__miyabi-mcp-bundle__git_worktree_list, mcp__miyabi-mcp-bundle__git_diff, mcp__miyabi-mcp-bundle__git_staged_diff, mcp__miyabi-mcp-bundle__git_remote_list, mcp__miyabi-mcp-bundle__git_branch_ahead_behind, mcp__miyabi-mcp-bundle__git_file_history, mcp__miyabi-mcp-bundle__git_stash_list, mcp__miyabi-mcp-bundle__git_blame, mcp__miyabi-mcp-bundle__git_show, mcp__miyabi-mcp-bundle__git_tag_list, mcp__miyabi-mcp-bundle__git_contributors, mcp__miyabi-mcp-bundle__git_conflicts, mcp__miyabi-mcp-bundle__git_submodule_status, mcp__miyabi-mcp-bundle__git_lfs_status, mcp__miyabi-mcp-bundle__git_hooks_list, Bash(git *), Read, Grep, Glob
---

# Miyabi Git Inspector

miyabi-mcp-bundleのGit Inspector カテゴリ（19ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `git_status` | ワーキングツリーの状態（変更・ステージ・未追跡ファイル） |
| `git_branch_list` | ローカル・リモートブランチ一覧（トラッキング情報付き） |
| `git_current_branch` | 現在チェックアウト中のブランチ名 |
| `git_log` | コミット履歴（author, date, message） |
| `git_worktree_list` | 全Gitワークツリー一覧（並行開発用） |
| `git_diff` | ステージされていない変更の差分表示 |
| `git_staged_diff` | ステージ済み変更の差分表示 |
| `git_remote_list` | リモート設定一覧（fetch/push URL） |
| `git_branch_ahead_behind` | ブランチのupstreamとの差分コミット数 |
| `git_file_history` | 特定ファイルのコミット履歴 |
| `git_stash_list` | スタッシュ一覧（説明付き） |
| `git_blame` | ファイル各行の最終変更者表示 |
| `git_show` | コミット詳細（diff・メタデータ含む） |
| `git_tag_list` | タグ一覧（関連コミット付き） |
| `git_contributors` | コントリビューター一覧（コミット数順） |
| `git_conflicts` | マージコンフリクトのあるファイル検出 |
| `git_submodule_status` | サブモジュールの状態表示 |
| `git_lfs_status` | Git LFS追跡ファイルの状態 |
| `git_hooks_list` | .git/hooksディレクトリのフック一覧 |

## 典型的なワークフロー

1. **現状把握**: `git_status` → `git_current_branch` → `git_diff`
2. **履歴調査**: `git_log` → `git_file_history` → `git_blame`
3. **ブランチ管理**: `git_branch_list` → `git_branch_ahead_behind`
4. **コンフリクト対応**: `git_conflicts` → `git_diff` → `git_blame`
5. **リリース確認**: `git_tag_list` → `git_contributors`

## 注意事項

- 読み取り専用操作が中心です。書き込み操作（commit, push等）はユーザー確認の上実行してください
- `git_worktree_list` は並行開発時のワークツリー状況確認に使用します
- `git_lfs_status` はLFS利用プロジェクトでのみ有効です
