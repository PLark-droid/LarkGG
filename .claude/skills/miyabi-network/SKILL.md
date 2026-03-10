---
name: miyabi-network
description: "Network Inspector - ネットワーク診断・接続確認・DNS・SSL・帯域幅監視。15ツールでネットワーク状態を包括的に可視化。トリガー: ネットワーク診断、接続確認、ポート確認、DNS、SSL証明書、WiFi情報、traceroute、帯域幅監視、ルーティング確認、ゲートウェイ確認"
allowed-tools: mcp__miyabi-mcp-bundle__network_interfaces, mcp__miyabi-mcp-bundle__network_connections, mcp__miyabi-mcp-bundle__network_listening_ports, mcp__miyabi-mcp-bundle__network_stats, mcp__miyabi-mcp-bundle__network_gateway, mcp__miyabi-mcp-bundle__network_ping, mcp__miyabi-mcp-bundle__network_bandwidth, mcp__miyabi-mcp-bundle__network_overview, mcp__miyabi-mcp-bundle__network_dns_lookup, mcp__miyabi-mcp-bundle__network_port_check, mcp__miyabi-mcp-bundle__network_public_ip, mcp__miyabi-mcp-bundle__network_wifi_info, mcp__miyabi-mcp-bundle__network_route_table, mcp__miyabi-mcp-bundle__network_ssl_check, mcp__miyabi-mcp-bundle__network_traceroute, Read
---

# Miyabi Network Inspector

miyabi-mcp-bundleのNetwork Inspector カテゴリ（15ツール）をClaude Codeから活用するスキルです。
ネットワーク全体の詳細診断に使用。概要レベルのネットワーク統計は `/miyabi-resource` も参照。

## 利用可能なMCPツール

### 基本情報
| Tool | 説明 |
|------|------|
| `network_interfaces` | ネットワークインターフェース一覧（IPアドレス付き） |
| `network_connections` | アクティブなTCP/UDP接続一覧 |
| `network_listening_ports` | サービスがリッスン中のポート一覧 |
| `network_stats` | ネットワークI/O統計 |
| `network_gateway` | デフォルトゲートウェイIP・インターフェース |
| `network_overview` | ネットワーク全体の概要 |
| `network_public_ip` | パブリックIPアドレス取得 |
| `network_wifi_info` | WiFi接続詳細 |
| `network_route_table` | IPルーティングテーブル |

### 診断ツール
| Tool | 説明 |
|------|------|
| `network_ping` | ホストへのping（接続確認） |
| `network_bandwidth` | 現在のネットワーク帯域幅使用状況 |
| `network_dns_lookup` | ホスト名からIPアドレス解決 |
| `network_port_check` | リモートホストのTCPポート開放確認 |
| `network_ssl_check` | SSL/TLS証明書チェック |
| `network_traceroute` | ホストへのネットワーク経路追跡 |

## 典型的なワークフロー

### 接続障害の診断
1. `network_overview` で全体状況確認
2. `network_ping` で対象ホストへの疎通確認
3. `network_dns_lookup` でDNS解決確認
4. `network_traceroute` で経路調査
5. `network_port_check` でポート開放確認

### サービス公開確認
1. `network_listening_ports` でリッスンポート確認
2. `network_public_ip` で外部IP確認
3. `network_ssl_check` でSSL証明書有効性確認

### パフォーマンス監視
1. `network_bandwidth` で帯域幅使用状況確認
2. `network_stats` でI/O統計確認
3. `network_connections` でアクティブ接続確認
