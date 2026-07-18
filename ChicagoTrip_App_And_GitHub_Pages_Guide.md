# Chicago Trip App And GitHub Pages Guide

This note documents the map-first Chicago trip app and the GitHub Pages deployment workflow.

## Main Files

- `index.html`
  Main static web app. GitHub Pages serves this as the homepage.

- `site.webmanifest`
  Home-screen app metadata for Android and other installable-browser flows.

- `icons/`
  Home-screen icons, including `apple-touch-icon.png` for iPhone/iPad.

- `.github/workflows/deploy.yml`
  GitHub Actions workflow for deploying the static site to GitHub Pages.

## App Shape

The app is now map-first. The main screen is:

- A large interactive Chicago map.
- Category filters: flights, hotels, culture, nature, steak/BBQ, cars, drives, airport.
- Day chips for 4-11 Oct.
- A compact side panel that changes when a map pin or visible-place item is selected.
- A small lower area for suggested flow, decisions, notes, weather, and sources.

This keeps most information behind interaction instead of showing long text sections.

## How To Edit

Open `index.html` and search for these data blocks:

- `routeLinks`: Google Maps and official route links.
- `places`: all map pins, notes, categories, dates, and primary actions.
- `routes`: visible route lines on the map.
- `weatherLocations`: live weather cards.
- `site.webmanifest` and `icons/`: mobile home-screen name, theme color, and icon assets.

Most updates should be made in `places`.

Example place:

```js
{ id: "example", label: "C", type: "culture", day: "oct7", title: "Example Place", coords: [41.88, -87.63], note: "Short note.", action: "Website", url: "https://example.com" }
```

Useful `type` values:

- `airport`
- `flight`
- `hotel`
- `culture`
- `nature`
- `food`
- `rental`
- `drive`

Useful `day` values:

- `all`
- `oct4`
- `oct5`
- `oct6`
- `oct7`
- `oct8`
- `oct9`
- `oct10`
- `oct11`

## How To Test Locally

Open `index.html` directly in a browser.

Quick JavaScript parse check from PowerShell:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const scripts=[...html.matchAll(/<script>([\s\S]*?)<\/script>/g)].map(m=>m[1]); for (const s of scripts) new Function(s); console.log('inline scripts parse ok');"
```

Expected output:

```text
inline scripts parse ok
```

Also check:

1. Map loads.
2. Category filters change visible pins.
3. Day chips change visible pins.
4. Clicking a pin updates the side panel.
5. Planning notes save in the browser.
6. The browser can load `site.webmanifest` and the files in `icons/`.

## GitHub Pages Deployment

The project is set up for GitHub Pages using:

```text
.github/workflows/deploy.yml
```

The workflow:

1. Runs on pushes to `main`.
2. Checks out the repository.
3. Configures GitHub Pages.
4. Copies `index.html` and supporting static files into `_site`.
5. Uploads `_site` as a Pages artifact.
6. Deploys it to GitHub Pages.

In the GitHub repository, set `Settings -> Pages -> Build and deployment -> Source` to `GitHub Actions`.
