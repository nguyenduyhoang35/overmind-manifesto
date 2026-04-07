# Overmind

### A Knowledge-Driven Development Manifesto

> You don't need AI to execute faster.
> You need AI to execute **correctly**.
> And "correctly" depends entirely on the quality of knowledge you give it.

---

## The Real Problem

Look back at the times AI gave you poor output. It wasn't because the model was bad. It wasn't because the prompt was wrong. It was because you didn't know clearly what you wanted — or you knew but couldn't express it.

You say "build an order management feature." AI builds something. Looks reasonable. But it assumes 1 order = 1 seller, while your business allows 1 order with multiple sellers. It assumes cancel = immediate refund, while the actual flow requires approval. Every wrong assumption = rework. Rework costs more than building from scratch.

You say "write a marketing strategy for a new product." AI produces something professional-looking. But it assumes the target audience is B2C, while your product is B2B. It assumes a big budget for paid ads, while you're bootstrapping. Same problem: AI lacks knowledge about your specific context.

This isn't AI's fault. This is the fault of **letting AI execute without giving it sufficient knowledge.**

This problem isn't limited to software development. Any field where you use AI to execute — writing content, data analysis, process design, market research, system operations — hits the same bottleneck: AI executes based on the knowledge you provide. Good knowledge → good output. Missing knowledge → AI assumes → wrong output.

Prompt engineering, context engineering, harness engineering — all solve "how to make AI execute better." But they share a hidden assumption: **you already know clearly what you want.** If you're not clear, no pipeline, however elegant, will run in the right direction.

Overmind solves at a deeper layer: **before discussing execution, make sure the knowledge is right.** This principle applies to any field — software development is just where it's most visible because the feedback loop is fast (code runs or doesn't run), but this thinking transfers to any domain where AI plays an execution role.

---

## The Core Idea

### What Is Knowledge?

Knowledge is not a document. Not data. Not information.

**Knowledge is anything that, if AI doesn't know it, it will have to assume — and that assumption could be wrong.**

"Orders under $500 don't need approval" — that's knowledge. If AI doesn't know, it will assume all orders need approval, or none do. Both are wrong.

"Use PostgreSQL because we need JSONB + full-text search" — that's knowledge. Not just the decision but the reason. When 6 months later someone asks "why not MongoDB?" — the answer is already there.

"Last time the agent kept recreating files that already existed in the worktree" — that's also knowledge. A lesson from a mistake, encoded so it won't repeat.

Knowledge comes in many forms: business rules, technical decisions, constraints, terminology, lessons from mistakes, external system behaviors, validated assumptions, unvalidated assumptions. Which form matters most depends on the project and changes over time. There's no fixed list — you'll recognize what knowledge needs to be captured when you see AI assume wrong because it was missing.

### Knowledge Determines Output Quality

Output is downstream of knowledge. When knowledge is right, AI execution is surprisingly accurate. When knowledge is wrong or missing, no tool can save the output. This is true for code, for content, for analysis, for any output AI produces.

This isn't theory. A real project ran 21 iterations with AI agents. First iteration, agents violated 7 guidelines due to incomplete knowledge — quality reached 84%. By iteration 21, the same AI, same model, but knowledge had accumulated through 21 learning cycles — quality reached 100%, all 106 tests passed, none skipped.

The 84% → 100% difference came **entirely** from knowledge, not from the model or prompt.

### Knowledge-First: Invest in Knowledge Before Execution

The investment ratio between knowledge and execution isn't fixed — it depends on how well you know the domain, the task's complexity, and the cost of getting it wrong.

New project in an unfamiliar domain? Most initial effort goes to discovering and capturing knowledge. Project that's run 20 iterations with a comprehensive knowledge store? Effort is mostly execution since knowledge is ready. PoC that needs to validate an idea in 1 day? Nearly all effort on execution, capture a few notes if needed.

The principle isn't "always spend X% on knowledge" but rather: **don't execute until you believe the knowledge is sufficient for AI not to assume important things.** Sometimes sufficient means 10 minutes writing down 3 decisions. Sometimes it means 1 week interviewing domain experts. You'll sense it — and over time, you'll sense it more accurately.

### Humans Recognize Patterns, AI Executes Patterns

