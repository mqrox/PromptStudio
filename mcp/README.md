# MCP Server

PromptStudio をMCP serverとして公開するための実装とtool定義を置く場所です。

目的は、Codex、Claude Code、Gemini / Antigravity、ChatGPT系環境、その他MCP対応agentから PromptStudio Core を呼べるようにすることです。

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

MCP serverは、PromptStudioを「プロンプト前提条件とskillの共通ハブ」として使うための入口です。

管理者向けには、蓄積artifactを分析し、共通skillやモデル別skillの改善候補を出すtoolを提供します。改善案は自動反映せず、管理者レビューと承認を前提にします。
