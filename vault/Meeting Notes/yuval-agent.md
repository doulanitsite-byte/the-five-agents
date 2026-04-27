# יובל — סוכן קריאייטיב דירקטור

## Overview
יובל הוא הסוכן הקריאייטיב של מערכת the-five-agents, אחראי על יצירת תמונות עם עקביות ויזואלית. הוא משתמש בסקיל `nano-banana-2` (Gemini 3.1 Flash Image / Nano Banana 2) דרך MCP server. זרימת העבודה: סריקת `reference/` → ניתוח סגנון → בניית פרומפט → יצירת תמונה → שמירה ב-`outputs/`. מודל: `sonnet`. קובץ הגדרה: `.claude/agents/yuval.md`.

## Open Questions
- אילו תמונות reference יוכנסו לתיקיית `reference/`?
- האם יובל צריך לתמוך גם בעריכת תמונות קיימות (edit_image)?
- האם רצוי מנגנון naming convention מפורט יותר עבור outputs/?

## Session Log

### 2026-04-27 — יצירת סוכן יובל + סקיל nano-banana-2 [shipped]
- **What was done:** יצירת `.claude/agents/yuval.md`, `.claude/skills/nano-banana-2/SKILL.md`, `.mcp.json` (nanobanana MCP server), תיקיות `reference/` ו-`outputs/`, `.gitignore`. עדכון `ceo_agent.md` (הוספת יובל ל-Available Agents) ו-`CLAUDE.md`.
- **Decisions:** מודל sonnet ליובל (מספיק לניתוח reference + prompt engineering). outputs/ ב-.gitignore (קבצים גדולים). .mcp.json ב-.gitignore (מכיל GOOGLE_API_KEY).
- **Notes / Caveats:** המשתמש חייב להחליף `YOUR_GOOGLE_API_KEY_HERE` ב-`.mcp.json`. MCP server: `nanobanana-mcp-server` דרך `uvx`.
- **Related:** [[ceo-agent]], [[project-documentation-vault-setup]]
