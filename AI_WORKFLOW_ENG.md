# AI Development Workflow – 3 Amigos Model

This document describes a practical, repeatable workflow for building applications using a combination of:
- a human idea owner,
- architectural validation,
- and Claude Code (AI implementer).

The goal is to:
- avoid overengineering,
- respect real framework constraints,
- keep a clear and persistent trail of decisions,
- and use AI as a multiplier, not as a leader.

This workflow is intentionally **decision-driven**, not chat-driven.

---

## 1. Core Concept – 3 Amigos (Without GWT)

This workflow does not use Given/When/Then formalism.
Instead, it uses the **3 Amigos concept as a conversational and decision-making model**.

The focus is on:
- shared understanding
- early clarification of constraints
- cutting wrong options early
- making decisions *before* writing code

---

## 2. Roles and Responsibilities

### 🧑‍💼 Amigo 1 – Product / Owner (Human)

- Has the idea or the problem
- Knows *why* something is being built
- Provides domain knowledge and priorities
- Defines boundaries, non-goals, and expectations
- Owns trade-offs and makes final decisions

This role is the **source of truth** for intent and value.

---

### 🧭 Amigo 2 – Architecture / Reality Check (ChatGPT)

- Does **not** write code
- Does **not** implement features
- Validates **decisions**, not lines of code
- Enforces constraints and long-term thinking
- Identifies:
  - hidden risks
  - framework limitations
  - future technical debt
  - wrong abstractions
- Explicitly cuts options and states what **should NOT be done**

This role focuses on **directional correctness**, not implementation details.

---

### 🤖 Amigo 3 – Implementer (Claude Code)

- Writes code
- Refactors code
- Follows explicit instructions
- Works in compound mode (plan → work → review)
- Produces decision artifacts (PLAN / WORK / REVIEW)
- Does **not** make product or architectural decisions

Claude Code is treated as an **executor**, not an author.

---

## 3. Why Claude Code Should Not Lead Architecture

Even with compound engineering, Claude Code:

- naturally gravitates toward generalized solutions
- favors abstraction and “best practices”
- proposes options instead of eliminating them
- optimizes for elegance over long-term maintainability
- lacks lived experience with technical debt

As a result:
- it is unreliable as an architect
- it is weak at defining boundaries
- it often suggests solutions that are technically correct but practically harmful

Claude Code excels at **implementation**, not **judgment**.

---

## 4. Claude Code Constraints (Must Be Explicit)

Claude must always operate under **explicitly stated constraints**.
If they are not written down, Claude will implicitly invent its own.

Typical constraints include:
- the framework has real limitations (e.g. Streamlit rerun model)
- no event-driven UI
- no fine-grained lifecycle control
- `session_state` must remain minimal
- expensive operations must be cached
- filesystem may be ephemeral
- no background jobs
- no “we’ll fix this later” assumptions

If these constraints are not explicitly defined, Claude will violate them.

---

## 5. Brainstorm Phase – Proper Use and Positioning

Claude Code supports a **Brainstorm phase**, which is useful but potentially dangerous if misused.

### 5.1 What Brainstorm IS

- a **divergent thinking phase**
- used to explore **alternative approaches**
- optimized for breadth, not correctness

Brainstorm is about *possibilities*, not decisions.

---

### 5.2 What Brainstorm IS NOT

Brainstorm is **not allowed** to:
- define scope
- change constraints
- introduce new features
- own architecture decisions
- decide priorities

Brainstorm without boundaries always leads to scope creep.

---

### 5.3 Correct Placement in This Workflow

Brainstorm is **never the first step**.

Correct order:
1.	Human idea / problem
2.	Human + ChatGPT planning and constraints
3.	Claude Brainstorm (within fixed boundaries)
4.	ChatGPT cuts options and selects direction
5.	Claude Planning (compound)
6.	Claude Implementation & Review

Brainstorm is allowed **only inside a clearly defined box**.

---

### 5.4 Brainstorm Rules for Claude

During Brainstorm, Claude must:
- stay within defined constraints
- not expand scope
- not introduce new features
- not change architecture assumptions
- explicitly list trade-offs and risks

Brainstorm without human judgment is informational, never authoritative.

## 6. Role of Architectural Validation (ChatGPT)

Architectural validation does NOT mean code review.

ChatGPT in this workflow:
- does NOT need access to the repository
- does NOT read diffs
- does NOT review individual lines of code

Instead, it validates:
- overall direction
- decisions that were made
- mental model behind the solution
- respect for defined constraints
- long-term maintainability risks

In short:
We validate HOW decisions are made, not WHAT code was written.

This allows architectural validation even when:
- sessions expire
- repositories are not accessible
- code changes frequently

---

## 7. Decision Artifacts as the Source of Truth

Chat sessions (ChatGPT or Claude) are ephemeral.
Documents are persistent.

Therefore:
No critical context should live only inside a chat conversation.

All important decisions must be written down.

### Required Decision Artifacts

Claude Code must always produce the following artifacts:

PLAN.md  
Describes intent BEFORE coding.
Includes:
- Goal
- Constraints
- Proposed Changes
- Out of Scope

WORK.md  
Describes what was ACTUALLY done.
Includes:
- Changes Made
- Deviations from Plan
- Open Questions

REVIEW.md  
Claude’s self-review from an architectural perspective.
Includes:
- hidden risks
- framework anti-patterns
- potential technical debt
- things that may break later

These documents enable architectural review WITHOUT code access.

---

## 8. Sessions vs Documents (Critical Distinction)

Chat sessions are temporary.
They may expire, reset, or become unavailable.

Documents are the only reliable long-term memory.

Rules:
- Never rely on a chat session as the sole source of context
- Always externalize decisions into documents
- Treat documents as canonical input for future sessions

### Canonical Documents

AI_WORKFLOW.md  
Defines HOW work is done.

PROJECT_BRIEF.md  
Defines WHAT is being built.

Feature briefs or decision logs  
Capture incremental decisions over time.

Any future ChatGPT or Claude session can resume work by providing these documents.

---

## 9. ChatGPT’s Role Across Sessions

ChatGPT is not long-term memory.
ChatGPT is an architectural reviewer.

When provided with the documents:
- ChatGPT can fully reconstruct context
- validate decisions
- detect risks
- suggest corrections

Continuity is achieved through documents, not through session persistence.

Key rule:
If a future session has the documents, it has the project.

## 10. End-to-End Workflow Summary

This workflow follows a strict order to avoid confusion and AI-driven drift.

1. The human has an idea or problem
2. Human + ChatGPT clarify:
   - the real problem
   - constraints
   - non-goals
3. The outcome is written into a Project or Feature Brief
4. Claude Code performs a Brainstorm phase strictly within defined boundaries
5. ChatGPT reviews brainstorm results and cuts options
6. Claude Code enters Planning mode (compound)
7. Claude Code implements and reviews
8. Claude Code produces PLAN / WORK / REVIEW documents
9. ChatGPT validates decisions using those documents
10. The human decides:
    - merge
    - adjust
    - rollback

Code is treated as a derived artifact, never as the source of truth.

---

## 11. Why This Workflow Works

This model:
- prevents premature coding
- prevents AI overengineering
- forces decisions to be explicit
- creates a persistent trail of reasoning
- allows architectural validation without code access
- scales from small personal tools to larger systems

Most importantly:
AI is used as a tool, not as an author.

---

## 12. Core Principle

Architecture is the sum of decisions made.  
Code is only the current implementation of those decisions.

If decisions are sound, code can be fixed.  
If decisions are wrong, code will always cause problems.

---

End of document.