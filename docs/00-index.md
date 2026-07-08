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
10. [09-why-antigravity.md](09-why-antigravity.md)
11. [10-agent-hub-mcp-cli.md](10-agent-hub-mcp-cli.md)
12. [11-current-synthesis.md](11-current-synthesis.md)
13. [12-user-raw-notes.md](12-user-raw-notes.md)

## 一文で言うと

PromptStudio は、広告、映像、デザイン、CG / VFX、ゲーム、アニメ、ブランド制作、SNSコンテンツなど、クリエイティブ制作における生成AIプロンプト作成を、個人技から会社の共通知識と改善サイクルへ変えるためのワークベンチです。

目的は、出力を平均化することではありません。各クリエイターの意図や個性を活かすために、AIに渡す前提条件を揃えることが本質です。

## 現時点で重要な判断

- 最初のユーザー体験は Chrome拡張のチャットUI
- 将来的な本体は PromptStudio Core であり、Chrome拡張、CLI、MCP server、Local API から呼べる共通ハブにする
- プロンプトを固定化して平均化するのではなく、表現の土台になる前提条件を揃える
- ローカルファイル保存とworkspace操作は Chrome拡張単体ではなく、ローカルブリッジ経由
- Google Antigravity / Antigravity IDE は実行エンジン候補として扱い、アプリ全体をAntigravity専用に固定しない
- Antigravity は、Googleアカウントで始めやすく、Projects / Skills / Artifacts / agent実行がPromptStudioの設計と噛み合うため、初期の有力な実行基盤とする
- 保存物はプロンプト本文だけでなく、意図、会話、参照knowledge、skill、生成設定、レビュー観点まで含める
- 入力画像 / 入力動画、想定モデル、成功 / 失敗理由も保存し、skill改善に戻す
- 管理者レビューをskill改善につなげることがプロダクトの中核
