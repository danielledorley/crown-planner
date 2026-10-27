# 👑 Crown Planner

Plan it ✦ slay it. A sea glass and gold hair planner that lives on your phone.

- **Style recipes**: each look has its products, tools, materials, steps, inspo pics and tutorial links (YouTube, TikTok, Instagram, Pinterest).
- **Hair haul list**: a shopping list that pulls missing items from any style. Checking an item off marks it as "have it" on the style.
- **Planner**: month calendar, quick adds (wash day, deep condition, trim…), repeating routines, and a "Plan this style" button that maps out shopping, prep night, install, refresh and take-down.
- **Google Calendar sync**: tasks you save can go straight to your Google Calendar, with your supply list and steps in the event notes.

Everything is saved on your phone. Use **Settings → Export backup** now and then.

---

## 1. Put it on GitHub Pages (GitHub Desktop)

1. In GitHub Desktop: **File → New repository**. Name it `crown-planner`. Create it.
2. **Repository → Show in Finder/Explorer**. Copy all the files from this folder into it (`index.html`, `icon*.png`, `icon.svg`, `manifest.webmanifest`, `README.md`, `.nojekyll`).
3. Commit to `main`, then **Publish repository**. Uncheck "Keep this code private" (free GitHub Pages needs a public repo).
4. On github.com, open the repo → **Settings → Pages**. Under **Build and deployment**, pick **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
5. In a minute or two your app is live at `https://YOUR-USERNAME.github.io/crown-planner/`.

**Add it to your home screen:** open that link in Safari → Share → **Add to Home Screen**.

> Tip: on iPhone, the home-screen app and Safari keep separate storage. Pick one and stick with it.

## 2. Connect Google Calendar (one time, ~10 min)

The app talks to Google directly from your phone. Google needs to know it's your app, so you make a free "Client ID".

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and create a project called **Crown Planner**.
2. Search for **Google Calendar API** and click **Enable**.
3. Open **Google Auth Platform** (formerly "OAuth consent screen"):
   - **Branding**: app name *Crown Planner*, your email as support and developer contact.
   - **Audience**: choose **External**. Leave it in **Testing**. Under **Test users**, add your own Gmail.
4. **Clients → Create client**:
   - Application type: **Web application**
   - **Authorized JavaScript origins**: `https://YOUR-USERNAME.github.io` (just the origin, no `/crown-planner` path)
   - Create, then copy the **Client ID** (ends in `.apps.googleusercontent.com`).
5. In the app: **Settings** → paste the Client ID → **Save** → **Connect**.
6. Google will warn that the app isn't verified. That's normal for your own app. Tap **Continue** and allow calendar access.

**Good to know**
- Events land on your main calendar in teal (Peacock). To use a separate calendar, create one in Google Calendar, copy its **Calendar ID** from its settings, and paste it in the app's Calendar field.
- Google logins from the app last about an hour. If a sync asks you to sign in again, that's why.
- Editing or deleting a task in the app updates or removes the Google event too. Changes made directly in Google Calendar don't flow back into the app.
- If the Google pop-up won't open from the home-screen app, open the app in Safari and connect there.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest`, `icon*.png`, `icon.svg` | Home-screen name and icon |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |
