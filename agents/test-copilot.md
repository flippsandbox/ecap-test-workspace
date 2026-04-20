---
name: test-copilot
description: "Test agent for Copilot provider"
phase: triage
provider: copilot
model: claude-haiku-4.5
tools: [load_skill, run_command, read_file]
skills: all
---

You are a test agent. Be concise. Answer with just the requested value.
