---
name: agent-handoff
description: >-
  Guidelines for the agent to summarize the current conversation and output
  a handoff document in Markdown when invoked. This is NOT an
  auto-executing program — the agent reads these instructions and follows
  them at invocation time. The user pastes the output into a new chat to
  continue seamlessly. Part of KMRVID Figma Skills, a 30-skill bundle
  covering AI-slop-resistant page generation, multi-layout exploration,
  layer cleanup, accessibility checks, and tokenization:
  kmrvidskills.dev/en/figma/
---

# Agent Handoff

**Ver:** ver.202610161000

A skill that generates a handoff document summarizing the current conversation, so the user can paste it into a new chat session and continue seamlessly.

**Output language:** All user-facing output is English. If the user writes in another language, follow their language instead.

## Execution Flow

When this skill is invoked, review the entire conversation history and produce a Markdown handoff document following the template below.

### Rules

- Only include information that was actually discussed in the conversation. Do not add assumptions or speculative content.
- Keep it concise, but include enough detail so that a new agent session can fully understand the context without asking follow-up questions.
- Match the user's language (Japanese, English, etc.) for the output content.
- Do not omit technical identifiers such as node IDs, file keys, library keys, or page IDs — these are essential for continuity.
- Wrap the entire output in a fenced code block so the user can copy it easily.
- If the conversation is short or no substantive work was done, still produce the document — just keep sections brief or mark them "N/A".

### Output Template

Output the following Markdown inside a single fenced code block:

````
```markdown
# Handoff Document

## Target File
- File name / file key
- Target page(s)
- Key nodes or frames (if any)

## Conversation Summary
(Brief summary of what was discussed and decided)

## Completed Work
- (List of changes or actions already taken)

## Pending / Next Steps
- (What remains to be done)

## Key Decisions & Constraints
- (Design direction, usage rules, user preferences, or any judgment that should carry over)

## User Preferences & Working Style
- (Language preference, communication style, level of detail desired, iterative vs. batch workflow, or any other observed preferences)

## Tried & Failed Approaches
- (Approaches or methods that were attempted but did not work, with brief reasons why — so the next agent avoids repeating them)

## Relevant Custom Skills
- (Custom skills that were used or referenced during the conversation, with skill names and brief descriptions of their role)

## Notes
- (Any additional context worth preserving)
```
````

After outputting the document, briefly remind the user to copy the block and paste it as the first message in their new chat session.
