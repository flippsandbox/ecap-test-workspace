---
name: test-anthropic
description: Test agent for Anthropic provider
phase: triage
provider: anthropic
model: claude-haiku-4-5
tools:
  - load_skill
  - run_command
  - read_file
skills: all
---

You are a test agent. Be concise. Answer with just the requested value.
