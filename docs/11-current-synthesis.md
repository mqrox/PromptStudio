# Current Synthesis

## この文書の目的

この文書は、これまでのユーザー原文メモと、現時点でリポジトリに存在するMarkdownを統合した要約である。

ここでの `raw文` は、ユーザーがチャットに貼った文章そのものを指す。原文は [12-user-raw-notes.md](12-user-raw-notes.md) に一次情報として保存し、この文書ではその原文から読み取れる本質と、既存Markdownで整理済みの内容を統合する。

目的は、PromptStudio が何を解決しようとしているのか、現在どこまで整理されているのか、今後どの方向へ実装していくのかを、経営者、管理者、制作スタッフ、実装者が同じ前提で理解できるようにすること。

## 一言で言うと

PromptStudio は、クリエイティブ制作における生成AIプロンプト作成を、個人の言語力やモデル知識に依存した作業から、会社全体で再現・保存・レビュー・改善できる制作プロセスへ変えるための運用基盤である。

最初の入口は Chrome拡張の対話UI。長期的な本体は PromptStudio Core であり、Chrome拡張、CLI、MCP server、Local API、将来のTeam Serverから同じskill、knowledge、artifact、レビュー改善サイクルを使えるようにする。

## ユーザー原文から読み取れる本質

ユーザーが最初に求めていたのは、Antigravity 2.0 IDE をエンジンとして使い、Chrome拡張上で ChatGPT に近いUXの対話操作ができるツールである。

背景には、VFX / CG制作会社をはじめとしたクリエイティブ現場で、社員それぞれが生成AIサービスのプロンプトを個別に考えている現状がある。生成AIを使っていないわけではなく、むしろ各自が ChatGPT や別モデル、画像生成、動画生成サービスをすでに使っている。

問題は、社員ごとに以下が違うこと。

- 参照しているコンテキスト
- モデルごとの知識
- プロンプト設計skill
- 言語化力
- 英語表現力
- 画像生成と動画生成それぞれの勘所
- 入力画像 / 入力動画 / 参照素材の扱い
- 過去の成功 / 失敗から学んだ知見

そのため、同じ制作意図でも、人によってプロンプトの前提が変わり、結果の品質や再現性がばらつく。

重要なのは、これは「AIにプロンプトを書いてもらえば解決する」問題ではないという点である。AIに渡す前提が人によって違えば、AIが作るプロンプトも人によってばらつく。必要なのは、プロンプト本文だけを生成する道具ではなく、AIが参照する前提、skill、knowledge、モデル別ノウハウ、保存とレビューの流れを会社として揃える仕組みである。

また、目的はプロンプトをガチガチに固定し、全員の出力を平均化することではない。各クリエイターの意図、個性、ディレクションを活かすために、表現以前でズレやすい前提条件を揃えることが本質である。

## 現状Markdownで整理済みの中核方針

現状のREADMEとdocsでは、PromptStudioを以下のように定義している。

- 広告、映像、デザイン、CG / VFX、ゲーム、アニメ、ブランド制作、SNSコンテンツなど、クリエイティブ制作全般に使えるツールにする
- 仕事でクリエイティブ制作に関わる生成AIプロンプトを考えるときは、まず PromptStudio を使う
- 社員が各自でChatGPTや別モデルを使うことは否定しない
- その前段に、会社共通の前提、skill、knowledge、保存、レビューを置く
- Chrome拡張は最初のUXであり、プロダクト全体の本体ではない
- 本体は PromptStudio Core とし、CLI、MCP server、Local API、将来のTeam Serverからも呼べるようにする
- Antigravity / Antigravity IDE は初期の有力な実行基盤だが、PromptStudioをAntigravity専用には固定しない
- 成果物はプロンプト本文だけでなく、依頼、会話、参照skill、参照knowledge、入力素材、設定、結果、成功 / 失敗、レビューまで保存する
- 管理者レビューを共通skill改善に戻し、改善を進める

## 解く課題

現場で起きている課題は、単なるプロンプト作成能力の不足ではない。

### 1. プロンプト品質が個人の前提に依存している

