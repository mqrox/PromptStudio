# Why Antigravity

## 目的

PromptStudio は、初期のローカル実行・agent基盤として Google Antigravity / Antigravity IDE を重視する。

ただし、PromptStudio全体をAntigravity専用に固定しない。Antigravity は有力な実行基盤であり、PromptStudio の本質である skill、knowledge、artifact、レビュー改善サイクルは独立した資産として設計する。

## まず正確に言う

Google Antigravity 2.0 は、単なるIDEではなく、standalone app、Antigravity IDE、CLI、SDK を含むエコシステムとして説明されている。

PromptStudio では、そのうち以下を使いたい。

- ローカルworkspaceを扱う実行面
- agentを動かす基盤
- project単位の設定
- skill呼び出し
- artifact生成
- browser / terminal / editor をまたぐ実行
- MCPや外部ツール連携

## ファクトチェック済みの事実

確認日: 2026-07-08

### 1. Google公式のagentic development platformである

Google Developers Blog は、Antigravity を agentic development platform として紹介している。agentが editor、terminal、browser をまたいで計画、実行、検証する設計が説明されている。

Source: [Build with Google Antigravity, our new agentic development platform](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/)

### 2. Antigravity 2.0 はagentの中央管理基盤として位置づけられている

Google Codelabs では、Antigravity 2.0 をAI agentsのcentral command centerと説明している。Antigravity、Antigravity IDE、CLI、SDK の構成も説明されている。

Source: [Getting Started with Google Antigravity](https://codelabs.developers.google.com/getting-started-google-antigravity)

### 3. Googleアカウントで利用開始する導線がある

Google Codelabs の導入手順では、Chrome browser と Gmail account が必要とされ、インストール後にGoogle accountでログインする流れが説明されている。

Source: [Getting Started with Google Antigravity](https://codelabs.developers.google.com/getting-started-google-antigravity)

### 4. 個人向け無料プランがある

Google Antigravity の公式pricingページでは、individual plan が $0/month として案内されている。

Source: [Google Antigravity Pricing](https://antigravity.google/pricing)

### 5. 有料プランでは利用上限や優先度を拡張できる

Google One Help では、Google AI Pro members が Google Antigravity で higher usage limits と prioritized traffic を得ること、baseline quota とAI creditsの仕組みがあることが説明されている。

Source: [Use Google AI Pro benefits - Google One Help](https://support.google.com/googleone/answer/14534406)

### 6. Gemini 3.5 Flash はagentic workflow向けの上位モデルとして説明されている

Google は Gemini 3.5 Flash を、agentic era 向けで、sub-agent deployment、multi-step workflows、long-horizon tasks に強いモデルとして説明している。

Source: [Gemini 3.5 Flash - Gemini API](https://ai.google.dev/gemini-api/docs/models/gemini-3.5-flash)

### 7. Gemini は画像・動画理解に強い

Google AI for Developers の image understanding ドキュメントでは、Gemini がmultimodal from the ground upであり、画像キャプション、分類、visual question answering などの画像処理に対応すると説明されている。

Source: [Image understanding - Gemini API](https://ai.google.dev/gemini-api/docs/image-understanding)

video understanding ドキュメントでは、Gemini が動画を処理し、映像と音声の両方から内容理解、説明、質問応答、タイムスタンプ参照ができると説明されている。

Source: [Video understanding - Gemini API](https://ai.google.dev/gemini-api/docs/video-understanding)

### 8. Skills と Artifacts の考え方がPromptStudioと近い

Google Codelabs では、Antigravity の Skills は必要なときだけ読み込まれるspecialized package of knowledgeとして説明されている。Artifacts についても、task lists、implementation plans、screenshots、browser recordingsなど、agentの作業を検証するための成果物として説明されている。

Source: [Getting Started with Google Antigravity](https://codelabs.developers.google.com/getting-started-google-antigravity)

## PromptStudioにとっての意味

### 業界導入の安心感

制作会社や広告・映像・ブランド部門に導入する場合、Google公式プロダクトであることは説明しやすい。

これは「絶対に安全」という意味ではない。セキュリティ、権限、保存先、機密情報の扱いはPromptStudio側でも明示的に設計する必要がある。

### 無料で始めやすい

個人向け無料プランがあるため、初期検証のハードルが低い。

ただし、無料で無制限に使えるという意味ではない。利用上限、容量、優先度はプランや時期によって変わる。

### トップレベルのモデル性能に近い

Antigravity はGoogleのGemini系agentic workflowと近い場所にある。Gemini 3.5 Flash は、公式ドキュメント上でfrontier-level intelligence、multi-step workflows、long-horizon tasks向けと説明されている。

PromptStudioでは、これを「上位モデルを使える実行基盤」として評価する。

### クリエイティブ制作と相性が良い

PromptStudioは、入力画像、入力動画、参照素材、生成結果、成功/失敗を扱う。

Geminiの画像理解・動画理解は、以下に使える。

- 入力画像の説明
- 参照画像の要素抽出
- 動画の内容理解
- カメラワークや動きの言語化
- 生成結果のレビュー補助
- 成功/失敗理由の分析補助

### Skill設計と相性が良い

PromptStudioの中核は、意図とモデルに応じたskill呼び出しである。

Antigravity側にも Skills の考え方があり、必要なときに専門知識を読み込む設計になっている。この思想は、PromptStudio の model-specific skill registry と近い。

### Artifact設計と相性が良い

PromptStudioは、プロンプトだけでなく、会話、参照knowledge、入力素材、生成結果、成功/失敗、レビューを保存する。

Antigravity の Artifacts は、agentの作業を人間が検証するための成果物として設計されているため、PromptStudio の review artifact と相性が良い。

## 注意点

### Antigravityは生成モデルそのものではない

Antigravity は、PromptStudioのローカル実行・agent基盤である。

GPT Image 2、Nano Banana Pro、Kling 3.0、Seedance 2.0、Runway系などのモデル別プロンプト設計は、PromptStudioのskill側で扱う。

### 日本語UXと実行指示は分ける

Google One Help では、Antigravity の prompts and instructions は English only とされている。

PromptStudioは、日本語で制作相談できるUXを提供し、必要に応じてAntigravity / Gemini / 各モデル向けの英語指示へ変換する。

### 無料利用には制限がある

無料プランは初期導入には有効だが、業務で継続利用する場合は上限、優先度、AI credits、Google AI Pro / Ultra、組織利用の条件を確認する。

### 仕様は変わる

Antigravity、Gemini、Google AI Studio、Google One の提供条件は更新される。

PromptStudioのドキュメントでは、公式情報の確認日、参照URL、skillの最終確認日を残す。

## 結論

Antigravityを使う理由は、Googleだから盲目的に選ぶということではない。

PromptStudioが必要とする以下の条件を、現時点でかなり満たしているからである。

- Googleアカウントで始めやすい
- 個人無料プランで検証しやすい
- 有料プランで利用上限を広げられる
- Gemini系の高性能agentic workflowに近い
- 画像・動画理解を含むマルチモーダル文脈に強い
- Projects / Skills / Artifacts がPromptStudioの設計と噛み合う
- editor、terminal、browser、MCPをまたいだagent実行ができる
- 将来のGoogle AI Studio、Workspace、Cloud、社内ツール連携へ広げやすい

そのうえで、PromptStudioはAntigravityに依存しすぎない。

Antigravityは初期の強い実行基盤。PromptStudioの本質は、前提条件を揃えるskill、knowledge、artifact、レビュー改善サイクルである。
