# PromptStudio ドキュメント入口

このドキュメント群は、PromptStudio の本質、MVP、設計原則、運用方法を共有するための入口です。

## まず読む順番

1. [00-product-brief.md](00-product-brief.md)
2. [01-mvp-scope.md](01-mvp-scope.md)
3. [02-architecture-principles.md](02-architecture-principles.md)
4. [03-prompt-skill-pdca.md](03-prompt-skill-pdca.md)
5. [04-implementation-roadmap.md](04-implementation-roadmap.md)
6. [05-repo-governance.md](05-repo-governance.md)
7. [06-decision-log.md](06-decision-log.md)
8. [07-business-pitch.md](07-business-pitch.md)
9. [08-model-skill-registry.md](08-model-skill-registry.md)

## 一文で言うと

PromptStudio は、広告、映像、デザイン、CG / VFX、ゲーム、アニメ、ブランド制作、SNSコンテンツなど、クリエイティブ制作における生成AIプロンプト作成を、個人技から会社の共通知識と改善サイクルへ変えるためのワークベンチです。

## 現時点で重要な判断

- 最初のユーザー体験は Chrome拡張のチャットUI
- ローカルファイル保存とworkspace操作は Chrome拡張単体ではなく、ローカルブリッジ経由
- Antigravity 2.0 IDE は実行エンジン候補として扱い、アプリ全体をIDE専用に固定しない
- 保存物はプロンプト本文だけでなく、意図、会話、参照knowledge、skill、生成設定、レビュー観点まで含める
- 入力画像 / 入力動画、想定モデル、成功 / 失敗理由も保存し、skill改善に戻す
- 管理者レビューをskill改善につなげることがプロダクトの中核
