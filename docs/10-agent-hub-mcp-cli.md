# Agent Hub / MCP / CLI

## 目的

PromptStudio は、最初はChrome拡張として実装する。

ただし、長期的な本体はChrome拡張ではない。PromptStudio の本体は、生成AIプロンプトを考えるための前提条件、skill、knowledge、artifact、レビューPDCAを提供する共通ハブである。

将来的には、ChatGPT系環境、Codex、Claude Code、Gemini / Antigravity、その他AIエージェントや社内ツールから呼べるようにする。

## なぜ必要か

現場では、社員やチームによって使うAI環境が変わる。

- ChatGPTで相談する人
- Codexで制作支援や実装を進める人
- Claude Codeで作業する人
- Gemini / Antigravityでagentを動かす人
- 社内ツールや自動化から生成AIを使う人

入口が違っても、会社として揃えるべき前提条件は同じである。

- 案件ルール
- ブランド文脈
- 公式ガイドライン
- モデル別skill
- 入力画像 / 入力動画の扱い
- 成功 / 失敗の蓄積
- 管理者レビュー

だから PromptStudio は、特定UIだけのツールではなく、agentが呼べる共通ハブにする。

## 全体像

```text
Chrome Extension
CLI
MCP Server
Local API
Future Team Server
  -> PromptStudio Core
    -> Skill Registry
    -> Knowledge Registry
    -> Artifact Store
    -> Review Feedback Loop
    -> Execution Adapters
```

## PromptStudio Core

Core は、どの入口から呼ばれても同じ判断を行う。

- 依頼意図を整理する
- 対象モデルを確認する
- 必要なskillを選ぶ
- 参照すべきknowledgeを集める
- 入力画像 / 入力動画 / 参照素材を記録する
- モデル別プロンプト、ネガティブ、設定、注意点を出す
- 成果物保存用のmetadataを作る
- 成功 / 失敗とレビュー結果を取り込む
- 蓄積artifactを分析し、管理者向けのskill改善案を作る

## 呼び出し口

### Chrome拡張

現場スタッフが毎日使う入口。

ChatGPTに近い対話UXで、制作意図を整理し、モデル別プロンプトを作る。

### CLI

ターミナルや自動処理から使う入口。

想定コマンド。

```text
promptstudio plan
promptstudio prompt
promptstudio save
promptstudio review
promptstudio analyze
promptstudio propose-skill-updates
promptstudio skill list
```

### MCP server

MCP対応agentから呼ぶ入口。

想定tool。

```text
promptstudio.resolve_context
promptstudio.select_skills
promptstudio.generate_prompt_package
promptstudio.save_artifact
promptstudio.record_review
promptstudio.analyze_artifacts
promptstudio.propose_skill_updates
```

### Local API

Chrome拡張、社内ツール、ローカルworkspaceから呼ぶHTTP/localhost API。

### Team Server

将来的に、チーム単位のskill、knowledge、artifact、レビュー履歴を管理するサーバー。

### 管理者用agent skill

Codex / Claude Code / Gemini / Antigravity から使う、管理者向けのskill群。

目的は、現場スタッフのprompt package生成ではなく、保存されたartifactから共通skillとknowledgeの改善候補を見つけることである。

想定skill。

- artifact-review: artifact単位で依頼、会話、入力素材、prompt、結果、reviewを点検する
- skill-gap-analysis: 複数artifactの失敗傾向から不足skillを見つける
- model-skill-maintenance: モデル別skillの更新候補、確認すべき公式情報、再テスト項目を出す
- review-summary: 管理者向けの週次 / 月次改善レポートを作る

出力には、改善提案、根拠artifact、対象skill / knowledge、影響範囲、confidence、管理者承認が必要であることを含める。

管理者用agent skillは、共通skillを自動で書き換えない。提案、レビュー、承認、反映を分ける。

## Prompt Package

agentや外部ツールへ返す基本単位を `prompt package` と呼ぶ。

含めるもの。

- 制作意図
- 対象モデル / 生成サービス
- 呼び出したskill
- skillの情報源、バージョン、最終確認日
- 参照knowledge
- 入力画像 / 入力動画 / 参照素材
- 生成プロンプト
- ネガティブプロンプト
- 推奨設定
- 注意点
- 保存先
- review metadata

## 想定フロー

### Chrome拡張から使う

1. 制作スタッフがChrome拡張で相談する
2. Chrome拡張が PromptStudio Core を呼ぶ
3. Core がskillとknowledgeを解決する
4. prompt packageを返す
5. ユーザーが保存する
6. artifactとreview metadataが残る

### Codex / Claude Code / Gemini / Antigravityから使う

1. agentがMCP serverまたはCLIでPromptStudioを呼ぶ
2. Core が意図、モデル、skill、knowledgeを整理する
3. prompt packageを返す
4. agentが生成、編集、検証、保存を進める
5. 成功 / 失敗、入力素材、生成結果、レビューをPromptStudioへ戻す
6. 共通skillが改善される

### 管理者が蓄積artifactを分析する

1. 管理者がCodex / Claude Codeから管理者用skillを起動する
2. CLIまたはMCP serverが対象期間、モデル、案件、skillを条件にartifactを集める
3. Core が成功 / 失敗、入力素材、モデル選択、skill呼び出し、reviewを横断分析する
4. 改善候補、根拠artifact、対象skill、影響範囲、confidenceを返す
5. 管理者が提案を確認し、必要なskill / knowledgeだけを承認して反映する

## 設計原則

- Chrome拡張だけにロジックを閉じ込めない
- skill / knowledge / artifact はUI非依存にする
- MCP / CLI / Local API から同じCoreを呼ぶ
- 保存形式を先に安定させる
- 外部agentに渡す情報はprompt packageとして構造化する
- 成功 / 失敗とレビュー結果をskill改善に戻す
- 管理者用skillは改善案を出すが、共通skillを自動変更しない
- Antigravity、Codex、Claude Code、Gemini、ChatGPT系環境のどれか1つに固定しない

## MVPとの関係

MVPでは、Chrome拡張とローカル保存を優先する。

ただし、最初からCoreをUIから分離する。これにより、後からMCP serverやCLIを追加しても、Chrome拡張用のロジックを作り直さずに済む。
