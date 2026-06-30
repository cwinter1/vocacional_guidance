# Career Guidance App — Project Plan

## Context

Built for a 41-year-old woman with ~20 years at Bank Hapoalim (BA in Business Administration). She works daily with CPAs, wants predictable/relaxed hours, strongly prefers in-person office work, and is exploring a career change. The original 12 hi-tech roles were too narrow — expanded to 20 roles thinking outside hi-tech.

The goal is a self-contained Hebrew single-page web app covering 5 phases of career change:
**self-assessment → career exploration → decision making → action planning → implementation**

Live at: `https://cwinter1.github.io/vocacional_guidance/`

---

## Architecture

Single file: `index.html`. No framework, no build step, no dependencies except Google Fonts. All CSS + JS inline. RTL Hebrew (`lang="he" dir="rtl"`).

---

## 20 Roles

### Hi-Tech (12)

| ID | Hebrew | English | Hours | Office |
|----|--------|---------|-------|--------|
| PM | מנהלת פרויקטים | Project Manager | בינוני | בינוני |
| SA | אנליסטית מערכות | System Analyst | נמוך | בינוני |
| BA | אנליסטית עסקית | Business Analyst | נמוך | בינוני |
| ERP | יועצת מערכות ERP | ERP Consultant | בינוני | גבוה |
| IMPL | מנהלת הטמעה | Implementation Manager | בינוני | גבוה |
| CSM | מנהלת הצלחת לקוח | Customer Success Manager | נמוך | בינוני |
| REGTECH | יועצת RegTech | RegTech Specialist | נמוך | גבוה |
| DATA | אנליסטית נתונים | Data Analyst | נמוך | בינוני |
| QA | מהנדסת בדיקות | QA Engineer | נמוך | בינוני |
| SCRUM | מנחת Scrum | Scrum Master | נמוך | בינוני |
| COACH | מאמנת קריירה | Career & Life Coach | נמוך | גבוה |
| CPA | רואת חשבון מוסמכת | Certified Public Accountant | גבוה | גבוה |

### Outside Hi-Tech (8)

| ID | Hebrew | English | Hours | Office |
|----|--------|---------|-------|--------|
| MORTGAGE | יועצת משכנתאות עצמאית | Independent Mortgage Advisor | נמוך | גבוה |
| INVEST | יועצת השקעות | Investment Advisor | בינוני | גבוה |
| TRAIN | מנהלת הדרכה ופיתוח | L&D Manager | נמוך | גבוה |
| OPS | מנהלת תפעול | Operations Manager | נמוך | גבוה |
| CX | מנהלת חוויית לקוח | Customer Experience Manager | נמוך | גבוה |
| CONTENT | כותבת תוכן פיננסי | Financial Content Writer | נמוך | בינוני* |
| COMPLY | מנהלת ציות ורגולציה | Senior Compliance Manager | נמוך | גבוה |
| FINLIT | מנחת חינוך פיננסי | Financial Literacy Educator | נמוך | גבוה |

*CONTENT: some remote work likely — flagged in card.

---

## 5 Career Domain Fields

Used for the animated % bar breakdown in results.

| ID | Hebrew | Icon | Role Weights |
|----|--------|------|--------------|
| COORD | ניהול ותיאום | 🗂 | PM:3, IMPL:3, SCRUM:3, OPS:2, TRAIN:2, BA:1, CSM:1 |
| ANALYSIS | ניתוח ומחקר | 🔍 | SA:3, BA:2, DATA:3, QA:2, COMPLY:1, INVEST:1 |
| FINANCE | פיננסים ורגולציה | 💰 | CPA:3, REGTECH:3, COMPLY:3, INVEST:3, MORTGAGE:3, DATA:1 |
| PEOPLE | אנשים ולקוחות | 🤝 | CSM:3, COACH:3, TRAIN:3, FINLIT:3, CX:3, IMPL:1, PM:1 |
| SYSTEMS | מערכות ותפעול | ⚙️ | ERP:3, QA:3, SA:2, IMPL:2, OPS:3 |

---

## Question Structure (30 total)

| Section | Hebrew | Questions | Scoring |
|---------|--------|-----------|---------|
| א | תגובה לשינוי ועמימות | Q0–Q4 | r:[] role IDs |
| ב | אנשים מול מערכות | Q5–Q9 | r:[] role IDs |
| ג | סמכות ואי-ודאות | Q10–Q14 | r:[] role IDs |
| ד | סגנון עבודה | Q15–Q19 | r:[] role IDs |
| ה | מיפוי כישורים מהבנק | Q20–Q24 | r:[] role IDs |
| ו | מה אני אוהבת ולאן אני רוצה ללכת | Q25–Q29 | f:[] field IDs |

Bridge questions (section ו) use `f:[]` arrays. Each bridge answer contributes 4 points directly to named fields.

---

## Scoring Logic

```
Field score = Σ(role_score[rid] × weight) + Σ(bridge_answers × 4)
Normalized to 0–100% for display.
```

CPA_RISK: answers indicating aversion to high hours subtract from CPA score.

---

## Results Screen

1. **Field % bars** — animated 0→pct over 0.9s (CSS transition + setTimeout 100ms)
2. **Top 3 role cards** — role name, score bar, description, next-steps list
3. **Hours × Office comparison table** — top 8 roles
4. **Accounting courses note** — CPA→yes, INVEST/COMPLY/REGTECH→maybe, others→no

---

## Deploy

GitHub Pages from `main` branch, root directory. Push to main = live update within ~30 seconds.
