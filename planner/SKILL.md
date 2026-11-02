---
name: planner
description: Create and continuously refine self-contained engineering plans through evidence-led, one-question-at-a-time discovery and explicit approval. Use implicitly for new software, substantial features, architecture changes, migrations, or complex fixes with unresolved design choices. Skip routine changes, factual questions, and implementation already covered by an approved plan.
metadata:
  short-description: Interview, design, and approve engineering plans
---

# Planner

Turn a software engineering goal into a plan that another engineer or agent can implement without the conversation. Write the plan during discovery, not only at the end. Resolve product and architecture choices with the user; leave bounded implementation details to the implementing agent.

## Activation and scope

- Apply implicitly when a described software goal needs substantial planning or unresolved decisions. An explicit request to use Planner also activates it. Respect a request to skip planning; do not force an interview onto a routine, well-specified change.
- If no goal has been described, ask for the goal before creating a file. Otherwise, create the working plan before the first discovery question, after only the inspection needed to choose its location.
- This workflow authorizes planning artifacts and in-scope research. Do not implement the software while interviewing. Approval finalizes the specification; start implementation only when the user also authorizes it, including a combined approval and instruction to proceed.

## Living plan file

1. Honor an explicitly requested destination first, then an existing repository convention. Otherwise create `work/plans/<goal-slug>-<unique-id>.md` inside the active workspace. On resume, locate and reuse the plan for this goal before creating another file; do not choose between ambiguous matches by guessing. Use a collision-safe identifier for new plans and never overwrite an unrelated plan. Report its actual path once created. If there is no writable workspace, resolve a writable destination before claiming a plan exists.
2. Read [assets/plan-template.md](assets/plan-template.md) when creating the plan. Adapt its sections to the goal. Replace template guidance with task-specific content; initially record unknowns honestly, then fill them as discovery progresses. Treat the file as temporary working material; do not commit, delete, relocate, or publish it automatically.
3. Record the original goal, status, revision, last update, constraints, confirmed facts, user decisions, proposed choices, assumptions, open questions, dependencies, and risks. Keep these states distinct. Proposals and recommendations are not agreed decisions until accepted; a low-impact inference may remain a clearly labeled assumption. Never use an assumption to conceal an undecided topic.
4. Maintain the same file continuously until the plan is complete. At every saved checkpoint it must contain all known, task-relevant planning information, not merely a progress summary or the final agreed choices. Update it after every substantive answer, repository finding, developed design detail, or integrated agent contribution, before the next question or handoff. Include partial architecture, flows, implementation details, alternatives, constraints, and pending topics as soon as they are known. Preserve still-valid information; mark corrected or superseded conclusions without leaving contradictory descriptions active. Keep each fact or decision in one authoritative place in the file and reference its ID elsewhere. This prevents duplication without losing information. Do not dump the chat transcript into it.
5. Save all information needed for implementation in this file, including summaries of external evidence and delegated findings. Cite repository paths, symbols, configuration, relevant commands, or authoritative sources for verification. Links and prior chat are supporting evidence, never substitutes for the actual agreed specification. Do not copy secrets or sensitive raw records into the plan.
6. Increment the content revision for substantive changes and update the timestamp. Keep a short review summary of what changed and the next unresolved decision; this is an index, not a replacement for the full specification. Use focused edits and check for intervening changes before overwriting content another writer may have updated. If a save fails, report it and repair the file before presenting it as current or requesting approval.
7. On resume, read the existing plan and check whether relevant source files, constraints, or user decisions changed since the recorded baseline. Continue the unresolved decision sequence instead of restarting. Revalidate only affected conclusions and propagate changes through requirements, architecture, contracts, flows, tasks, and verification. Record blocked dependencies explicitly while a conflict is unresolved. Do not silently broaden scope. Material changes to approved scope or design return the plan to draft unless the user has explicitly approved that specific revision; editorial corrections do not invalidate approval.

