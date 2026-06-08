# ETF Prospectus Reader — Claude Skill

A Claude Code skill that reads any ETF or fund prospectus (S-1, S-1/A, or similar legal filing) and extracts the creation and redemption mechanics into a clean, structured process flow document.

---

## What It Does

Give it a prospectus and it will:
- Identify all parties involved (sponsor, custodian, transfer agent, clearing agent, etc.)
- Map every step in the creation and redemption process
- Identify what moves at each step (cash, assets, shares, or just instructions)
- Identify timing (T-day, T+1, T+2)
- Flag decision points and approval gates
- Note anything the prospectus leaves ambiguous or at Sponsor's discretion
- Output a clean structured markdown document ready to feed into the n8n-financial-workflow-builder skill

---

## Requirements

- [Claude Code](https://claude.ai/code) installed

> **Also recommended:** Pair this with the n8n-financial-workflow-builder skill to automatically turn the output document into a deployed n8n workflow:
> ```
> install barnet-c/n8n-financial-workflow-builder
> ```

---

## Installation

### Option 1 — Claude Code terminal (recommended)
```
/plugin install barnet-c/etf-prospectus-reader
```

### Option 2 — VS Code chat panel (manual)
If you are using Claude inside VS Code chat, `/plugin install` does not work there. Install manually instead:

1. Download `skill.md` from this repo
2. Create this folder on your computer and place `skill.md` inside it:
```
~/.claude/skills/etf-prospectus-reader/skill.md
```
3. Restart VS Code

---

## How To Use

1. Open Claude Code or VS Code chat
2. Paste in your prospectus text, or attach the PDF
3. Type:
```
read this prospectus
```
4. Claude will extract all parties, map every creation and redemption step, and save a structured markdown document
5. At the end it will ask if you want to build it as an n8n workflow

---

## Example Output

The skill produces a document like this for every prospectus:

```
# [ETF Name] — Process Flow Document

## Product Summary
## Parties (table)
## Creation Flow — T Day (numbered steps)
## Creation Flow — T+1 Settlement Day (numbered steps)
## Redemption Flow — T Day (numbered steps)
## Redemption Flow — T+1 Settlement Day (numbered steps)
## Special Mechanisms
## Decision Points
## Notes and Ambiguities
```

Each step includes: who acts, what they do, what moves, and the flow type (Asset Movement / Messaging / both).

---

## Two-Skill Pipeline

For the best results, use both skills together:

```
Prospectus  →  etf-prospectus-reader  →  Process Flow Doc  →  n8n-financial-workflow-builder  →  n8n Workflow
```

1. Run this skill on the prospectus → get a structured document
2. Say "build this as an n8n workflow" → workflow is built and deployed automatically
