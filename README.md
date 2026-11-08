# Invites

Animated digital wedding invitations, hosted free on GitHub Pages. A builder page lets anyone make a new invitation by filling in a form, with no coding and no git. Each couple gets their own folder and link.

| | Link |
|---|---|
| Builder | https://kajendran97.github.io/invites/ |
| An invitation | `https://kajendran97.github.io/invites/<couple>/` |
| Example | https://kajendran97.github.io/invites/mr-mrs/ |

> If you fork this repo, replace `kajendran97` with your own GitHub username.

## What a guest sees
1. A sealed envelope cover with the couple's monogram. Tapping the seal opens the letter.
2. The invitation:
   - names and families, with a countdown to the ceremony
   - date, time and venue, with **Add to calendar** and **Open in Maps** buttons
   - the day's schedule
   - a photo or illustration
3. **RSVP via WhatsApp:** the guest picks how many people are coming and the message is filled in for them.
4. Tap-to-call or copy-number cards for each contact, plus falling petals and lamp blessings.

### Personal guest links
Add `#First-Last` to the end of any invitation link:

```
https://kajendran97.github.io/invites/mr-mrs/#Mr-and-Mrs-Silva
```

The cover then says **"Dear Mr and Mrs Silva"** and their name is pre-filled in the RSVP. Dashes become spaces.

## Add a new couple (no coding, no git)
1. Open the **builder** → **New blank** (or **Start from sample** to see a filled example).
2. Fill in the form. The preview on the right updates as you type.
   - **Couple & families:** names, "Son of / Daughter of" lines, parents
   - **Date & time:** date, start and end time, ceremony time, time zone
   - **Venue:** name and area. The Maps link is made automatically.
   - **Contacts & RSVP:** phone numbers (the WhatsApp number fills in, e.g. `077…` → `9477…`) and the maximum guests per RSVP
   - **The day:** schedule rows. Add, remove and reorder them, and tick the key moment.
   - **Theme & photo:** gold, rose, emerald or navy, and a photo (resized automatically)
   - **Wording:** every line of text and the lamp blessings
3. Check **Folder name** (e.g. `nimal-kumudu`). **Site address** fills in automatically on the live site.
4. Click **Download invitation (.zip)** and unzip it. You get a folder like `nimal-kumudu/` containing:
   - `index.html`, the invitation
   - `photo.webp`
   - `share.jpg`, the image WhatsApp and Facebook show when the link is shared
5. On GitHub, open this repo → **Add file → Upload files** → drag the **folder** in → **Commit changes**.
6. Wait about a minute, then share `https://kajendran97.github.io/invites/nimal-kumudu/`.

## Edit an existing invitation
1. On GitHub, open the couple's folder → `index.html` → **Download raw file**.
2. In the builder, click **Load existing…** and pick that file. Every field comes back.
3. Make your changes, download the zip again, and upload it over the old folder.
   - If you didn't pick a new photo, upload just the new `index.html`. The existing `photo.webp` and `share.jpg` stay as they are.

## First-time setup (one-off)
1. Create a **public** repo named `invites` on a personal GitHub account. Free GitHub Pages needs a public repo.
2. Push these files to `main`:
   - `index.html`, `README.md`, `.gitignore`, `.nojekyll`
   - `template/`
   - `mr-mrs/`
3. Repo → **Settings → Pages** → **Deploy from a branch** → `main` / `(root)` → **Save**.
4. After 1–2 minutes the builder is live at `https://kajendran97.github.io/invites/`.

If you have Claude Code, `DEPLOY_WITH_CLAUDE.md` (shared separately, never committed) walks through all of this step by step.

## Project structure
```
invites/
├─ index.html               Builder: form, live preview, zip download. Runs in the browser only.
├─ template/
│  ├─ invite.html           The invitation design. Couple details live in one JSON block.
│  └─ sample-photo.webp     Photo for "Start from sample"
├─ mr-mrs/           One folder per couple, made by the builder
│  ├─ index.html            Self-contained: later template changes never affect it
│  ├─ photo.webp
│  └─ share.jpg             1200×630 link-preview image
├─ .nojekyll                Serve files as-is on GitHub Pages
└─ README.md
```

### How it works
- `template/invite.html` holds all couple details in a single `<script id="invite-data" type="application/json">` block. The page builds itself from that data:
  - countdown
  - calendar link
  - WhatsApp and phone links
  - schedule
  - theme
- The builder fetches the template, puts the form's data into that block, fills in the link-preview tags (`og:title`, `og:url`, `og:image`), and zips the result with the photo and preview image.
- Everything happens in the browser. The builder never talks to GitHub, so it needs no tokens or passwords.
- Themes are CSS variables at the top of `template/invite.html` (`[data-theme="rose"]` and so on). To add a theme, copy one block, change the colours, and add the option in the builder.

## Preview locally
The builder loads the template with `fetch`, so it needs a web server. Double-clicking `index.html` won't work.

```bash
npx serve .
```

Then open the address it prints, for example `http://localhost:3000`.

## Troubleshooting
| Problem | Fix |
|---|---|
| New invitation shows 404 | Wait 1–2 minutes for Pages to redeploy. Check the folder was uploaded with `index.html` directly inside it. |
| WhatsApp shows no preview or an old one | WhatsApp caches previews. Try the link in a new chat, or add `?v=2` to the end. Check **Site address** was filled in before downloading. |
| Builder preview is blank when run locally | Use a local server (see above), not a double-clicked file. |
| Wrong time in the calendar | Check the **Time zone** in the builder (Sri Lanka is +05:30). |

## Privacy
Because the repo is public, the names and phone numbers in each invitation can be seen in the source.
- Every page has `noindex, nofollow`, so search engines don't list them.
- An invitation can only be found by someone who has its link.
- Remove a couple's folder after the wedding if you prefer.
