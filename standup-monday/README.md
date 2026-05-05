# Oswald Daily Standup Dashboard

Team standup dashboard backed by Monday.com — no extra accounts, no JSONBin, no setup beyond what you already have.

## How it Works

All standup data (goals, blockers, announcements, attendance, leaderboard, PTO) is stored as a JSON blob inside a Monday.com item update on board 18293041857 (Non-Campaign Work), inside a group called "Daily Standup." A new item is created automatically each day. The dashboard auto-syncs every 30 seconds.

## Deploy to Vercel (5 minutes)

This must go on **Vercel** (not GitHub Pages) because the Monday.com API blocks direct browser requests — the `api/monday.js` file is a tiny serverless proxy that handles this.

### Step 1 — Push to GitHub

```bash
git init
git add .
git commit -m "Oswald standup dashboard"
git remote add origin https://github.com/YOUR-ORG/oswald-standup.git
git push -u origin main
```

### Step 2 — Deploy on Vercel

1. Go to [vercel.com](https://vercel.com) → New Project
2. Import your GitHub repo
3. Framework Preset: **Other** (no build needed)
4. Hit **Deploy** — live in ~30 seconds

No environment variables needed. Each user's Monday token is stored in their own browser only.

### Step 3 — Share the URL

Send the Vercel URL to your team. Bookmark it on the standup TV.

## First-Time Use (each team member)

1. Open the Vercel URL
2. Select your name
3. Paste your Monday.com API token
   - Monday → click avatar → Developers → API v2 Token → Copy
4. Click **Open Dashboard**

Credentials save to your browser. You only do this once per device.

## Updating

Edit `index.html` → push to GitHub → Vercel auto-redeploys in ~20 seconds.

## Customizing Team Members

In `index.html`, find:

```javascript
const TEAM = ['Randy Capehart','Tammy Shaw','Tyler Shaw','Kelsey Dus','Lauren Raben'];
```

Also update the `<option>` lists in the HTML for the attendance and PTO dropdowns.

## Data & Privacy

- All standup data lives in your existing Monday.com account
- Monday tokens are stored in each user's browser localStorage only
- The Vercel proxy passes tokens directly to Monday — they are never logged or stored server-side
- Data auto-resets each morning (goals, attendance, announcements, blockers)
- Leaderboard and PTO persist across days
