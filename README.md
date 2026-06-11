# Webinar Archive — Setup Guide

## Files in this folder

```
webinar-archive/
├── index.html       ← the entire website (one file)
├── webinars.json    ← all your webinar data
├── config.js        ← your Anthropic API key goes here
└── README.md        ← this file
```

---

## Step 1 — Run it locally (right now, no internet needed)

**Mac:**
Open Terminal, drag the `webinar-archive` folder into it, type:
```
cd <folder path>
python3 -m http.server 8000
```
Then open: http://localhost:8000

**Windows:**
Open Command Prompt in the folder and run:
```
python -m http.server 8000
```
Then open: http://localhost:8000

> Why not just open index.html directly? Browsers block local JSON file loading for security. The server fixes this.

---

## Step 2 — Add your Vimeo IDs

In `webinars.json`, replace each `"YOUR_VIMEO_ID_1"` with the actual Vimeo video ID.

The Vimeo ID is the number in the URL:
- `https://vimeo.com/123456789` → ID is `123456789`

---

## Step 3 — Enable the AI search bar

1. Go to https://console.anthropic.com and create a free account
2. Create an API key (starts with `sk-ant-api03-...`)
3. Open `config.js` and paste your key:
   ```js
   const ANTHROPIC_API_KEY = 'sk-ant-api03-YOUR-KEY-HERE';
   ```
4. Save and refresh the browser

---

## Step 4 — Customize your webinars

Edit `webinars.json` — each webinar has:

```json
{
  "id": 1,
  "title": "Your Webinar Title",
  "date": "2024-01-15",
  "vimeoId": "123456789",
  "duration": "58 min",
  "summary": "2-3 sentence description shown on the card and detail view.",
  "tags": ["tag1", "tag2", "tag3"],
  "transcript": "Full transcript text here. The AI uses this for search but it is never shown to users."
}
```

---

## Step 5 — Put it online (free, 2 minutes)

**Option A — Netlify Drop (easiest, no account needed):**
1. Go to https://app.netlify.com/drop
2. Drag your `webinar-archive` folder onto the page
3. Done — you get a live URL instantly

**Option B — GitHub Pages (free, requires GitHub account):**
1. Create a new GitHub repository
2. Upload all files
3. Go to Settings → Pages → Deploy from main branch
4. Your site is live at `https://yourusername.github.io/repo-name`

---

## Customization guide

### Change the site name
In `index.html`, find:
```html
<title>Webinar Archive</title>
```
and
```html
<h1>Webinar Archive</h1>
```

### Change the color scheme
In `index.html`, find the `:root` block at the top of `<style>` and change `--accent`:
```css
--accent: #2d5a8e;   /* change this to any color */
```

### Add/remove webinars
Just add or remove objects in `webinars.json`. Make sure IDs are unique.

### Add more tags
Tags are auto-generated from whatever you put in the `tags` arrays in `webinars.json`.

### Hide transcripts from users
Transcripts in `webinars.json` are used only for AI search and keyword matching — they are never displayed in the UI. This is already the default behavior.

---

## What works right now (without AI key)

- Browse all 10 webinars in a card grid
- Search by title, summary, and transcript text
- Filter by topic/tag
- Sort by date or alphabetically
- Click any card to open the detail modal with Vimeo embed and summary
- Transcript keyword match count shown on cards
- Click tags to filter

## What requires the AI key

- "Ask about this webinar" box in the detail modal
- "Ask a question across all webinars" at the bottom of the page