### Undecided topics must remain visible

- Retain every identified but undecided topic in the file, including topics not yet reached in the interview. Put the exact tag `[NEEDS USER DECISION]` beside its heading or entry in the relevant section. Do not omit an unsettled section, replace its substance with a vague placeholder, or remove a topic merely to make the plan appear complete.
- Assign each topic a stable decision ID such as D1. Make its entry in the decision register authoritative: record the decision needed, known constraints, available options and recommendation when supported, impact of leaving it unresolved, and dependent requirements/tasks. Keep the same ID and tag beside the topic in the relevant section, referencing the entry rather than duplicating its reasoning. Synchronize statuses in the same update.
- After a user decision, replace the tag with `[DECIDED]`, record the answer, rationale, and approval or evidence source, and update the affected design and tasks. If the user explicitly delegates the choice, use `[DELEGATED TO IMPLEMENTATION]` and record the bounds, authorization source, and escalation trigger. Existing instructions to leave routine details to the implementing agent count as delegation within that scope; do not ask again for each local choice. Silence does not delegate a decision, and delegated topics remain visible until resolved.
- An explicit deferral does not settle the topic. Keep `[NEEDS USER DECISION]`, record the deferral and its scope, and identify the dependent work that cannot proceed. Approval may cover a bounded scope that excludes that work when the user explicitly accepts the deferral. Otherwise, unresolved material decisions block approval. Never remove pending entries on approval or handoff.

## Evidence-led discovery

Maintain a concise working index in the file: goal, success criteria, scope, actors, constraints, decisions, assumptions, unresolved questions, dependencies, and confidence where uncertainty affects a choice. This index supplements the full known planning information; brevity must not discard details needed to understand or implement the plan.

Before each question, determine whether its answer can be verified from in-scope artifacts. Inspect those artifacts first. For repository work, identify the project shape, entry points, configuration, dependencies, affected modules, relevant tests, and documentation. Follow references only as needed to resolve the next decision. Distinguish observed behavior from proposed behavior and label unverified paths or APIs as proposed. For a new project, record the absence of an existing architecture rather than inventing repository facts. Once a search resolves the question, stop; do not explore the entire repository for completeness.

Use read-only discovery and relevant, safe checks. Do not modify product files, run destructive operations, contact people, mutate external systems, or broaden the task merely to answer a planning question. If evidence is unavailable, state the gap and ask only when its answer materially affects the plan.

Explore from foundations to consequences, resolving prerequisite choices before their dependents. Usually cover purpose and measurable success, scope and actors, inputs and outputs, existing constraints, architecture and data, interfaces and dependencies, behavior and edge cases, failures and recovery, security and privacy, performance, operations, testing, rollout, and maintenance. Scale depth to the task and explicitly mark irrelevant areas out of scope. Do not make the user answer a fixed checklist.

Classify uncertainty before choosing the next action:

- **Fact to verify:** Inspect evidence instead of asking for a preference. Record the source and what remains unverified. If missing evidence could invalidate the architecture, define the smallest bounded research task to resolve it before dependent decisions. A recommendation cannot prove technical feasibility. Do not implement a prototype without the required authorization.
- **User-owned choice:** Ask when an answer materially affects outcomes, scope, external behavior, contracts, data handling, risk, or a costly architectural commitment. Keep `[NEEDS USER DECISION]` until resolved or explicitly delegated.
- **Delegated implementation detail:** For choices already delegated by the user, record the freedom and constraints instead of asking about every helper, file name, library call, or test arrangement. Escalate only if it could change the agreed design or outcome.

Separate confirmed constraints from preferences. Compare realistic alternatives against the agreed criteria before recommending a consequential design. A low-impact assumption may support progress only when clearly labeled, reversible, and not a disguised user-owned decision. Match planning depth to uncertainty and impact, rather than a target document length or question count.

## Interview contract

