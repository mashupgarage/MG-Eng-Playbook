---
id: reference.ai.agent-skills
title: "Agent Skills: Template and Best Practices"
type: reference
responsible_role: Author and reviewer
status: draft
applicability: Engineers learning to author reusable agent skills
last_reviewed: 2026-10-16
---

# Agent Skills: Template and Best Practices

Agent skills are reusable instructions for repeatable tasks, team conventions, and specialized knowledge. They help an agent discover when guidance applies and load task details when needed. Use a skill when a task recurs and its steps, context, and expected result can be stated clearly.

## Key concepts

- **Frontmatter** is YAML metadata between `---` lines at the start of `SKILL.md`. In the portable Agent Skills format, `name` and `description` are required; the rest of the file is Markdown instructions. The description says what the skill does and when it applies. [The specification](https://agentskills.io/specification) defines this compact structure.
- **Discovery** is how a host finds a skill and decides whether to load it. Descriptive metadata supports discovery; complete instructions and optional resources can be loaded as needed. [The overview](https://agentskills.io/home) describes this progressive loading model.
- **Scope** distinguishes global skills intended for use across projects from project-local skills intended for one repository or workspace.
- **Precedence** determines which copy a host chooses if discovered skills share a name. Paths and precedence vary by platform; avoid duplicate names unless an intentional override is documented.

## Minimal structure

`SKILL.md` is the only required file. Add optional folders when they contain useful material for the task:

```text
skill-name/
├── SKILL.md
├── references/    # Optional detailed guidance
├── scripts/       # Optional repeatable operations
└── assets/        # Optional templates or static resources
```

Use relative paths for resources and explain when to consult them. Do not add empty folders or place essential instructions in a resource that may not be loaded.

## Choose a scope and activation style

Put a skill in the host’s documented global location when it should work across unrelated projects. Use a project-local location when it depends on that repository or workspace. Portable path shapes are:

```text
Global:       <user-config>/skills/<skill-name>/
Project-local: <project-root>/<agent-config>/skills/<skill-name>/
```

These are placeholders, not literal universal paths. Check the target host’s documentation for discovery locations and precedence.

An **automatic** skill exposes its description to the agent, which may load it when a request matches. A **manual-only** skill is intended to load only when the user invokes it. Hosts implement this differently; no portable field guarantees manual-only activation. Choose the behavior based on the task, then verify the host-specific mechanism.

### OpenCode V2 example

OpenCode V2 documents `metadata.opencode/autoinvoke: "false"` to remove a skill from model-facing discovery while leaving it registered and loadable by ID. For the skill below, the documented explicit invocation is `@deploy`. This controls discovery, not authorization.

```markdown
---
name: deploy
description: Deploy the application to production.
metadata:
  opencode/autoinvoke: "false"
---

# Deployment instructions

Follow the deployment procedure approved for this project.
```

This is a documented, version-specific example; it was not runtime-tested. See [OpenCode V2 skills](https://dev.opencode.ai/v2/docs/skills/). The example does not establish a universal manual-only field.

## Get started

Build a first skill in a few focused steps:

1. Choose one small task you repeatedly explain.
2. Choose project-local scope unless the guidance should apply across projects.
3. Create the documented skill directory and add `SKILL.md`.
4. Start with the generic template below; replace every placeholder and remove unused sections.
5. Try a request that should activate the skill and a nearby request that should not. Check the procedure and output, then clarify any confusing instructions.

## Generic `SKILL.md` template

Use this as a starting shape, not a required schema. Adapt sections to the task; do not keep empty headings or placeholder commands.

```markdown
---
name: skill-name
description: >
  [What this skill does]. Use when [specific trigger].
---

# Goal

Produce [expected result].

# Workflow

1. Inspect [input].
2. Perform [main action].
3. Run the relevant commands, if applicable.
4. Verify the result.
5. Return the output.

# Commands

- `[verified command]` — [purpose and preconditions]

# Rules

- If [condition], do [action].
- Read `references/details.md` only when [condition].
- Ask for input when required information is missing.
- Do not run destructive commands without explicit authorization.

# Output

Return [result], [verification], and [unresolved issues, if any].
```

## Complete worked example: release notes

This example is a complete skill file. The Git commands are illustrative and unexecuted. Use them only in the intended repository, with confirmed refs; for previous-release notes, confirm `<base>` is an ancestor of `<head>`. `git log <base>..<head>` lists commits reachable from head but not base. `git diff <base> <head>` compares the endpoint trees, as described in [Git’s diff documentation](https://git-scm.com/docs/git-diff).

```markdown
---
name: release-notes
description: Create user-facing release notes from a Git diff or commit range. Use for release summaries, changelogs, or product updates.
---

# Goal

Summarize user-visible changes accurately.

# Workflow

1. Confirm the repository and requested change range.
2. Review the diff and commits.
3. Group confirmed changes by user outcome.
4. Draft the notes and verify every claim against the change evidence.

# Commands

- `git diff <base> <head>` — inspect endpoint changes; confirm both refs first.
- `git log --oneline <base>..<head>` — review commits; for a previous-release range, confirm base is an ancestor of head.

# Rules

- Lead with user impact.
- Omit internal refactors unless they change behavior a reader notices.
- Do not invent benefits, fixes, or issue numbers.
- Do not modify files unless asked.

# Output

Return only applicable sections: Added, Changed, Fixed, and Known limitations.
```

## Best practices

- Describe both what the skill does and when it should activate.
- Keep `SKILL.md` focused on the normal path, important decisions, commands, and output.
- Move conditional detail into `references/`; put repeated deterministic operations in scripts only when they are useful and verified.
- Give every command a purpose and preconditions; state any required authorization.
- Use relative paths and avoid proprietary fields in a portable template.
- Check observable results, and try normal, ambiguous, missing-input, and failure cases.
- Review third-party skills, especially their instructions, scripts, and commands, before use.

## Common pitfalls

- Vague descriptions or unfinished placeholders that fail to identify real triggers, inputs, actions, and outputs.
- Turning `SKILL.md` into a manual instead of keeping the normal path there and conditional detail in references.
- Commands without a purpose, preconditions, or required authorization.
- Duplicated rules or empty optional folders that add maintenance without value.
- Assuming paths, precedence, or activation settings work the same on every platform.
- Claiming success without an observable result.

## Suggested length targets

Use these as optional editorial starting points, not specification limits:

- Description: 25–70 words.
- Main `SKILL.md`: 300–800 words or roughly 50–150 lines.
- Workflow: 4–8 short steps.
- Commands and rules: usually 3–10 focused entries each.
- Split conditional detail into references when `SKILL.md` approaches about 1,200 words.

Keep discovery metadata brief, put the normal workflow in `SKILL.md`, and load conditional detail from references only when needed.

## Related guidance

- [Building and Maintaining Agent Skills](building-and-maintaining-skills.md) — a worked walkthrough of scoping, testing, revising, and maintaining a skill.
- [AI-assisted development levels](../learning/ai/ai-assisted-development-levels.md)
- [Creating effective pull requests](../standards/source-control/creating-effective-pull-requests.md)

## Sources

- [Agent Skills specification](https://agentskills.io/specification)
- [Agent Skills overview](https://agentskills.io/home)
- [OpenCode V2 skills](https://dev.opencode.ai/v2/docs/skills/)
- [Git diff documentation](https://git-scm.com/docs/git-diff)
