# Pain Tracker

## Goal
A simple web app for people with chronic pain to track their recovery over time. Instead of
the traditional 1-10 pain scale (which is hard to use consistently), users answer one
question per tracker per day: "Did it get better, stay the same, or get worse?" Over time,
this builds a meaningful recovery trend graph. Users can also add free-text notes for context.

## Key Decisions
- Better/Same/Worse instead of numeric scale: reduces cognitive load, leverages humans' strength at relative comparison
- Multi-tracker support: users create named trackers (e.g. "knee pain", "back pain") each with independent data and graphs
- Responsive web app first, PWA later: avoids asking non-technical users to understand PWA install flows
- Local-only storage for MVP (IndexedDB): fastest path to working product, no backend needed
- Architecture must be extendable for auth + cloud DB later: keep data layer abstracted so we can swap in a backend
- Security is a high priority: even in MVP, treat health data with care (no analytics/tracking, no data leakage)
- Graph starts at 0, plots cumulative trend: +1 for better, 0 for same, -1 for worse, normalized over time
- Free-text notes per entry: no tagging for MVP, but data model should allow adding structured tags later

## MVP Scope
**In:**
- Create/rename/delete named pain trackers
- Daily check-in per tracker: better / same / worse
- Optional free-text note per check-in
- Recovery trend graph per tracker (cumulative score over time)
- All data stored locally in browser (IndexedDB)
- Mobile-friendly responsive design
- No third-party analytics or tracking scripts

**Out (future):**
- User accounts and cloud sync
- PWA install + offline support + push notification reminders
- Structured tags on notes (activity, sleep, stress)
- Data export (CSV/PDF)
- Sharing/doctor view
- Reminder notifications

## Tech Stack
- Next.js (static export, no server needed for MVP)
- Tailwind CSS for styling
- IndexedDB via Dexie.js for local storage
- Chart.js or Recharts for the trend graph
- Deploy to Vercel (free tier)

## Tasks
- [x] Scaffold Next.js project with Tailwind
- [x] Set up Dexie.js with data model (trackers, entries with better/same/worse + notes + timestamp)
- [x] Build data access layer abstracted behind an interface (so backend can be swapped in later)
- [x] Home screen: list of trackers with quick-glance status
- [x] Create/rename/delete tracker flow
- [x] Daily check-in UI: better/same/worse buttons + optional note field
- [x] Store check-in entries in IndexedDB
- [x] Recovery trend graph per tracker (cumulative score over time)
- [x] Mobile-responsive layout and polish
- [x] Deploy to Vercel
