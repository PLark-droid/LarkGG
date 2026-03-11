---
name: miyabi-docker
description: "Docker管理 - コンテナ・イメージの操作・監視・ビルド。ps, images, logs, inspect, stats, exec, start/stop/restart, build の10ツール。トリガー: Docker操作、コンテナ管理、イメージビルド、コンテナログ確認、コンテナリソース監視、コンテナ内コマンド実行"
allowed-tools: mcp__miyabi-mcp-bundle__docker_ps, mcp__miyabi-mcp-bundle__docker_images, mcp__miyabi-mcp-bundle__docker_logs, mcp__miyabi-mcp-bundle__docker_inspect, mcp__miyabi-mcp-bundle__docker_stats, mcp__miyabi-mcp-bundle__docker_exec, mcp__miyabi-mcp-bundle__docker_start, mcp__miyabi-mcp-bundle__docker_stop, mcp__miyabi-mcp-bundle__docker_restart, mcp__miyabi-mcp-bundle__docker_build, Bash(docker *), Read, Grep, Glob
---

# Miyabi Docker Manager

miyabi-mcp-bundleのDocker カテゴリ（10ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `docker_ps` | コンテナ一覧（ステータス・ポート付き） |
| `docker_images` | イメージ一覧（サイズ・タグ付き） |
| `docker_logs` | コンテナログ取得 |
| `docker_inspect` | コンテナ/イメージの詳細JSON設定 |
| `docker_stats` | コンテナのCPU/メモリ使用状況（スナップショット） |
| `docker_exec` | 実行中コンテナ内でコマンド実行 |
| `docker_start` | 停止中コンテナを起動 |
| `docker_stop` | 実行中コンテナを停止 |
| `docker_restart` | コンテナを再起動 |
| `docker_build` | Dockerfileからイメージビルド |

## 典型的なワークフロー

### コンテナ状態確認
1. `docker_ps` で稼働中コンテナ確認
2. `docker_stats` でリソース使用状況確認
3. `docker_logs` で問題のあるコンテナのログ確認

### デバッグ
1. `docker_inspect` でコンテナ設定詳細確認
2. `docker_exec` でコンテナ内に入りコマンド実行
3. `docker_logs` でエラーログ確認

### ビルド・デプロイ
1. `docker_build` でイメージビルド
2. `docker_images` でビルド結果確認
3. `docker_start` / `docker_restart` でコンテナ起動

## 注意事項

- `docker_stop` / `docker_restart` は本番環境では慎重に実行
- `docker_exec` は実行中コンテナでのみ使用可能
- 個別コンテナの操作はこのスキル、Composeサービス全体の操作は `/miyabi-compose` を使用
