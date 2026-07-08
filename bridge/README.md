# Local Bridge

Chrome拡張とローカルworkspaceをつなぐ処理を置く場所です。

初期MVPでは、localhost API または Native Messaging host として実装する想定です。

担当するもの。

- workspaceパスの確認
- skill / knowledge の読み取り
- 成果物フォルダーへの保存
- Google Antigravity / Antigravity IDE への実行依頼
- 将来の別実行エンジンへの差し替え境界

長期的には、Chrome拡張専用の橋ではなく、PromptStudio Core を CLI、MCP server、Local API から呼ぶためのローカル境界として整理します。