同じ案件、同じモデル、同じ素材でも、担当者によって出力が変わる。これは制作力の差だけではなく、モデル理解、言語化、案件文脈、入力素材の扱い方、過去知見へのアクセス差によって起きる。

### 2. 良いノウハウが会社の資産にならない

うまくいったプロンプトや失敗した指定が、個人のチャット履歴やメモに閉じる。別の社員は同じ試行錯誤を繰り返す。

### 3. AIにプロンプトを書かせても前提が揃わない

汎用AIチャットに「良いプロンプトを書いて」と頼んでも、そのAIが会社の案件ルール、ブランド文脈、モデル別ノウハウ、過去の成功 / 失敗を知らなければ、担当者の入力品質に依存する。

### 4. 画像生成と動画生成で必要なskillが違う

画像生成では構図、スタイル、ライティング、参照画像の扱いが重要になる。動画生成では時間変化、カメラワーク、動き、カット尺、入力動画や参照素材の扱いが重要になる。これらを共通skillとして扱う必要がある。

### 5. 管理者が改善できる材料が残らない

最終プロンプトだけ残っても、なぜそのプロンプトになったのか、どのskillが効いたのか、どの入力素材が失敗原因だったのかが分からない。レビューからskill改善へ戻せない。

## 解決すること

PromptStudio は、制作スタッフが日本語で作りたいものを相談すると、会社共通のskill、knowledge、案件ルール、モデル別ノウハウを参照し、用途とモデルに合ったprompt packageを作る。

同時に、以下を保存する。

- 最初の依頼
- 対話ログ
- 生成プロンプト
- ネガティブプロンプト
- 推奨設定
- 想定モデル / 生成サービス
- 呼び出したskill
- skillの情報源、バージョン、最終確認日
- 参照したknowledge
- 入力画像 / 入力動画 / 参照素材
- 生成結果
- 成功 / 失敗
- 失敗理由
- 管理者レビュー

これにより、プロンプトはその場限りの文章ではなく、会社が改善できる制作資産になる。

## 対象モデルとskillの考え方

初期対応候補として、以下のようなモデル別skillを想定している。

- GPT Image 2
- Nano Banana Pro
- Kling 3.0
- Seedance 2.0
- Runway Aleph / Runway系
- 今後登場する画像生成、動画生成、3D、音声、編集、合成系モデル

モデル別skillには、公式ガイドライン、公開仕様、社内検証、成功例、失敗例、入力画像 / 入力動画の扱い、ネガティブ指定、推奨設定、レビュー観点、情報源、バージョン、最終確認日を含める。

skillはテンプレートではない。表現を縛るものではなく、制作意図をモデルが理解しやすい形へ変換し、前提条件の抜け漏れを防ぐための実務ノウハウである。

## skillとknowledgeの違い

skill は「どう考えるか」である。

例。

- 画像生成向けの意図分解
- 動画生成向けの時間、動き、カメラ指定
- モデル別の得意不得意
- 入力画像 / 入力動画の扱い
- 失敗しやすい条件
- レビュー観点
- ネガティブプロンプトの考え方

knowledge は「何を前提にするか」である。

例。

- 案件の世界観
- ブランドルール
- キャラクター設定
- 商品情報
- 禁止事項
- 用語集
- 社内レビュー基準
- 過去の成功例と失敗例

PromptStudio は、skill と knowledge を分けて扱うことで、モデル別ノウハウと案件文脈を混ぜすぎずに管理する。

## MVPで作るもの

MVPで最優先するのは、現場スタッフがChrome上で自然に相談でき、管理者が後からレビューできる保存形式が残ることである。

作るもの。

- Chrome拡張のサイドパネルチャットUI
- 日本語の対話入力
- 用途選択
- モデル選択
- skill / knowledge / workspace / 保存先フォルダーの設定
- 生成プロンプトの表示
- 保存ボタン
- ローカルブリッジ経由の成果物保存
- 1相談 = 1成果物フォルダーの保存形式

後回しにするもの。

- 本格的なクラウド同期
- チーム別ダッシュボード
- Google Workspace連携
- 複雑な権限管理
- 生成AIサービスへの直接投稿
- 画像や動画の自動評価

## アーキテクチャ

