# To-Do App Engineering Playbook

You (Engineer) own the implementation. Use this skill when working on features or bug fixes for the To-Do app.

## Typical workflow

1. Read the ticket: `jira issue view TBT-XX` → confirm scope and AC
2. Move ticket to "In Progress": `jira issue move TBT-XX "In Progress"`
3. Checkout a branch: `git checkout -b todo/TBT-XX-short-description`
4. Make changes. Prefer small, focused edits
5. Run tests locally: `npm test` (or the equivalent for the repo)
6. Commit with the ticket ID in the message: `git commit -m "[TBT-XX] Add delete button"`
7. Open a PR referencing the ticket: `gh pr create --title "[TBT-XX] …" --body "Closes TBT-XX"`
8. Move ticket to "In Review" once the PR is up
9. Summarize back to the Scrum Master: what changed, PR URL, any blockers

## What to avoid

- Don't modify tests just to make them pass — understand why they failed first
- Don't refactor unrelated code in a ticket PR (creates review noise)
- Don't close tickets or merge PRs — those are human-gated actions
- Don't use `git push --force` or `git reset --hard` on shared branches

## Reporting back

Keep reports tight. A good status update:
- **Done:** what's implemented
- **PR:** link
- **Blockers:** anything you couldn't resolve
- **Next:** single next step

Don't dump full diffs unless asked.
