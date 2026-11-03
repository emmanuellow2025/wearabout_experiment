# Wearabouts – Iter 2.5 Wardrobe Experiment

A Vue 3 Composition API (`<script setup>`) prototype for a between-subjects comparison of **A: category navigation + tag filters** and **B: functional free-text search**. Both variants share the same 87 items, target clothing, layout, and selection behavior.

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

The site must always be opened with one of these links. Without `?version=`, the start screen only says "Please open the study using the link provided by the researcher." and there is no way to choose a version.

Randomly allocate participants yourself (e.g. 10 to each for your planned 20 participants). The links do **not** automatically randomize. Avoid telling participants which interface is expected to be better.

## Task

> You are going for dinner with friends. Find the three pieces shown in the reference images. Select each item and add it to your basket.

The reference images appear beside the wardrobe on larger screens and above it on mobile, without item names. Each reference is marked as found after its matching item is added.

Clothing is shown with real product photos (`public/images/`), each photo used once, all on the same light grey background. The three targets come from different categories (a top, a bottom and shoes), each is the only item of its colour in its category, and they sit near the end of the list (positions 62, 74 and 84 of 87). The required occasion and weather are given in the task instructions, and wardrobe cards show the same details in both versions (category, or colour inside a category), never the occasion or weather.

The app recognizes the *Mustard Shirt* (Tops · Yellow · Casual · Sunny), *Green Ruffled Skirt* (Bottoms · Green · Party · Sunny), and *Pink Sneakers* (Shoes · Pink · Casual · Sunny) as targets; other items can be selected but do not satisfy the task. The **Finish** button under the reference pictures is disabled until all three targets are in the basket. Clicking it stops the timer, shows "You have finished the test, thank you." and changes the address to end with `/success`, which can be set as the success screen in Maze.

## Data collection

Results are collected through Maze (time, clicks, paths, and success when the `/success` address is reached). The finished page no longer offers a CSV download.

If the site is hosted on Netlify or Vercel, refreshing on `/success` needs a rewrite rule that serves `index.html` for all paths; otherwise the host shows a 404.

For perceived ease-of-use and satisfaction, use identical 1–5 post-task Maze questions (or another survey) for both groups.

## Important limits

- This is a research prototype, not the full app. Clothing photos are product images used for academic research only. The previous drawn (SVG) wardrobe with 192 items is kept on the `drawn-wardrobe` branch.
- With the current 87-item mock wardrobe, benchmark results describe this prototype, not the larger real wardrobe; add all actual items to `wardrobe` in `src/App.vue` if you want closer fidelity.
- Searching is case-insensitive AND matching across name, category, colour, occasion, weather; it is genuinely typed input, not a predetermined suggestion click.
- Version A's filters act immediately after clicking a tag; the Apply button closes the filter panel. If your Figma design requires delayed application, change this behavior before testing.
- Use identical devices/screen sizes where feasible; because A supports more taps while B supports keyboard input, raw click counts are **not** a completely equivalent effort measure. Prefer completion time, success, and subjective ease of use as primary outcomes.
- No automatic collection of abandonment sessions; only completed tasks expose the summary/CSV. For reliable failure data, use an external experiment tool with a timeout and abort criteria, or add researcher controls before formal testing.
- Maze website-test capabilities depend on the plan. Verify availability in your team's account. Otherwise conduct moderated tests and record results manually.
