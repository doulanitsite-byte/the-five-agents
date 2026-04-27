# CEO Agent — סוכן המנכ"ל

## Overview
סוכן המנכ"ל הוא נקודת הכניסה הראשית של מערכת the-five-agents. הוא מקבל כל קלט מהמשתמש (עברית/אנגלית), מנתח את הכוונה, ומאציל לסוכן הכפוף המתאים. מודל: `opus`. הסוכן לא יוצר תוכן בעצמו — תפקידו ניהול ותיאום בלבד. הקובץ `.claude/agents/ceo_agent.md` מגדיר את הסוכן ב-Claude Code sub-agent format. ה-PRD המלא נמצא ב-`docs/prd-ceo-agent.md`.

## Open Questions
- מה הם 4 הסוכנים הכפופים המדויקים ותחומי האחריות שלהם?
- האם המנכ"ל צריך כלים (tools) ספציפיים?
- האם לציין בתגובה איזה סוכן טיפל? (verbose mode on/off)
- מה אסטרטגיית ה-fallback אם סוכן כפוף נכשל?

## Session Log

### 2026-04-27 — יצירת PRD ו-agent.md ראשוניים [shipped]
- **What was done:** יצירת `docs/prd-ceo-agent.md` (PRD מלא) ו-`.claude/agents/ceo_agent.md` (הגדרת הסוכן). תוקן ערך המודל מ-`claude-opus-4-6` ל-`opus` בהתאם לפורמט Claude Code.
- **Decisions:** מודל `opus` לסוכן המנכ"ל — מתאים להחלטות ניתוב קריטיות. שפה: מגיב בשפת הקלט.
- **Notes / Caveats:** ה-Available Agents table ריקה כרגע (TBD) — יש לעדכן כשהסוכנים הכפופים יוגדרו.
- **Related:** [[project-documentation-vault-setup]], [[claude-md]]
