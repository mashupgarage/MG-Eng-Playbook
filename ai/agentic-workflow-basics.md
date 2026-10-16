---
id: reference.ai.agentic-workflow-basics
title: Agentic Workflow Basics
type: reference
responsible_role: Author and reviewer
status: draft
applicability: Engineers learning to delegate bounded coding tasks
last_reviewed: 2026-10-16
---

# Agentic Workflow Basics

An agentic workflow lets you delegate a bounded implementation task while keeping responsibility for the result. You define success, scope, constraints, and evidence up front; the agent investigates, makes changes, and checks them; you review the result and decide what to accept. Start with a task whose intended behavior you can judge.

## 1. The core loop: define, act, verify

Use a simple loop:

1. **Define:** State the outcome, permitted scope, constraints, and how success will be checked. Decide what the agent should do if it encounters uncertainty or needs broader access.
2. **Act:** Let the agent inspect relevant context and make the bounded change. For difficult or ambiguous work, ask it to outline an approach before editing. Planning is a useful option, not a required mode or approval gate for every change. [OpenAI’s best-practices guide](https://learn.chatgpt.com/guides/best-practices) recommends planning for difficult tasks and gives guidance on stating goals and constraints.
3. **Verify:** Review the full diff and the reported checks. Compare behavior with the requested outcome, and ask for corrections when needed. A passing check alone does not show that the right behavior was implemented.

Clarify requirements before edits when you cannot independently judge what a correct result should be. For smaller tasks with clear expected behavior, a concise prompt and careful review may be enough.

## 2. Beginner-friendly tasks

Choose localized changes with observable results:

- **Visual or UI bugs:** Fix a layout misalignment or broken link; verify the relevant screen at the affected size or state.
- **Basic input validation:** Add a frontend check, such as requiring an email address to contain an `@`; verify both rejected input and a valid submission, following the actual product rules.
- **Utility tests:** Add tests for an existing function whose behavior is understood; check known inputs and outputs, including a meaningful edge case.

Keep the first task small enough that you can inspect the changed files and judge the evidence yourself.

## 3. Reasoning effort and task scope

Reasoning effort describes how much computational work a model is encouraged to spend on a response or task. It is a relative tradeoff: lower effort can favor speed and resource efficiency, while higher effort can support more thorough work at greater time or token cost. The exact labels, defaults, and behavior vary by model and tool. Use the supported default first, then adjust based on observed results and your task budget. A setting is not a guarantee of quality.

These examples are selection heuristics, not promises about output. Even a narrow task can be difficult when its behavior is subtle:

| Effort | Example for a bounded coding task | Typical tradeoff |
| --- | --- | --- |
| Low | Apply a specified label or style change in one known file. | Favors a quick response for a clear, familiar change. |
| Medium | Investigate and fix a localized bug with an observable expected result. | A middle ground when the agent needs to inspect context and compare options. |
| High | Trace a subtle edge case that spans several components, while keeping the requested change bounded. | Allows more thorough reasoning at higher time and resource cost. |

Task scope, reasoning effort, and permissions remain separate choices. A broad task does not automatically need broader file access, and higher effort does not grant more autonomy or permission. Define the desired outcome and file boundaries separately, and verify the result against your success criteria. Documentation describes effort as a relative thoroughness and resource tradeoff, with recommendations and available levels differing across model families. [OpenAI models](https://learn.chatgpt.com/docs/models) · [Anthropic effort](https://platform.claude.com/docs/en/build-with-claude/effort)

## 4. Architecture and models

An agent works by combining a language model with tools and feedback from its environment. It may read files, edit code, run checks, and use other available tools. The useful cycle is action followed by observed feedback, with checkpoints and a clear condition for stopping. More connected steps can add latency and cost, so keep the workflow as simple as the task allows. [Anthropic’s overview of effective agents](https://www.anthropic.com/engineering/building-effective-agents)

You do not need access to an agent’s private reasoning trace to assess its work. Ask for a concise account of files changed, checks run and their results, assumptions, and unresolved issues; evaluate those against the diff and task requirements.

## 5. Tools and costs

Depending on the product and granted access, an agent may use file tools, a terminal to run project checks, or web search for documentation. The tools available and their permissions are environment-specific. Keep the task’s permitted scope clear, and inspect changes before accepting them.

Long tasks and repeated tool use can consume more time and tokens, but costs do not follow a universal exponential rule. Monitor actual usage where the product exposes it. Some APIs can reduce the cost of repeated prompt prefixes when caching applies and a cache hit occurs; savings depend on model and configuration and are not a universal application toggle. [OpenAI prompt caching documentation](https://developers.openai.com/api/docs/guides/prompt-caching)

## 6. Guardrails, review, and recovery

Use boundaries that fit the task: name the files or areas in scope, avoid sharing secrets or unrelated private data, and ask the agent to stop and report if the task requires broader changes or an important requirement is unclear. For a first change, work in an isolated branch or learning project when available, then review the diff before integrating it. Isolation makes changes easier to inspect and discard; it is not a substitute for configuring actual tool permissions. Do not treat `.gitignore` as an access-control boundary. Set a time, usage, or retry budget that fits the task, and stop to reassess after repeated failures or when the budget is reached. There is no universal loop count that suits every task.

Before accepting work, inspect the complete diff, compare it with the stated success criteria, and confirm which checks passed, failed, were skipped, or could not run. Keep review and approval for merge or release with the responsible human. For review prompts, see the [source-control reviewer checklist](../standards/source-control/reviewer-checklist.md). For related delegation competencies, see [AI-assisted development levels](../learning/ai/ai-assisted-development-levels.md) and [Agent Skills: Template and Best Practices](skill-practices.md).

**Illustrative first task prompt** (replace the example scope and checks with facts from your project):

> Fix the misaligned submit button on the registration form at desktop width. Keep the change limited to the form’s existing UI files; do not change validation or add dependencies. First inspect the relevant component and styles. Verify the button alignment at the affected width and check that the existing form behavior is unchanged. Report the files changed, checks performed and results, and anything you could not verify. Stop and ask if fixing it requires changes outside that scope.

When the agent finishes, inspect the diff and compare the screen against the expected alignment and unchanged form behavior. If the layout still fails or the agent reports a failed check, clarify the expected result, request a focused correction, and review the new diff and evidence. If the task needs broader scope, decide whether to redefine it before more edits proceed. This example is illustrative and has not been run in a project.

## Sources

- [OpenAI: Best practices](https://learn.chatgpt.com/guides/best-practices)
- [OpenAI: Models](https://learn.chatgpt.com/docs/models)
- [Anthropic: Effort](https://platform.claude.com/docs/en/build-with-claude/effort)
- [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [OpenAI: Prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching)
