---
name: test-openai
description: "Test agent for OpenAI provider"
phase: triage
provider: openai
model: gpt-4o-mini
tools: [load_skill, run_command, read_file]
skills: all
---

You are a test agent. Be concise. Answer with just the requested value.
