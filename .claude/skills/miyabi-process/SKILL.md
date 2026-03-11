---
name: miyabi-process
description: "Process Inspector - プロセス監視・分析・管理。プロセス一覧、検索、ツリー表示、リソース使用状況、ファイルディスクリプタ、スレッド情報等14ツール。トリガー: プロセス詳細確認、PID検索、プロセスツリー、プロセスキル、ポート使用プロセス特定、プロセスI/O、スレッド確認"
allowed-tools: mcp__miyabi-mcp-bundle__process_info, mcp__miyabi-mcp-bundle__process_list, mcp__miyabi-mcp-bundle__process_search, mcp__miyabi-mcp-bundle__process_tree, mcp__miyabi-mcp-bundle__process_file_descriptors, mcp__miyabi-mcp-bundle__process_environment, mcp__miyabi-mcp-bundle__process_children, mcp__miyabi-mcp-bundle__process_top, mcp__miyabi-mcp-bundle__process_kill, mcp__miyabi-mcp-bundle__process_ports, mcp__miyabi-mcp-bundle__process_cpu_history, mcp__miyabi-mcp-bundle__process_memory_detail, mcp__miyabi-mcp-bundle__process_threads, mcp__miyabi-mcp-bundle__process_io_stats, Read
---

# Miyabi Process Inspector

miyabi-mcp-bundleのProcess Inspector カテゴリ（14ツール）をClaude Codeから活用するスキルです。
個別プロセスの詳細分析に使用。システム全体のリソース概要は `/miyabi-resource` を参照。

## 利用可能なMCPツール

### プロセス情報
| Tool | 説明 |
|------|------|
| `process_info` | PIDによるプロセス詳細情報 |
| `process_list` | プロセス一覧（CPU/メモリ使用量付き） |
| `process_search` | 名前・コマンドラインによるプロセス検索 |
| `process_tree` | プロセス階層（親子関係）表示 |
| `process_children` | 親PIDの子プロセス一覧 |
| `process_top` | リソース使用量トップNプロセス |

### 詳細分析
| Tool | 説明 |
|------|------|
| `process_file_descriptors` | プロセスのオープンファイル・ソケット一覧 |
| `process_environment` | 実行中プロセスの環境変数取得 |
| `process_ports` | プロセスが使用中のネットワークポート |
| `process_cpu_history` | プロセスのCPU使用率トレンド |
| `process_memory_detail` | メモリ使用量の詳細内訳 |
| `process_threads` | プロセス内スレッド一覧 |
| `process_io_stats` | ディスクI/O統計 |

### プロセス操作
| Tool | 説明 |
|------|------|
| `process_kill` | PIDによるプロセス終了 |

## 典型的なワークフロー

### リソースボトルネック調査
1. `process_top` でCPU/メモリ消費上位プロセス確認
2. `process_info` で問題プロセスの詳細確認
3. `process_cpu_history` でCPU使用率の推移確認
4. `process_memory_detail` でメモリ内訳確認

### ポート競合調査
1. `process_ports` で特定プロセスのポート使用確認
2. `process_search` で名前からプロセス検索
3. `process_file_descriptors` でオープンリソース確認

### ディスクI/Oボトルネック調査
1. `process_top` でリソース消費上位確認
2. `process_io_stats` でI/O統計確認
3. `process_threads` でスレッド状態確認

## 注意事項

- `process_kill` は破壊的操作のため、必ずユーザー確認を取ること
- `process_environment` は機密情報を含む可能性があるため出力に注意
