# .claude/settings.local.json

## Overview
קובץ הגדרות מקומיות של Claude Code עבור הפרויקט הזה בלבד. מגדיר הרשאות (permissions) שמותרות אוטומטית ללא צורך באישור ידני של המשתמש. כרגע מאשר רק את הפקודה `npm init -y`. הקובץ ממוקם ב-`.claude/` ואינו מיועד לשיתוף (local). משויך ל-Claude Code ולתצורת הסביבה המקומית.

## Open Questions
- האם יש צורך להוסיף הרשאות נוספות ככל שהפרויקט מתפתח?
- האם הקובץ הזה צריך להיות ב-.gitignore?

## Session Log

### 2026-04-27 — הגדרת vault ותיעוד ראשוני [wip]
- **What was done:** יצירת קובץ תיעוד עבור `.claude/settings.local.json` במסגרת הקמת vault הפרויקט
- **Decisions:** הקובץ הועלה ל-GitHub למרות שהוא "local" — ייתכן שיש לשקול הוספתו ל-.gitignore
- **Notes / Caveats:** ההרשאה `Bash(npm init -y)` היא שארית מיצירת ה-package.json הראשוני
- **Related:** [[claude-md]], [[package-json]], [[project-documentation-vault-setup]]
