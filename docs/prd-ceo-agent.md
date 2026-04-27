# PRD — מיכל / סוכן המנכ"ל

**גרסה:** 1.0
**תאריך:** 2026-04-27
**סטטוס:** Draft

---

## 1. Overview

| שדה | ערך |
|-----|-----|
| **שם הסוכן** | מיכל / סוכן המנכ"ל |
| **קובץ הגדרה** | `.claude/agents/ceo_agent.md` |
| **מודל** | `claude-opus-4-6` |
| **שפות** | עברית + אנגלית (מגיב בשפת הקלט) |
| **נקודת כניסה** | ראשית ויחידה — כל בקשה עוברת דרכו |

הסוכן הוא ה"מנכ"ל" של מערכת חמשת הסוכנים. הוא מקבל כל קלט מהמשתמש, מבין את הכוונה, ומחליט מי מהסוכנים הכפופים מתאים לטפל במשימה. המשתמש אף פעם לא פונה ישירות לסוכן אחר — רק למנכ"ל.

---

## 2. Problem Statement

מערכת מרובת סוכנים ללא נקודת ניהול מרכזית גורמת ל:
- בלבול — המשתמש צריך לדעת לאיזה סוכן לפנות
- חוסר עקביות — כל סוכן מגיב בסגנון שונה
- אין זיכרון הקשר בין סוכנים — כל אחד עובד בבועה

**הפתרון:** סוכן מנכ"ל שהוא שכבת ה-orchestration: מנתב, מתאם, ומאחד תוצאות.

---

## 3. Goals

### ✅ חובה (MVP)
- [ ] קבלת קלט חופשי מהמשתמש בעברית ו/או אנגלית
- [ ] זיהוי שפת הקלט ותגובה באותה שפה
- [ ] ניתוח כוונת המשתמש (intent classification)
- [ ] בחירת הסוכן המתאים מרשימת הסוכנים הזמינים
- [ ] העברת המשימה לסוכן הנבחר עם הקשר מלא
- [ ] קבלת תוצאה מהסוכן והחזרתה למשתמש
- [ ] טיפול במקרה של כוונה לא ברורה — בקשת הבהרה

### 🔜 עתידי (לאחר הגדרת הסוכנים הכפופים)
- [ ] הפעלת מספר סוכנים במקביל (parallel execution)
- [ ] איחוד תוצאות מכמה סוכנים לתגובה אחת
- [ ] ניהול תור משימות

---

## 4. Non-Goals (בשלב זה)

- ❌ המנכ"ל **לא** יוצר תוכן בעצמו — הוא רק מנתב
- ❌ אין webhook / API חיצוני בשלב א'
- ❌ אין persistent memory חיצוני (DB/vector store) — בשלב א' context window בלבד
- ❌ אין UI גרפי — רק Claude Code chat

---

## 5. User Stories

| # | כמשתמש... | אני רוצה... | כדי ש... |
|---|-----------|------------|---------|
| US-01 | כותב/ת בעברית | לקבל תגובה בעברית | התקשורת תהיה טבעית |
| US-02 | כותב/ת בקשה כללית | שהמנכ"ל יבין ויפנה לסוכן הנכון | לא אצטרך לזכור את שמות הסוכנים |
| US-03 | שולח/ת בקשה עמומה | שהמנכ"ל ישאל אותי שאלת הבהרה | לא יתחיל לעבוד על הדבר הלא נכון |
| US-04 | רוצה לדעת מה קורה | שהמנכ"ל יאמר לי לאיזה סוכן הוא מנתב | יש לי visibility |

---

## 6. Agent Architecture

```
משתמש
    │
    ▼
┌─────────────────────────────────────┐
│           CEO Agent                 │
│  ┌──────────────────────────────┐   │
│  │  1. Language Detection       │   │
│  │  2. Intent Classification    │   │
│  │  3. Agent Selection          │   │
│  │  4. Context Packaging        │   │
│  │  5. Result Aggregation       │   │
│  └──────────────────────────────┘   │
└──────┬──────┬──────┬──────┬─────────┘
       │      │      │      │
       ▼      ▼      ▼      ▼
   Agent1  Agent2  Agent3  Agent4
   [TBD]   [TBD]   [TBD]   [TBD]
   (יוצר   (יוצר   (יוצר   (יוצר
   תוכן)   תוכן)   תוכן)   תוכן)
```

---

## 7. Decision Logic — Agent Selection

### שלב 1: זיהוי שפה
```
if קלט מכיל עברית → שפת_תגובה = עברית
else → שפת_תגובה = אנגלית
```

### שלב 2: ניתוח כוונה
```
analyze(קלט) → intent_category

intent_category:
├─ content_creation  → [Agent TBD - יוצר תוכן]
├─ [category_2]      → [Agent 2 - TBD]
├─ [category_3]      → [Agent 3 - TBD]
├─ [category_4]      → [Agent 4 - TBD]
└─ unclear           → ask_for_clarification()
```

### שלב 3: הפעלה ואיחוד
```
selected_agents = select(intent_category)

if len(selected_agents) == 1:
    result = invoke(selected_agents[0], context)
elif len(selected_agents) > 1:
    results = invoke_parallel(selected_agents, context)
    result = aggregate(results)

return format_response(result, שפת_תגובה)
```

---

## 8. Communication Protocol

### קלט שמקבל המנכ"ל
```
{
  user_message: string,     // טקסט חופשי מהמשתמש
  conversation_history: [], // היסטוריית שיחה (מ-context window)
}
```

### פלט שמחזיר המנכ"ל
```
{
  response: string,         // תגובה בשפת הקלט
  agent_used: string,       // שם הסוכן שטיפל (לשקיפות)
  status: "success" | "clarification_needed" | "error"
}
```

### טיפול בכוונה לא ברורה
כאשר המנכ"ל לא מצליח לסווג את הכוונה, הוא **לא מנחש** — הוא שואל:
> "כדי לעזור לך בצורה הטובה ביותר, תוכל/י לפרט יותר מה בדיוק את/ה רוצה?"

---

## 9. `ceo_agent.md` Specification

ראה קובץ: [`.claude/agents/ceo_agent.md`](../.claude/agents/ceo_agent.md)

הקובץ מכיל:
- **YAML frontmatter** — `name`, `description`, `model`
- **Role** — הגדרת תפקיד המנכ"ל
- **Capabilities** — מה הסוכן יכול לעשות
- **Available Agents** — רשימת הסוכנים הכפופים (תתעדכן)
- **Decision Rules** — כללי ניתוב
- **Response Format** — פורמט תגובה אחיד

---

## 10. Open Questions

| # | שאלה | דחיפות | מי מחליט |
|---|------|---------|---------|
| OQ-01 | מה הם 4 הסוכנים הכפופים המדויקים? | גבוהה | המשתמש |
| OQ-02 | האם המנכ"ל צריך גישה לכלים (tools) ספציפיים? | בינונית | המשתמש |
| OQ-03 | האם לציין בתגובה איזה סוכן טיפל? (verbose mode) | נמוכה | המשתמש |
| OQ-04 | מה קורה אם סוכן כפוף נכשל? fallback strategy? | בינונית | המשתמש |

---

## 11. Future Scope

- הוספת סוכנים נוספים מעבר ל-4 (extensible registry)
- persistent memory בין sessions (vector DB / external store)
- webhook trigger מ-Slack / Telegram
- dashboard לניטור פעילות הסוכנים
