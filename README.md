# PromptStudio

PromptStudio は、VFX / CG 制作会社のための **生成AIプロンプト運用基盤** です。

社員ごとの言語力、生成AI経験、画像生成 / 動画生成のモデル知識の差によって、プロンプト品質や再現性がばらつく問題を、会社共通の skill / knowledge / レビュー運用で補正します。

最初のプロダクト像は、Chrome 上で ChatGPT に近い対話UXを持つ拡張機能です。社員は「作りたい画」「動かしたい映像」「守りたい案件条件」を自然に相談し、PromptStudio が会社の共有コンテキストを使って、用途に合うプロンプト、ネガティブプロンプト、生成設定、レビュー用の副産物をまとめます。

裏側では Antigravity 2.0 IDE をローカル実行エンジンとして使い、workspace、skill、knowledge、保存先フォルダーを扱える構成を目指します。

## 目指すこと

- VFX / CG 制作現場で使える、再現性のあるプロンプト作成を支援する
- 画像生成、動画生成、参照画像利用、スタイル統一、案件ルール反映を共通スキル化する
- 生成結果だけでなく、意図、会話、参照知識、生成設定、副産物を保存する
- 管理者が保存物をレビューし、skill と knowledge を改善するPDCAを回す
- 社員は難しいプロンプト設計を意識せず、対話しながら制作意図を具体化できる

## 最初に作るもの

最初のMVPは、以下に絞ります。

1. Chrome拡張のサイドパネルで対話できる
2. skill、knowledge、workspace、成果物保存先を設定できる
3. 画像生成 / 動画生成の目的に応じてプロンプトを組み立てる
4. 会話、生成プロンプト、参照情報、設定、副産物をレビュー可能な形で保存する
5. 保存された実例を管理者が見て、skill 改善に使える

Googleアカウントログイン、権限管理、チーム単位のダッシュボードは重要ですが、MVPでは「誰が作った成果物かを記録できる設計」に留め、後から拡張します。

## リポジトリの読み方

- [docs/00-index.md](docs/00-index.md): ドキュメント入口
- [docs/00-product-brief.md](docs/00-product-brief.md): プロダクトの本質と対象ユーザー
- [docs/01-mvp-scope.md](docs/01-mvp-scope.md): 最初に作る範囲
- [docs/02-architecture-principles.md](docs/02-architecture-principles.md): Chrome拡張、ローカルブリッジ、Antigravity IDE の責務分離
- [docs/03-prompt-skill-pdca.md](docs/03-prompt-skill-pdca.md): skill / knowledge / 保存物 / レビュー改善サイクル
- [docs/04-implementation-roadmap.md](docs/04-implementation-roadmap.md): 実装ロードマップ
- [docs/05-repo-governance.md](docs/05-repo-governance.md): リポジトリ運用ルール
- [docs/06-decision-log.md](docs/06-decision-log.md): 重要な意思決定ログ

## 現時点の設計方針

- Chrome拡張はUXと設定入力に集中する
- 任意フォルダー保存やローカルworkspace操作は、Chrome拡張から直接ではなく、ローカルブリッジ経由にする
- Antigravity 2.0 IDE への依存は抽象化し、将来ほかの実行エンジンにも差し替えられるようにする
- skill は「プロンプトの作法」だけでなく、モデル別制約、制作会社のレビュー観点、案件コンテキストを含める
- 成果物は後からレビューしやすい単位で保存する
