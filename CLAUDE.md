# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Agent Routing — MANDATORY

**Every user request MUST be routed through the `michal` agent.**

Use the `michal` sub-agent for ALL tasks without exception.
Do not handle any user request directly — always delegate to מיכל first.

```
כל בקשה → מיכל (michal agent) → סוכן מתאים
```

## Project Overview

מערכת חמשת הסוכנים (the-five-agents) — מערכת סוכני AI לניהול ויצירת תוכן.
בראש המערכת עומד סוכן המנכ"לית **מיכל** שמנהל צוות של 4 סוכני תוכן (בפיתוח).

## Architecture

```
משתמש
  ↓
מיכל — סוכן המנכ"ל (.claude/agents/ceo_agent.md)
  ↓
יובל | יעל   | חן    | גיא
[תמונות] [תוכן]  [רשת]   [QA]
```

- PRD מלא: `docs/prd-ceo-agent.md`
- תיעוד vault: `vault/Meeting Notes/`

## Agents

| שם | קובץ | תחום |
|----|------|------|
| מיכל | `.claude/agents/ceo_agent.md` | מנכ"לית — ניתוב |
| יובל | `.claude/agents/yuval.md` | קריאייטיב — יצירת תמונות |
| יעל | `.claude/agents/yael.md` | כתיבת תוכן — שכתוב מאמרים |
| חן | `.claude/agents/chen.md` | חיפוש רשת — Web Research |
| גיא | `.claude/agents/guy.md` | QA — סוגר לולאה |
| landing-page-agent-ilanit | `.claude/agents/landing-page-agent-ilanit.md` | דפי נחיתה — רב מסר |

## Skills

| שם | קובץ | שימוש |
|----|------|-------|
| nano-banana-2 | `.claude/skills/nano-banana-2/SKILL.md` | יצירת תמונות עם Gemini 3.1 Flash Image |
| landing-page-ilanit | `.claude/skills/landing-page-ilanit/SKILL.md` | מבנה + DNA לדפי נחיתה של אילנית |

## MCP Servers

| שם | קובץ | תחום |
|----|------|------|
| nanobanana | `.mcp.json` | Nano Banana 2 image generation |

> ⚠️ יש להחליף `YOUR_GOOGLE_API_KEY_HERE` ב-`.mcp.json` במפתח האמיתי

## Commands

<!-- TODO: add build, test, lint commands -->

## Notes

- שפת תקשורת: עברית + אנגלית (מיכל מגיבה בשפת הקלט)
- מודל מיכל: `opus` | מודל יובל: `sonnet` | מודל יעל: `sonnet`
- תמונות reference: `reference/` | תמונות מוגמרות: `outputs/`
- Content Pipeline: `Content/` (גלם) → `Output/` (תוצר) → `Content/Ready/` (ארכיב)
- Memory Pipeline: `Memory/searches.md` ← יומן חיפושים של חן
- QA Pipeline: `Output/` → גיא → `QA_Reports/` → מיכל → משתמש
- Landing Page Pipeline: `LandingPages/Briefs/` → landing-page-agent-ilanit → `LandingPages/Output/` → גיא → מיכל
