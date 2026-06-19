# claude-code-playbook

**Operating conventions for a Claude Code agent — the rules that make a long-running coding agent trustworthy, not just fast.**

A curated, copy-pasteable set of conventions for your global `~/.claude/CLAUDE.md` (loaded into every session, every project). MIT-licensed. Prose, not code — drop in what fits, ignore the rest.

> A capable agent without operating discipline drifts to plausible-but-wrong: it converges on the first idea, fabricates specifics when grounding is thin, and silently mutates source-of-truth. These conventions are the guardrails — most of them learned the hard way.

> Sibling to **[claude-memory-hygiene](https://github.com/tsalkin/claude-memory-hygiene)** — that keeps the agent's memory index lean; this keeps its *behavior* disciplined.

---

## How to use

Claude Code loads `~/.claude/CLAUDE.md` into **every** session of **every** project. Paste the conventions you want there; a project's own `CLAUDE.md` overrides/extends per repo. These are principles, not config — adapt the wording to your voice.

---

## 1. Research before building — prior-art + external multi-LLM

For **non-trivial** tasks or phases, the research stage includes:

- **Prior-art scan.** Search the web **and GitHub** for similar solutions → a *Prior Art* section: links, what to borrow, what to avoid, a license note. Discipline: **learn, don't copy**; verify it actually fits your stack.
- **External multi-LLM research prompt** *(agent's judgment — not every task)*. When a decision is high-stakes / novel / contested / an architecture fork, the agent writes a **self-contained research prompt** (background + specific questions + desired answer format, so an external model with no repo access can answer), **saves it to disk** (`docs/research/<date>_<topic>_research_prompt.md`), you run it through several LLMs by hand, and the agent **synthesizes** the answers into a `_SYNTHESIS` + `_DECISIONS` doc that feeds the spec.

Skip both for trivial/mechanical work. The point: don't reinvent, and don't converge on one model's first answer.

## 2. Reasoning effort

`auto` is the baseline. Raise it **deliberately** where the cost of error is high and depth pays off: hard debugging (especially the *"several bugs, one root"* class), designing a new subsystem, core changes with cascading effects. Keep it low for known-path mechanics (restarts, version bumps, routine deploys).

## 3. Choices & recommendations

For any choice: explain each option in plain language, show **first- and second-order** consequences, and give a recommendation with reasoning. Always include the option that serves **long-term health** (not a quick patch) and flag it explicitly as such.

## 4. Engineering discipline

- **Verify your own change end-to-end** — run the real path and confirm the result; *"code written" ≠ "it works"*.
- **Find a field's source of truth before changing it** — the field name lies; mismatches here are the root of whole bug classes.
- **No silent automation of source-of-truth** — mutations to key data (settings, bindings, status) require an explicit action/confirmation. Auto = invisible failure mode.
- **Secrets in chat = compromised** — revoke + rotate immediately; new ones only via the terminal.
- **Paid actions need explicit confirmation** — *"I have a key/access" ≠ permission*.
- **Capture deferred ideas** into a backlog/notes — nothing gets lost.
- **Report outcomes faithfully** — if tests fail, say so with the output; if a step was skipped, say that.

## 5. Memory hygiene

Session handoff lives in **git-tracked project files** (e.g. `RESUME`/`STATE`), not the agent's memory directory; memory holds only durable facts. Keep the always-loaded index lean → **[claude-memory-hygiene](https://github.com/tsalkin/claude-memory-hygiene)**.

## 6. Docs & narrative

Keep a low-friction **decision log** (DEVLOG); promote key decisions to **article-ready deep-docs**; keep a **jargon-free narrative layer** for a wider audience. Document decisions while fresh — they're the source for articles later.

---

## Why a playbook (and not just habits)

Habits don't survive context resets or new projects. A global `CLAUDE.md` does. Writing the conventions down — once, globally — is what makes an agent behave consistently across sessions instead of relearning the same lessons.

## License

MIT © 2026 Maxim Tsalkin