現状の設計では、責務を以下に分ける。

```text
Chrome Extension / CLI / MCP Server / Local API
  -> PromptStudio Core
    -> Skill Registry
    -> Knowledge Registry
    -> Artifact Store
    -> Review Feedback Loop
    -> Execution Adapters
      -> Google Antigravity / Antigravity IDE
      -> Other agents and model tools
```

Chrome拡張は、毎日使う入口である。チャットUI、設定画面、結果表示、保存操作の起点を担当する。

PromptStudio Core は、意図整理、モデル解決、skill選択、knowledge参照、prompt package生成、artifact保存形式、レビュー結果の取り込み、管理者向け分析を担当する。

ローカルブリッジは、Chrome拡張とローカルworkspaceをつなぐ。任意フォルダー保存、skill / knowledge読み取り、Antigravity / IDE / CLI / MCPとの接続境界を担当する。

CLIとMCP serverは、Codex、Claude Code、Gemini / Antigravity、ChatGPT系環境、社内ツールから PromptStudio Core を呼ぶ入口である。

## Antigravityを使う理由

Antigravity / Antigravity IDE は、PromptStudioの初期ローカル実行・agent基盤として重視している。

理由。

- Google公式プロダクトとして、業界導入時に説明しやすい
- Googleアカウントで始められる
- 個人向け無料プランから検証しやすい
- 有料プランで利用上限や優先度を拡張できる
- Gemini系モデルのagentic workflowと近い
- Geminiは画像・動画理解を含むマルチモーダル文脈に強い
- Projects / Skills / Artifacts の考え方が PromptStudio の設計と近い
- editor、terminal、browser、MCPをまたいだagent実行ができる
- Windows / macOS / Linux に対応している

ただし、AntigravityはPromptStudioの本体ではない。あくまで初期の有力な実行基盤である。PromptStudioの本質は、skill、knowledge、artifact、レビュー改善サイクルであり、これらはAntigravity外でも再利用できる形式にする。

注意点として、Antigravity自体は画像・動画生成モデルではない。また、公式情報ではAntigravityのプロンプトと指示は英語のみ対応とされているため、日本語UXと英語実行指示の変換層をPromptStudio側に持つ前提で設計する。

## agent hub / MCP / CLI の将来像

PromptStudio は、最初はChrome拡張として始めるが、長期的には生成AIプロンプトの共通ハブにする。

想定する呼び出し元。

- Chrome拡張
- Codex
- Claude Code
- Gemini / Antigravity
- ChatGPT系環境
- CLI
- MCP対応agent
- 社内ツール

想定CLI。

```text
promptstudio plan
promptstudio prompt
promptstudio save
promptstudio review
promptstudio analyze
promptstudio propose-skill-updates
promptstudio skill list
```

想定MCP tool。

```text
promptstudio.resolve_context
promptstudio.select_skills
promptstudio.generate_prompt_package
promptstudio.save_artifact
promptstudio.record_review
promptstudio.analyze_artifacts
promptstudio.propose_skill_updates
```

入口が違っても、会社として参照する前提条件、skill、knowledge、保存形式、レビュー改善サイクルは同じにする。

## 管理者用skill

管理者用skillは、制作スタッフが使うプロンプト生成skillとは別のレイヤーである。

現場スタッフ用skillは、制作意図を整理し、モデルに合うprompt packageを作るためのもの。

管理者用skillは、保存されたartifactを横断分析し、共通skillとknowledgeの改善候補を見つけるためのもの。

初期候補。

- `artifact-review`: 保存された成果物を読み、依頼、入力素材、モデル選択、prompt、結果、reviewを点検する
- `skill-gap-analysis`: 失敗例やレビューコメントから、不足しているskillや古くなったskillを見つける
- `model-skill-maintenance`: 公式ガイドライン、社内検証、失敗傾向をもとにモデル別skillの更新候補を出す
- `review-summary`: 週次 / 月次で成功例、失敗例、改善候補を管理者向けに要約する

管理者用skillが出すもの。

- 改善提案
- 根拠artifact
- 成功 / 失敗の傾向
- 対象skill / knowledge
- 影響範囲
- 公式情報の再確認が必要な箇所
- confidence
- 管理者承認が必要であること

