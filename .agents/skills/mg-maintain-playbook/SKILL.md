---
name: mg-maintain-playbook
description: Draft, revise, or review substantive Markdown guidance for this repository’s MG Engineering Playbook. Use for playbook content, not application-repository work.
---

# Goal

Keep the playbook accurate, useful, and verifiable while distinguishing adopted guidance from proposals. The workflow applies whether one contributor performs each pass or contributors share the work. Follow [repository guidance](../../../AGENTS.md).

# Workflow

1. **Choose a path.** Make tiny mechanical edits directly with proportionate checks. For review-only requests, set scope, gather relevant sources and applicable contracts, then review the existing page; do not rewrite or integrate unless asked. Use the full workflow for substantive drafting or revision.
2. **Set the brief.** Record deliverable, scope, sources, acceptance evidence, open decisions, and file ownership; add audience, outcome, applicability, version, or destination as relevant. For shared work, assign clear ownership, pass the brief and evidence, and avoid concurrent writes to the same artifact. Use `work/playbook/backlog.md` and `work/playbook/reviews/<slug>.md` for substantive work.
3. **Ground the work.** Read the relevant page, index, [migration map](../../../maintenance/migration-map.md), and necessary linked sources. For changing technical facts, use and cite current primary sources. Read [content contracts](references/content-contracts.md) when drafting, revising, or reviewing actionable pages. Distinguish facts, recommendations, assumptions, and proposals.
4. **Draft.** Draft from the brief and evidence. When contributors share work, assign the draft to a writer and make the owned files explicit.
5. **Review.** Review the draft or existing page against the brief, sources, and applicable contracts in a distinct pass. A single contributor may self-review using those inputs; report this as self-review, not independent review. Independent review may use another reviewer in a separate context; require it only when the task or policy says so. Provide the same context without steering the verdict. Distinguish missing/unknown evidence from evidence that contradicts a claim. Record findings in the review file.
6. **Revise and recheck.** Resolve findings with evidence, dispute them with evidence, or record the consequence of deferring them. Recheck substantive revisions. Accept only when the brief is met and no blocker or major finding remains open. After two unresolved revision rounds, stop at `needs-review`. If the task or policy requires independent review and none is available, leave it `needs-review`; do not claim an independent verdict.
7. **Integrate and verify.** Integrate assigned navigation, links, and tracking. Substantive integration or technical edits that could change approved content require another review pass using the appropriate method. For moves, update the migration map and local links in the same change; retain forwards through the first post-migration release per the map. Do not extend retention based on an unadopted proposal. Stop when accepted.

# Commands

Run these read-only Git commands from the repository root when Git is available:

- `git status --short` — see changed and untracked paths.
- `git diff --` — inspect tracked unstaged changes; inspect untracked files directly.
- `git diff --check` — check whitespace in unstaged tracked changes.

# Rules

- Ask only when missing information materially blocks scope or grounded work; otherwise make routine choices, state needed assumptions, and continue unaffected work.
- Do not invent commands, owners, statuses, dates, verification, or policy. Use secret placeholders; explain destructive effects and safer verification. Execute examples only within authorized scope.
- Run only relevant checks supported by repository files or available tools. Report exact results; distinguish illustrative examples from executed checks. If a relevant check is unavailable, say so instead of claiming a pass. Do not invent checkers/CI, create new check frameworks, or expand into application pilots.
- Keep shared operational guidance generic until the project supplies verified owners, environments, access, commands, and recovery evidence. Documentation does not authorize publication, release, production operation, or external writes.

# Output

Report changed paths, sources, checks and results, unverified examples, evidence gaps, finding dispositions, remaining decisions, and review method (self or independent). Report any review limitation honestly.
