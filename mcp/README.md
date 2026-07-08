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
```

MCP serverは、PromptStudioを「プロンプト前提条件とskillの共通ハブ」として使うための入口です。
