# README Design Details

## この文書の目的

この文書は、メインの `README.md` をGPTPRO版ベースの読みやすいピッチ資料にするため、READMEから分離した設計情報をまとめる。

READMEは、社長、管理者、制作スタッフ、初見の関係者が短時間で価値を理解するための入口にする。

詳細な設計判断、責務分離、Core、CLI、MCP、管理者用スキル、保存形式、運用ガードレールは、この文書と `docs/` 配下の詳細文書に置く。

## READMEに残す情報

READMEには、以下を残す。

- PromptStudio が何を解決するか
- なぜ今必要か
- 誰のためのツールか
- どのような業界に使えるか
- MVPで最初に作るもの
- 保存される成果物の概要
- Antigravity を初期実行基盤として重視する理由
- 将来的な共通ハブ構想
- ビジネス価値
- 詳細ドキュメントへの導線

READMEでは、実装責務や保存スキーマの細部を深追いしない。

## READMEから分離する設計情報

READMEから分離してdocs側で扱う情報は以下。

- Chrome拡張、PromptStudio Core、ローカルブリッジ、CLI、MCP server、Local API、Team Serverの責務分離
- skill / knowledge / artifact の詳しい定義
- model-specific skill registry の管理方法
- admin skill の分析出力、承認フロー、反映ガードレール
- Prompt Package の構造
- artifact保存フォルダーの詳細
- Antigravity / ExecutionEngine の抽象境界
- Googleログイン、権限、Team Serverの段階的導入
- GitHubリポジトリの運用ルール

## 中核アーキテクチャ

PromptStudio は、最初からChrome拡張だけにロジックを閉じ込めない。

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

### Chrome Extension

現場スタッフが毎日使う入口。

- サイドパネルのチャットUI
- 設定画面
- 用途選択
- 生成プロンプトの表示
- 保存操作の起点

Chrome拡張は、任意のローカルファイル操作や重い生成処理を直接持たない。

### PromptStudio Core

どの入口から呼ばれても同じ判断を行う中核。

- 制作意図の整理
- 対象モデル / 生成サービスの解決
- skill選択
- knowledge参照
- 入力画像 / 入力動画 / 参照素材の記録
- モデル別prompt package生成
- artifact保存形式の生成
- 成功 / 失敗、レビュー結果の取り込み
- 蓄積artifactの横断分析
- 管理者向けskill改善提案の生成

Core は、特定UI、特定IDE、特定AIモデルに依存しない。

### Local Bridge

Chrome拡張とローカルworkspaceをつなぐ境界。

- workspaceパスの確認
- skill / knowledge の読み取り
- 成果物フォルダーへの保存
- Google Antigravity / Antigravity IDE への実行依頼
- 将来の別実行エンジンへの差し替え境界

Chrome拡張からローカルファイルへ自由アクセスする設計は避ける。

### CLI / MCP Server / Local API

将来的に、PromptStudio Coreを外部agentや社内ツールから呼ぶ入口。

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

## skill / knowledge / artifact

### skill

skill は、単なるプロンプトテンプレートではない。

制作意図を生成AIが扱いやすい形に変換するための実務ノウハウであり、以下を含む。

- 画像生成向けの意図分解
- 動画生成向けの時間、動き、カメラ指定
- 広告、映像、CG / VFX、デザイン制作で必要な画作りの観点
- モデルごとの得意不得意
- モデルごとに必要な前提、入力形式、指定の粒度
- 入力画像 / 入力動画の扱い方
- ネガティブプロンプトの考え方
- 案件ルールや禁止事項
- レビューでよく指摘される失敗パターン
- 公式ガイドラインから取り込むべき注意点
- 社内の成功 / 失敗蓄積から改善された判断基準

skill は、全員の表現を平均化するためではなく、表現以前の前提条件の抜け漏れを防ぐために使う。

### knowledge

knowledge は、案件や会社で共有する文脈。

- 案件ごとのトーン、世界観、禁止事項
- ブランドガイドライン
- キャラクター設定
- 商品情報
- 用語集
- 参照作品の分析メモ
- 社内レビュー基準
- 過去の成功例と失敗例