This is the most accurate division of labor between humans and AI in any field. Humans are good at recognizing "every time AI writes a proposal for an enterprise client, it always forgets to mention compliance requirements." AI is good at following the rule "when writing proposals for enterprise clients, always include a compliance section." Humans discover patterns, encode them as rules, AI follows the rules forever.

In software: "every time agents implement a cross-context feature, they always forget to check the event contract" → rule: "check event contract before implementing."

In content: "every time AI writes a blog post, it uses a tone too formal for our audience" → rule: "conversational tone, no jargon, write as if talking."

Same pattern everywhere. This is also why someone with 2 years of experience who can recognize patterns is more valuable than someone with 5 years who only follows checklists. Anyone can follow a checklist — AI follows them even better than humans. Recognizing when a new checklist is needed — that's the human's job.

### Knowledge Becomes Better Than Any Single Contributor

A natural property of this approach: when AI has access to the knowledge store during interaction with humans, the knowledge produced is more accurate than the original input. Humans provide domain truth, AI cross-references with existing knowledge — the result is refined knowledge that neither side could create alone. The knowledge store becomes something smarter than any individual contributor, because it accumulates and connects everyone's perspectives over time.

---

## Three Things You Need

Not a complex framework. Not an enterprise system. Three things:

### 1. A Place to Record Knowledge

Call it a knowledge store, knowledge base, or even just a structured folder — doesn't matter. What matters is:

**All important knowledge must be in one place that both humans and AI agents can read.** Not in your head. Not in last week's Slack message. Not in meeting notes nobody reads again.

What does knowledge include? Depends on the project. Could be:
- Business rules ("orders under $500 don't need approval")
- Technical decisions ("use PostgreSQL because we need JSONB + full-text search")
- Constraints ("no direct imports between modules")
- Lessons from mistakes ("agent keeps recreating existing files in worktree — must state explicitly 'file ALREADY EXISTS, DO NOT recreate'")
- Terminology ("PO = Purchase Order, not Post Office")
- API behaviors ("Shopee webhook delays 5-30 seconds, not realtime")
- Anything that, if AI doesn't know, it will assume wrong

Start simple. A folder with structured markdown files is enough. Add complexity when and only when simplicity falls short.

### 2. Skills to Interact with Knowledge

A skill is a structured interaction between human and AI. Instead of ad-hoc prompts ("write me a user management API"), a skill guides you through a structured process.

You only need 5 basic skills:

**Discover** — AI acts as facilitator, helping you extract knowledge from your head. Not AI teaching you — AI asks the right questions so you answer them yourself. "When a customer cancels an order after it's shipped, what happens?" You answer, AI records it with structure, you confirm, knowledge enters the store.

**Decide** — Record decisions with reasons. Not just "use Redis" but "use Redis because we need a cache with TTL, considered Memcached but it lacks data structures, considered local cache but we need shared across instances." When 6 months later someone asks "why Redis?" — the answer is already in the knowledge store.

**Plan** — Take knowledge from the store, assemble it into context for AI execution. "This iteration builds the payment feature. Relevant knowledge: business rules about refunds, decision to use Stripe, PCI compliance constraints, lessons from the last time we implemented payment in another project."

**Retro** — After each iteration, ask: "what went wrong? why? what rule do we encode so it doesn't happen again?" Output goes straight into the knowledge store as constraints or failure patterns.

**Query** — Ask anything about the knowledge store. "What constraints relate to the payment module?" "What decisions have been made about authentication?" "What mistakes have occurred with frontend testing?"

These five skills are enough for any project. When you recognize a new pattern ("every time we reverse-engineer legacy code we need to extract business rules"), you create a new skill (`/reverse-discover`). The framework doesn't predict skills for you — the framework gives you the mechanism to create skills when needed.

### 3. Feedback Loop: Execution → Knowledge

This is what transforms the system from static to living. Every time AI executes, the result must feedback into the knowledge store:

- Test fails → why? → what knowledge was missing? → add it
- Agent assumes wrong → which assumption? → record explicitly in knowledge
- Code review finds a bad pattern → create a new constraint
- Project completes → retro → lessons → knowledge for the next project

The system doesn't get smarter because of a newer model. The system gets smarter because **every mistake is encoded as knowledge** for next time.

