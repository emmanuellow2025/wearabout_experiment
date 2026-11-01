# Wearabouts – Iter 2.5 Wardrobe Experiment

A Vue 3 Composition API (`<script setup>`) prototype for a between-subjects comparison of **A: category navigation + tag filters** and **B: functional free-text search**. Both variants share the same 24 items, target clothing, layout, and selection behavior.

## Run locally

Requirements: Node.js (current LTS) and npm.

```bash
npm install
npm run dev
```

Open the local address Vite prints (usually `http://localhost:5173/`).

For production: `npm run build` and publish the `dist/` folder to Netlify, Vercel, or another static host.

## Share participant links

- Version A: `https://YOUR-DEPLOYED-URL/?version=A`
- Version B: `https://YOUR-DEPLOYED-URL/?version=B`

Randomly allocate participants yourself (e.g. 10 to each for your planned 20 participants). The links do **not** automatically randomize. Avoid telling participants which interface is expected to be better.

## Task

> You are going for dinner with friends. Find the three pieces shown in the reference images. Select each item and add it to your outfit.

The reference images appear beside the wardrobe on larger screens and above it on mobile, without item names. Each reference is marked as found after its matching item is added.

The app recognizes the *Silk Blouse* (green), *Brown Pants*, and *White Sneakers* as targets; other items can be selected but do not satisfy the task. Timer stops when all three targets are selected.

## Data collection

The end-of-task CSV includes participant code (if entered), variant, completion, time, number of non-typing interactions, search input update count, selected items, and timestamped action log. The file is downloaded **locally only**. It is not transmitted or saved to a server. Ask participants to submit their exported CSV or have the researcher export it on a shared device.

For perceived ease-of-use and satisfaction, use identical 1–5 post-task Maze questions (or another survey) for both groups.

## Important limits

- This is a research prototype, not the full app. Clothing is rendered using simple SVG silhouettes, not the original Figma assets. You can replace the silhouettes with your approved project images for better fidelity.
- With the current 24-item mock wardrobe, benchmark results describe this prototype, not the larger real wardrobe; add all actual items to `wardrobe` in `src/App.vue` if you want closer fidelity.
- Searching is case-insensitive AND matching across name, category, colour, occasion, weather; it is genuinely typed input, not a predetermined suggestion click.
- Version A's filters act immediately after clicking a tag; the Apply button closes the filter panel. If your Figma design requires delayed application, change this behavior before testing.
- Use identical devices/screen sizes where feasible; because A supports more taps while B supports keyboard input, raw click counts are **not** a completely equivalent effort measure. Prefer completion time, success, and subjective ease of use as primary outcomes.
- No automatic collection of abandonment sessions; only completed tasks expose the summary/CSV. For reliable failure data, use an external experiment tool with a timeout and abort criteria, or add researcher controls before formal testing.
- Maze website-test capabilities depend on the plan. Verify availability in your team's account. Otherwise conduct moderated tests and record results manually.
