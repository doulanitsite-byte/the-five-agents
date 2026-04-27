# package.json

## Overview
קובץ תצורת Node.js הראשי של הפרויקט. מגדיר את שם החבילה (`workspace`), גרסה (`1.0.0`), נקודת כניסה (`index.js`), ומציין שהפרויקט משתמש ב-`commonjs` כמערכת המודולים. כרגע אין dependencies מותקנות ואין script test ממשי. הקובץ נוצר אוטומטית על-ידי `npm init -y`.

## Open Questions
- איזה framework/library ישמשו את חמשת הסוכנים?
- האם ישתמשו ב-ESM או CommonJS?
- האם נדרש TypeScript?

## Session Log

### 2026-04-27 — הגדרת vault ותיעוד ראשוני [wip]
- **What was done:** יצירת קובץ תיעוד עבור package.json במסגרת הקמת vault הפרויקט
- **Decisions:** הוגדר כ-wip — הפרויקט בתחילת דרכו, אין dependencies עדיין
- **Notes / Caveats:** `main: "index.js"` — הקובץ `index.js` עדיין לא קיים בפרויקט
- **Related:** [[claude-md]], [[claude-settings-local]], [[project-documentation-vault-setup]]