---

## The Loop

There is only 1 loop:

```
Knowledge → Execute → Feedback → Knowledge (updated)
```

Everything in this approach is a manifestation of that loop.

You discover domain knowledge → AI executes → test fails → you realize the spec missed an edge case → update knowledge → AI executes again → passes. That's the loop with execution = AI generates code, feedback = test result.

You re-read 2 existing constraints → realize they imply an additional rule → add it to the knowledge store. That's the loop with execution = thinking, feedback = insight. No AI agent needed.

Two people work in parallel, both update knowledge → conflict → resolve → consistent knowledge. That's the loop with feedback = conflict signal.

New project, empty knowledge store → intensive discovery → first knowledge enters the store → plan the first iteration. That's the loop running for the first time.

No need to remember "how many types of loops." Just remember: **every execution ends with knowledge being updated.** If you execute and the knowledge store doesn't change — you're losing information. If the knowledge store changes after every execution — the system is learning.

The first iteration is always rough — because the knowledge store is nearly empty. Each loop, knowledge grows richer, output becomes more accurate. A real project: iteration 0 quality 84%, iteration 21 quality 100% — same AI, same model, the only difference was knowledge accumulated through 21 loops.

---

## Applying to Any Field

### Step 1: Ask "What Knowledge Is Most Important for This?"

Each field has different knowledge types:

**Software Development:** business rules, domain models, technical constraints, API behaviors, architectural decisions, failure patterns.

**Content & Marketing:** brand voice, target audience behaviors, competitive positioning, channel-specific constraints, performance data from previous campaigns.

**Operations & Process:** workflow rules, exception handling procedures, compliance requirements, supplier behaviors, SLA commitments.

**Research & Analysis:** methodology standards, data source characteristics, bias patterns, terminology definitions, previous findings.

**Product Development:** user pain points, market assumptions (validated/unvalidated), technical feasibility findings, competitor behaviors.

You don't need to know everything upfront. Ask: **"if AI doesn't know something, what will it assume most wrongly?"** That's the knowledge to capture first.

### Step 2: Create Skills Suited to Discovering That Knowledge

Different knowledge requires different discovery approaches:

- Business rules → **interview domain experts** (AI asks, expert answers)
- API behaviors → **experiment and log** (try calling API, observe behavior, record)
- Legacy business logic → **read code and extract** (AI reads code, proposes rules, human verifies)
- User experience → **observation** (watch users, record pain points)
- Technical feasibility → **spike/prototype** (build small, measure performance, record conclusions)
- Market knowledge → **research and validate** (AI synthesizes data, human validates assumptions)
- Process knowledge → **walk through with operators** (AI asks step by step, records exceptions)

Each discovery approach can become a skill when you notice yourself repeating it often. Create skills when you see the pattern — no need to create them in advance.

### Step 3: Establish the Feedback Loop

Ask: "when execution happens, how does the result feed back into the knowledge store?"

Simplest: after each iteration, run a retro, record lessons. More complex: automated monitoring detects when knowledge is outdated (API behavior changes, schema drift).

No need to be perfect from the start. Begin with manual retros. Automate when you notice repeating patterns.

### Step 4: Let AI Execute with Existing Knowledge

This is the step most people start with — and that's wrong. It should be the last step. When knowledge is sufficient, execution is nearly automatic. When knowledge is missing, execution costs many times more.

Execution can use any tool suited to the job — Claude Code, Cursor, or any AI tool that can read context from the knowledge store. The framework doesn't tie you to a specific tool.

### Step 5: Every Mistake = 1 New Rule

This is the most important step and also the easiest to skip.

When execution fails: don't just fix the code. Ask: "why did it fail? what knowledge was missing? what rule do we add so it doesn't fail again?"

Encode the answer as a constraint or convention in the knowledge store. The next agent reads the rule → doesn't make the same mistake. The system accumulates wisdom over time.

A project started with 0 constraints. After 21 iterations: 33 constraints, each noting "this rule was born from this mistake in this iteration." A new team member reads 33 constraints = receives accumulated experience from 21 iterations without going through them.

---

## The Role Shift

### From Executor → Knowledge Owner