- On a question-bearing turn, ask exactly one substantive question and wait for its answer before asking the next. A question may resolve one decision among alternatives; do not conceal several independent decisions in one prompt. Progress updates and artifact inspection do not require a manufactured question. Do not send a batch questionnaire or interview agenda in place of the next question.
- Every question must include a clearly labeled recommended answer, a short evidence-based rationale, and the condition that would change the recommendation when useful. For a missing goal, recommend the level of specificity to provide rather than inventing a product goal.
- Select the highest-impact unresolved decision whose prerequisites are settled. Briefly explain a dependency when it determines why this question comes next.
- Check each answer against repository evidence and earlier decisions before treating it as settled. Resolve a brief answer such as "yes" only against the one pending question. Acknowledge what changed and update every affected section, including tags and blocked task dependencies. An uncertain reply or "you decide" is not approval of the whole plan; record the scope of any delegated choice and use the next single question to resolve a material conflict.
- Challenge vague goals, unsupported assumptions, contradictions, unnecessary complexity, and missing acceptance criteria. Use concrete examples, failure cases, and realistic alternatives. Challenge only when the answer could change scope, correctness, architecture, or delivery; do not manufacture objections.
- Do not repeat settled questions without new contradictory evidence. At useful checkpoints, summarize what is agreed and identify the remaining decision with the greatest impact.
- Continue until material choices are resolved and the plan can be approved, or the user explicitly stops. If the user stops early, preserve the partial plan as draft and list the unresolved blockers. Do not infer approval from silence, elapsed time, or exhaustion of questions.

Use this structure for discovery and the final approval question:

**Current understanding:** One or two sentences about the relevant evidence or decisions. Include the plan path when it helps review.

**Recommended answer:** The choice you recommend and why; state meaningful uncertainty.

**Question:** Exactly one question that resolves the next decision.

When using a question tool, put only that single question in it; give the understanding and recommendation alongside it without asking a second question in prose.

## Engineering detail and implementation handoff

Write for a software engineer. Use precise domain terms, contracts, data structures, states, and failure semantics. Include diagrams, tables, pseudocode, or concrete examples when they clarify an actual decision. Explain the chosen design and consequential alternatives without padding.

Make the implementation section the most detailed part of the plan. Decompose the agreed design into ordered, reviewable work packages. For each package, include:

- Stable task ID, intended outcome, prerequisite task and decision IDs, and linked requirement IDs. State explicitly when an unresolved decision blocks the package.
- Existing files, symbols, tests, and interfaces to change, or clearly proposed paths for new components. Explain the actual behavior to add or replace, rather than saying only "implement backend" or "add tests."
- Relevant schemas, API/event contracts, validation rules, state transitions, error behavior, authorization boundaries, configuration, and migration/backward compatibility obligations.
- Implementation sequence and important algorithms or pseudocode where they affect correctness. Capture verified constraints; avoid fabricated exact line numbers, signatures, or commands.
- Acceptance criteria, focused verification, relevant existing test commands, and required project checks. Distinguish commands discovered in configuration, checks actually executed with their outcome, and checks merely planned for implementation. Mark commands to discover later when they cannot be verified now.
- Delegation suitability, ownership boundary, integration point, and completion evidence. For sequential work, explain which shared dependency prevents parallel execution.

Prefer an early, small end-to-end increment that validates an important contract or risk when it fits the project. Follow the actual dependencies rather than automatically separating all backend, frontend, and testing work. Include a task only when it supports an agreed requirement, a necessary enabling constraint, or a material risk; keep optional improvements outside the committed scope.

Specify task-specific details as fully as current evidence supports. Do not generate complete production code or lock down inconsequential local mechanics. Explicitly identify what the implementing agent may decide, the constraints on those decisions, and when a discovery would require returning to the user. Defer details only when they cannot materially change the approved outcome, scope, architecture, or contracts. Detail is not evidence: do not invent estimates, performance targets, verified signatures, or exact future file layouts to make a plan look complete.

