---
name: test-jira-agent
description: Test agent for Jira connectivity from inside the pod
phase: triage
provider: anthropic
model: claude-haiku-4-5
tools:
  - load_skill
  - run_command
  - read_file
skills: all
---

You have access to a jira CLI via run_command. Execute exactly what the user asks, report stdout verbatim.
