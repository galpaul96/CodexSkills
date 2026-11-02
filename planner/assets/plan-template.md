# Engineering plan: {goal title}

Status: Draft | Awaiting approval | Approved
Content revision: {current revision; increment for substantive changes}
Last updated: {date/time with timezone when relevant}
Workspace/repository: {actual root and relevant branch/revision if available; note relevant uncommitted state}
Evidence baseline: {sources checked and any material gaps or changed constraints}
Approval: {pending, or exact approved content revision, scope, and concise user approval evidence}

Current checkpoint: {what changed since the previous checkpoint, next decision ID, and blocked tasks if any}

Use this as a working structure, not an interview checklist. Continuously update this same file throughout planning. At each saved checkpoint, it must contain all currently known, task-relevant planning information, including partial designs, repository findings, architecture, flows, implementation details, alternatives, and unresolved topics. Preserve earlier valid information; do not reduce the file to a rolling summary or postpone writing details until final approval.

Replace guidance with concrete content. During discovery, retain every identified undecided topic with the exact tag `[NEEDS USER DECISION]`, including topics the interview has not reached. Put the tag beside the topic in its relevant section and list its stable decision ID in section 8. If existing user instructions delegate a category of implementation details, mark those entries `[DELEGATED TO IMPLEMENTATION]` and record the bounds and authorization instead of asking again for each choice. Replace empty placeholders with a description of the actual gap; never remove an undecided topic to make the document appear complete. State why truly irrelevant areas are out of scope. Add or combine sections when the project needs it. Keep each fact or decision in one authoritative place and reference its ID elsewhere in this file. Include the actual specification here so a reader does not need the conversation.

## 1. Goal and success criteria

Record the original goal, the problem and intended users, the desired outcome, and observable success criteria. Preserve user constraints and the reason the work matters.

## 2. Scope and constraints

State what is included, excluded, and intentionally deferred. Record product, technology, compatibility, delivery, resource, and environmental constraints that affect the design. Distinguish fixed requirements from preferences. Record any user-granted decision authority and its limits, especially routine details left to the implementing agent.

## 3. Existing system and evidence

Describe the relevant current behavior, components, data, integrations, and tests, with repository paths/symbols and concise evidence. Separate confirmed facts from inferences and proposed additions. For a new system, state the starting environment and absence of existing components. Summarize essential evidence here even when linking sources. Identify feasibility gaps that could invalidate the design, their affected decisions/tasks, and the smallest bounded investigation that could resolve them. Distinguish a fact to verify from a choice the user must make.

## 4. Requirements and acceptance criteria

Assign stable IDs such as R1. For each functional requirement, state actor/trigger, required behavior, observable acceptance criteria, priority when useful, and implementing task IDs. Include task-relevant quality requirements such as security, accessibility, latency, throughput, reliability, or compatibility with measurable targets when justified. Do not invent targets merely to fill the template. Mark requirements blocked by pending decision IDs; update these links when a decision changes.

## 5. Architecture and rationale

Describe components and their responsibilities, boundaries, deployment/runtime shape, dependency direction, and integration points. Explain consequential technology/design choices, alternatives considered against agreed criteria, and tradeoffs. Reference decision IDs for their authoritative rationale. Include a small diagram if it improves understanding. Mark choices as proposed or agreed, and propagate changed decisions through this design and its dependent contracts, flows, and tasks.

## 6. Data and interface contracts

Define relevant entities, fields/types, relationships, constraints, invariants, storage ownership, and lifecycle. Specify API/event/interface inputs, outputs, validation, authentication/authorization, error semantics, idempotency/concurrency, and compatibility where applicable. Include concrete request/response or data examples when needed. Capture migration and retention obligations. Identify proposed names explicitly.

## 7. End-to-end flows

For each important user or system flow, give the entry condition, ordered interactions across components, state/data transitions, result, failure paths, and recovery behavior. Include relevant edge cases, retries, cancellations, concurrency, and permissions. Use stable flow IDs such as F1 when cross-references help; link requirements, contracts, and implementing tasks. A diagram supplements the flow specification rather than replacing essential behavior.

## 8. Decisions, assumptions, and open questions

Record consequential decisions with their status, rationale, supporting evidence or user answer, and impact. Identify assumptions, their confidence where material, how they can be checked, and what changes if they fail. This register is authoritative for decision details; relevant sections carry matching IDs/tags and reference it. Keep it ordered by dependency and impact, including topics not yet discussed. Each entry must include:

