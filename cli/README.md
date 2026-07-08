# CLI

`promptstudio` CLI の実装を置く場所です。

将来的には、ターミナル、Codex、Claude Code、Gemini / Antigravity、社内自動処理から PromptStudio Core を呼べるようにします。

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

CLIは、Chrome拡張を使わない自動処理やagent連携の入口です。

管理者はCLIから蓄積artifactを分析し、成功 / 失敗傾向、モデル別skillの改善候補、公式情報の再確認が必要な箇所を抽出できるようにします。
