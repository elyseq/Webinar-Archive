# Webinar Archive

A searchable website for the USC Child Interview Laboratory webinar collection. Users can browse archived webinars, search by topic, and (eventually) ask questions across transcripts using AI.

Designed to be simple enough for future lab members to maintain without programming experience.

---

## Project Files

```
index.html        Homepage and webinar library
webinar.html      Individual webinar pages with Vimeo embeds
webinars.json     All webinar data (the only file you'll regularly edit)
config.js         Anthropic API key — not committed to GitHub
transcripts/      Transcript text files (planned)
```

---

## Running Locally

Browsers block local JSON loading for security, so you need a simple server instead of opening `index.html` directly.

**Mac** — open Terminal in the project folder and run:
```
python3 -m http.server 8000
```

**Windows** — open Command Prompt in the project folder and run:
```
python -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in your browser.

---

## Adding a New Webinar

### Step 1 — Upload to Vimeo

Upload the recording to Vimeo and copy the video ID from the URL:
- `https://vimeo.com/123456789` → ID is `123456789`

### Step 2 — Edit `webinars.json`

Each webinar entry looks like this:

```json
{
  "id": 85,
  "title": "Title of the Webinar",
  "date": "2025-04-18",
  "vimeoId": "123456789",
  "summary": "A short description of the webinar.",
  "tags": ["descriptive tag", "descriptive tag"],
  "transcript": ""
}
```

Copy the entry closest to the bottom of the file, paste it after the last entry, and update the fields. The `id` should be the next number in the list.

**Date format:** `YYYY-MM-DD`

**Tags:** Add all applicable tags from this list:
`physical abuse` `placement preferences` `positive pairing` `female perps` `narrative practice` `adolescent` `recantation` `delayed disclosure` `caregiver support` `overcoming reluctance` `suicide assessment` `credibility assessment` `male victims` `identifying individual episodes` `commercial sexual exploitation` `remote interviewing` `police skepticism` `prior disclosures` `clarifying body part terminology` `recency bias` `negative questions` `resolving inconsistencies` `clothing placement` `note taking` `trauma responses` `script and episodic memory`

**Transcript:** Leave as `""` for now — transcripts are filled in separately.

> Make sure there is a comma after the `}` of the entry above yours, and no comma after your new entry (the last entry never has a trailing comma).

### Step 3 — Save and verify

Save the file and refresh the browser. The webinar should appear automatically. No other files need to be changed.

---

## Contributing via GitHub Desktop

You do not need to know how to code to update the archive. A detailed first-time setup guide with screenshots is here: **[Webinar Archive Setup Guide](https://docs.google.com/document/d/1Z6nMfVLgREws9Tpc78Z9erEHxSp-OEsW2Ir5-C6Sxy4/edit?tab=t.x54u4k1fbrxb#heading=h.ywaf027ondt9)**

### First-time setup

1. Create a [GitHub account](https://github.com/signup)
2. Install [GitHub Desktop](https://desktop.github.com/)
3. Install [Visual Studio Code](https://code.visualstudio.com/)
4. In GitHub Desktop: *File → Clone Repository*, paste this repo's URL, and click **Clone**
5. Go to *File → Options → Integrations* and set the External Editor to **Visual Studio Code**

### Updating the archive

1. Open **GitHub Desktop**
2. Click **Open in Visual Studio Code**
3. Edit `webinars.json`
4. Save (`Ctrl+S` on Windows / `Cmd+S` on Mac)
5. Return to GitHub Desktop — your changes will appear automatically
6. Write a short summary (e.g. `Add webinar - Jane Doe April 2025`)
7. Click **Commit to main**
8. Click **Push origin**

The website will update within a few minutes.

---

## Search

The search bar searches webinar titles, summaries, transcripts, and tags. Results update automatically while typing. Tags are also clickable to filter by category.

---

## AI Search (Work in Progress)

The AI search interface is built and visible on the site, but the backend is still under development. The goal is to let users ask questions like *"Which webinars discuss delayed disclosure?"* and get relevant results across all transcripts.

### Enabling AI features locally

1. Go to [https://console.anthropic.com](https://console.anthropic.com) and create an account
2. Generate an API key (starts with `sk-ant-api03-...`)
3. Open `config.js` and paste your key:
   ```js
   const ANTHROPIC_API_KEY = 'sk-ant-api03-YOUR-KEY-HERE';
   ```
4. Save and refresh the browser

AI features (per-webinar Q&A and cross-webinar search) require this key. Everything else works without it.

---

## Customizing Colors

The accent color is defined near the top of both `index.html` and `webinar.html`:

```css
:root {
  --accent:
  --accent-light:
  --accent-hover:
}
```

Changing these three values updates the color scheme across the entire site.

---

## Updating the Sign-Up Button

The "Sign up for webinars & archive access" button is in the `<header>` of `index.html`. Replace the Google Form link there if the form ever changes.

---

## Future Plans

- AI-powered transcript search (RAG)
- AI-generated webinar summaries
- Transcript files stored separately from `webinars.json`
- Improved filtering options
- Admin interface for adding webinars

---

## Technologies

**Current:** HTML · CSS · JavaScript · JSON · Vimeo · Google Forms  
**Planned:** Open-source LLM · Retrieval-Augmented Generation · Transcript indexing