Whether you're a developer, marketer, analyst, or operations manager — the role shifts with the same pattern: you're no longer the one who **produces** the output. AI produces output. You're the one who **ensures AI has sufficient knowledge to produce correctly**, and **verifies output matches the defined knowledge.**

In software development: developers don't write code — developers own knowledge quality, orchestrate AI execution, review output. Write code? AI handles that. Understand business logic to know what "correct" looks like? Developer's job. Recognize patterns to create new rules? Developer's job.

In marketing: marketers don't write content — marketers own brand knowledge, audience insights, campaign learnings. AI writes drafts, marketer verifies it matches tone, audience, facts.

Same pattern in every field: **humans shift from executor to knowledge owner + quality gatekeeper.**

### Everyone Is a Knowledge Contributor

The difference between a team that uses AI poorly and a team that uses AI well: the poor team has 1 person prompting AI. The good team has **everyone contributing knowledge** to the same knowledge store — business analysts contribute business rules, developers contribute technical constraints, testers contribute failure patterns, domain experts contribute domain knowledge, operations contribute real-world behaviors.

AI uses all of that knowledge to execute. The more perspectives, the more comprehensive the knowledge, the more accurate the output. Knowledge isn't one person's responsibility — it's the team's shared asset.

---

## When NOT to Use This Approach

Transparent: this approach has overhead. If the overhead exceeds the value, don't use it.

**Quick prototype that needs validation in 1 day** — just prompt AI, see the result, decide. Capture a few notes if the prototype succeeds and needs to be built for real.

**Task is too simple** — "write an order confirmation email" or "create a CRUD endpoint for 1 entity" doesn't need knowledge ceremony. A clear enough prompt, AI produces correctly.

**You're already a complete expert in the domain** — knowledge is already in your head, and the task is small enough that you can describe it fully in 1 prompt. No need for an external knowledge store for what you already know clearly and can express.

**Wrong output is easy to fix** — if a mistake takes 5 minutes to fix, don't spend 30 minutes capturing knowledge.

Principle: **use it when the cost of getting it wrong > cost of knowledge ceremony.** If getting it wrong means 2 weeks of rework, spending 2 days capturing knowledge is a worthwhile investment. You'll feel where the line is — and you'll feel it more accurately with experience.

---

## Where to Start

### Day 1

Create a `knowledge/` folder in your project. Create 3 files:

- `decisions.md` — each important technical decision, with reasons
- `constraints.md` — rules that everyone (and AI) must follow
- `glossary.md` — project terminology, unified meanings

That's knowledge store v1. Enough to start.

### Week 1

When using AI to perform tasks, before each task: read `constraints.md`, provide relevant rules as context for AI. After each task: if AI got something wrong, add 1 rule to `constraints.md`.

End of week: you'll have 5-10 accumulated constraints. AI starts making fewer mistakes.

### Month 1

Patterns will emerge:
- You find yourself repeating the same prompt template when discovering → create a skill
- You find the constraints file is getting long → reorganize into categories
- You find multiple people need to read the same knowledge → need shared access
- You find AI needs programmatic access → need MCP

Add complexity only when real pain appears. Don't build infrastructure before you need it.

### Month 3

Knowledge store has 30+ constraints, dozens of decisions, multiple team members contributing. You start seeing: a new team member joins, reads the knowledge store for 1 day, productive by day 2 because knowledge has been externalized. AI produces significantly higher quality output than in month 1. When starting a new project, you bring applicable knowledge (constraints, conventions, decisions) → head start instead of starting from zero.

That's Overmind working.

---

## In Summary

Not a tool. Not a process. A way of thinking.

**Before asking "how does AI execute?" → ask "what does AI know?"**

**Before fixing wrong output → ask "what knowledge is missing?"**

**Before creating complex processes → ask "what pattern is repeating?"**

Every mistake is a chance to encode 1 new rule. Every new rule makes the system smarter once. After enough loops, the system knows nearly everything it needs — and AI produces correct output almost by default.

Start simple. 1 folder, 3 files. Add complexity when pain demands it. Trust the process: first iteration is rough, 10th iteration is smooth, 20th iteration is nearly automatic.

Knowledge-first. Execution-last. Humans recognize patterns. AI follows rules. Each loop, both get better.
