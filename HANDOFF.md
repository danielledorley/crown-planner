# Crown Planner – Handoff

## What I need from you (ChatGPT)

1. Using the GitHub plugin, create a **public** repo named `crown-planner` under my account.
2. Upload every file from the attached `crown-planner.zip` to the repo root, keeping the names as they are. Include the hidden `.nojekyll` file:
   - `index.html`
   - `manifest.webmanifest`
   - `icon.svg`, `icon-192.png`, `icon-512.png`
   - `README.md`, `HANDOFF.md`
   - `.nojekyll`
3. Turn on GitHub Pages: branch `main`, folder `/ (root)`.
4. Give me the live URL (`https://<username>.github.io/crown-planner/`) and the origin to use in Google Cloud (`https://<username>.github.io`).
5. If the plugin can't turn on Pages or upload binary files (the PNGs), tell me which steps I need to do by hand.

Please don't rewrite or restyle the app. It's built and tested. Only make changes I ask for.

---

## About the app

Crown Planner is a personal hair planning web app for kinky coily hair. My mom may also use it on her own phone.

- **Styles**: style "recipes" with products, tools and materials (with a have-it check), ordered steps, inspo photos, and tutorial links. YouTube, TikTok, Instagram and Pinterest links play in the app. Other links open in a new tab.
- **List**: a shopping list grouped by category. It can pull a style's missing items, and checking an item off marks it as owned on the style.
- **Planner**: month calendar, day view, quick-add templates, repeating tasks, and "Coming up" for the next 3 weeks.
- **Plan this style** wizard: from one wash day date it creates a supply run (3 days before), wash day, style day (same day to 3 days later), a mid-way refresh and a take-down. The task notes come from the chosen wash routine and the style's steps.
- **Google Calendar sync**: one-way, app to Google. Saving a task creates or updates the event, and deleting a task removes it.
- **Settings**: Google Client ID and calendar ID, sync-all, backup export/import (JSON, includes photos), add starter looks, erase everything.

Design: sea glass and gold, glossy Y2K buttons, frosted glass cards, sparkles, Great Vibes script with Quicksand. Mobile first, and it can be added to the home screen.

## Tech notes

- **Single file, no build step.** All HTML, CSS and JS are in `index.html`, inside one IIFE. There's no framework.
- **External scripts:**
  - Google Fonts.
  - Google Identity Services, from `https://accounts.google.com/gsi/client`.
- **Storage:**
  - `localStorage` key `crownPlanner.v1` holds all the data.
  - IndexedDB database `crownPlanner`, store `photos`, holds the photos as compressed JPEG data URLs keyed by photo id.
  - `sessionStorage` key `cp.tok` holds the Google access token.
- **Rendering:** `render()` rebuilds `#view` from template strings. Click, submit and change events are handled through delegation using `data-act`, `data-form` and `data-change`, mapped to the `ACT`, `FORMS` and `CHG` objects. Pop-up forms open in a bottom sheet through `openSheet()`.
- **Google auth:**
  - Uses the GIS token client with the `calendar.events` scope and Calendar API v3 calls through `fetch` in `gApi()`.
  - Tokens last about an hour.
  - The Client ID is entered in Settings, not hard-coded.
- **Recurrence:**
  - Inside the app, repeats are expanded by `occursOn()`.
  - On Google they're sent as an RRULE: WEEKLY with an interval of 1, 2, 4 or 6, or MONTHLY.
  - Each repeat is marked done separately through `task.doneDates[]`.

### Data model

```js
{
  v: 1,
  styles: [{ id, name, emoji, notes,
             items: [{ id, name, cat: 'product'|'tool'|'material', have }],
             steps: [{ id, text }],
             inspo: [photoId],                 // IndexedDB keys
             videos: [{ id, url, title }] }],
  shopping: [{ id, name, cat, done, styleId, styleItemId }],
  tasks: [{ id, title, date: 'YYYY-MM-DD', allDay, time: 'HH:MM', duration /*min*/,
            repeat: 'none'|'w1'|'w2'|'w4'|'w6'|'m1', reminder /*min, -1 = Google default*/,
            notes, styleId, sync, gEventId, gLink, doneDates: [] }],
  settings: { clientId, calendarId: 'primary', autoSync, gLinked }
}
```

Starter looks come from `seed()`: Wash Day Reset, Twist Out, Two-Strand Twists, Twists with Added Hair. My wash day steps are in `WASH_STEPS`.

## Google Calendar setup

I'll do this after the site is live. The full steps are in `README.md` and in the app under Settings. In short:

1. Create a Google Cloud project.
2. Enable the Calendar API.
3. Set up the consent screen with the audience set to External and Testing. Add my Gmail and my mom's as test users.
4. Create a Web OAuth client with the origin `https://<username>.github.io`.

## Known limits

- Data stays on each device and doesn't sync between phones. Backup export and import is the workaround.
- On iPhone, Safari and the home-screen app keep separate storage.
- Sync only goes from the app to Google.
- TikTok `vm.` short links and Pinterest `pin.it` links can't be embedded. They show as "Open in…" links.

## Rules if I ask for changes

- Keep everything in `index.html` with no build tools.
- Don't change the `crownPlanner.v1` key or the data model without a migration in `load()`.
- Keep the sea glass and gold look.
- Test at 390px wide.
