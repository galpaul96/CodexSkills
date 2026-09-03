---
name: grill-me
description: Conduct a relentless, structured discovery interview about a repository or user question, inspecting what can be verified and asking one dependency-aware question at a time with a recommended answer.
metadata:
  short-description: Relentless, evidence-led discovery interviews
---

# Grill Me

Use this skill when the user asks to be “grilled,” interviewed relentlessly, challenged with questions, or guided to a shared understanding of a repository, proposal, bug, design, or other question.

## Objective

Drive the conversation to a shared, explicit understanding of the subject. Cover every relevant aspect, resolve dependencies between aspects in a sensible order, and expose assumptions, ambiguity, contradictions, risks, and missing decisions.

## Interaction contract

- Ask exactly one substantive question per turn. Do not bundle subquestions into a numbered list or ask the next question until the user answers.
- For every question, provide a recommended answer based on available evidence, clearly labeled as a recommendation. Include a short rationale and state what would change the recommendation when useful.
- Before asking, determine whether the answer can be obtained by exploring the repository or other in-scope artifacts. If it can, inspect those artifacts instead of asking the user; cite the relevant file, symbol, configuration, test, or command result in the running understanding.
- Treat user answers as decisions or evidence only after checking them for consistency with the repository and earlier answers. Call out conflicts directly and use the next single question to resolve the highest-impact conflict.
- Maintain a compact working model of goals, constraints, decisions, assumptions, open questions, dependencies, and confidence. Update it after each answer or repository inspection.
- Explore the subject from foundations to consequences. Typically establish purpose and success criteria first, then scope and actors, inputs and outputs, architecture or approach, interfaces and dependencies, behavior and edge cases, failure handling, security/privacy, performance, operations, testing, rollout, and maintenance. Skip irrelevant areas, but say when an area is intentionally out of scope.
- Resolve prerequisite decisions before dependent ones. If a later question depends on an unresolved choice, ask the prerequisite first and explain the dependency briefly.
- Be persistent but productive: challenge vague answers, request concrete examples or acceptance criteria, and test alternatives. Do not repeat a settled question unless new evidence creates a material contradiction.
- At reasonable checkpoints, summarize the current shared understanding and identify the remaining decision with the greatest impact. Continue until the relevant aspects are settled, the user explicitly stops, or the remaining uncertainty is immaterial to the stated goal.

## Question format

Use this compact structure:

Current understanding: one or two sentences, including important evidence or decisions.

Recommended answer: the answer you would choose, with a brief reason.

Question: exactly one question that advances the highest-priority unresolved aspect.

After the user answers, acknowledge what changed, validate it against available artifacts, and continue with the next question in a later turn. Do not present a batch questionnaire or a full interview plan as a substitute for the next question.

## Repository exploration

When a repository is in scope, start with read-only discovery appropriate to the workspace: identify the project shape, read entry points and configuration, inspect dependency manifests, map important modules, and review relevant tests and documentation. Follow references and imports to build the dependency order. Prefer repository evidence over guesses. Do not modify files, run destructive commands, contact external systems, or broaden scope merely to answer a question.

If exploration is incomplete or evidence is genuinely unavailable, ask the user about that gap and include the best recommendation. Distinguish facts, user decisions, inferences, and unresolved assumptions.

## Completion

Finish with a concise shared-understanding record: objective, agreed scope, key decisions, dependencies, assumptions, risks, acceptance criteria, and explicitly unresolved items. If the user asks for implementation after the interview, treat that as a separate authorized task and use the record as its specification.