- **Decision ID and topic:** For example, `D1 [NEEDS USER DECISION] {actual topic}`; link it to the relevant section.
- **Decision needed:** The specific unresolved choice, known constraints, options and recommendation when supported.
- **Impact and dependencies:** What remains uncertain, prerequisite decisions, affected sections, and which requirements/tasks are blocked or need revision if the answer changes.
- **Resolution and authority:** Pending, or the user's answer, rationale, and evidence source. Use `[DECIDED]` only once resolved. For delegated choices, use `[DELEGATED TO IMPLEMENTATION]` and record the bounds, existing or new user authorization, and escalation trigger. Retain delegated entries until resolved.
- **Deferral, if any:** Keep `[NEEDS USER DECISION]` for a deferred topic, record the user's explicit deferral, and identify dependent work excluded from the approved scope.

At approval and handoff, retain every unresolved entry and its tag. State whether any material blockers remain for the approved scope; do not present deferred topics as settled decisions.

## 9. Detailed implementation plan

Start with the dependency sequence and critical integration points. Make this the most detailed section. Use one work package per coherent, reviewable outcome; do not force an arbitrary number of phases. Where useful, start with a small end-to-end increment that validates a key contract or risk. Keep dependencies acyclic and do not present blocked packages as ready for parallel execution. Every task must serve an agreed requirement, necessary enabling constraint, or material risk.

### T1. {work package outcome}

- **Requirements and dependencies:** Requirement IDs, prerequisite task and decision IDs, explicit blockers, and what becomes possible afterward.
- **Code and ownership:** Verified existing paths/symbols to change, clearly proposed new paths, and write ownership boundaries.
- **Implementation:** Specific changes in a useful order, affected behavior and contracts, relevant data/schema changes, algorithms, validation, errors, authorization, configuration, and compatibility. Include migration or integration mechanics when needed.
- **Verification and done criteria:** Observable outcome, focused checks/tests, commands discovered in configuration, and required repository checks. Distinguish checks already executed and their outcome from checks planned for implementation. Record any command that still needs discovery instead of inventing it.
- **Delegation:** Candidate or sequential work, prerequisites for parallel execution, bounded objective, required inputs, owned files/sections, expected output, integration owner, and completion evidence.
- **Implementation discretion:** Details the implementing agent can resolve, constraints it must preserve, and discoveries that require escalation.

Repeat for the remaining tasks. Include final integration and required validation as explicit work when those span packages.

## 10. Planning research and delegation record

Identify worthwhile bounded research/design tasks, if any. For each, record objective, inputs, exclusions, dependencies, owned plan sections, expected deliverable, acceptance checks, integration owner, and status (candidate/dispatched/integrated). Summarize integrated findings and their design impact in this document. State when delegation adds no value or is unavailable; do not create extra work to populate the section.

## 11. Validation strategy

Map requirements to appropriate tests and review evidence. Cover the actual cross-component risks, important failure paths, fixtures/environments, and required project checks. Separate planning-time evidence from proposed implementation checks; do not claim an unexecuted check passed. State known verification limitations. Keep routine local choices with their implementation tasks rather than duplicating them here.

Before approval, walk the primary flow and one relevant failure/recovery path through requirements, contracts, tasks, and acceptance checks. Resolve missing references, dependency cycles, inconsistent tags, stale decisions, unagreed tasks, and any material choice an implementer would still need to guess.

## 12. Delivery, operations, and recovery

Specify relevant rollout order, deployment/configuration changes, migrations, observability, operational ownership, compatibility windows, rollback/recovery, and maintenance implications. Mark areas out of scope when justified, such as deployment for a purely local library change.

## 13. Risks and dependencies

Record material risks, external dependencies, likelihood/impact where useful, mitigation, and early warning or escalation trigger. Distinguish accepted residual risk from unresolved blockers.

## 14. Approval and implementation handoff

Record the exact content revision presented for review, explicit approval evidence when received, approved scope/exclusions and conditions, and whether implementation is authorized. Approval bookkeeping does not increment the content revision; substantive changes require establishing approval of the changed revision. Summarize the starting task, required prerequisites, material remaining uncertainty, and the boundary of implementing-agent discretion. List all remaining `[NEEDS USER DECISION]` IDs, their explicit deferrals if accepted, and dependent work that cannot proceed. This section must allow a fresh engineer or agent to start from this file and the repository without consulting the chat.
