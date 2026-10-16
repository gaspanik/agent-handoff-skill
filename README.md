# agent-handoff — Figma Agent Conversation Handoff

Register this skill in Figma's custom skill feature and run it from the chat at any point — no selection needed. It reviews the entire conversation so far and outputs a single Markdown document you can paste into a brand-new chat session to continue exactly where you left off.

---

## What this is

Figma agent conversations don't carry over when you start a new chat — context window limits, a fresh session, or just wanting a clean slate all mean the next session starts from zero. Re-explaining which file, which frame, what was already decided, and what didn't work is tedious and error-prone; details get dropped, and the new session ends up repeating mistakes the old one already ruled out.

This skill isn't a program that runs automatically in the background — it's a set of instructions the agent follows the moment you invoke it. It reads back through the conversation and writes a structured handoff document covering the target file, what's done, what's pending, key decisions, your working style, and dead ends already explored — so the next session can pick up cold without asking you to repeat any of it.

```
Invoke the skill mid-conversation
        │
        ▼
Agent reviews the full conversation history
        │
        ▼
Fills out the handoff template:
  ├─ Target File            (file key, page, key nodes)
  ├─ Conversation Summary
  ├─ Completed Work
  ├─ Pending / Next Steps
  ├─ Key Decisions & Constraints
  ├─ User Preferences & Working Style
  ├─ Tried & Failed Approaches
  └─ Relevant Custom Skills
        │
        ▼
Outputs everything as one fenced Markdown code block
        │
        ▼
You copy it and paste it as the first message in a new chat
```

---

## Scope

- **Operates on the conversation, not the canvas.** Unlike most Figma-agent skills, this one doesn't touch nodes, variables, or components — it reads the chat history and writes text.
- **No selection needed.** Run it any time, regardless of what's selected on the canvas.
- **Reports only what was actually discussed.** The agent is instructed not to invent or assume details that never came up — if something is genuinely unknown, the relevant section is marked "N/A" rather than guessed.
- **Preserves technical identifiers.** Node IDs, file keys, library keys, and page IDs are carried over verbatim, since a new session can't do anything useful without them.
- **Output language follows the user.** The instructions default to English but explicitly defer to whatever language you were using in the conversation.
- **You do the pasting.** The skill produces the document and reminds you to copy it — it doesn't (and can't) create the new chat session for you.

---

## Requirements

- **Figma (Design Agent / custom skill feature).** This skill is a plain instruction set with no tool calls of its own — register `SKILL.md` as a custom skill and invoke it directly from the chat.

---

## Repo structure

```
skills/
  agent-handoff/
    SKILL.md          — skill definition to register in Figma's custom skill feature
    LICENSE
```

---

## Getting started

**Once published on Figma Community**, you'll be able to add this skill directly from the [AI Skills library](https://www.figma.com/community/ai-skills) — no download needed. Until then, register it from source:

**From source:** clone this repo and register the skill file yourself.

```bash
git clone https://github.com/gaspanik/agent-handoff-skill
```

**1. Register `skills/agent-handoff/SKILL.md`** in Figma's custom skill feature.

**2. Run it from the chat, whenever you want a handoff** — no selection needed.

```
/agent-handoff
```

```
Summarize this conversation so I can continue in a new chat
```

```
このやりとりを引き継ぎ用にまとめて
```

---

## Example output

```markdown
# Handoff Document

## Target File
- File key: abc123XYZ
- Target page(s): Home
- Key nodes or frames: Hero section (node 42:108)

## Conversation Summary
Worked on tokenizing the Hero section's hardcoded colors and font sizes
into variables, then generated a mobile (390px) version.

## Completed Work
- Ran figma-tokenize on the Hero section — 6 colors, 3 font sizes bound
- Generated Hero_mobile via figma-mobile-convert

## Pending / Next Steps
- Tokenize the Features section next
- Review mobile nav pattern (currently hamburger, user wants to compare
  against a bottom tab bar)

## Key Decisions & Constraints
- Accent color must stay #B62A2D across all breakpoints
- Heading font weight must match desktop exactly

## User Preferences & Working Style
- Prefers to confirm each step rather than run unattended
- Responses in Japanese

## Tried & Failed Approaches
- Attempted a single figma-systematize pass first — user asked to stop
  and do layer renaming and tokenization as separate confirmed steps
  instead

## Relevant Custom Skills
- figma-tokenize — used for variable extraction
- figma-mobile-convert — used for the mobile version

## Notes
- File also has a Figma-japanese-web-guideline note pending review
```

---

## Part of a larger set

This skill is one of 30 Figma-agent skills bundled in **KMRVID Figma Skills** — covering AI-slop-resistant page generation, multi-layout-pattern exploration, layer cleanup, contrast/accessibility checks, tokenization, component audits, ALT text suggestions, and more: [kmrvidskills.dev/en/figma/](https://kmrvidskills.dev/en/figma/)

---

Built by Masaaki Komori - [@cipher](https://x.com/cipher) · Skill for [Figma](https://www.figma.com/)