重要なのは、管理者用skillが共通skillを勝手に書き換えないこと。改善提案、レビュー、承認、反映を分ける。

## 現状のMarkdown構成

現状の主な文書は以下。

- `README.md`: 社長や非エンジニアにも伝わる全体説明、課題、解決策、MVP、Antigravity、ビジネス価値
- `docs/00-product-brief.md`: プロダクトの本質、対象ユーザー、作るもの / 作らないもの
- `docs/01-mvp-scope.md`: MVPで作る範囲と後回しにする範囲
- `docs/02-architecture-principles.md`: Chrome拡張、Core、ローカルブリッジ、CLI、MCP、Antigravityの責務分離
- `docs/03-prompt-skill-improvement-loop.md`: skill、knowledge、artifact保存、レビュー改善サイクル
- `docs/04-implementation-roadmap.md`: Phase 0からTeam Serverまでのロードマップ
- `docs/05-repo-governance.md`: リポジトリ運用とディレクトリ方針
- `docs/06-decision-log.md`: 重要な意思決定ログ
- `docs/07-business-pitch.md`: ビジネスピッチとしての要約
- `docs/08-model-skill-registry.md`: モデル別skillの考え方
- `docs/09-why-antigravity.md`: Antigravityを使う理由とファクトチェック
- `docs/10-agent-hub-mcp-cli.md`: MCP / CLI / agent hub構想
- `docs/11-current-synthesis.md`: ユーザー原文と現状Markdownを統合したサマリー
- `docs/12-user-raw-notes.md`: ユーザーがチャットに貼ったraw文の一次情報

## 現時点でまだ実装されていないもの

現状のリポジトリは、主にプロダクト設計とドキュメント整理の段階である。

まだ実装されていないもの。

- Chrome拡張本体
- サイドパネルUI
- 設定画面
- PromptStudio Coreの実装
- ローカルブリッジ
- CLI
- MCP server
- 実際のskillファイル
- 実際のknowledgeサンプル
- artifact保存処理
- 管理者用skillの実装
- Googleログイン
- Antigravity連携

ただし、実装前に重要な設計判断はかなり固まっている。

## 今後の実装順序

現状Markdownから読み取れる現実的な順序は以下。

1. Chrome拡張の骨格を作る
2. 設定画面でworkspace、skill、knowledge、保存先を指定できるようにする
3. ローカルブリッジで設定先へ保存できるようにする
4. PromptStudio Coreを切り出し、意図整理、skill選択、prompt package生成を集約する
5. 画像生成 / 動画生成の基本skillを作る
6. モデル別skillレジストリを作る
7. 1相談 = 1artifactフォルダーで保存する
8. 管理者レビュー用の保存形式を安定させる
9. Antigravity / Antigravity IDE連携を実験する
10. CLI / MCP serverからCoreを呼べるようにする
11. 管理者用skillで蓄積artifactの分析と改善提案を行う
12. 将来的にTeam Serverやチーム運用へ広げる

## このプロダクトで守るべき原則

- 単なるChatGPTクローンにしない
- プロンプト本文だけを作るツールにしない
- 生成AIサービスそのものを置き換えようとしない
- 特定モデルや特定IDEに固定しない
- Chrome拡張にローカルファイル操作を詰め込みすぎない
- skillを固定テンプレートとして扱わない
- 出力の平均化を目的にしない
- 保存形式を軽視しない
- 管理者レビューとskill改善の導線を後回しにしすぎない
- 実案件の機密情報やAPIキーを公開リポジトリに入れない

## 最終的に目指す状態

PromptStudio が目指すのは、生成AIに強い一部の社員だけが成果を出す状態ではない。

クリエイティブチーム全体が、会社のskillとknowledgeを使って前提条件を揃えながら、それぞれの意図や個性を活かしたプロンプトを作り、入力素材、生成結果、成功 / 失敗、レビューを保存し、次のskill改善へ戻せる状態である。

生成AIを、個人が便利に使う外部ツールから、会社の制作力を拡張する運用基盤へ変えることが PromptStudio の目的である。
