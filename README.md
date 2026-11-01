# Wearabouts – Iter 2.5 Wardrobe Experiment

A Vue 3 Composition API (`<script setup>`) prototype for a between-subjects comparison of **A: category navigation + tag filters** and **B: functional free-text search**. Both variants share the same 68 items, target clothing, layout, and selection behavior.

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

To stop scrolling from being a shortcut, each target has look-alike distractors (other blue jeans photographed the same way, other white sneakers, other brown/rust knits), and the targets sit deep in the list (positions 47, 56 and 65 of 68). The order is written out in `wardrobe` in `src/App.vue`, so it is the same for every participant and both versions.

The app recognizes the *Brown Sweater*, *Blue Jeans*, and *White Sneakers* as targets; other items can be selected but do not satisfy the task. Timer stops when all three targets are selected.

## Data collection

The end-of-task CSV includes participant code (if entered), variant, completion, time, number of non-typing interactions, search input update count, selected items, and timestamped action log. The file is downloaded **locally only**. It is not transmitted or saved to a server. Ask participants to submit their exported CSV or have the researcher export it on a shared device.

For perceived ease-of-use and satisfaction, use identical 1–5 post-task Maze questions (or another survey) for both groups.

## Important limits

- This is a research prototype, not the full app. Clothing photos are loaded from Unsplash (see *Photo credits*), so participants need an internet connection.
- With the current 68-item mock wardrobe, benchmark results describe this prototype, not a real user's wardrobe; edit `wardrobe` in `src/App.vue` if you want closer fidelity.
- Searching is case-insensitive AND matching across name, category, colour, occasion, weather; it is genuinely typed input, not a predetermined suggestion click.
- Version A's filters act immediately after clicking a tag; the Apply button closes the filter panel. If your Figma design requires delayed application, change this behavior before testing.
- Use identical devices/screen sizes where feasible; because A supports more taps while B supports keyboard input, raw click counts are **not** a completely equivalent effort measure. Prefer completion time, success, and subjective ease of use as primary outcomes.
- No automatic collection of abandonment sessions; only completed tasks expose the summary/CSV. For reliable failure data, use an external experiment tool with a timeout and abort criteria, or add researcher controls before formal testing.
- Maze website-test capabilities depend on the plan. Verify availability in your team's account. Otherwise conduct moderated tests and record results manually.

## Photo credits

