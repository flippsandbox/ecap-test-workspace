# Jira TBT Board — To-Do App Conventions

All engineering work for the To-Do app is tracked on the Jira **TBT** project board.
Use this when you need to read tickets, update status, or add comments.

## Read the board

```bash
# List recent open tickets
jira issue list --project TBT --status "To Do,In Progress" --limit 10

# View a single ticket
jira issue view TBT-42

# Find tickets by keyword
jira issue list --project TBT --jql 'text ~ "delete button"'
```

## Move ticket status (Engineer / Scrum Master)

```bash
# Valid transitions: "To Do" → "In Progress" → "In Review" → "Done"
jira issue move TBT-42 "In Progress"
jira issue move TBT-42 "Done"
```

## Comment on a ticket

```bash
jira issue comment add TBT-42 "Implemented the delete button per AC. Ready for QA."
```

## Ticket hygiene (when writing new tickets)

- Title: imperative, short — "Add delete button to todo items"
- Body: User story + Acceptance Criteria (AC) as a numbered list
- Always link related PRs via `--pr <url>` or a comment

## When you don't know

- If a ticket field is ambiguous, read the ticket with `jira issue view` before acting
- If status transition fails, `jira issue transitions TBT-42` shows valid next states
- Never close a ticket as "Done" until QA has signed off in the ticket
