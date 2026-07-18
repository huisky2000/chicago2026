# Chicago Trip App And GitHub Pages Guide

This note documents how the Chicago trip app is organized and how to publish it with GitHub Pages.

## Main Files

- `index.html`
  Main static web app. GitHub Pages serves this as the homepage.

- `.github/workflows/deploy.yml`
  GitHub Actions workflow for deploying the static site to GitHub Pages.

## What `index.html` Contains

The app is a single static HTML file. It does not need a build system.

Main sections:

- `Dashboard`
- `Flights`
- `Hotels`
- `Rentals`
- `Plan`
- `Map`
- `Drives`
- `Steak`
- `Notes`
- `Weather`
- `Sources`

Important features:

- Booking cards and planning cards open detail dialogs.
- The map uses Leaflet/OpenStreetMap and needs internet access.
- Map filters include hotels, culture, steak/grill, car rental, driving routes, and airport.
- Weather uses Open-Meteo and needs internet access.
- Editable planning notes are saved in the browser with local storage.

## How To Edit The HTML

Open `index.html` and search for the relevant section.

Common edits:

- Dashboard: search for `<section id="dashboard">`
- Flight bookings: search for `<section id="flights">`
- Hotel shortlist: search for `<section id="hotels">`
- Car rental shortlist: search for `<section id="rentals">`
- Draft plan: search for `<section id="timeline">`
- Map controls: search for `<section id="map">`
- Food ideas: search for `<section id="food">`
- Route links and detail data: search for `const routeLinks`
- Map points: search for `const mapPlaces`
- Map route lines: search for `const mapRoutes`
- Detail dialogs: search for `const detailWindows`

## How To Test Locally

Because this is static, you can open `index.html` directly in a browser.

Recommended quick check from PowerShell:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const scripts=[...html.matchAll(/<script>([\s\S]*?)<\/script>/g)].map(m=>m[1]); for (const s of scripts) new Function(s); console.log('inline scripts parse ok');"
```

Expected output:

```text
inline scripts parse ok
```

## GitHub Pages Deployment

The project is set up for GitHub Pages using:

```text
.github/workflows/deploy.yml
```

The workflow:

1. Runs on pushes to `main`.
2. Checks out the repository.
3. Configures GitHub Pages.
4. Copies `index.html` and any supporting static files into `_site`.
5. Uploads `_site` as a Pages artifact.
6. Deploys it to GitHub Pages.

## GitHub Repository Settings

In the GitHub repository:

1. Go to `Settings`.
2. Go to `Pages`.
3. Under `Build and deployment`, set `Source` to `GitHub Actions`.
4. Push changes to the `main` branch.
5. Open the `Actions` tab and watch the deployment workflow.

The published site URL appears in the deployment job.

## Useful Update Checklist

After changing `index.html`:

1. Run the inline JavaScript parse check.
2. Open `index.html` in a browser.
3. Click a booking card and confirm the detail dialog opens.
4. Open the map and test the filters.
5. Click several map markers.
6. Commit and push to `main`.
7. Check the GitHub Actions deployment.
