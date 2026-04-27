---
name: chen-web-research
description: >
  Use when חן needs to perform web research — guides effective query building,
  source evaluation, and content extraction for the Content/ pipeline.
  Invoke before every search to ensure quality and consistency.
---

# Chen Web Research Skill

מדריך לחיפוש אפקטיבי — לשימוש חן לפני ובמהלך כל חיפוש רשת.

---

## 1. בניית Query אפקטיבי

### כלל ברזל: ספציפי > כללי
```
❌ "שיווק לעסקים קטנים"
✅ "אסטרטגיית תוכן לעצמאים 2025 site:medium.com OR site:linkedin.com"
```

### תבניות מנצחות:
| מטרה | תבנית |
|------|--------|
| תוכן עדכני | `<נושא> 2025 OR 2026` |
| מחקר מעמיק | `<נושא> in-depth guide` |
| דעה מקצועית | `<נושא> perspective expert opinion` |
| נתונים | `<נושא> statistics data research 2025` |
| עברית | `<נושא בעברית>` — לתכנים ישראלים ספציפיים |

### הוסף מגבלות אתר לאיכות גבוהה:
```
site:medium.com OR site:substack.com OR site:hbr.org OR site:forbes.com
```

---

## 2. הערכת מקור — Checklist לפני בחירה

**✅ מקור טוב — כל הבאים אמורים להיות נכונים:**
- [ ] יש מחבר מזוהה עם שם
- [ ] התאריך ידוע (עדיף 2024-2026)
- [ ] האתר מוכר / בעל מוניטין
- [ ] המאמר מעמיק (מעל 500 מילה)
- [ ] יש מידע מקורי — לא רק סיכום של אחרים

**❌ הימנע מ:**
- ויקיפדיה (יכולה להשתנות, חסרת קול)
- אתרים עם 15+ פרסומות פופ-אפ
- תוכן ללא תאריך
- כותרות clickbait ללא תוכן ממשי
- "Top 10" רשימות ללא מקורות
- תוכן שנראה AI-generated filler

---

## 3. חילוץ תוכן — מה לכלול בקובץ

### חובה:
- URL מלא
- כותרת מקורית
- תאריך המאמר (אם ידוע)
- תמצית בעברית (2-3 פסקאות)
- 2-3 ציטוטים מדויקים מהמאמר

### מומלץ:
- כל הרעיונות המרכזיים — גם אם לא בציטוט מדויק
- נתונים וסטטיסטיקות ספציפיות
- מסקנות והמלצות של הכותב

### מה לא להעתיק:
- פרסומות ובאנרים
- תוכן sidebar לא קשור
- כפתורי שיתוף / CTA של האתר המקור

---

## 4. Anti-Patterns — טעויות נפוצות

| טעות | פתרון |
|------|-------|
| חיפוש כללי מדי | הוסף מילות מפתח ספציפיות |
| בחירת ראשון בתוצאות | השווה 3 מקורות לפחות |
| העתקה עיוורת | קרא, הבן, ואז תמצת |
| דילוג על בדיקת Memory | **תמיד** בדוק קודם |
| שמירה בלי URL | URL הוא חובה בכל קובץ |

---

## 5. פורמט קובץ סטנדרטי

שם קובץ: `Content/YYYYMMDD_<slug>.md`

דוגמה: `Content/20260427_content-marketing-strategy.md`

```markdown
---
source_url: https://example.com/article
source_title: The Complete Guide to Content Marketing
date_found: 2026-04-27
topic: אסטרטגיית תוכן לעסקים
---

# The Complete Guide to Content Marketing

**מקור:** [HBR](https://example.com/article)
**תאריך מקורי:** March 2025

## תמצית
[2-3 פסקאות בעברית]

## ציטוטים מרכזיים
- "Content is not king, consistency is."
- "The best marketing doesn't feel like marketing."

## תוכן מלא / קטעים נבחרים
[הקטעים הכי רלוונטיים מהמאמר]
```
