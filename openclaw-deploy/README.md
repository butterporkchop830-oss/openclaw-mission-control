# ⚡ OpenClaw Mission Control Dashboard

A full-featured Staff Command Center for managing multiple AI agent nodes in real-time.

## 📁 Files

| File | Size | Purpose |
|------|------|---------|
| `index.html` | ~187 KB | Complete dashboard — all CSS & JS inline |
| `skills-index.json` | ~8.5 KB | Pre-indexed skills manifest (24 skills) |
| `vercel.json` | < 1 KB | Vercel deployment config |

## 🚀 Deploy to Vercel

### Option A — Vercel CLI (fastest)
```bash
npm i -g vercel
cd openclaw-deploy
vercel --prod
```

### Option B — Vercel Dashboard (drag & drop)
1. Go to [vercel.com/new](https://vercel.com/new)
2. Drag this entire folder onto the deploy zone
3. Click **Deploy**

### Option C — GitHub → Vercel (recommended for updates)
```bash
git init
git add .
git commit -m "Initial deploy — OpenClaw Mission Control"
git remote add origin https://github.com/YOUR_USERNAME/openclaw-mission-control.git
git push -u origin main
```
Then connect the repo in Vercel dashboard — auto-deploys on every push.

---

## ⚙️ Configuration

All config lives at the top of `index.html` around **line 2888**. Search for `WS_URL`:

```js
const WS_URL   = 'ws://100.69.83.7:18789';
const WS_TOKEN = 'f13a0ffe9b413751d90a306d657d131641374a480a6253bd';
```

> ⚠️ **Note:** The WebSocket connects to your private VPS at `100.69.83.7`. 
> Vercel hosts the frontend only — the WS connection still goes direct to your VPS.
> This means the dashboard works from anywhere in the world as long as your VPS is running.

---

## 🗂️ Tabs

1. **Overview** — Node status cards, CPU/RAM/GPU, health scores
2. **Agents** — Profile cards with photos, colors, roles, notes
3. **Tasks** — Kanban board (Backlog → In Progress → Done)
4. **Skills** — Searchable skills manifest
5. **Calendar** — Event tracking
6. **Telegram Log** — Chat interface
7. **Meeting Room** — Agent-to-agent communication log
8. **Activity Feed** — Live scrolling event log
9. **Memory** — Agent memories organized by day + long-term memory
10. **Docs** — Document repository (searchable, auto-categorized)
11. **Projects** — Project tracker with progress bars
12. **Team** — Org chart + editable Mission Statement
13. **Office** — Live 2D pixel art office with animated agents

## 💾 Persistence

All data auto-saves to **localStorage** in the browser:
- Agent photos, names, roles, accent colors
- Tasks and kanban state
- Meeting room log
- Sticky notes
- Memory entries and documents

---

## 🔌 WebSocket Protocol

The dashboard connects to your VPS gateway on load:

```
ws://100.69.83.7:18789
Auth: f13a0ffe9b413751d90a306d657d131641374a480a6253bd
```

Expected inbound message format:
```json
{
  "type": "node_update",
  "node": "vps",
  "cpu": 42,
  "ram": 61,
  "gpu": 15,
  "ping": 12,
  "model": "qwen3.5-flash",
  "health": 87
}
```

Auto-reconnects every 5 seconds if connection drops.

---

Built for the OpenClaw AI agent fleet 🐾
