<script setup>
import { ref, computed, watch, onUnmounted } from 'vue'
import ClothingImage from './components/ClothingImage.vue'
import AppIcon from './components/AppIcon.vue'

const wardrobe = [
  { id: 'beige-sweater', name: 'Beige Sweater', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', image: '/images/beige-sweater.png' },
  { id: 'white-ruffled-skirt', name: 'White Ruffled Skirt', category: 'Bottoms', colour: 'White', occasion: 'Party', weather: 'Sunny', image: '/images/white-ruffled-skirt.png' },
  { id: 'denim-jacket', name: 'Denim Jacket', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/denim-jacket.png' },
  { id: 'grey-sweatpants', name: 'Grey Sweatpants', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', image: '/images/sweatpants.png' },
  { id: 'black-dress', name: 'Black Dress', category: 'Dresses', colour: 'Black', occasion: 'Party', weather: 'Sunny', image: '/images/black-dress.png' },
  { id: 'khaki-shorts', name: 'Khaki Shorts', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/khaki-shorts.png' },
  { id: 'blue-camisole', name: 'Blue Camisole', category: 'Tops', colour: 'Blue', occasion: 'Party', weather: 'Sunny', image: '/images/blue-camisole.png' },
  { id: 'black-midi-skirt', name: 'Black Midi Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', image: '/images/black-midi-skirt.png' },
  { id: 'white-pants', name: 'White Pants', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', image: '/images/white-pant.png' },
  { id: 'green-ruffled-skirt', name: 'Green Ruffled Skirt', category: 'Bottoms', colour: 'Green', occasion: 'Party', weather: 'Sunny', image: '/images/green-ruffled-skirt.png' },
  { id: 'blue-tank-top', name: 'Blue Tank Top', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/tank-top.png' },
  { id: 'brown-miniskirt', name: 'Brown Miniskirt', category: 'Bottoms', colour: 'Brown', occasion: 'Party', weather: 'Cloudy', image: '/images/brown-miniskirt.png' },
  { id: 'white-dress', name: 'White Dress', category: 'Dresses', colour: 'White', occasion: 'Party', weather: 'Sunny', image: '/images/white-dress.png' },
  { id: 'denim-midi-skirt', name: 'Denim Midi Skirt', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/denim-midi-skirt.png' },
  { id: 'green-shirt', name: 'Green Shirt', category: 'Tops', colour: 'Green', occasion: 'Casual', weather: 'Sunny', image: '/images/greenblouse.png' },
  { id: 'grey-joggers', name: 'Grey Joggers', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', image: '/images/sweatpants2.png' },
  { id: 'silk-blouse', name: 'Silk Blouse', category: 'Tops', colour: 'Yellow', occasion: 'Formal', weather: 'Sunny', image: '/images/silk-blouse.png' },
  { id: 'beige-skirt', name: 'Beige Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', image: '/images/beige-skirt.png' },
  { id: 'black-formal-pants', name: 'Black Formal Pants', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', image: '/images/formal-pants.png' },
  { id: 'brown-cami', name: 'Brown Cami', category: 'Tops', colour: 'Brown', occasion: 'Party', weather: 'Sunny', image: '/images/brown-cami.png' },
  { id: 'brown-pants', name: 'Brown Pants', category: 'Bottoms', colour: 'Brown', occasion: 'Formal', weather: 'Sunny', image: '/images/brownpants.png' },
  { id: 'ruffled-miniskirt', name: 'Ruffled Miniskirt', category: 'Bottoms', colour: 'Beige', occasion: 'Party', weather: 'Sunny', image: '/images/ruffled-miniskirt.png' },
  { id: 'blue-track-pants', name: 'Blue Track Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/blue-track-pants.png' },
  { id: 'white-formal-skirt', name: 'White Formal Skirt', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', image: '/images/white-formal-skirt.png' },
  { id: 'straight-jeans', name: 'Straight Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', image: '/images/straight-jeans.png' },
  { id: 'denim-shorts', name: 'Denim Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', image: '/images/shorts.png' }
]
const targets = ['silk-blouse', 'brown-pants', 'straight-jeans'].map(id => wardrobe.find(item => item.id === id))
const params = new URLSearchParams(window.location.search)
const initialVersion = ['A', 'B'].includes(params.get('version')?.toUpperCase()) ? params.get('version').toUpperCase() : ''
const version = ref(initialVersion)
const participant = ref('')
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
const tagGroups = { Occasion: ['Formal', 'Casual', 'Party'], Weather: ['Sunny', 'Rainy', 'Cloudy'], Colours: ['Green', 'Brown', 'White', 'Black', 'Grey', 'Beige', 'Blue', 'Yellow'] }
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
const seconds = computed(() => Math.round((finishedAt.value || elapsed.value) / 100) / 10)
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
function csvEscape(value) { return `"${String(value ?? '').replaceAll('"', '""')}"` }
function exportCsv() {
  const summary = {
    participant: participant.value || 'anonymous', version: version.value,
    completed: complete.value, duration_seconds: seconds.value,
    total_interactions: actions.value.filter(a => a.type !== 'search_query_change').length,
    search_edits: actions.value.filter(a => a.type === 'search_query_change').length,
    selected_items: collected.value.map(id => wardrobe.find(i => i.id === id)?.name).join(' | '),
    wrong_picks: collected.value.filter(id => !targets.some(t => t.id === id)).length,
    event_log_json: JSON.stringify(actions.value)
  }
  const csv = Object.keys(summary).join(',') + '\n' + Object.values(summary).map(csvEscape).join(',') + '\n'
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8' })
  const url = URL.createObjectURL(blob)
  const anchor = document.createElement('a')
  anchor.href = url; anchor.download = `wearabouts-${version.value}-${(participant.value || 'anonymous').replace(/[^a-zA-Z0-9_-]/g, '_')}.csv`
  anchor.click(); URL.revokeObjectURL(url)
}
</script>

<template>
  <div class="app-shell">
    <div class="study-header"><span class="study-kicker">ITER 2.5 · USABILITY STUDY</span><span class="study-subtitle">Wearabouts · Wardrobe discovery</span></div>
    <div v-if="phase !== 'done'" class="study-layout" :class="{ 'setup-layout': phase === 'setup' }">
    <section v-if="phase === 'setup'" class="intro panel">
      <div class="logo">Wearabouts<span class="logo-dot">.</span></div>
      <div class="eyebrow">WARDROBE FINDABILITY STUDY</div>
      <h1>Find your outfit, your way.</h1>
      <p>You are heading to dinner with friends. Find the three pieces shown in the reference images and add them to your basket.</p>
      <label class="field-label" for="participant">Participant code (optional)</label>
      <input id="participant" v-model="participant" placeholder="e.g. P01" autocomplete="off" />
      <div v-if="!initialVersion" class="version-picker">
        <div class="field-label">Researcher: choose the assigned version</div>
        <button class="version-choice" :class="{ chosen: version === 'A' }" @click="version = 'A'">A · Category navigation + tag filters</button>
        <button class="version-choice" :class="{ chosen: version === 'B' }" @click="version = 'B'">B · Free-text keyword search</button>
      </div>
      <div v-else class="version-note">Your assigned study interface is ready.</div>
      <button class="primary wide" :disabled="!version" @click="start">Start task <span>→</span></button>
      <p class="fine-print">The timer begins when you press Start. Select each clothing item to add it to your basket.</p>
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

    <aside class="reference-panel" aria-labelledby="reference-heading">
      <h2 id="reference-heading">Find these pieces</h2>
      <p>Match the pictures to items in your wardrobe.</p>
      <div class="reference-grid">
        <div v-for="(item, index) in targets" :key="item.id" class="reference-card" :class="{ found: collected.includes(item.id) }">
          <ClothingImage :item="item" role="img" :aria-label="`Reference item ${index + 1}`" />
          <span v-if="collected.includes(item.id)" class="reference-found"><span aria-hidden="true">✓ </span>Found</span>
        </div>
      </div>
      <button v-if="phase === 'test'" class="primary wide finish-btn" :disabled="!complete" @click="finish">Finish</button>
    </aside>
    </div>

    <section v-else class="intro panel done-panel"><h1>You have finished the test, thank you.</h1></section>
  </div>
</template>