All clothing photos are from [Unsplash](https://unsplash.com/?utm_source=wearabouts_study&utm_medium=referral) and used under the [Unsplash License](https://unsplash.com/license). Each item's pop-up also credits its photographer.

- Beige Blazer: photo by [tian dayong](https://unsplash.com/@tonnnyj?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-glasses-a-ball-of-yarn-a-pair-of-sunglasses-and-9Pspyy5lEMw?utm_source=wearabouts_study&utm_medium=referral)
- Black Blazer: photo by [Victoria Priessnitz](https://unsplash.com/@victoriapriessnitz?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-suit-jacket-on-white-plastic-clothes-hanger-VsCBt8j-qg4?utm_source=wearabouts_study&utm_medium=referral)
- Black Block Heels: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-high-heel-with-geometric-pattern-Hgt-pfNS49k?utm_source=wearabouts_study&utm_medium=referral)
- Black Leather Jacket: photo by [Anna Evans](https://unsplash.com/@anevans?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-black-shoes-and-a-black-leather-jacket-Vfy9pP8tkQg?utm_source=wearabouts_study&utm_medium=referral)
- Black Pumps: photo by [Pesce Huang](https://unsplash.com/@pesce?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-and-brown-leather-peep-toe-heeled-shoes-pEzLon__DfM?utm_source=wearabouts_study&utm_medium=referral)
- Black Skinny Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-black-jeans-sitting-on-top-of-a-white-floor-h6PKsr0wDH4?utm_source=wearabouts_study&utm_medium=referral)
- Black Slingbacks: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-patent-leather-slingback-shoe-BbqotoFK8gA?utm_source=wearabouts_study&utm_medium=referral)
- Black Straight Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-black-jeans-sitting-on-top-of-a-white-surface-MmwrZZy7WtM?utm_source=wearabouts_study&utm_medium=referral)
- Black Tee: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-black-shirt-with-a-white-logo-on-it-k1WdkXkTKHk?utm_source=wearabouts_study&utm_medium=referral)
- Blue Crochet Top: photo by [boris misevic](https://unsplash.com/@borisview?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-blue-dress-hanging-on-a-brick-wall--BRNiWQuJOQ?utm_source=wearabouts_study&utm_medium=referral)
- Blue Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-jeans-sitting-on-top-of-a-white-surface-eoLn6faE5xk?utm_source=wearabouts_study&utm_medium=referral)
- Brown Fleece Jacket: photo by [Nikola Tasic](https://unsplash.com/@tasae34?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-brown-jacket-hanging-on-a-wooden-wall-gJtwWqMiyUw?utm_source=wearabouts_study&utm_medium=referral)
- Brown Leather Jacket: photo by [Derick McKinney](https://unsplash.com/@derickray?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/brown-leather-jacket-hanging-on-brown-wooden-wall-hook-3OFBcQQTN64?utm_source=wearabouts_study&utm_medium=referral)
- Brown Sweater: photo by [Meghna R](https://unsplash.com/@darkandflawed?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/brown-crew-neck-shirt-on-white-table-iN-Zmxm46Oo?utm_source=wearabouts_study&utm_medium=referral)
- Brown Tulle Skirt: photo by [Gaelle Marcel](https://unsplash.com/@gaellemarcel?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/brown-skirt-hanged-on-wall-1PKjyPsH8sw?utm_source=wearabouts_study&utm_medium=referral)
- Chunky White Sneakers: photo by [Brian Hall](https://unsplash.com/@bfhall121?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-nike-air-force-1-x5aavOm7PFc?utm_source=wearabouts_study&utm_medium=referral)
- Cream Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/person-in-cream-cargo-pants-UrKqhKvHcrw?utm_source=wearabouts_study&utm_medium=referral)
- Dark Wash Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-dark-blue-jeans-on-a-white-background-wNP79A-_bRY?utm_source=wearabouts_study&utm_medium=referral)
- Denim Jacket: photo by [kemal alkan](https://unsplash.com/@kemalalkan?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/blue-washed-jacket-hanging-on-white-door-_BDBEP0ePQc?utm_source=wearabouts_study&utm_medium=referral)
- Denim Shorts: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/blue-denim-shorts-on-white-surface-Hd4nlxLgIbA?utm_source=wearabouts_study&utm_medium=referral)
- Faded Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-jeans-sitting-on-top-of-each-other-rJQCoHb8XxA?utm_source=wearabouts_study&utm_medium=referral)
- Floral Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/floral-print-wide-leg-trousers-3OhqJD8Uf2I?utm_source=wearabouts_study&utm_medium=referral)
- Folded Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/the-back-of-a-pair-of-blue-jeans-UinXCaBz44A?utm_source=wearabouts_study&utm_medium=referral)
- Green Cable Knit: photo by [Asiya Bhat](https://unsplash.com/@istaber?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-green-knitted-piece-of-clothing-GcSXNqXdPOk?utm_source=wearabouts_study&utm_medium=referral)
- Green Knit Sweater: photo by [Ksenia Makagonova](https://unsplash.com/@dearseymour?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/green-knitted-cloth-5NRMrUdILG4?utm_source=wearabouts_study&utm_medium=referral)
- Green Romper: photo by [Nellie Adamyan](https://unsplash.com/@nellie_adamyan?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-green-dress-hanging-on-a-clothes-rack-7tDTX5PU5mw?utm_source=wearabouts_study&utm_medium=referral)
- Green Utility Jacket: photo by [Toa Heftiba](https://unsplash.com/@heftiba?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/person-holding-green-denim-jacket-gX8dF8Zoegg?utm_source=wearabouts_study&utm_medium=referral)
- Grey Boots: photo by [Erwin Bosman](https://unsplash.com/@erwinbosman?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-gray-baby-boots-with-a-giraffe-toy-8QIJdenxJPw?utm_source=wearabouts_study&utm_medium=referral)
- Grey Coat: photo by [Lisa Anna](https://unsplash.com/@lisaanna195?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-coat-hanging-on-a-coat-rack-in-a-closet-pvCjWi5bATg?utm_source=wearabouts_study&utm_medium=referral)
- Grey High-Tops: photo by [Piyush Haswani](https://unsplash.com/@piyushh29?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-shoes-asD3pM3lSkA?utm_source=wearabouts_study&utm_medium=referral)
- Grey Hoodie: photo by [Anastasiia Polishchuk](https://unsplash.com/@polishuchka?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-hoodie-is-hanging-on-a-closed-door-VXEca6MPGKk?utm_source=wearabouts_study&utm_medium=referral)
- Grey Sweater: photo by [Tamas Pap](https://unsplash.com/@tamasp?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/silver-and-black-necklace-on-white-table-WnSRF41M3oQ?utm_source=wearabouts_study&utm_medium=referral)
- Grey Track Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/sweatpants-with-white-stripes-and-sneakers-iKgtAUOInA4?utm_source=wearabouts_study&utm_medium=referral)
- Hand-Knit Jumper: photo by [Yuliia Pakhomova](https://unsplash.com/@yuliia_pak?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/knitted-brown-sweater-with-stitch-markers-and-yarn-ball-x2ItoW3Llus?utm_source=wearabouts_study&utm_medium=referral)
- Indigo Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-jeans-sitting-on-top-of-each-other-aO5KpUZ8bSc?utm_source=wearabouts_study&utm_medium=referral)
- Lavender Sneakers: photo by [Anastasiya Badun](https://unsplash.com/@badun?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-shoes-sitting-on-top-of-a-sandy-beach-EbF44cX9PdI?utm_source=wearabouts_study&utm_medium=referral)
- Light Blue Shirt: photo by [Background Foto Pixell Design](https://unsplash.com/@pixelldesign?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/blue-polo-shirt-on-pink-textile-OsvD4y41C4g?utm_source=wearabouts_study&utm_medium=referral)
- Light Wash Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-jeans-sitting-on-top-of-each-other-KVHIG5biScQ?utm_source=wearabouts_study&utm_medium=referral)
- Lilac Blazer: photo by [agust moto](https://unsplash.com/@agustmoto?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-coat-on-a-tree-wDPCi-wmW2g?utm_source=wearabouts_study&utm_medium=referral)
- Mid Wash Jeans: photo by [TuanAnh Blue](https://unsplash.com/@blueeyeaa?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-blue-jeans-on-a-white-background-9yoXrG6Er_g?utm_source=wearabouts_study&utm_medium=referral)
- Mint Tee: photo by [tian dayong](https://unsplash.com/@tonnnyj?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-light-green-t-shirt-with-cotton-branches-oLSnyhU2BVU?utm_source=wearabouts_study&utm_medium=referral)
- Navy Dress: photo by [H&CO](https://unsplash.com/@hngstrm?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-sleeveless-top-hanging-on-wardrobe-cp-VMJ-mdKs?utm_source=wearabouts_study&utm_medium=referral)
- Navy Graphic Tee: photo by [Geoffroy Danest](https://unsplash.com/@geoffroydanest?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/black-and-white-crew-neck-t-shirt-eD8PIv_7CTg?utm_source=wearabouts_study&utm_medium=referral)
- Pink Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/mauve-cropped-pants-with-drawstring-waist-NvPnm0uvvkE?utm_source=wearabouts_study&utm_medium=referral)
- Purple Joggers: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-woman-in-a-white-shirt-and-purple-pants-D3pnJMIeBLk?utm_source=wearabouts_study&utm_medium=referral)
- Raw Denim Jeans: photo by [Anthony Massaro](https://unsplash.com/@tamassaro?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-jeans-laying-on-a-tile-floor-jll9ZPrAVms?utm_source=wearabouts_study&utm_medium=referral)
- Red Joggers: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/woman-in-red-sweatpants-and-top-zwTOVBDiKMI?utm_source=wearabouts_study&utm_medium=referral)
- Red Palm Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/wide-leg-trousers-with-palm-leaf-print-3QieDBgNQFs?utm_source=wearabouts_study&utm_medium=referral)
- Running Shoes: photo by [mostafa mahmoudi](https://unsplash.com/@mostafa_mahmoudi24?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-close-up-of-a-shoe-on-a-white-background-P_RXel_thDA?utm_source=wearabouts_study&utm_medium=referral)
- Rust Bomber Jacket: photo by [Tobias Tullius](https://unsplash.com/@tobiastu?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/brown-bomber-jacket-on-hanger-Fg15LdqpWrs?utm_source=wearabouts_study&utm_medium=referral)
- Rust Knit Sweater: photo by [Yuliia Pakhomova](https://unsplash.com/@yuliia_pak?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-knitted-rust-colored-sweater-with-loose-yarn-e9W-oPLQOp8?utm_source=wearabouts_study&utm_medium=referral)
- Silver Heels: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/silver-high-heel-sandals-II0C5gsfxlc?utm_source=wearabouts_study&utm_medium=referral)
- Slogan Tee: photo by [Old Youth](https://unsplash.com/@oldyouth?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-white-t-shirt-that-says-dont-sweat-eat-its-cool-EaEMK2xuHdA?utm_source=wearabouts_study&utm_medium=referral)
- Striped T-Shirt Dress: photo by [Tayla Brand](https://unsplash.com/@taylabrandpics?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/whit-and-black-striped-shirt-hanging-on-white-wall-cjbcOjHnNUo?utm_source=wearabouts_study&utm_medium=referral)
- White Cargo Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-cargo-joggers-with-black-top-9D9ipHUgzOo?utm_source=wearabouts_study&utm_medium=referral)
- White Court Sneakers: photo by [SJ 📸](https://unsplash.com/@uxsj_ph?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-white-sneaker-with-a-green-stripe-on-the-side--YE65Y0kgws?utm_source=wearabouts_study&utm_medium=referral)
- White Dress Shirt: photo by [Nimble Made](https://unsplash.com/@nimblemade?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/person-holding-white-button-up-shirt-Jf7JqVazm-4?utm_source=wearabouts_study&utm_medium=referral)
- White Knit Sweater: photo by [Shelter](https://unsplash.com/@shelter?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-knit-sweater-on-white-wooden-surface-xEraWP_ZRGU?utm_source=wearabouts_study&utm_medium=referral)
- White Lace Dress: photo by [Cate Bligh](https://unsplash.com/@catebligh?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-floral-lace-sleeveless-dress-B_P6nONZk58?utm_source=wearabouts_study&utm_medium=referral)
- White Leather Sneakers: photo by [Mnz](https://unsplash.com/@mnzoutfits?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/pair-of-white-low-top-sneakers-BeClz11lyXY?utm_source=wearabouts_study&utm_medium=referral)
- White Low-Tops: photo by [Sanju Pandita](https://unsplash.com/@spxclicks?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-white-nike-sneakers-on-a-red-background-36MiHf2KKr8?utm_source=wearabouts_study&utm_medium=referral)
- White Pants: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/woman-in-white-cargo-pants-UiVhtwXLkUo?utm_source=wearabouts_study&utm_medium=referral)
- White Skate Shoes: photo by [David Chavez](https://unsplash.com/@designsdavidc?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pair-of-white-and-black-shoes-on-a-white-surface-1Us_GlM9j-M?utm_source=wearabouts_study&utm_medium=referral)
- White Sneakers: photo by [The DK Photography](https://unsplash.com/@deepain108?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-nike-athletic-shoes-on-white-background-A8HaTLON5Gg?utm_source=wearabouts_study&utm_medium=referral)
- White Sweatshirt: photo by [Mediamodifier](https://unsplash.com/@mediamodifier?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/white-crew-neck-long-sleeve-shirt-7cERndkOyDw?utm_source=wearabouts_study&utm_medium=referral)
- White Tee: photo by [mockupbee](https://unsplash.com/@mockupbee?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-white-shirt-on-a-white-background-4rUYuwJ2vGw?utm_source=wearabouts_study&utm_medium=referral)
- Wide-Leg Denim: photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/person-wearing-blue-denim-trousers-TCRgPA4kbq4?utm_source=wearabouts_study&utm_medium=referral)
- Yellow Hoodie: photo by [Kelvin Lutan](https://unsplash.com/@kelvinlutan?utm_source=wearabouts_study&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/yellow-toxic-peeps-pullover-hoodie-AT5-DnsNq70?utm_source=wearabouts_study&utm_medium=referral)
