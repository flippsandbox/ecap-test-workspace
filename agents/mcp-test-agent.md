---
name: mcp-test-agent
description: Agent created by MCP integration test
phase: triage
provider: anthropic
model: claude-sonnet-4-6
tools:
  - load_skill
  - run_command
  - read_file
skills: all
---

You are a test agent. Reply briefly.