skill が「どう考えるか」だとすると、knowledge は「何を前提にするか」である。

### artifact

1回の相談結果を、1つのレビュー可能な成果物として保存する。

```text
artifacts/
  2026-07-08_153000_campaign-visual-idea/
    request.md
    conversation.md
    prompt.md
    prompt.json
    inputs.md
    result.md
    references.md
    metadata.json
    review.md
```

保存するのはプロンプト本文だけではない。依頼、会話、参照skill、参照knowledge、入力素材、生成設定、結果、成功 / 失敗、レビューまで残す。

## モデル別skill

PromptStudio は1つのモデルだけに最適化しない。

初期対応候補。

- GPT Image 2
- Nano Banana Pro
- Kling 3.0
- Seedance 2.0
- Runway Aleph / Runway系

モデル別skillには、少なくとも以下を含める。

- 公式ガイドラインや公開仕様から得られる注意点
- 社内検証で改善されたプロンプト構造
- 得意な表現
- 苦手な指定
- 必要な入力情報
- 入力画像 / 入力動画の扱い方
- 推奨される生成設定
- ネガティブ指定や避けるべき表現
- 成功パターン
- 失敗パターン
- レビュー観点
- 情報源
- バージョン
- 最終確認日

公式ガイドラインやモデル仕様は変わるため、出どころと確認日を残す。

## 管理者用skill

管理者用skillは、現場スタッフが使うプロンプト生成skillとは別レイヤー。

現場スタッフ用skillは、制作意図を整理し、対象モデルに合ったprompt packageを作るためのもの。

管理者用skillは、保存されたartifactを分析し、共通skillとknowledgeを改善するためのもの。

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

管理者用skillは、共通skillを勝手に書き換えない。提案、レビュー、承認、反映を分ける。

## Antigravity の位置づけ

Google Antigravity / Antigravity IDE は、初期のローカル実行・agent基盤として重視する。

ただし、PromptStudio全体をAntigravity専用に固定しない。

Antigravity は実行基盤候補であり、PromptStudio の本質である skill、knowledge、artifact、レビューPDCAは独立した資産として設計する。

設計上は、`ExecutionEngine` のような抽象境界を置き、その実装の1つとしてAntigravityを扱う。

注意点。

- Antigravity自体は画像・動画生成モデルではない
- 利用上限、対応モデル、料金、対応言語は変わる可能性がある
- Googleのヘルプでは、Antigravity のプロンプトと指示は英語のみ対応とされている
- PromptStudio は日本語UXを提供し、必要に応じて英語指示やモデル別プロンプトへ変換する

## 設計原則

- Chrome拡張だけにロジックを閉じ込めない
- skill / knowledge / artifact はUI非依存にする
- MCP / CLI / Local API から同じCoreを呼ぶ
- 保存形式を先に安定させる
- 外部agentに渡す情報はprompt packageとして構造化する
- 成功 / 失敗とレビュー結果をskill改善に戻す
- 管理者用skillは改善案を出すが、共通skillを自動変更しない
- Antigravity、Codex、Claude Code、Gemini、ChatGPT系環境のどれか1つに固定しない

## 関連ドキュメント

- [00-product-brief.md](00-product-brief.md): プロダクトの本質と対象ユーザー
- [01-mvp-scope.md](01-mvp-scope.md): 最初に作る範囲
- [02-architecture-principles.md](02-architecture-principles.md): アーキテクチャ方針
- [03-prompt-skill-pdca.md](03-prompt-skill-pdca.md): skill / knowledge / 保存物 / レビュー改善サイクル
- [04-implementation-roadmap.md](04-implementation-roadmap.md): 実装ロードマップ
- [06-decision-log.md](06-decision-log.md): 重要な意思決定ログ
- [08-model-skill-registry.md](08-model-skill-registry.md): モデル別skill設計
- [09-why-antigravity.md](09-why-antigravity.md): Antigravityを使う理由と確認済み事実
- [10-agent-hub-mcp-cli.md](10-agent-hub-mcp-cli.md): MCP / CLI / agent hub 構想
