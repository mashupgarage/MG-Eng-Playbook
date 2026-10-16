---
name: skill-practices
description: Create, revise, or review reusable agent skills using the playbook's skill practices. Use when turning a repeatable task or article into a SKILL.md workflow, improving skill discovery and scope, or reviewing skill structure and verification. Do not use for ordinary tasks that merely invoke an existing skill.
---

# Goal

Produce a focused, usable agent skill with clear activation criteria, actionable instructions, and observable verification. Adapted from [Agent Skills: Template and Best Practices](../../../ai/skill-practices.md); consult the article when examples or additional rationale are needed.

# Workflow

1. **Define the task.** Identify the recurring request, inputs, expected result, and nearby requests that should not activate the skill. For an article conversion, extract operational decisions and constraints instead of copying explanatory prose. Ask for missing information only when it materially affects the result.
2. **Choose scope and host.** Respect the requested destination. Otherwise prefer project-local scope for repository-dependent guidance and global scope for guidance intended across projects. Inspect existing skills before creating a duplicate. Check the target host's current documentation when discovery paths, precedence, or activation settings matter; do not assume these are portable.
3. **Write discovery metadata.** Use a short, descriptive, lowercase hyphenated name matching the folder. Start SKILL.md with YAML frontmatter containing `name` and `description`. State what the skill does and when it applies, adding a boundary where it prevents likely misrouting. Keep host-specific settings separate from the portable core where practical.
4. **Write working instructions.** State the intended outcome, normal workflow, important decisions, required context, and expected output. Include guidance that changes the agent's decisions or improves its work. Replace scaffold placeholders and remove unused headings. Treat example structures and length targets as optional editorial aids.
5. **Add resources selectively.** Keep essential instructions in SKILL.md. Move substantial conditional detail into relative `references/` files and state when to read them. Add scripts for useful repeatable operations and assets when the output needs them. Avoid empty optional folders, duplicated rules, and copied manuals.
6. **Review and verify.** Check metadata, resource links, scope, commands, and observable outputs. Use an available host validator when appropriate, and run new or changed scripts in an authorized test context. Try a matching request and a nearby nonmatching request; exercise ambiguity, missing inputs, and failures when relevant. Distinguish manual scenario review from actual host activation or execution tests.

# Decisions and constraints

- Preserve the user's task, chosen tools, destination, and authorization. Activation settings do not authorize external writes or destructive operations.
- When automatic versus explicit-only activation matters, use the host's documented mechanism. Preserve existing settings unless asked to change them; do not present proprietary fields as portable conventions.
- Give commands a purpose and preconditions. Confirm repository context, paths, and refs as applicable. Label illustrative commands as unexecuted; do not invent successful runs or required checkers.
- Before using a third-party skill, inspect its instructions, scripts, and commands for relevance and unintended effects.
- Verify meaningful results rather than only wording or headings. A valid file does not prove discovery, correct task execution, or useful behavior.
- For review-only requests, return evidence-backed findings and suggested corrections without rewriting files unless requested.

# Output

Return created or changed skill paths, a brief description of trigger and scope, checks performed and results, and remaining gaps. For reviews, identify actionable findings with file locations and consequences. Report self-review and independent review accurately; do not imply runtime testing when only static checks were performed.
