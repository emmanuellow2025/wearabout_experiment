<script setup>
defineProps({ name: { type: String, required: true } })
</script>

<template>
  <svg class="app-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
    <template v-if="name === 'back'"><path d="M20 12H4M10 18l-6-6 6-6" /></template>
    <template v-else-if="name === 'filter'"><path d="M3 4h18l-7 8.5V19l-4 2v-8.5z" /></template>
    <template v-else-if="name === 'basket'"><path d="M4.5 10h15l-1.6 9.2a1 1 0 0 1-1 .8H7.1a1 1 0 0 1-1-.8z" /><path d="M2.5 10h19M8 10l3-6M16 10l-3-6M9 13.5v3.5M12 13.5v3.5M15 13.5v3.5" /></template>
    <template v-else-if="name === 'plus'"><path d="M12 5v14M5 12h14" /></template>
    <template v-else-if="name === 'search'"><circle cx="11" cy="11" r="7" /><path d="m20 20-4-4" /></template>
    <template v-else-if="name === 'home'"><path d="M3 11 12 3l9 8v9a1 1 0 0 1-1 1h-5v-6H9v6H4a1 1 0 0 1-1-1z" fill="currentColor" stroke="none" /></template>
    <template v-else-if="name === 'wardrobe'"><rect x="5" y="3" width="14" height="17" rx="2" /><path d="M12 3v17M10 10.5v3M14 10.5v3M7 20v1.5M17 20v1.5" /></template>
    <template v-else-if="name === 'hanger'"><path d="M10 5.5a2 2 0 1 1 2.6 1.9c-.4.1-.6.5-.6.9V9" /><path d="M12 9 3 16.2c-.6.5-.3 1.6.6 1.6h16.8c.9 0 1.2-1.1.6-1.6z" /></template>
    <template v-else-if="name === 'people'"><g fill="currentColor" stroke="none"><circle cx="12" cy="8" r="3" /><circle cx="5.5" cy="9.5" r="2.2" /><circle cx="18.5" cy="9.5" r="2.2" /><path d="M6.5 19a5.5 5.5 0 0 1 11 0zM1.5 18a4 4 0 0 1 5.4-3.7A7 7 0 0 0 5.2 18zM22.5 18a4 4 0 0 0-5.4-3.7 7 7 0 0 1 1.7 3.7z" /></g></template>
    <template v-else-if="name === 'layers'"><path d="M12 3 2 8l10 5 10-5z" /><path d="m2 12.5 10 5 10-5M2 16.5l10 5 10-5" /></template>
    <template v-else-if="name === 'archive'"><rect x="3" y="4" width="18" height="4" rx="1" /><path d="M5 8v11a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V8M10 12h4" /></template>
    <template v-else-if="name === 'sparkle'"><path d="M11 3l1.8 5.2L18 10l-5.2 1.8L11 17l-1.8-5.2L4 10l5.2-1.8z" /><path d="M19 15l.6 1.8 1.8.6-1.8.6-.6 1.8-.6-1.8-1.8-.6 1.8-.6z" /></template>
  </svg>
</template>
