# Skilllab — AI Skills Dashboard PWA

## What this is
A single-file PWA (`ai-skills-dashboard.html`) for tracking AI skills and projects Bailey is building. Connected to Supabase for real-time sync. Deployed via GitHub Pages.

**Live URL:** https://baileyn111.github.io/skilllab/ai-skills-dashboard.html  
**Repo:** https://github.com/BaileyN111/skilllab  
**Local clone:** `C:\Users\baile\skilllab\`

---

## Supabase
- **Project ref:** zsefxchjujndqumfktiq  
- **URL:** https://zsefxchjujndqumfktiq.supabase.co  
- **Anon key** is hardcoded in the HTML (safe — RLS controls access)
- **Table:** `projects`

### Schema
```
id           int8        primary key
name         text
description  text
stage        int4        (0–4)
tags         jsonb       (kept in DB, hidden in UI — can restore later)
notes        text
priority     jsonb       DEFAULT '{}'  ← MUST BE ADDED if not done yet
created_at   timestamptz
```

**✅ `priority` column confirmed added (June 2026).** Priority scoring is fully live.

---

## Design system
- **Font:** Syne (headings/UI) + Space Mono (monospace labels/badges)
- **Dark theme:** `--bg: #0a0a0f`, `--surface: #12121a`, `--border: #1e1e2e`
- **Accent colours:** `--accent: #7c3aed` (purple), `--accent2: #06b6d4` (cyan), `--accent3: #f59e0b` (amber)
- **High contrast buttons:** solid white fill (`#ffffff`), dark text (`#0a0a0f`), `font-weight:800`, `2px` borders
- **Stage colours:** grey → purple → cyan → green → amber (maps to stages 0–4)
- Cards have a 2px top colour bar per stage

---

## Features built (in order)
1. ✅ Core CRUD — add/edit/delete projects with name, description, stage, notes
2. ✅ Real-time Supabase sync with live indicator dot
3. ✅ Stage pipeline (Ideation → Creation → Integration → Testing → Refining)
4. ✅ Tags removed from UI (data kept in DB)
5. ✅ **+ New Skill** button — bold white pill in header (Option C)
6. ✅ Search — 🔍 toggle in header, slide-down input, filters name + desc + notes live
7. ✅ Priority scoring system:
   - Formula: `(freq × annoyance × 0.4) + (leverage × 2) + (activation × 2) + (transferability × 2)` = max 100
   - Collapsible ⚡ panel inside each card's detail modal
   - 5 sliders (1–10) with tailored descriptions based on Bailey's actual projects
   - Amber score badge on every card
   - 4 sort modes: ⚡↓ ⚡↑ Stage↑ Stage↓
   - Auto-saves to Supabase 800ms after last slider move

---

## Remaining items (from [meta] card in Skilllab)
### Next: KPI Timeline Tracker
Track how the stage distribution of all projects changes over time. Goals:
- Store a daily/weekly snapshot of stage counts in a new Supabase table (e.g. `snapshots`)
- Show a small chart in the app of how the portfolio is progressing
- Could use a cron job or trigger on the Supabase side to auto-snapshot
- Reward mechanism when Bailey is making progress

### After that: Desktop Widget / Dynamic Background
An always-on tracker showing:
- Skilllab KPIs (skills in progress, avg priority score, stage distribution)
- Fitness goals
- Wellbeing (sleep, mindfulness)
- Budget / financial goals
- Reading goals

Options explored: dynamic desktop wallpaper, Electron app overlay, browser-based always-on window. Big project — needs its own session.

---

## Bailey's preferences (coding style)
- Explain before implementing — describe what you're going to do, get approval
- Do changes in stages, one at a time
- Offer aesthetic options before making visual choices
- High contrast, bold lines, `2px` borders on interactive elements
- No comments in code unless non-obvious
- Keep everything in the single HTML file — no build tools, no frameworks
- Single GitHub commit per feature stage with descriptive message
