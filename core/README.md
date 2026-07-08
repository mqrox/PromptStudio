# PromptStudio Core

PromptStudio Core は、Chrome拡張、CLI、MCP server、Local API から共通で呼ばれる中核です。

担当するもの。

- 制作意図の整理
- 対象モデル / 生成サービスの解決
- skill選択
- knowledge参照
- 入力画像 / 入力動画 / 参照素材の記録
- モデル別prompt package生成
- artifact保存形式の生成
- 成功 / 失敗、レビュー結果の取り込み
- skill改善に戻すためのmetadata生成

Core は、特定のUI、IDE、AIモデルに依存しません。
