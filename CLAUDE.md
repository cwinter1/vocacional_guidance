# vocacional_guidance — Project Instructions

## What this is

A Hebrew single-page career guidance web app. Self-assessment questionnaire (30 questions) → 20 role matches → 5 career field % bars → action plan.

Live: `https://cwinter1.github.io/vocacional_guidance/`

## Architecture

- **Single file**: `index.html` — no framework, no build step, no npm
- **All inline**: CSS + JS in `<style>` and `<script>` blocks
- **Language**: Full Hebrew, RTL (`lang="he" dir="rtl"`)
- **Fonts**: Space Grotesk (display), Manrope (body), JetBrains Mono (mono), Instrument Serif (italic) — via Google Fonts

## Design Tokens

```css
--bg:    #0e1116
--fg:    #e8e5dd
--sub:   #8a8478
--card:  #16191e
--card2: #1c1f25
--accent: #7aa676
--hair:  rgba(255,255,255,0.10)
--pill:  rgba(255,255,255,0.06)
--mono:  rgba(232,229,221,0.55)
```

Same token set as `workout`, `maya-math`, and `winter-finance` repos.

## Data Structures

```javascript
// Role
{ id:'PM', icon:'🗓', he:'מנהלת פרויקטים', en:'Project Manager',
  hours:'בינוני', office:'גבוה', coding:false,
  summary:'...', day:['...'], note:'...' }

// Question (role-based, Q0–Q24)
{ s:0, q:'...', ctx:'', opts:[ { t:'...', r:['PM','BA'] }, ... ] }

// Question (bridge, Q25–Q29)
{ s:5, q:'...', ctx:'...', opts:[ { t:'...', f:['PEOPLE'] }, ... ] }

// FIELDS (career domain)
{ id:'COORD', he:'ניהול ותיאום', icon:'🗂', desc:'...', roles:{ PM:3, BA:1 } }

// ROLE_RESULTS
PM: { desc:'...', steps:['...'] }
```

## Scoring

- Q0–Q24: `opt.r[]` → increment `scores[rid]`
- Q25–Q29: `opt.f[]` → `fieldScores[fid] += 4`
- Field score = Σ(role_score × weight) + bridge scores
- Normalized to 0–100% for display
- `CPA_RISK` in `r[]` subtracts from CPA score (strict hours preference)

## Deploy

```bash
git add index.html
git commit -m "your message"
git push origin main
```

GitHub Pages serves from `main` branch, root directory. Live within ~30 seconds.

## Context

See `plan.md` for full role list, field weights, and project rationale.
