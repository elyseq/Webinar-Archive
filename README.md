# Webinar Archive

The Webinar Archive is a searchable website for the USC Child Interview Laboratory webinar collection.

The goal of this project is to provide a simple way for users to browse archived webinars, search webinar topics, and (eventually) ask questions across webinar transcripts using AI.

The website is intentionally designed to be simple to maintain so that future lab members can continue updating it without needing extensive programming experience.

---

# Current Features

The website currently supports:

- Webinar library
- Individual webinar pages
- Vimeo video embeds
- Search by title, transcript, summary, and tags
- Webinar tags/categories
- AI search interface (backend still under development)
- Google Form sign-up button for webinar registration

---

# Website Structure

The project consists of only a few files.

```
index.html
Homepage containing the webinar library

webinar.html
Individual webinar page

webinars.json
Stores all webinar information

config.js
Stores AI configuration (not committed to GitHub!)

transcripts/
(eventually)
Stores transcript text files if transcripts are moved out of webinars.json
```

Most future edits will only require changes to **webinars.json**.

---

# Adding a New Webinar

## Step 1: Upload the video to Vimeo

Upload the webinar to Vimeo and copy the Vimeo video ID.

The Vimeo ID is the number in the URL:
- `https://vimeo.com/123456789` → ID is `123456789`


---

## Step 2: Open `webinars.json`

Every webinar looks something like this:

,{
  "id": ...,
  "title": "...",
  "date": "0000-00-00",
  "vimeoId": "...",
  "duration": "... mins",
  "summary": "...",
  "tags": ["...", "...", "..."],
  "transcript": "..."
}

Copy an existing webinar and update the information.

---

## Step 3: Save

Refresh the webpage.

The webinar should automatically appear.

No other code needs to be changed.

---

# Editing Existing Webinars

The following can all be edited inside `webinars.json`:

- Title
- Date
- Vimeo ID
- Duration
- Summary
- Tags
- Transcript

Nothing else needs to be updated.

---

# Search

The search bar currently searches:

- Webinar title
- Summary
- Transcript
- Tags

Results update automatically while typing.

---

# AI Search (Work in Progress)

The website already includes an AI search interface.

The eventual goal is to allow users to ask questions such as:

> Which webinars discuss delayed disclosure?

Instead of searching by keywords, the AI will search across webinar transcripts and recommend the most relevant webinars.

The current interface is complete, but the backend is still under development.

---

# Customizing Colors

The main color of the website is controlled near the top of both `index.html` and `webinar.html`.

```css
:root {
    --accent:
    --accent-light:
    --accent-hover:
}
```

Changing these values updates the color scheme throughout the website.

---

# Updating the Sign-Up Button

The "Sign up for webinars & archive access" button is located in the `<header>` of `index.html`.

Simply replace the Google Form link if the form ever changes.

---

# Future Improvements

Possible future additions include:

- Full AI-powered transcript search
- AI-generated webinar summaries
- Transcript files stored separately from `webinars.json`
- Better filtering options
- User login system
- Admin dashboard for adding webinars
- Automatic transcript processing

---

# Technologies Used

Current:

- HTML
- CSS
- JavaScript
- JSON
- Vimeo
- Google Forms

Planned:

- Open-source LLM
- Retrieval-Augmented Generation (RAG)
- Transcript indexing

---

# Philosophy of This Project

The website is intentionally designed to remain simple.

Instead of requiring a database or complicated server setup, webinar information is currently stored in a single JSON file. This makes the archive easy to understand, easy to edit, and easy to maintain by future lab members.

As the archive grows, additional features (AI search, transcript indexing, login systems, etc.) can be added without redesigning the website from scratch.


# Webinar Archive — Setup Guide

## Files in this folder

```
webinar-archive/
├── index.html       ← the entire website (one file)
├── webinar.html     ← individual webinars with vimeo embeds
├── webinars.json    ← all your webinar data
├── config.js        ← your Anthropic API key goes here
└── README.md        ← this file
```

---

## Run it locally (right now, no internet needed)

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

## Enable the AI search bar

1. Go to https://console.anthropic.com and create a free account
2. Create an API key (starts with `sk-ant-api03-...`)
3. Open `config.js` and paste your key:
   ```js
   const ANTHROPIC_API_KEY = 'sk-ant-api03-YOUR-KEY-HERE';
   ```
4. Save and refresh the browser

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
