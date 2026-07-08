# Implementation Roadmap

## Phase 0: リポジトリ整備

- プロダクトの本質をREADMEとdocsにまとめる
- MVP範囲を明確にする
- Chrome拡張、ローカルブリッジ、skill / knowledge の責務を分ける
- 保存形式の初期案を作る

## Phase 1: Chrome拡張の骨格

- Manifest V3 のChrome拡張を作る
- サイドパネルを表示する
- チャット風UIを実装する
- 設定画面を作る
- ローカル設定を保存する

## Phase 2: ローカルブリッジ

- localhost API または Native Messaging host を用意する
- Chrome拡張から設定済み保存先へ書き込めるようにする
- skill / knowledge の読み取りを実装する
- workspaceパスの存在確認を行う

## Phase 3: プロンプト生成フロー

- 画像生成向けの基本skillを作る
- 動画生成向けの基本skillを作る
- モデル別skillレジストリを作る
- GPT Image 2、Nano Banana Pro、Kling 3.0、Seedance 2.0、Runway系などの初期対応候補を定義する
- 意図とモデルに応じて公式ガイドライン由来skillと社内蓄積skillを呼び分ける
- ユーザーの依頼を用途別に整理する
- プロンプト、ネガティブプロンプト、生成設定を出力する
- 参照したskill / knowledgeを記録する

## Phase 4: 保存とレビュー

- 1相談 = 1成果物フォルダーで保存する
- `request.md`、`conversation.md`、`prompt.md`、`prompt.json`、`inputs.md`、`result.md`、`references.md`、`metadata.json`、`review.md` を生成する
- 管理者がレビューしやすい形式に整える
- レビュー結果からskill改善へ戻す手順を作る
- 成功 / 失敗、入力画像 / 入力動画、参照素材、生成結果を蓄積する

## Phase 5: Antigravity 2.0 IDE連携

- Antigravity 2.0 IDE で扱えるworkspace構造を確認する
- 実行エンジン境界を設計する
- Chrome拡張からローカルブリッジ経由で実行依頼できるようにする
- Antigravityに依存しすぎないインターフェースを保つ

## Phase 6: ユーザー識別とチーム運用

- Googleアカウントログインを検討する
- ユーザーIDを成果物に記録する
- 管理者レビュー権限を設計する
- 将来のGoogle Workspace / クラウド同期を検討する

## 優先順位

最優先は、現場スタッフが使える対話体験と、管理者が改善できる保存形式である。

きれいな管理画面、複雑な権限、クラウド同期は、その後でよい。
