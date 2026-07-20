# Design Demo Hub

A single page that lists your Claude design prototypes so contractors can open them and you can track status in one place.

Important: this version hosts the actual demo files inside the repo, instead of linking out to Claude. Links to Claude Enterprise artifacts only work for people signed into your org, so contractors could not open them. Hosting the exported file on GitHub Pages means anyone with the link can open it, no Claude login needed.

## What is in this repo

- `index.html`: the page contractors will open. It reads `demos.json` and displays each demo as a card with a status badge, filters, and search.
- `demos.json`: the data file. Each entry points to a demo file inside the `demos` folder.
- `demos/`: the actual demo pages, exported from Claude. `m1-checkin-flow.html` is a placeholder example, replace it with your real export.
- `README.md`: this file.

## One time setup on GitHub

1. Go to github.com and create a new repository. Suggested name: `design-demo-hub`. Set it to public, since GitHub Pages on a free plan only serves public repos.
2. Upload `index.html`, `demos.json`, `README.md`, and the whole `demos` folder to the repo. Easiest way: on the repo page, click "Add file" then "Upload files," drag in everything, and commit.
3. Go to the repo's Settings tab, then Pages in the left sidebar.
4. Under "Build and deployment," set Source to "Deploy from a branch," pick the `main` branch and the `/ (root)` folder, then Save.
5. GitHub will give you a live URL, usually `https://yourusername.github.io/design-demo-hub/`. It can take a minute or two to go live.
6. Send that URL to your contractors. That is the page they open to view and track demos.

## Exporting a Claude artifact so it can be hosted here

**If the artifact is HTML:**
1. Open the artifact in Claude, click the code view icon in the artifact panel.
2. Select all and copy the code.
3. Paste it into a new file inside `demos`, for example `demos/people-profile-admin.html`.
4. It should run as is, no changes needed.

**If the artifact is React:**
React artifacts depend on Claude's built in libraries (React, Tailwind, lucide icons, and similar) and will not run if you just copy the code into a plain HTML file. You have two options:
- Ask Claude to rebuild it as a self-contained HTML file that loads React and Babel from a CDN, so it runs anywhere with no build step. Paste the artifact code back to me and I can do this conversion for you.
- If interactivity is not essential for the review, export a screenshot or short screen recording instead and embed that image in a simple HTML page.

## Adding a new demo to the hub

1. Export the artifact using the steps above and save it into `demos`.
2. Open `demos.json` in the repo (click the file, then the pencil icon to edit).
3. Copy one of the existing entries and paste it as a new item, then update the fields:
   - `name`: what the demo is
   - `module`: `M1 App` or `People Module`
   - `link`: the relative path to your file, for example `demos/screen-name.html`
   - `status`: `In Review`, `Needs Feedback`, or `Approved`
   - `date`: when you last updated it
   - `owner`: your name
   - `notes`: a short note for context
4. Commit the change. The live page updates automatically within a minute.

## A note on confidentiality

Because GitHub Pages on the free plan requires a public repo, anyone with the URL can open the hub and any demo inside it, whether or not they have a GitHub account. This solves the login problem but the tradeoff is that the link itself becomes the only barrier, similar to an unlisted video. If these designs are sensitive or pre-release, consider:

- Upgrading to GitHub Team or Enterprise, which allows Pages on a private repo, then adding contractors as collaborators with Read access.
- Adding a simple shared password check in `index.html` as a light deterrent, though this is not real security since the page code is still visible to anyone who looks.
- Keeping the repo private and having contractors clone it or view files directly in GitHub instead of through Pages, which requires them to have a GitHub account added as a collaborator.

## Tracking status over time

The `status` field doubles as your tracker. At a glance you can see what is still `In Review`, what contractors flagged as `Needs Feedback`, and what is `Approved`. GitHub's commit history on `demos.json` also keeps a full log of every edit with timestamps.
