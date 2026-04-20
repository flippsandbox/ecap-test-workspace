# Agent Inspector

Inspect this harness's agents — their configured provider, model, prompt, tools, and skills. Use this when a user asks about how agents are set up or which models are being used.

## How to answer questions about agents

### When user asks: "What agents are configured?" / "Who can I talk to?"

Run:
```
curl -s http://localhost:3000/api/agents
```

Returns a JSON array. For each agent, present:
- **name** — the agent ID
- **description** — one-line purpose
- **provider + model** — e.g. `anthropic / claude-sonnet-4-20250514`
- **phase** — orchestrate / triage / execute / review

Format the reply as a short bulleted list.

### When user asks: "What model does <agent> use?" / "How is <agent> configured?"

Run:
```
curl -s http://localhost:3000/api/agents/<agent-name>
```

Returns a single agent with:
- `provider`, `model`, `temperature`, `maxTokens`
- `frontmatterTools` — enabled LLM tools
- `skills` — assigned skills (array or `"all"`)
- `systemPrompt` — the agent's system prompt

Keep the reply focused on what the user asked. Don't dump the full prompt unless asked.

### When user asks: "What models are available?" / "Can I switch to a local model?"

Run:
```
curl -s http://localhost:3000/api/llm/catalog
```

Returns `providers[]` with `name` + `models[]`, plus temperature / maxTokens presets.

To list only locally-hosted models (Ollama, etc.):
```
curl -s http://localhost:3000/api/local-models
```

## Guardrails

- **Read-only by default.** Do not `PUT` agent config or prompts unless the user explicitly asks you to change something and approves the target value.
- Never reveal API keys or secrets — the endpoints above never include them, but don't run commands that would (e.g. `env | grep KEY`).
- If the user asks about an agent that doesn't exist, say so — don't invent one.

## Response style

- Short. Bullet lists beat paragraphs.
- Use code formatting for names: `triage-bot`, `gemma4:e4b`.
- If reporting multiple agents, group by provider for readability.
