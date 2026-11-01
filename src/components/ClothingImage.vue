<script setup>
defineProps({ item: { type: Object, required: true } })
</script>

<template>
  <div class="item-image" :style="{ '--cloth': item.tone }">
    <svg class="cloth-svg" viewBox="0 0 100 100" aria-hidden="true">
      <path v-if="item.shape === 'pants'" d="M28 13 L72 13 L77 88 L56 88 L50 48 L44 88 L23 88Z" />
      <path v-else-if="item.shape === 'shoe'" d="M16 58 Q35 68 54 42 L70 61 L86 70 Q93 79 85 83 L16 83 Q9 77 16 58Z" />
      <path v-else-if="item.shape === 'skirt'" d="M39 17 L61 17 L83 86 L17 86Z" />
      <path v-else-if="item.shape === 'shorts'" d="M29 16 L71 16 L77 63 L54 63 L50 47 L46 63 L23 63Z" />
      <path v-else-if="item.shape === 'dress'" d="M37 12 L63 12 L70 36 L85 88 L15 88 L30 36Z" />
      <path v-else d="M35 14 L65 14 L84 28 L94 52 L77 61 L69 47 L70 87 L30 87 L31 47 L23 61 L6 52 L16 28Z" />
    </svg>
  </div>
</template>
