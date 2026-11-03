<script setup>
import { ref, computed, watch, onUnmounted } from 'vue'
import ClothingImage from './components/ClothingImage.vue'
import AppIcon from './components/AppIcon.vue'

const wardrobe = [
  { id: 'straight-jeans', name: 'Straight Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/straight-jeans.webp' },
  { id: 'beige-ruffle-skirt', name: 'Beige Ruffle Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Party', weather: 'Sunny', image: '/images/beige-ruffle-skirt.webp' },
  { id: 'brown-oxford-shoes', name: 'Brown Oxford Shoes', category: 'Shoes', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', image: '/images/brown-oxford-shoes.webp' },
  { id: 'beige-collar-jacket', name: 'Beige Collar Jacket', category: 'Outerwear', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', image: '/images/beige-collar-jacket.webp' },
  { id: 'navy-graphic-sweatshirt', name: 'Navy Graphic Sweatshirt', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/navy-graphic-sweatshirt.webp' },
  { id: 'brown-straight-pants', name: 'Brown Straight Pants', category: 'Bottoms', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', image: '/images/brown-straight-pants.webp' },
  { id: 'chunky-sneakers', name: 'Chunky Sneakers', category: 'Shoes', colour: 'Grey', occasion: 'Party', weather: 'Sunny', image: '/images/chunky-sneakers.webp' },
  { id: 'plum-parka', name: 'Plum Parka', category: 'Outerwear', colour: 'Purple', occasion: 'Casual', weather: 'Rainy', image: '/images/plum-parka.webp' },
  { id: 'navy-cropped-pants', name: 'Navy Cropped Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/navy-cropped-pants.webp' },
  { id: 'grey-striped-tee', name: 'Grey Striped Tee', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', image: '/images/grey-striped-tee.webp' },
  { id: 'suede-slippers', name: 'Suede Slippers', category: 'Shoes', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', image: '/images/suede-slippers.webp' },
  { id: 'stone-shorts', name: 'Stone Shorts', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/stone-shorts.webp' },
  { id: 'navy-wide-pants', name: 'Navy Wide Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', image: '/images/navy-wide-pants.webp' },
  { id: 'gingham-shorts', name: 'Gingham Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/gingham-shorts.webp' },
  { id: 'black-ruffle-dress', name: 'Black Ruffle Dress', category: 'Dresses', colour: 'Black', occasion: 'Party', weather: 'Sunny', image: '/images/black-ruffle-dress.webp' },
  { id: 'dark-brown-trousers', name: 'Dark Brown Trousers', category: 'Bottoms', colour: 'Brown', occasion: 'Formal', weather: 'Sunny', image: '/images/dark-brown-trousers.webp' },
  { id: 'camel-short-jacket', name: 'Camel Short Jacket', category: 'Outerwear', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/camel-short-jacket.webp' },
  { id: 'white-ruffled-skirt', name: 'White Ruffled Skirt', category: 'Bottoms', colour: 'White', occasion: 'Party', weather: 'Sunny', image: '/images/white-ruffled-skirt.webp' },
  { id: 'khaki-trench-coat', name: 'Khaki Trench Coat', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Rainy', image: '/images/khaki-trench-coat.webp' },
  { id: 'denim-shirt-dress', name: 'Denim Shirt Dress', category: 'Dresses', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/denim-shirt-dress.webp' },
  { id: 'mint-tee', name: 'Mint Tee', category: 'Tops', colour: 'Green', occasion: 'Casual', weather: 'Sunny', image: '/images/mint-tee.webp' },
  { id: 'pink-shirt', name: 'Pink Shirt', category: 'Tops', colour: 'Pink', occasion: 'Formal', weather: 'Sunny', image: '/images/pink-shirt.webp' },
  { id: 'grey-sweatpants', name: 'Grey Sweatpants', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', image: '/images/grey-sweatpants.webp' },
  { id: 'light-blue-ribbed-tank', name: 'Light Blue Ribbed Tank', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/light-blue-ribbed-tank.webp' },
  { id: 'pink-blouse', name: 'Pink Blouse', category: 'Tops', colour: 'Pink', occasion: 'Formal', weather: 'Sunny', image: '/images/pink-blouse.webp' },
  { id: 'beige-knit-sweater', name: 'Beige Knit Sweater', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', image: '/images/beige-knit-sweater.webp' },
  { id: 'denim-jacket', name: 'Denim Jacket', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/denim-jacket.webp' },
  { id: 'khaki-skort', name: 'Khaki Skort', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/khaki-skort.webp' },
  { id: 'black-chore-jacket', name: 'Black Chore Jacket', category: 'Outerwear', colour: 'Black', occasion: 'Casual', weather: 'Rainy', image: '/images/black-chore-jacket.webp' },
  { id: 'white-pants', name: 'White Pants', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', image: '/images/white-pants.webp' },
  { id: 'beige-blazer', name: 'Beige Blazer', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', image: '/images/beige-blazer.webp' },
  { id: 'blue-tee', name: 'Blue Tee', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/blue-tee.webp' },
  { id: 'brown-tweed-blazer', name: 'Brown Tweed Blazer', category: 'Outerwear', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', image: '/images/brown-tweed-blazer.webp' },
  { id: 'blue-running-shoes', name: 'Blue Running Shoes', category: 'Shoes', colour: 'Blue', occasion: 'Casual', weather: 'Rainy', image: '/images/blue-running-shoes.webp' },
  { id: 'black-blazer', name: 'Black Blazer', category: 'Outerwear', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', image: '/images/black-blazer.webp' },
  { id: 'brown-parka', name: 'Brown Parka', category: 'Outerwear', colour: 'Brown', occasion: 'Casual', weather: 'Rainy', image: '/images/brown-parka.webp' },
  { id: 'grey-ringer-tee', name: 'Grey Ringer Tee', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', image: '/images/grey-ringer-tee.webp' },
  { id: 'olive-half-zip', name: 'Olive Half-Zip', category: 'Tops', colour: 'Green', occasion: 'Casual', weather: 'Cloudy', image: '/images/olive-half-zip.webp' },
  { id: 'white-trainers', name: 'White Trainers', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Sunny', image: '/images/white-trainers.webp' },
  { id: 'white-pleated-skirt', name: 'White Pleated Skirt', category: 'Bottoms', colour: 'White', occasion: 'Casual', weather: 'Sunny', image: '/images/white-pleated-skirt.webp' },
  { id: 'black-leather-jacket', name: 'Black Leather Jacket', category: 'Outerwear', colour: 'Black', occasion: 'Party', weather: 'Cloudy', image: '/images/black-leather-jacket.webp' },
  { id: 'grey-raglan-top', name: 'Grey Raglan Top', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', image: '/images/grey-raglan-top.webp' },
  { id: 'brown-leather-sneakers', name: 'Brown Leather Sneakers', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', image: '/images/brown-leather-sneakers.webp' },
  { id: 'ivory-henley-top', name: 'Ivory Henley Top', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Cloudy', image: '/images/ivory-henley-top.webp' },
  { id: 'ivory-sweater', name: 'Ivory Sweater', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Cloudy', image: '/images/ivory-sweater.webp' },
  { id: 'brown-cami', name: 'Brown Cami', category: 'Tops', colour: 'Brown', occasion: 'Party', weather: 'Sunny', image: '/images/brown-cami.webp' },
  { id: 'navy-camisole', name: 'Navy Camisole', category: 'Tops', colour: 'Blue', occasion: 'Party', weather: 'Sunny', image: '/images/navy-camisole.webp' },
  { id: 'grey-joggers', name: 'Grey Joggers', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', image: '/images/grey-joggers.webp' },
  { id: 'navy-jacket', name: 'Navy Jacket', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/navy-jacket.webp' },
  { id: 'brown-shirt-jacket', name: 'Brown Shirt Jacket', category: 'Outerwear', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', image: '/images/brown-shirt-jacket.webp' },
  { id: 'denim-shorts', name: 'Denim Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/denim-shorts.webp' },
  { id: 'striped-polo-sweater', name: 'Striped Polo Sweater', category: 'Tops', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', image: '/images/striped-polo-sweater.webp' },
  { id: 'white-clogs', name: 'White Clogs', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Sunny', image: '/images/white-clogs.webp' },
  { id: 'brown-wide-trousers', name: 'Brown Wide Trousers', category: 'Bottoms', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', image: '/images/brown-wide-trousers.webp' },
  { id: 'taupe-blazer', name: 'Taupe Blazer', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Cloudy', image: '/images/taupe-blazer.webp' },
  { id: 'black-denim-jacket', name: 'Black Denim Jacket', category: 'Outerwear', colour: 'Black', occasion: 'Casual', weather: 'Cloudy', image: '/images/black-denim-jacket.webp' },
  { id: 'olive-blazer', name: 'Olive Blazer', category: 'Outerwear', colour: 'Green', occasion: 'Formal', weather: 'Cloudy', image: '/images/olive-blazer.webp' },
  { id: 'blue-track-pants', name: 'Blue Track Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/blue-track-pants.webp' },
  { id: 'white-running-shoes', name: 'White Running Shoes', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Rainy', image: '/images/white-running-shoes.webp' },
  { id: 'baby-blue-tank-top', name: 'Baby Blue Tank Top', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/baby-blue-tank-top.webp' },
  { id: 'green-shirt', name: 'Green Shirt', category: 'Tops', colour: 'Green', occasion: 'Casual', weather: 'Sunny', image: '/images/green-shirt.webp' },
  { id: 'mustard-shirt', name: 'Mustard Shirt', category: 'Tops', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', image: '/images/mustard-shirt.webp' },
  { id: 'blue-flannel-shirt', name: 'Blue Flannel Shirt', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/blue-flannel-shirt.webp' },
  { id: 'olive-polo-sweater', name: 'Olive Polo Sweater', category: 'Tops', colour: 'Green', occasion: 'Formal', weather: 'Cloudy', image: '/images/olive-polo-sweater.webp' },
  { id: 'white-ruffle-dress', name: 'White Ruffle Dress', category: 'Dresses', colour: 'White', occasion: 'Party', weather: 'Sunny', image: '/images/white-ruffle-dress.webp' },
  { id: 'white-tank-top', name: 'White Tank Top', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Sunny', image: '/images/white-tank-top.webp' },
  { id: 'red-sneakers', name: 'Red Sneakers', category: 'Shoes', colour: 'Red', occasion: 'Casual', weather: 'Sunny', image: '/images/red-sneakers.webp' },
  { id: 'plum-shirt', name: 'Plum Shirt', category: 'Tops', colour: 'Purple', occasion: 'Formal', weather: 'Cloudy', image: '/images/plum-shirt.webp' },
  { id: 'charcoal-ruched-top', name: 'Charcoal Ruched Top', category: 'Tops', colour: 'Grey', occasion: 'Party', weather: 'Sunny', image: '/images/charcoal-ruched-top.webp' },
  { id: 'beige-mini-skirt', name: 'Beige Mini Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/beige-mini-skirt.webp' },
  { id: 'polka-dot-skirt', name: 'Polka Dot Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Party', weather: 'Sunny', image: '/images/polka-dot-skirt.webp' },
  { id: 'black-bermuda-shorts', name: 'Black Bermuda Shorts', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', image: '/images/black-bermuda-shorts.webp' },
  { id: 'red-long-sleeve-top', name: 'Red Long-Sleeve Top', category: 'Tops', colour: 'Red', occasion: 'Party', weather: 'Cloudy', image: '/images/red-long-sleeve-top.webp' },
  { id: 'green-ruffled-skirt', name: 'Green Ruffled Skirt', category: 'Bottoms', colour: 'Green', occasion: 'Party', weather: 'Sunny', image: '/images/green-ruffled-skirt.webp' },
  { id: 'denim-midi-skirt', name: 'Denim Midi Skirt', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/denim-midi-skirt.webp' },
  { id: 'beige-midi-skirt', name: 'Beige Midi Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/beige-midi-skirt.webp' },
  { id: 'tweed-sleeveless-top', name: 'Tweed Sleeveless Top', category: 'Tops', colour: 'Black', occasion: 'Party', weather: 'Sunny', image: '/images/tweed-sleeveless-top.webp' },
  { id: 'white-maxi-skirt', name: 'White Maxi Skirt', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', image: '/images/white-maxi-skirt.webp' },
  { id: 'black-midi-skirt', name: 'Black Midi Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', image: '/images/black-midi-skirt.webp' },
  { id: 'black-graphic-tee', name: 'Black Graphic Tee', category: 'Tops', colour: 'Black', occasion: 'Casual', weather: 'Sunny', image: '/images/black-graphic-tee.webp' },
  { id: 'floral-culottes', name: 'Floral Culottes', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/floral-culottes.webp' },
  { id: 'wide-leg-jeans', name: 'Wide-Leg Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/wide-leg-jeans.webp' },
  { id: 'grey-denim-shorts', name: 'Grey Denim Shorts', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', image: '/images/grey-denim-shorts.webp' },
  { id: 'pink-sneakers', name: 'Pink Sneakers', category: 'Shoes', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', image: '/images/pink-sneakers.webp' },
  { id: 'navy-fleece-hoodie', name: 'Navy Fleece Hoodie', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Rainy', image: '/images/navy-fleece-hoodie.webp' },
  { id: 'brown-leather-skirt', name: 'Brown Leather Skirt', category: 'Bottoms', colour: 'Brown', occasion: 'Party', weather: 'Cloudy', image: '/images/brown-leather-skirt.webp' },
  { id: 'black-sailor-pants', name: 'Black Sailor Pants', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', image: '/images/black-sailor-pants.webp' }
]
const targets = ['mustard-shirt', 'green-ruffled-skirt', 'pink-sneakers'].map(id => wardrobe.find(item => item.id === id))
const params = new URLSearchParams(window.location.search)
const initialVersion = ['A', 'B'].includes(params.get('version')?.toUpperCase()) ? params.get('version').toUpperCase() : ''
const version = ref(initialVersion)
// Opening the /success address directly (e.g. after a refresh) shows the finished page again
const phase = ref(window.location.pathname.endsWith('/success') ? 'done' : 'setup')
const query = ref('')
const category = ref('All Items')
const filtersOpen = ref(false)
const selectedTags = ref({ Occasion: [], Weather: [], Colours: [] })
const collected = ref([])
const startedAt = ref(0)
const finishedAt = ref(0)
const elapsed = ref(0)
const actions = ref([])
const lastAction = ref('')
const selectedItem = ref(null)
let intervalId
const categories = ['All Items', 'Tops', 'Bottoms', 'Dresses', 'Outerwear', 'Shoes']
const tagGroups = { Occasion: ['Formal', 'Casual', 'Party'], Weather: ['Sunny', 'Rainy', 'Cloudy'], Colours: ['Green', 'Brown', 'White', 'Black', 'Grey', 'Beige', 'Blue', 'Yellow', 'Pink', 'Red', 'Purple'] }
const searchTerms = (s) => s.toLowerCase().trim().split(/\s+/).filter(Boolean)
const visible = computed(() => {
  if (version.value === 'B') {
    const words = searchTerms(query.value)
    return wardrobe.filter(item => words.every(word => `${item.name} ${item.category} ${item.colour} ${item.occasion} ${item.weather}`.toLowerCase().includes(word)))
  }
  return wardrobe.filter(item => {
    if (category.value !== 'All Items' && item.category !== category.value) return false
    return Object.entries(selectedTags.value).every(([kind, values]) => !values.length || values.includes(kind === 'Colours' ? item.colour : item[kind === 'Occasion' ? 'occasion' : 'weather']))
  })
})
const inCategory = computed(() => version.value === 'A' && category.value !== 'All Items')
const activeFilterCount = computed(() => Object.values(selectedTags.value).flat().length)
const navItems = [{ label: 'Home', icon: 'home' }, { label: 'Wardrobe', icon: 'wardrobe' }, { label: 'Fitting Room', icon: 'hanger' }, { label: 'WearTogether', icon: 'people' }]
// Fixed placeholder details so every item page has the same layout as the app
const itemStats = (item) => {
  const n = wardrobe.findIndex(i => i.id === item.id)
  return { outfits: (n * 7) % 19 + 3, lastAdded: (n * 5) % 13 + 1 }
}
const complete = computed(() => targets.every(t => collected.value.includes(t.id)))
function record(type, detail = '') {
  if (phase.value !== 'test') return
  actions.value.push({ seconds: Math.round((performance.now() - startedAt.value) / 100) / 10, type, detail })
  lastAction.value = type
}
function start() {
  if (!version.value) return
  category.value = 'All Items'; query.value = ''; collected.value = []; filtersOpen.value = false
  selectedTags.value = { Occasion: [], Weather: [], Colours: [] }
  actions.value = []; selectedItem.value = null; finishedAt.value = 0; elapsed.value = 0
  phase.value = 'test'
  startedAt.value = performance.now()
  intervalId = setInterval(() => { elapsed.value = performance.now() - startedAt.value }, 100)
}
function stop() {
  if (intervalId) clearInterval(intervalId)
  finishedAt.value = performance.now() - startedAt.value
  phase.value = 'done'
}
function openFilters() { filtersOpen.value = true; record('toggle_filter_panel', 'open') }
function closeFilters() { filtersOpen.value = false; record('toggle_filter_panel', 'closed') }
function applyFilters() { filtersOpen.value = false; record('apply_filters') }
function setCategory(next) { category.value = next; record('select_category', next) }
function toggleTag(kind, value) {
  const arr = [...selectedTags.value[kind]]
  const index = arr.indexOf(value)
  if (index >= 0) arr.splice(index, 1); else arr.push(value)
  selectedTags.value = { ...selectedTags.value, [kind]: arr }
  record('toggle_filter', `${kind}: ${value}`)
}
function clearFilters() { selectedTags.value = { Occasion: [], Weather: [], Colours: [] }; record('clear_filters') }
function openItem(item) { selectedItem.value = item; record('open_item', item.name) }
function addItem() {
  const item = selectedItem.value
  if (!item) return
  if (!collected.value.includes(item.id)) collected.value = [...collected.value, item.id]
  record('select_item', item.name)
  selectedItem.value = null
}
// Only possible once all three targets are found; the /success address lets Maze detect completion
function finish() {
  if (!complete.value) return
  record('finish')
  stop()
  history.pushState(null, '', import.meta.env.BASE_URL + 'success')
}
watch(query, newValue => { record('search_query_change', newValue) })
onUnmounted(() => { if (intervalId) clearInterval(intervalId) })
</script>

<template>
  <div class="app-shell">
    <div class="study-header"><span class="study-kicker">ITER 2.5 · USABILITY STUDY</span><span class="study-subtitle">Wearabouts · Wardrobe discovery</span></div>
    <div v-if="phase !== 'done'" class="study-layout" :class="{ 'setup-layout': phase === 'setup' }">
    <section v-if="phase === 'setup'" class="intro panel">
      <div class="logo">Wearabouts<span class="logo-dot">.</span></div>
      <h1>Find your outfit, your way.</h1>
      <template v-if="version">
        <p>You are heading to dinner with friends and need three pieces from your wardrobe.</p>
        <ol class="steps">
          <li>After you start, pictures of the three pieces appear beside the wardrobe.</li>
          <li>Find each piece and add it to your basket.</li>
          <li>Press Finish once all three are in your basket.</li>
        </ol>
        <button class="primary wide" @click="start">Start when you're ready <span>→</span></button>
        <p class="fine-print">The timer starts when you press the button.</p>
      </template>
      <p v-else class="link-note">Please open the study using the link provided by the researcher.</p>
    </section>

    <div v-else-if="phase === 'test'" class="phone">
      <header class="phone-top">
        <span>9:41</span>
        <svg class="status-icons" viewBox="0 0 60 14" aria-hidden="true"><g fill="currentColor"><rect x="0" y="9" width="3" height="4" rx=".7" /><rect x="4.5" y="6.5" width="3" height="6.5" rx=".7" /><rect x="9" y="4" width="3" height="9" rx=".7" /><rect x="13.5" y="1.5" width="3" height="11.5" rx=".7" /><path d="M29 12.5 26.6 10a3.4 3.4 0 0 1 4.8 0zM24.6 8a6.2 6.2 0 0 1 8.8 0l1.4-1.4a8.2 8.2 0 0 0-11.6 0z" /><rect x="40" y="2.5" width="16" height="9" rx="2.4" fill="none" stroke="currentColor" stroke-width="1.1" opacity=".5" /><rect x="41.6" y="4.1" width="12.8" height="5.8" rx="1.3" /><path d="M57.3 5.5v3a1.6 1.6 0 0 0 0-3z" opacity=".5" /></g></svg>
      </header>

      <div class="phone-scroll">
        <!-- Stays at the top while scrolling so search, tabs and the filter button are always reachable -->
        <div class="sticky-controls">
        <div class="page-head">
          <button v-if="inCategory" class="circle-btn" aria-label="Back to all items" @click="setCategory('All Items')"><AppIcon name="back" /></button>
          <div class="page-title">
            <h1>{{ inCategory ? category : 'Wardrobe' }}</h1>
            <span>{{ inCategory ? `${visible.length} Items` : `Total ${visible.length} items` }}</span>
          </div>
          <div class="head-actions">
            <button v-if="version === 'A'" class="circle-btn" aria-label="Filter" @click="openFilters"><AppIcon name="filter" /><span v-if="activeFilterCount" class="badge">{{ activeFilterCount }}</span></button>
            <span class="circle-btn" aria-hidden="true"><AppIcon name="basket" /><span v-if="collected.length" class="badge">{{ collected.length }}</span></span>
            <span class="circle-btn" aria-hidden="true"><AppIcon name="plus" /></span>
          </div>
        </div>


        <div v-if="version === 'A'" class="tabs"><button v-for="cat in categories" :key="cat" :class="{ active: category === cat }" @click="setCategory(cat)">{{ cat }}</button></div>
        <template v-else>
          <div class="search-wrap"><AppIcon name="search" /><input v-model="query" aria-label="Search your wardrobe" type="search" placeholder="Search clothing, colour or tag..." autocomplete="off" /></div>
        </template>
        </div>

        <div class="item-grid" :class="{ 'two-col': inCategory }">
          <button v-for="item in visible" :key="item.id" class="item-card" @click="openItem(item)">
            <ClothingImage :item="item" />
            <div class="item-title">{{ item.name }}</div>
            <div class="item-meta">{{ inCategory ? item.colour : item.category }}</div>
            <span v-if="collected.includes(item.id)" class="item-added">✓ Added</span>
          </button>
        </div>
        <p v-if="visible.length === 0" class="empty">No matching items. Try a different {{ version === 'A' ? 'filter' : 'search' }}.</p>
      </div>

      <nav class="bottom-nav" aria-hidden="true">
        <span v-for="nav in navItems" :key="nav.label" :class="{ 'nav-current': nav.label === 'Wardrobe' }"><span class="nav-icon"><AppIcon :name="nav.icon" /></span><small>{{ nav.label }}</small></span>
      </nav>

      <div v-if="filtersOpen" class="screen">
        <div class="screen-head"><button class="circle-btn" aria-label="Back" @click="closeFilters"><AppIcon name="back" /></button><h1>Filter</h1></div>
        <div class="screen-body">
          <div v-for="(options, kind, index) in tagGroups" :key="kind" class="filter-group">
            <div class="filter-group-head"><h2>{{ kind }}</h2><button v-if="index === 0" class="text-btn" @click="clearFilters">Clear Selection</button></div>
            <div class="chip-row"><button v-for="tag in options" :key="tag" class="chip" :class="{ selected: selectedTags[kind].includes(tag) }" @click="toggleTag(kind, tag)">{{ tag }}</button></div>
          </div>
          <div class="filter-actions">
            <button class="pill-primary" @click="applyFilters">Apply</button>
            <button class="pill-outline" @click="closeFilters">Back To Wardrobe</button>
          </div>
        </div>
      </div>

      <div v-if="selectedItem" class="screen">
        <div class="screen-head"><button class="circle-btn" aria-label="Close item details" @click="selectedItem = null"><AppIcon name="back" /></button><h1>Item details</h1></div>
        <div class="screen-body">
          <div class="detail-image"><ClothingImage :item="selectedItem" /></div>
          <div class="detail-name"><h2>{{ selectedItem.name }}</h2><span>{{ selectedItem.category }}</span></div>
          <div class="chip-row detail-tags"><span class="chip">{{ selectedItem.occasion }}</span><span class="chip">{{ selectedItem.colour }}</span><span class="chip">{{ selectedItem.weather }}</span></div>
          <div class="detail-row"><AppIcon name="layers" /><span>Saved outfits</span><strong>{{ itemStats(selectedItem).outfits }} outfits</strong></div>
          <div class="detail-row"><AppIcon name="basket" /><span>Last added to basket</span><strong>{{ itemStats(selectedItem).lastAdded }} days ago</strong></div>
          <div class="detail-row"><AppIcon name="archive" /><span>Location</span><strong>Wardrobe</strong></div>
          <div class="ai-note"><AppIcon name="sparkle" /><div><small>AI STYLING NOTE</small><p>Works well for {{ selectedItem.occasion.toLowerCase() }} looks on {{ selectedItem.weather.toLowerCase() }} days</p></div></div>
        </div>
        <div class="detail-actions">
          <button class="pill-outline" @click="selectedItem = null">Back</button>
          <button class="pill-primary" :disabled="collected.includes(selectedItem.id)" @click="addItem"><AppIcon name="basket" />{{ collected.includes(selectedItem.id) ? 'Added to Basket' : 'Add to Basket' }}</button>
        </div>
      </div>
    </div>

    <aside v-if="phase === 'test'" class="reference-panel" aria-labelledby="reference-heading">
      <h2 id="reference-heading">Find these pieces</h2>
      <p>Match the pictures to items in your wardrobe.</p>
      <div class="reference-grid">
        <div v-for="(item, index) in targets" :key="item.id" class="reference-card" :class="{ found: collected.includes(item.id) }">
          <ClothingImage :item="item" role="img" :aria-label="`Reference item ${index + 1}`" />
          <span v-if="collected.includes(item.id)" class="reference-found"><span aria-hidden="true">✓ </span>Found</span>
        </div>
      </div>
      <button class="primary wide finish-btn" :disabled="!complete" @click="finish">Finish</button>
    </aside>
    </div>

    <section v-else class="intro panel done-panel">
      <h1>You have finished the test, thank you.</h1>
      <h2>Please press the "task complete" button in the pop up</h2>
    </section>
  </div>
</template>
