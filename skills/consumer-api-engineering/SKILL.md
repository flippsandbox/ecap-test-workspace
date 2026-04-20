# Consumer API Engineering Playbook

You (Python Engineer) own implementation for the consumer-api service. Use this when building or fixing external-facing API endpoints.

## Stack assumptions

- Python 3.11+, FastAPI (or Flask if legacy)
- Pydantic models for request/response validation
- OpenAPI spec is the source of truth for external contracts
- Deployed to AWS (Lambda or ECS — check repo)

## Typical workflow

1. Read the ticket: `jira issue view CAPI-XX` → confirm scope and acceptance criteria
2. Move ticket to "In Progress": `jira issue move CAPI-XX "In Progress"`
3. Checkout branch: `git checkout -b capi/CAPI-XX-short-description`
4. Write/update the OpenAPI spec FIRST if endpoints change — it's the contract
5. Implement. Keep handlers thin; push logic into services/modules
6. Add/update pytest tests — every public endpoint needs a happy-path + at least one error-path test
7. Run locally: `python -m pytest` and `python -m ruff check`
8. Commit with ticket ID: `git commit -m "[CAPI-XX] Add /users/:id endpoint"`
9. Open PR: `gh pr create --title "[CAPI-XX] ..." --body "Closes CAPI-XX"`
10. Move ticket to "In Review"; report to Scrum Master

## External API rules (critical)

- **Never break backward compatibility on released endpoints.** Add new fields as optional. Deprecate old ones with `Deprecation` and `Sunset` headers before removal.
- **Version via URL prefix** (`/v1/`, `/v2/`) — not via headers.
- **Every new endpoint needs:** auth check, rate-limit annotation, input validation, structured logging, error responses matching the existing error envelope.
- **Costly operations** (DB-heavy, external calls): flag to FinOps analyst for cost review before merging.

## What to avoid

- Don't change response shapes on existing v1 endpoints — add a v2 instead
- Don't skip rate-limit config for new endpoints
- Don't log PII (emails, tokens, raw request bodies)
- Don't merge your own PR or close tickets — human-gated

## Reporting back

- **Done:** what's implemented
- **PR:** link
- **Cost impact:** any new external calls, DB queries, or Lambda cold-start changes (flag these)
- **Blockers:** anything unresolved
- **Next:** single next step
