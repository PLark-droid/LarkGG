---
name: miyabi-k8s
description: "Kubernetes管理 - Pod・Deployment操作、ログ取得、リソース適用・削除。トリガー: Kubernetes操作、Pod確認、デプロイメント管理、kubectl操作、k8sリソース管理、namespace切替、Service確認"
allowed-tools: mcp__miyabi-mcp-bundle__k8s_get_pods, mcp__miyabi-mcp-bundle__k8s_get_deployments, mcp__miyabi-mcp-bundle__k8s_logs, mcp__miyabi-mcp-bundle__k8s_describe, mcp__miyabi-mcp-bundle__k8s_apply, mcp__miyabi-mcp-bundle__k8s_delete, Bash(kubectl *), Read
---

# Miyabi Kubernetes Manager

miyabi-mcp-bundleのKubernetes カテゴリ（6ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `k8s_get_pods` | Pod一覧（ステータス付き） |
| `k8s_get_deployments` | Deployment一覧（レプリカ数付き） |
| `k8s_logs` | Podログ取得 |
| `k8s_describe` | リソースの詳細情報取得（Events含む） |
| `k8s_apply` | Kubernetesマニフェスト適用 |
| `k8s_delete` | Kubernetesリソース削除 |

## 典型的なワークフロー

### 状態確認
1. `k8s_get_deployments` でデプロイメント状況確認
2. `k8s_get_pods` でPod状態確認
3. `k8s_logs` で問題Podのログ確認
4. `k8s_describe` でリソース詳細・Events調査

### デプロイ
1. `k8s_apply` でマニフェスト適用
2. `k8s_get_pods` でPod起動確認
3. `k8s_logs` で起動ログ確認

### ロールバック
1. `k8s_get_deployments` でデプロイメント確認
2. `k8s_describe` で問題のEvents確認
3. `k8s_apply`（旧マニフェスト）でロールバック

## 注意事項

- `k8s_delete` は破壊的操作のため、必ずユーザー確認を取ること
- `k8s_apply` は本番環境への適用時は特に注意