## Extra agents

Identify bounded opportunities both during complex planning decisions and in future implementation. Actual delegation is conditional on available agent tools and applicable authorization; naming a candidate does not require spawning an agent. If delegation is unavailable, preserve the same work packages for sequential execution.

- During planning, good candidates include tracing an unfamiliar subsystem, checking a migration constraint, comparing a bounded architectural alternative against agreed criteria, or developing a detailed work package after its prerequisites are settled. A planning agent may research and elaborate the plan, not implement the product or settle a user-owned choice.
- For implementation, identify packages that can proceed after shared contracts are fixed, with disjoint write ownership or explicit integration sequencing. Keep shared schemas, migrations, cross-cutting changes, and final integration under a named owner. Do not describe dependent tasks as immediately parallel. Delegate only when the bounded result is worth the coordination cost; keep tightly coupled or very small work together.
- Specify each candidate's objective, inputs and evidence, scope/exclusions, prerequisite decisions/tasks, owned files or plan sections, expected output, acceptance checks, and integration owner. Record whether it is only proposed, dispatched, or integrated; do not invent agent results.
- Keep the primary planner accountable for questions and consistency. Default to a single writer for the plan: agents return findings and proposed section text, and the planner verifies and merges it. If direct edits are appropriate, allocate disjoint sections/files explicitly and reconcile them before the next user-facing decision. Prevent competing edits to the same plan sections or product files.
- Save the substance of accepted findings and decision rationale in the plan. Agent messages, identifiers, or external artifacts alone are insufficient for a self-contained handoff.

## Approval and completion

Before requesting approval, ensure the file is saved, human-readable, internally consistent, and sufficient for a fresh engineer or agent to implement. Check that:

- The goal, scope boundaries, requirements, architecture, data/contracts, important flows, and relevant operational constraints are explicit.
- Every requirement maps to implementation work and observable acceptance criteria; tasks have a coherent dependency order and realistic delegation boundaries.
- Material product and architectural decisions for the approved scope are resolved. All remaining undecided topics retain `[NEEDS USER DECISION]` in their sections and the open-decision register; any deferral is explicitly accepted and dependent work is excluded from the approved scope. Remaining assumptions and delegated implementation discretion have bounded impact, with a trigger for escalation where needed.
- The plan includes testing, rollout/recovery where relevant, risks, dependencies, and enough source context to verify its claims. No essential information lives only in the conversation or an agent's response.
- The continuously maintained file contains all currently known planning information, including partial findings and tagged pending topics. Earlier valid details have not been lost through summarization or rewriting.

Walk the primary flow and one task-relevant failure or recovery path through requirements, contracts, work packages, and acceptance checks. Check that task/decision references exist, dependencies have no cycles, pending decisions block the right work, and no task adds unagreed scope. Read the file as a fresh implementer: if starting requires guessing a material choice, resolve or explicitly defer it before approval. Treat this as a focused consistency review, not a new audit or a reason to reopen settled decisions.

Set status to `Awaiting approval`, identify the revision, and provide a concise review summary and the file link. Ask one explicit approval question with the recommendation to approve only if the plan is ready. If changes are requested, revise the same file, resolve any material uncertainty one question at a time, and present the revised plan for approval.

Only a clear user approval of the presented revision, or an unambiguous instruction to implement it, changes status to `Approved`. Record the exact approved content revision, approval evidence, approved scope and exclusions, and any accepted deferrals. Approval bookkeeping does not create a new content revision. If approval includes a change, propagate it first: approval covers the resulting revision only when the condition is precise, fully satisfied, and leaves no material choice unresolved. Otherwise present the revised plan for approval rather than approving stale or uncertain content. Save the completed record and end with the plan link and its status. Do not begin implementation unless authorized; an instruction to implement the presented plan supplies that authorization without another confirmation.
