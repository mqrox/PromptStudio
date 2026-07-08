# AGENTS.md

このリポジトリは、PromptStudio のプロダクト設計、Chrome拡張、ローカル実行ブリッジ、skill / knowledge 運用を管理する場所です。

## 基本方針

- ユーザー向け・運用向けドキュメントは日本語で書く
- 実装より先に、制作現場で使える責務分離と保存形式を崩さない
- Chrome拡張、PromptStudio Core、ローカルブリッジ、Google Antigravity / Antigravity IDE 連携、CLI、MCP server、skill / knowledge は別レイヤーとして扱う
- 特定のAIモデルやIDEに深く結合しすぎない
- プロンプトだけでなく、意図、参照情報、設定、レビュー結果まで保存対象として扱う
- 管理者用skillは蓄積artifactの分析と改善提案を担当し、共通skillを自動で書き換えない

## 追加するファイルの置き場所

- `docs/`: プロダクト設計、運用、意思決定
- `extension/`: Chrome拡張の実装
- `bridge/`: Chrome拡張とローカルworkspace / IDEをつなぐ処理
- `core/`: PromptStudio Core。skill選択、knowledge参照、prompt package生成、artifact保存形式の中心
- `cli/`: `promptstudio` CLI
- `mcp/`: MCP server とtool定義
- `skills/`: 会社共通のプロンプトskill
- `knowledge/`: 共有コンテキストのサンプルや構造定義
- `examples/`: 保存される成果物の例

## 変更時の注意

- 既存ドキュメントと矛盾する方針を入れる場合は、`docs/06-decision-log.md` に理由を残す
- 新しい機能を足す前に、MVPの範囲に入るかを `docs/01-mvp-scope.md` で確認する
- 保存形式を変える場合は、管理者レビューとskill改善に使えるかを優先して判断する
- 認証、課金API、外部AIサービスは安全なデフォルトを置き、実運用キーはコミットしない
- 管理者用skillを追加する場合は、提案、根拠、影響範囲、承認要否が追える形式にする
