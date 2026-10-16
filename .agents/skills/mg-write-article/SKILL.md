---
name: mg-write-article
description: Draft or substantively rewrite focused Markdown articles for this repository’s MG Engineering Playbook. Use when creating or materially revising article content, not for general review.
---

# Goal

Turn the supplied brief and verified source packet into clear, complete playbook prose for its intended reader. This skill covers composition only; the [maintenance workflow](../mg-maintain-playbook/SKILL.md) owns research, source verification, collaboration, review, and integration. Do not restart or redelegate that workflow.

# Workflow

1. **Read the handoff.** Use the supplied reader, outcome, article type, destination, applicability/version, canonical examples/contracts, adopted MG decisions, and verified public-source packet. Default to an MG engineer comfortable with programming but new to the topic or project; adapt for onboarding, leads, reviewers, or learners. Ask the workflow owner only when a missing detail materially blocks composition.
2. **Choose a shape.** Use the supplied article type and examples. Follow [content contracts](../mg-maintain-playbook/references/content-contracts.md) when applicable. Do not search for local conventions or independently discover/research sources; ask the workflow owner for missing inputs.
3. **Compose.** Use plain, direct language, descriptive headings, and examples that clarify the task. Keep only sections useful to this article type and audience. Cite supplied public sources near supported claims and include a concise **Sources** or **References** section with their direct links. Include project-specific commands only when supplied and verified for the stated environment.
4. **Fit the length.** As a soft editor heuristic, start around 400–800 prose words for a focused article; shorter is fine when complete. This is not policy or a claim of optimality. Complex procedures may need 800–1,200 words; above 1,200, consider splitting by task or linking deeper reference material. Do not cut prerequisites, verification, recovery, or useful examples to meet a count. Exclude code and source lists when estimating prose length. Honor user-specified audience, length, and format.
5. **Edit against the packet.** Check clarity, structure, internal consistency, and whether each cited source entry matches the support supplied. Do not browse, test public access, refresh docs, independently fact-check, or validate MG policy adoption. If a claim needs evidence, a source is missing/unverified/private, or the packet conflicts, return a `research-needed` gap to the workflow owner; do not invent or silently fill it.

# Rules

- Use internal briefs and pages only as supplied context for scope or adopted decisions. Never place private task details, internal admin documents, Trello cards, PR discussions, private Drive/chat material, ignored work files, client identifiers, or confidential examples in the article or its sources.
- Only use public sources and claim support marked verified by the workflow owner. A public-looking URL or approval label is not enough. Public technical evidence does not establish MG policy adoption.
- If the required source packet is incomplete, leave unsupported claims out and return the gap; do not perform source research yourself or claim source access was checked.

# Output

Return the article in the assigned Markdown file or as complete draft text when no writable destination is assigned. Include the supplied relevant public citations. Separately report the intended reader, citations used, unverified examples, and `research-needed` or scope gaps. Do not claim that you verified sources or publish/share the article.
