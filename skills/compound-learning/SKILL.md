---
name: compound-learning
description: Capture and codify what was learned after completing a task so that future work benefits from past effort. Use after shipping a fix, feature, or investigation — especially when the solution was non-obvious.
---

# Compound Learning

## What this is for

Every solved problem is an opportunity to make the next one easier. This skill turns completed work into findable, reusable knowledge — so the same problem is never solved from scratch twice.

The core principle: each unit of engineering work should make subsequent units easier, not harder.

## When to use it

- After fixing a non-trivial bug where the root cause was surprising.
- After completing a feature where the approach involved trade-offs worth documenting.
- After an investigation that uncovered patterns, constraints, or gotchas.
- When a solution required knowledge that is not obvious from the code alone.
- When you catch yourself thinking "I wish I had known this when I started."

## When to skip it

- The fix was mechanical and the solution is obvious from the code.
- The commit message and code comments already capture everything worth knowing.
- The knowledge is already documented elsewhere.

## Gather first

- The work you just completed — diff, commits, related files.
- Any brainstorm docs, specs, findings, or progress files from the task.
- Related past solutions if a solutions directory already exists.

## Workflow

### 1. Decide if this is worth documenting

Ask three questions about the work you just finished:

1. **What was the hardest decision?** — What required judgment, not just execution?
2. **What alternatives did you reject, and why?** — What looked promising but did not work?
3. **What would you tell someone starting this task from scratch?** — What is not obvious from the code?

If any question produces a substantive answer, proceed. If all three are "nothing interesting," skip it.

### 2. Classify the knowledge

| Type | What it captures | Structure |
|---|---|---|
| **Bug track** | Problem → symptoms → failed attempts → solution → prevention | Focus on the diagnostic journey |
| **Knowledge track** | Context → guidance → rationale → when to apply | Focus on the reusable insight |

Most completed features produce knowledge-track docs. Most debugging sessions produce bug-track docs. Pick whichever fits.

### 3. Write the solution document

**Bug track format:**
```markdown
# [Descriptive title]

## Problem
[What was broken — observable symptoms, not internal mechanics]

## What Didn't Work
[Approaches tried and why they failed — this is the most valuable section]

## Solution
[What fixed it and how]

## Why This Works
[Root cause explanation — connect the fix to the underlying issue]

## Prevention
[How to avoid this class of problem in the future]
```

**Knowledge track format:**
```markdown
# [Descriptive title]

## Context
[When and why this knowledge matters]

## Guidance
[The actual advice — concrete, actionable]

## Why This Matters
[What goes wrong without this knowledge]

## When to Apply
[Specific situations where this is relevant]

## Examples
[Concrete examples if they clarify]
```

### 4. Check for overlap

Before creating a new document, search existing solutions/docs for related content:

- **High overlap** — update the existing document instead of creating a new one.
- **Moderate overlap** — create a new document but cross-reference the existing one.
- **No overlap** — create a new document.

### 5. Make it findable

The document only compounds if future work can discover it. Ensure:

- The filename is descriptive (`solving-mount-race-condition.md` not `fix-2024-03.md`).
- The title includes keywords someone would search for.
- The document lives where convention says it should (e.g., `docs/solutions/`, project wiki, or alongside the code it relates to).
- If the project has an agent instruction file (AGENTS.md, CLAUDE.md), verify it points to the solutions directory.

### 6. Consider broader updates

Sometimes the learning is bigger than a single solution doc:

- **Pattern change?** — Update coding guidelines, style guides, or agent instructions.
- **New constraint discovered?** — Update architecture docs or decision records.
- **Recurring failure mode?** — Add it to the relevant skill's "Failure modes" section.
- **Missing test coverage?** — Add the test, not just the doc.

Do not over-rotate here. Most learnings are a single solution doc. Only escalate when the learning genuinely changes how future work should be done.

## Decision rules

- Bias toward writing. A mediocre solution doc that exists beats a perfect one you never write.
- Spend at most 10-15 minutes on documentation per task. If it takes longer, the scope is too broad — split it.
- The "What Didn't Work" section is often the most valuable part. Future solvers will try the same things you did.
- Date your documents (in filename or frontmatter). Knowledge decays — a reader should know when this was written.
- Do not document internal implementation details that are obvious from reading the code. Document the *why* — the reasoning, constraints, and trade-offs that the code cannot express.

## Failure modes

- **Documenting everything.** Not every task produces learnings worth capturing. The three-question check (step 1) is the filter.
- **Writing for an audience of zero.** If no one will ever search for this knowledge, do not write it.
- **Solution docs that describe the code.** "We added a mutex to the mount function" is not useful. "Concurrent mounts race on the stash manifest because reads and writes are not atomic" is useful.
- **Never reviewing old docs.** Solution docs can become stale. When you encounter one that is wrong or outdated, update or remove it.
- **Skipping the compound step under time pressure.** This is when it matters most. The 50/50 principle: half your time ships features, half improves the system. Even 5 minutes of documentation after a hard fix pays dividends.

## Output

A solution document in the project's convention location. Optionally, updates to broader documentation (agent instructions, guidelines, decision records) when the learning warrants it.
