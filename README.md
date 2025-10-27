# CrossSlip Ultra Pro

CrossSlip Ultra Pro is a self-contained React + Tesseract.js prototype for parsing sportsbook slip screenshots, extracting bets, and surfacing implied probability plus bankroll guidance.

This repository ships as a static bundle so you can drop it into any static hosting provider or embed it inside an existing project without a complex build step.

## Quick start

1. **Clone the repo**
   ```bash
   git clone https://github.com/your-org/CrossSlipPro.git
   cd CrossSlipPro
   ```
2. **Open the app**
   - Double-click `index.html`, or
   - Serve the folder with any static file server:
     ```bash
     python -m http.server 4173
     ```
     Then browse to <http://localhost:4173>.

No additional build tooling is required—the bundled UMD builds of React and Tesseract.js are loaded via CDN.

## Adding the analyzer to another project

Because everything lives in a single HTML file, there are three lightweight ways to embed the analyzer elsewhere:

### 1. Direct link/iframe
- Deploy this repo as-is (Netlify, Vercel, GitHub Pages, S3, etc.).
- In your primary app, render it inside an `<iframe>` pointing to the deployed URL.
- Pass configuration via query params (e.g., bankroll, default theme) if needed.

### 2. Import the markup into an existing static site
1. Copy `index.html`, `logo.png`, and `slipscan-logo.png` into your project’s `public` folder.
2. Ensure the `<script>` tags that load React, ReactDOM, and Tesseract.js stay at the bottom of the `<body>`.
3. If your app already loads React from a different version, remove the duplicated CDN scripts and rely on your bundler’s React build.

### 3. Integrate with a bundler
If you need tighter integration inside a React/Vite/Next.js codebase:

1. Copy the `<style>` block into a dedicated stylesheet (e.g., `src/styles/csu.css`) and import it where appropriate.
2. Convert the inline React components at the bottom of `index.html` into standard component files. The main entry point is `App`, rendered with `ReactDOM.createRoot`.
3. Replace the global `localStorage` keys (`csu_results_v3`, `csu_teams_v2`) if they conflict with your app.
4. Install dependencies:
   ```bash
   npm install react react-dom tesseract.js
   ```
5. Wrap the analyzer component wherever you want it to appear.

## Customization tips

- Update the `DEFAULT_TEAMS` object in `index.html` for project-specific defaults.
- Adjust the summary badges and CSV export columns inside the `App` component to match your reporting needs.
- To replace branding, swap out `logo.png`/`slipscan-logo.png` and the `wordmark` copy in the header.

## Deploying updates

Because the app is static:

1. Commit changes to `index.html` and any assets.
2. Push to your hosting provider or GitHub Pages.
3. Bust CDN cache or update the deployment URL if you need instant refresh.

## Troubleshooting

- **OCR accuracy issues:** ensure screenshots are sharp and high-contrast; tweak the Tesseract `lang` option if you need non-English slips.
- **LocalStorage errors:** browser privacy modes may block storage; the app will fall back to an in-memory session, but persistent data may reset.
- **CSV exports won’t open:** confirm your spreadsheet locale uses commas as separators; otherwise, import the CSV specifying UTF-8 encoding.

## License

Specify your project’s license here.
