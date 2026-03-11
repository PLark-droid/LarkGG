---
name: miyabi-github
description: "GitHub Integration - Issue・PR・Actions・Labels・Releases・Reviews管理。21ツールでGitHub操作を完全カバー。トリガー: Issue作成、PR作成、ラベル管理、ワークフロー確認、リリース管理、コードレビュー、CI確認、Actions状態、PRマージ"
allowed-tools: mcp__miyabi-mcp-bundle__github_list_issues, mcp__miyabi-mcp-bundle__github_get_issue, mcp__miyabi-mcp-bundle__github_create_issue, mcp__miyabi-mcp-bundle__github_update_issue, mcp__miyabi-mcp-bundle__github_add_comment, mcp__miyabi-mcp-bundle__github_list_prs, mcp__miyabi-mcp-bundle__github_get_pr, mcp__miyabi-mcp-bundle__github_create_pr, mcp__miyabi-mcp-bundle__github_merge_pr, mcp__miyabi-mcp-bundle__github_list_labels, mcp__miyabi-mcp-bundle__github_add_labels, mcp__miyabi-mcp-bundle__github_list_milestones, mcp__miyabi-mcp-bundle__github_list_workflows, mcp__miyabi-mcp-bundle__github_list_workflow_runs, mcp__miyabi-mcp-bundle__github_repo_info, mcp__miyabi-mcp-bundle__github_list_releases, mcp__miyabi-mcp-bundle__github_list_branches, mcp__miyabi-mcp-bundle__github_compare_commits, mcp__miyabi-mcp-bundle__github_list_pr_reviews, mcp__miyabi-mcp-bundle__github_create_review, mcp__miyabi-mcp-bundle__github_submit_review, Bash(gh *), Read, Grep, Glob
---

# Miyabi GitHub Integration

miyabi-mcp-bundleのGitHub Integration カテゴリ（21ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

### Issue管理
| Tool | 説明 |
|------|------|
| `github_list_issues` | フィルター付きIssue一覧取得 |
| `github_get_issue` | Issue詳細情報取得 |
| `github_create_issue` | 新規Issue作成 |
| `github_update_issue` | Issue更新（タイトル・本文・状態・アサイン） |
| `github_add_comment` | Issue/PRにコメント追加 |

### Pull Request管理
| Tool | 説明 |
|------|------|
| `github_list_prs` | PR一覧取得 |
| `github_get_pr` | PR詳細情報取得 |
| `github_create_pr` | PR作成 |
| `github_merge_pr` | PRマージ |
| `github_list_pr_reviews` | PRレビュー一覧取得 |
| `github_create_review` | PRレビュー作成 |
| `github_submit_review` | 保留中PRレビュー送信 |

### リポジトリ管理
| Tool | 説明 |
|------|------|
| `github_list_labels` | リポジトリラベル一覧 |
| `github_add_labels` | Issue/PRにラベル追加 |
| `github_list_milestones` | マイルストーン一覧 |
| `github_repo_info` | リポジトリメタデータ取得 |
| `github_list_releases` | リリース一覧（タグ・アセット付き） |
| `github_list_branches` | ブランチ一覧（保護状態付き） |
| `github_compare_commits` | ブランチ/コミット比較 |

### GitHub Actions
| Tool | 説明 |
|------|------|
| `github_list_workflows` | ワークフロー一覧 |
| `github_list_workflow_runs` | 最近のワークフロー実行一覧 |

## 典型的なワークフロー

### Issue駆動開発
1. `github_list_issues` で未対応Issue確認
2. `github_get_issue` で詳細把握
3. 実装後 `github_create_pr` でPR作成
4. `github_add_labels` でラベル付与

### コードレビュー
1. `github_list_prs` でレビュー待ちPR確認
2. `github_get_pr` でPR詳細確認
3. `github_list_pr_reviews` で既存レビュー確認
4. `github_create_review` → `github_submit_review` でレビュー実施

### リリース管理
1. `github_list_milestones` でマイルストーン確認
2. `github_compare_commits` で差分把握
3. `github_list_workflow_runs` でCI状態確認

## 注意事項

- `github_merge_pr` は本番ブランチへのマージに注意。必ずユーザー確認の上実行
- `github_create_issue` / `github_create_pr` は外部に公開される操作のため確認推奨
