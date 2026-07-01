---
name: goal-prompt-composer
description: Create concise loop-based Goal prompts from rough objectives. Use when the user wants an informal goal turned into an iterative execution prompt with a work loop, completion criteria, validation checks, constraints, stop conditions, progress reporting, and optional allocation across subagents, threads, or parallel workstreams.
---

# Goal Prompt Composer

## Overview

Transform a vague or simple objective into a compact, loop-based prompt suitable for starting or guiding a Goal. Preserve the user's intent, add operational clarity, and make the executor repeat small cycles of action, verification, and decision-making until the goal is complete or blocked.

## Workflow

1. Identify the core objective in one sentence.
2. Infer missing operational details conservatively from the user's wording and available context.
3. Define a short loop that repeats: inspect, choose the next small action, execute, verify, decide whether to continue.
4. Add only the conditions that make progress and completion observable: loop checks, done criteria, validation, constraints, stop conditions, and delegation guidance.
5. Ask a question only when ambiguity would change the actual target, risk profile, allowed scope, or loop termination.
6. Output the final prompt first. Include notes only when the user asked for rationale or when an assumption materially affects execution.

## Prompt Shape

Prefer this compact structure:

```text
Goal: <one concrete outcome>

Loop:
1. Inspect the current state and identify the smallest useful next step.
2. Do that step.
3. Verify the result with <check, command, review, or artifact>.
4. Decide: continue, adjust approach, ask for input, or stop as complete/blocked.
5. Repeat until the completion criteria are met or a stop condition occurs.

Complete when:
- <observable completion condition>
- <quality or acceptance condition>

Verify by:
- <test, command, review, artifact check, or reasoning check>

Constraints:
- <scope, safety, time, dependency, style, or non-goal constraint>

Stop if:
- <condition that should pause, ask, or mark blocked>
- <repeated failure, missing dependency, destructive action, or unclear requirement>

Work allocation:
- <main thread does X; subagents/parallel threads do Y only if useful>

Report:
- After each meaningful loop, briefly state what changed, what was verified, and the next decision.
- Final report: <summary, evidence, remaining risks>
```

Omit sections that would add no value. Keep most outputs between 130 and 260 words unless the user requests detail.

## Guidance

- Write in the same language as the user's request unless they specify otherwise.
- Use imperative, agent-facing wording.
- Prefer loop instructions over a long one-shot plan.
- Make each loop small enough that verification can happen before the next step.
- Make completion conditions measurable rather than motivational.
- Make verification concrete: commands, file checks, screenshots, comparison criteria, citations, or manual review points.
- Include constraints that prevent overreach, such as "do not change unrelated files", "do not spend money", "do not use network unless needed", or "preserve existing behavior".
- Include stop conditions for repeated failures, destructive actions, missing credentials, unclear requirements, safety/legal/financial risk, or external dependency blockers.
- Mention subagents or separate threads only when parallelism would reduce risk or time: independent research, test reproduction, code review, design critique, data inspection, or long-running alternatives.
- Assign subagents to independent loops with clear inputs and merge criteria. Do not assign them to work that needs shared mutable state unless coordination is explicit.
- Avoid over-specifying implementation when the executor should discover the best approach from context.

## Examples

User objective:
```text
README を整えて
```

Goal prompt:
```text
Goal: Improve the README so a new user can understand what the project does, how to set it up, and how to verify it works.

Loop:
1. Inspect the README and nearby project files for the next missing or stale section.
2. Update only that section.
3. Verify the change against the repository files and any referenced commands.
4. Decide whether another section needs work, the approach needs adjustment, or the README is complete.
5. Repeat until the completion criteria are met or a stop condition occurs.

Complete when:
- The README has clear purpose, setup, usage, verification, and troubleshooting sections.
- Existing facts are preserved and unsupported claims are avoided.

Verify by:
- Read the final README end to end for broken commands, missing prerequisites, and stale references.
- Spot-check referenced commands against available project files.

Constraints:
- Do not change application code unless a README command is demonstrably wrong.

Stop if:
- Required behavior cannot be inferred from the repository.
- A command or feature claim cannot be verified without missing credentials or external systems.

Work allocation:
- Main thread inspects repo structure and edits the README loop by loop. Use a subagent only for an independent accuracy pass if the project is large.

Report:
- After each meaningful loop, note the section changed and how it was checked. Final report summarizes changed sections and any unverified commands.
```
