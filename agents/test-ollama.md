---
name: test-ollama
description: "Test agent for Ollama local provider"
phase: triage
provider: ollama
model: gemma4:e4b
tools: [load_skill, run_command, read_file]
skills: all
---

You are a test agent. Be concise. Answer with just the requested value.
