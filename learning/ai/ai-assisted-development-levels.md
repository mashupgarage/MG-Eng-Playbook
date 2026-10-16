---
id: learning.ai.assisted-development-levels
title: AI-Assisted Development Levels
type: learning
responsible_role: Author and reviewer
status: draft
applicability: Engineers learning to use AI for development work
last_reviewed: 2026-10-16
---

# AI-Assisted Development Levels

These four cumulative maturity levels describe how reliably you can use AI to deliver development work. Reaching a level means you can perform its workflow consistently and demonstrate the earlier levels too; trying it once is not enough. Use earlier workflows whenever they suit the task. At every level, you remain responsible for the result. Level 3, Delegate (Agentic), is the recommended minimum learning target in this draft; this is not adopted company policy.

## 1. Ask (Chatbot)

**What it means:** AI explains or suggests; you do the work. Use it to understand code, errors, or documentation.

**Registration-form example:** Ask where the form handles the supplied rules: require a name, require a valid email, show errors beside fields, block invalid submissions, and preserve valid submissions. Ask AI to explain the current submission flow and point out likely validation locations and edge cases without editing code. Check the explanation against the source before making changes.

**Your responsibility:** Provide only relevant context you are allowed to share. Confirm requirements yourself; verify explanations against the code and authoritative documentation.

**Watch out:** A confident answer can still be wrong or invent business rules. Do not use a fix you cannot explain.

**Ready to Collaborate when:** Across multiple questions, you can explain the relevant code, identify uncertainty, and check important answers. You can also review and test a small generated change.

## 2. Collaborate (Generator)

**What it means:** AI drafts a bounded function, test, component, query, or documentation section. You refine the draft and integrate it yourself.

**Registration-form example:** Give AI the form rules, existing validation helper, and a relevant project example. Ask it to draft a validation function and focused tests. Inspect and refine the draft, then integrate it yourself. Check that blank names and invalid emails produce field errors and are blocked, while valid submissions still work.

**Your responsibility:** Give enough context to fit existing code and conventions, and state what the draft must do. Review requirements and test assertions as carefully as the implementation; then verify the integrated result.

**Watch out:** AI may invent APIs or write tests that repeat its own mistaken assumptions. Check behavior independently against the supplied rules and known results.

**Ready to Delegate when:** Across multiple changes, you can refine and integrate generated work correctly, define success and permitted files, and verify the complete result.

## 3. Delegate (Agentic)

**What it means:** You delegate implementation instead of writing the code manually. The agent reads relevant files, applies code and tests, runs checks, and refines its work. You define the goal and boundaries, then review the completed changes.

**Registration-form example:** Give the agent the form rules, allowed files, constraints, and required checks. Ask it to use existing helpers, preserve API behavior, and avoid new dependencies. Let it implement and test the change. The agent should stop if the task needs a wider scope. When it finishes, inspect the full diff and check report, verify the behavior yourself, and send corrections back for implementation when needed. Confirm the revised diff before accepting the work.

**Your responsibility:** Define success, scope, constraints, and stopping conditions before work begins. Check all applied changes and evidence afterward. Require the agent to report failed, skipped, or unavailable checks and unresolved questions. You retain responsibility for approval to merge or release.

**Watch out:** A vague goal can invite unrelated edits. Passing tests alone does not prove that the requested behavior is correct; clarify requirements and verify the form’s valid and invalid cases.

**Ready to Orchestrate when:** You can repeatedly delegate bounded work, review it accurately, and define clear dependencies, handoffs, and checks between stages.

## 4. Orchestrate (Orchestrator)

**What it means:** A repeatable automated workflow connects specialized agents through defined roles and handoffs. Requirements, changes, and check results pass between stages automatically. The workflow routes findings for bounded correction and stops when failures remain unresolved. You review the combined result after execution. This is an optional extension of delegation.

**Registration-form example:** An implementation agent makes the change from the supplied form rules. The workflow automatically passes those requirements and the resulting changes to a specialized checking agent, which verifies blank-name and invalid-email errors, blocked invalid submissions, and preserved valid submissions. It passes results to a review agent, routing findings back for a limited correction cycle. The workflow stops on unresolved failures and returns the final diff and evidence for your review.

**Your responsibility:** Define each agent’s role, inputs, outputs, dependencies, retry limits, and stop conditions. Check that automated handoffs preserve the original requirements and enough context. Review the combined changes, check results, and unresolved items after the workflow stops. Merging and release remain human decisions.

**Watch out:** Automation can repeat mistakes or lose context between stages. Stop when a failure remains unresolved, and avoid a workflow whose coordination adds more complexity than value.

**Ready to expand when:** A small automated workflow passes requirements, changes, and results reliably; bounded corrections and stop conditions work; and you can verify the combined outcome. Expand only when the workflow’s handoffs and checks remain understandable.

## Good habits at every level

Use only relevant context you are allowed to share, and keep credentials and unrelated private data out of prompts. State the intended result and important constraints. Read AI’s output critically, check assumptions, and use meaningful tests or manual checks. Distinguish checks that passed from those that failed, were skipped, or could not run. Take responsibility for the final result at every level.

## Where to start

Begin at Ask with a small function whose behavior you already know. Ask AI to explain its inputs, output, and one example without rewriting it. Compare the answer with the source and a check result you understand. Then ask it to draft one test with a known expected result; review the test and run it yourself.

Next, try a small, reversible bug fix in an isolated branch or learning project. State success, permitted files, constraints, and expected checks; let an agent implement and test it. Review the diff and reported results, and ask it to implement any needed corrections. The examples in this article are illustrative and unexecuted; they assume no particular project, test command, or environment.

## Further reading

- [Developer competencies](../competencies/README.md)
- [Agent skills reference](../../ai/skill-practices.md)
- [Source-control reviewer checklist](../../standards/source-control/reviewer-checklist.md)
- [Building effective agents (Anthropic)](https://www.anthropic.com/engineering/building-effective-agents) — supports general concepts such as connected workflows, clear stopping conditions, and human review; it does not define these four levels.
