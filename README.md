# Ye Concert Preservation

A fan-made, non-commercial concert archive and custom viewing experience by [Jayanth.mov](https://jayanth.mov).

The first release preserves Ye's SoFi Stadium Night 2 performance from April 3, 2026. The player is built around the concert rather than a generic embed: it includes a chapter-aware timeline, full setlist navigation, custom playback controls, cinema and fullscreen modes, responsive mobile layouts, credits, and shareable timestamp links.

## Live site

- Concert experience: [ye.jayanth.mov](https://ye.jayanth.mov)
- Main Jayanth.mov links: [jayanth.mov](https://jayanth.mov)

## Project structure

```text
.
├── index.html                  # Jayanth.mov link page
├── IMG_7547 2.JPG             # Link-page profile image
├── Ye.png                     # Concert and preservation hero image
└── ye
    ├── index.html              # Concert player and setlist
    ├── favicon.svg
    └── preservation
        └── index.html          # Preservation project page
```

The site is intentionally framework-free. Each page is self-contained HTML, CSS, and JavaScript, so it can be served by any static host.

## Run locally

From the repository root:

```bash
python3 -m http.server 8080
```

Then open:

- `http://localhost:8080/`
- `http://localhost:8080/ye/`
- `http://localhost:8080/ye/preservation/`

## Video hosting

The concert video is not stored in this repository. The player currently streams a separately hosted MP4 from Oracle Cloud Object Storage. Keeping the media external prevents a roughly 18 GB source file from entering Git history and lets the browser request byte ranges for seeking.

For a larger archive, the planned direction is adaptive HLS playback backed by object storage so viewers on slower or more distant connections can receive an appropriate bitrate.

## Deploy

The Ye site is currently deployed to Cloudflare Pages. Build the small deployment directory and publish it with Wrangler:

```bash
rm -rf .deploy/ye
mkdir -p .deploy/ye
cp ye/index.html ye/favicon.svg Ye.png .deploy/ye/
cp -R ye/preservation .deploy/ye/preservation
npx wrangler@latest pages deploy .deploy/ye \
  --project-name ye-jayanth-mov \
  --branch main
```

Wrangler will prompt for Cloudflare authentication when needed. Never commit API tokens or account credentials.

## Preservation and credits

This is an independent preservation project and is not affiliated with Ye or his team. The current concert compilation combines footage recorded by Jayanth.mov in the pit with credited community recordings and material from the official live concert stream. Full recording credits are available inside the player.

To support or contribute to the preservation effort, use the contact options on the [preservation page](https://ye.jayanth.mov/preservation/).

