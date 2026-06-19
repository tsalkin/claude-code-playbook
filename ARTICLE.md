# My AI Agent Was Fast and Capable — and That Was Exactly the Problem

For a while I was thrilled with my coding agent. It was fast. It read across a codebase in seconds, proposed plans, wrote the change, ran the tests. Capability was never the issue.

Trust was.

Because a capable agent, left without operating discipline, doesn't fail loudly. It fails *plausibly*. It grabs the first explanation that fits and stops looking. When the retrieved context is thin, it fills the gap with confident, well-formed invention. It quietly changes a value that should never change without asking. None of these throw an error. All of them quietly erode trust.

## The reveal

The clearest case: a query kept returning the wrong answer. I asked the agent why. It found a plausible cause and fixed it — the bug stayed. It found a *second* plausible cause, equally convincing — also wrong. The real reason was a single character: one part of the system spelled a program name with an underscore, another with a hyphen, and they silently failed to match. Two confident diagnoses, both mirages. What finally found it wasn't a smarter guess — it was *refusing to guess* and checking the facts one more time.

That shape repeated. The lesson wasn't "the agent is bad." It was: **capability without discipline reverts to plausible-but-wrong, and speed only gets you there faster.**

## The insight

The fixes were never clever. They were *conventions* — small rules a careful engineer already follows and an eager agent skips:

- **Don't converge on the first idea.** For anything non-trivial, research first: scan prior art (the web, GitHub), and when the call is high-stakes or contested, write a self-contained prompt and run it past several *other* models before committing. Don't reinvent; don't trust one model's first answer — including your own.
- **Verify your own change end-to-end.** "Code written" is not "it works."
- **Find a field's source of truth before changing it** — the name lies.
- **When grounding is thin, say "not found"** — never fabricate the specifics.
- **Never silently mutate source-of-truth.** Paid actions need a yes. Secrets pasted into chat are burned.

## The resolution

Habits don't survive a context reset, and they don't travel to the next project. So I stopped relying on the agent to *remember* to be careful and wrote the conventions down — once, globally — in the file it loads into every session (`~/.claude/CLAUDE.md`).

That's what `claude-code-playbook` is: not a tool, just the rules, copy-pasteable. Its sibling, [claude-memory-hygiene](https://github.com/tsalkin/claude-memory-hygiene), keeps the agent's *memory* lean; the playbook keeps its *behavior* disciplined. One makes the agent see; the other makes it trustworthy.

## An honest credit

Most of these were learned the expensive way — by catching the agent (and myself) taking the plausible shortcut. Writing them down is how the lesson stops being relearned every session.
