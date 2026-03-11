---
name: miyabi-resource
description: "Resource Monitor - CPU・メモリ・ディスク・負荷・バッテリー・温度等のシステムリソース監視。10ツールでシステムヘルスを包括的に監視。トリガー: システムリソース概要、ディスク容量、システム負荷、バッテリー残量、温度確認、スワップ使用量、アップタイム"
allowed-tools: mcp__miyabi-mcp-bundle__resource_cpu, mcp__miyabi-mcp-bundle__resource_memory, mcp__miyabi-mcp-bundle__resource_disk, mcp__miyabi-mcp-bundle__resource_load, mcp__miyabi-mcp-bundle__resource_overview, mcp__miyabi-mcp-bundle__resource_processes, mcp__miyabi-mcp-bundle__resource_uptime, mcp__miyabi-mcp-bundle__resource_network_stats, mcp__miyabi-mcp-bundle__resource_battery, mcp__miyabi-mcp-bundle__resource_temperature, Read
---

# Miyabi Resource Monitor

miyabi-mcp-bundleのResource Monitor カテゴリ（10ツール）をClaude Codeから活用するスキルです。
システム全体のリソース概要に使用。個別プロセスの詳細分析は `/miyabi-process`、ネットワーク詳細診断は `/miyabi-network` を参照。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `resource_cpu` | CPU使用率（パーセンテージ） |
| `resource_memory` | RAM・スワップメモリ使用状況 |
| `resource_disk` | マウントされたファイルシステムのディスク使用量 |
| `resource_load` | システム負荷平均 |
| `resource_overview` | システム全体の包括的な概要 |
| `resource_processes` | CPU/メモリ使用量順のトッププロセス |
| `resource_uptime` | システム稼働時間・起動タイムスタンプ |
| `resource_network_stats` | ネットワークインターフェースのトラフィック統計（概要レベル） |
| `resource_battery` | ノートPCバッテリー状態 |
| `resource_temperature` | CPU・システム温度 |

## 典型的なワークフロー

### システムヘルスチェック
1. `resource_overview` でシステム全体の概要確認
2. `resource_cpu` + `resource_memory` で主要リソース確認
3. `resource_disk` でディスク空き容量確認
4. `resource_temperature` で過熱チェック

### パフォーマンス問題調査
1. `resource_load` でシステム負荷確認
2. `resource_processes` でリソース消費上位プロセス特定
3. `resource_cpu` + `resource_memory` で詳細確認

### 定期ヘルスレポート
1. `resource_uptime` でシステム稼働時間確認
2. `resource_overview` で全体概要取得
3. `resource_battery` でバッテリー状態確認（ノートPC）
