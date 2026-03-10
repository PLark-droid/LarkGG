---
name: miyabi-tmux
description: "Tmux Monitor - tmuxセッション・ウィンドウ・ペインの監視・操作。マルチエージェント実行環境の管理。トリガー: tmux操作、セッション管理、ペイン監視、ウィンドウ管理、マルチエージェント実行"
allowed-tools: mcp__miyabi-mcp-bundle__tmux_list_sessions, mcp__miyabi-mcp-bundle__tmux_list_windows, mcp__miyabi-mcp-bundle__tmux_list_panes, mcp__miyabi-mcp-bundle__tmux_send_keys, mcp__miyabi-mcp-bundle__tmux_pane_capture, mcp__miyabi-mcp-bundle__tmux_pane_search, mcp__miyabi-mcp-bundle__tmux_pane_tail, mcp__miyabi-mcp-bundle__tmux_pane_is_busy, mcp__miyabi-mcp-bundle__tmux_pane_current_command, mcp__miyabi-mcp-bundle__tmux_session_info, Bash(tmux *), Read
---

# Miyabi Tmux Monitor

miyabi-mcp-bundleのTmux Monitor カテゴリ（10ツール）をClaude Codeから活用するスキルです。

## 利用可能なMCPツール

| Tool | 説明 |
|------|------|
| `tmux_list_sessions` | 全tmuxセッション一覧（ウィンドウ数・ステータス付き） |
| `tmux_list_windows` | tmuxセッション内のウィンドウ一覧 |
| `tmux_list_panes` | tmuxウィンドウ内のペイン一覧 |
| `tmux_send_keys` | tmuxペインにキーストローク/テキスト送信 |
| `tmux_pane_capture` | ペインのターミナル出力キャプチャ |
| `tmux_pane_search` | ペイン内容のパターン検索 |
| `tmux_pane_tail` | ペイン出力の末尾N行取得 |
| `tmux_pane_is_busy` | ペインでコマンド実行中か確認 |
| `tmux_pane_current_command` | ペインで現在実行中のコマンド取得 |
| `tmux_session_info` | tmuxセッション詳細情報 |

## 典型的なワークフロー

### マルチエージェント監視
1. `tmux_list_sessions` でアクティブセッション確認
2. `tmux_list_panes` で各ペインの状態確認
3. `tmux_pane_is_busy` で実行状態確認
4. `tmux_pane_capture` / `tmux_pane_tail` で出力確認

### エージェント操作
1. `tmux_send_keys` でコマンド送信
2. `tmux_pane_current_command` で実行コマンド確認
3. `tmux_pane_search` でパターン検索（エラー等）

### エラー発生時のペインログ収集
1. `tmux_pane_search` でエラーパターン検索
2. `tmux_pane_capture` で全出力取得
3. `tmux_pane_tail` で直近の出力確認

## 注意事項

- `tmux_send_keys` は任意コマンド実行が可能な強力な操作です。送信内容を慎重に確認してください
