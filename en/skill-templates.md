# Overmind — Skill Templates

> These are starter templates for the two skills that generate the most knowledge: Discover and Retro.
> They are not rigid scripts. Adapt the flow to your context. The structure exists to prevent you from skipping steps — not to slow you down.
> More skill templates will emerge as you practice. When you notice yourself repeating a pattern 3+ times — that's a new skill waiting to be written.

---

## Discover

### Trigger

Use Discover when:
- Starting a new project or feature and domain knowledge is unclear
- AI keeps making wrong assumptions about a specific area
- You're about to build something but can't confidently describe the business rules
- A new domain expert joins and their knowledge needs to be externalized
- You inherited legacy code/process and need to extract implicit rules

Don't use Discover when:
- You already know the domain well enough to write the rules yourself — just write them directly
- The task is a quick prototype where wrong assumptions are cheap to fix

### Input

Before starting a Discover session, prepare:
- **Scope** — what area of knowledge are you exploring? ("order cancellation flow", "pricing rules for enterprise clients", "authentication requirements")
- **Known unknowns** — what do you already know you don't know? ("I don't know what happens when a partial refund is requested")
- **Existing knowledge** — point AI to relevant files in the knowledge store so it doesn't re-ask what's already captured

### Flow

**Step 1: AI asks, human answers**

AI's role is facilitator, not teacher. AI asks open-ended questions about the scoped area. One question at a time. Each question should probe for specifics, edge cases, and exceptions.

Example:
```
AI: "When a customer cancels an order after it's been shipped, what happens?"
Human: "We offer a return label. Refund happens after we receive the item."
AI: "What if the item is damaged when returned?"
Human: "Partial refund based on condition assessment."
AI: "Who does the condition assessment? Is there a time limit?"
Human: "Warehouse team, within 3 business days of receiving. If they miss the deadline, full refund by default."
```

The session is done when:
- Questions start getting answered with "that's the same as what I already said"
- You've covered the scope defined in Input
- New questions are about edge cases too rare to matter now

**Step 2: AI structures the answers**

AI takes the raw answers and structures them into knowledge format:
- Business rules as clear, testable statements
- Decisions with reasons
- Constraints as must/must-not rules
- Open questions flagged as "unvalidated assumptions"

**Step 3: Human reviews and confirms**

Human reads the structured output. Corrects anything AI misunderstood. Confirms accuracy. This is critical — AI will misinterpret some answers. Don't skip this step.

### Output Format

Knowledge enters the store in this structure:

```markdown
## [Area]: [Topic]
Source: Discover session, [date]
Participants: [who contributed]

### Business Rules
- Orders cancelled after shipping → return label issued, refund after item received
- Damaged returns → partial refund based on warehouse condition assessment
- Assessment deadline: 3 business days. Missed deadline → full refund by default

### Decisions
- [decision]: [reason]

### Constraints
- [must/must-not rule]

### Open Questions
- What happens if the customer disputes the condition assessment? (unvalidated — needs legal input)
```

---

## Retro

### Trigger

Use Retro when:
- An iteration/sprint/task is completed
- AI produced output that required significant correction
- A bug or failure occurred that wasn't caught by existing knowledge
- You notice the same type of mistake happening more than once
- Before starting the next iteration — to capture lessons while they're fresh

Don't use Retro when:
- The mistake was trivial and already obvious (typo, syntax error)
- The fix took less effort than capturing the lesson would

### Input

Before starting a Retro session, prepare:
- **What was executed** — the task, iteration, or feature that just completed
- **What went wrong** — specific failures, wrong assumptions, rework that happened
- **What went right** — approaches that worked well (these are also knowledge worth encoding)
- **Current constraints** — point AI to existing constraints so new rules don't duplicate or contradict them

### Flow

**Step 1: Identify what happened**

Walk through the execution. AI asks targeted questions:

```
AI: "What went wrong in this iteration?"
Human: "Agent implemented payment module but assumed all currencies use 2 decimal places."
AI: "What was the actual requirement?"
Human: "JPY uses 0 decimals, BHD uses 3. We need per-currency decimal config."
AI: "Was there existing knowledge that should have prevented this?"
Human: "No, we hadn't captured currency rules yet."
```

**Step 2: Root cause → missing knowledge**

For each failure, AI helps trace back to the missing knowledge:

- Was there a rule that should have existed but didn't? → **New rule needed**
- Was there a rule that existed but was wrong/outdated? → **Rule needs update**
- Was there a rule that existed but AI didn't receive it as context? → **Process issue, not knowledge issue**
- Was there a rule that existed, AI received it, but still violated it? → **Rule needs to be clearer/more specific**

**Step 3: Encode new rules**

Each failure produces exactly 1 new rule (or 1 updated rule). AI drafts the rule. Human confirms.

**Step 4: Capture what worked**

Don't only learn from failure. If an approach worked well, encode it too:
- "Providing the full entity relationship diagram as context eliminated all FK mistakes" → convention: "always include ERD in context for data model tasks"

### Output Format

```markdown
## Retro: [Iteration/Task name]
Date: [date]
Participants: [who participated]

### What went wrong
| Issue | Root cause | Missing knowledge | New rule |
|-------|-----------|-------------------|----------|
| Currency decimal error | No currency config rules | Per-currency decimal rules not captured | "All monetary calculations must use currency-specific decimal precision. JPY=0, BHD=3, default=2." |
| ... | ... | ... | ... |

### What went right
| What worked | Why it worked | Encode as |
|-------------|--------------|-----------|
| ERD in context | AI had full relationship picture | Convention: include ERD for data model tasks |

### Updated knowledge store
- Added: [list of new rules with file locations]
- Updated: [list of updated rules with what changed]
- Flagged for review: [rules that might be outdated based on this retro]
```

---

## Creating New Skills

When you notice yourself repeating a structured interaction pattern 3+ times, extract it into a skill using this template:

```markdown
## [Skill Name]

### Trigger
When to use / when not to use

### Input
What to prepare before starting

### Flow
Step-by-step interaction between human and AI

### Output Format
How the result enters the knowledge store
```

Keep the template lightweight. A skill that takes longer to follow than to ad-hoc is a failed skill. The structure should save time, not add ceremony.
