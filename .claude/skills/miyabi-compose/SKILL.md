---
name: miyabi-compose
description: "Docker Compose管理 - Composeサービスの状態確認・起動・停止・ログ取得。トリガー: docker-compose操作、docker compose、サービス管理、Compose起動/停止、Composeログ確認、マルチコンテナ管理"
allowed-tools: mcp__miyabi-mcp-bundle__compose_ps, mcp__miyabi-mcp-bundle__compose_up, mcp__miyabi-mcp-bundle__compose_down, mcp__miyabi-mcp-bundle__compose_logs, Bash(docker compose *), Bash(docker-compose *), Read
---

# Miyabi Docker Compose Manager

miyabi-mcp-bundleのDocker Compose カテゴリ（4ツール）をClaude Codeから活用するスキルです。
Docker Composeで管理されているマルチサービス環境を操作する場合はこのスキルを使用。個別コンテナの操作は `/miyabi-docker` を使用してください。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `compose_ps` | Composeサービスのステータス一覧 |
| `compose_up` | Composeサービスを起動 |
| `compose_down` | Composeサービスを停止 |
| `compose_logs` | Composeサービスの統合ログ取得 |

## 典型的なワークフロー

### 通常運用
1. `compose_ps` で現在のサービス状態確認
2. `compose_up` で全サービス起動
3. `compose_logs` でログ監視
4. `compose_down` で全サービス停止

### デバッグ
1. `compose_ps` でサービス状態確認
2. `compose_logs` で特定サービスのログ確認
3. 問題解決後 `compose_up` で再起動

### サービス再構築
1. `compose_down` で全停止
2. 設定変更後 `compose_up` で再起動
3. `compose_ps` で起動確認

## 注意事項

- `compose_down` はコンテナ・ネットワークを削除します。永続データが失われる可能性があるため確認の上実行してください
