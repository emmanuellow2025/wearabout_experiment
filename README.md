# Wearabouts – Iter 2.5 Wardrobe Experiment

A Vue 3 Composition API (`<script setup>`) prototype for a between-subjects comparison of **A: category navigation + tag filters** and **B: functional free-text search**. Both variants share the same 192 items, target clothing, layout, and selection behavior.

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

The wardrobe is large so scrolling alone is slow, and the targets sit deep in the list (positions 126, 155 and 183 of 192).

Every item is easy to tell apart: each colour uses one fixed shade (no in-between shades like olive or cream), the 12 colours are clearly different from each other, and there are 16 different silhouettes. No two items share the same silhouette and colour, except each target and its decoy.

Each target has one **decoy** that looks the same (same silhouette and colour) but has a different tag, and it appears earlier in the list:

| Target | Decoy (not accepted) |
|---|---|
| Silk Blouse · Formal · Sunny | Green Blouse · Casual · Sunny |
| Brown Pants · Formal · Sunny | Brown Trousers · Casual · Sunny |
| White Sneakers · Casual · Sunny | White Trainers · Casual · Rainy |

The reference pictures show only what each piece looks like. The required occasion and weather are given in the task instructions, so participants must check tags (with filters, search, or by opening items) to pick the right one. Only one item matches each picture and its tags. Wardrobe cards show the same details in both versions (category, or colour inside a category), never the occasion or weather.

The app recognizes the *Silk Blouse* (green), *Brown Pants*, and *White Sneakers* as targets; other items can be selected but do not satisfy the task. Timer stops when all three targets are selected.

## Data collection

The end-of-task CSV includes participant code (if entered), variant, completion, time, number of non-typing interactions, search input update count, selected items, wrong picks (any non-target item added), decoy picks (look-alikes added), and timestamped action log. The file is downloaded **locally only**. It is not transmitted or saved to a server. Ask participants to submit their exported CSV or have the researcher export it on a shared device.

For perceived ease-of-use and satisfaction, use identical 1–5 post-task Maze questions (or another survey) for both groups.

## Important limits

- This is a research prototype, not the full app. Clothing is rendered using simple SVG silhouettes, not the original Figma assets. You can replace the silhouettes with your approved project images for better fidelity.
- With the current 192-item mock wardrobe, benchmark results describe this prototype, not the larger real wardrobe; add all actual items to `wardrobe` in `src/App.vue` if you want closer fidelity.
- Searching is case-insensitive AND matching across name, category, colour, occasion, weather; it is genuinely typed input, not a predetermined suggestion click.
- Version A's filters act immediately after clicking a tag; the Apply button closes the filter panel. If your Figma design requires delayed application, change this behavior before testing.
- Use identical devices/screen sizes where feasible; because A supports more taps while B supports keyboard input, raw click counts are **not** a completely equivalent effort measure. Prefer completion time, success, and subjective ease of use as primary outcomes.
- No automatic collection of abandonment sessions; only completed tasks expose the summary/CSV. For reliable failure data, use an external experiment tool with a timeout and abort criteria, or add researcher controls before formal testing.
- Maze website-test capabilities depend on the plan. Verify availability in your team's account. Otherwise conduct moderated tests and record results manually.
