# AI Development Workflow – 3 Amigos Model

This document describes a practical workflow for building applications using a combination of:
- a human idea owner,
- architectural validation,
- and Claude Code (AI implementer).

The goal is to:
- avoid overengineering,
- respect real framework constraints,
- keep a clear trail of decisions (decision log),
- and use AI as a multiplier, not as a leader.

---

## 1. Core Concept – 3 Amigos (Without GWT)

This workflow does not use Given/When/Then formalism.
Instead, it uses the **3 Amigos concept as a conversational and decision-making model**.

### Roles

#### 🧑‍💼 Amigo 1 – Product / Owner (Human)
- Has the idea or the problem
- Knows *why* something is being built
- Defines boundaries, non-goals, and expectations
- Makes final decisions

#### 🧭 Amigo 2 – Architecture / Reality Check (ChatGPT)
- Does **not** write code
- Does **not** implement features
- Validates **decisions**, not lines of code
- Enforces constraints and warns about:
  - framework limitations
  - future technical debt
  - wrong abstractions
- Cuts options and gives clear judgments (what NOT to do)

#### 🤖 Amigo 3 – Implementer (Claude Code)
- Writes code
- Refactors code
- Follows instructions
- Works in compound mode (plan → work → review)
- Does **not** make product or architectural decisions

---

## 2. Why Claude Code Should Not Lead Architecture

Even with compound engineering, Claude Code:

- naturally gravitates toward generalized solutions
- favors abstraction and “best practices”
- proposes options instead of eliminating them
- lacks long-term pain awareness (technical debt)

As a result:
- it is unreliable as an architect
- it is weak at defining boundaries
- it often suggests solutions that are elegant but impractical

Claude is an **excellent executor**, but a poor decision maker.

---

## 3. Claude Code Constraints (Must Be Explicit)

Claude must always operate under explicit constraints.
If they are not stated, it will ignore them.

Typical constraints include:
- the framework has real limitations (e.g. Streamlit rerun model)
- no event-driven UI
- no fine-grained lifecycle control
- `session_state` must remain minimal
- expensive operations must be cached
- filesystem may be ephemeral
- no background jobs
- no “we’ll fix this later” assumptions

If these constraints are not written down, Claude will violate them.

---

## 4. Role of Architectural Validation (ChatGPT)

Architectural validation:
- does NOT require access to the code
- does NOT require diffs
- does NOT require line-by-line review

What is validated:
- **direction**
- **decisions**
- **mental model**
- **respect for constraints**

In short:
> We validate *how decisions are made*, not *what code was written*.

---

## 5. Artifacts Claude Must Produce

To enable validation without reading code, Claude must leave **decision artifacts**.

Minimum required set:

### 5.1 PLAN.md
Describes **what is intended before any code is written**.

Required sections:
- Goal
- Constraints
- Proposed Changes
- Out of Scope

### 5.2 WORK.md
Describes **what was actually done**.

Required sections:
- Changes Made
- Deviations from Plan
- Open Questions

### 5.3 REVIEW.md
Claude’s self-review from an architectural perspective.

Required focus:
- hidden risks
- framework anti-patterns
- potential technical debt
- things that may break later

---

## 6. End-to-End Workflow

1. The human has an idea or a problem
2. Human + ChatGPT conduct a **planning conversation**
3. The conversation is formalized into a **Project or Feature Brief**
4. Claude receives:
   - a clear task
   - explicit constraints
   - a requirement to produce PLAN / WORK / REVIEW
5. Claude works in compound mode
6. The human collects the `.md` files
7. ChatGPT validates:
   - decisions
   - direction
   - risks
8. The human decides:
   - merge
   - adjust
   - rollback

Code is treated as a **derived artifact**, not the source of truth.

---

## 7. Why This Model Works

- prevents premature coding
- prevents AI-driven overengineering
- creates a persistent decision trail
- enables architectural validation without code access
- scales from solo projects to more complex systems

Most importantly:
> AI is used as a **tool**, not as an author.

---

## 8. Core Principle of This Document

> Architecture is the sum of decisions made.  
> Code is only the current implementation of those decisions.

If decisions are sound, code can be fixed.  
If decisions are wrong, code will always cause problems.

---

End of document.