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
      <path v-else-if="item.shape === 'dress'" d="M36 10 L44 10 Q50 20 56 10 L64 10 L64 38 L84 90 L16 90 L36 38Z" />
      <path v-else-if="item.shape === 'tank'" d="M38 14 L45 14 Q50 24 55 14 L62 14 L66 36 L70 87 L30 87 L34 36Z" />
      <path v-else-if="item.shape === 'hoodie'" d="M30 32 Q28 4 50 4 Q72 4 70 32 L84 34 L94 58 L77 66 L69 52 L70 92 L30 92 L31 52 L23 66 L6 58 L16 34Z" />
      <path v-else-if="item.shape === 'jacket'" d="M33 18 L44 18 L50 30 L56 18 L67 18 L86 30 L92 70 L78 72 L71 46 L72 76 L28 76 L29 46 L22 72 L8 70 L14 30Z" />
      <path v-else-if="item.shape === 'coat'" d="M38 6 L62 6 L74 14 L84 66 L74 68 L68 36 L82 96 L18 96 L32 36 L26 68 L16 66 L26 14Z" />
      <path v-else-if="item.shape === 'widepants'" d="M30 13 L70 13 L88 88 L58 88 L50 44 L42 88 L12 88Z" />
      <path v-else-if="item.shape === 'miniskirt'" d="M34 30 L66 30 L78 64 L22 64Z" />
      <path v-else-if="item.shape === 'longdress'" d="M39 6 L43 6 L45 22 L55 22 L57 6 L61 6 L62 32 L78 96 L22 96 L38 32Z" />
      <path v-else-if="item.shape === 'boot'" d="M30 14 L52 14 L54 58 L82 68 Q92 74 86 84 L30 84Z" />
      <path v-else-if="item.shape === 'heel'" d="M14 42 L24 42 Q42 64 68 68 L86 70 Q94 75 88 80 L56 80 Q36 76 27 62 L25 90 L19 90 L18 58Z" />
      <path v-else-if="item.shape === 'sandal'" d="M10 74 L88 74 Q94 79 87 83 L13 83 Q6 79 10 74Z M28 74 L36 52 L45 52 L39 74Z M56 74 L60 54 L69 54 L66 74Z" />
      <path v-else d="M35 14 L65 14 L84 28 L94 52 L77 61 L69 47 L70 87 L30 87 L31 47 L23 61 L6 52 L16 28Z" />
    </svg>
  </div>
</template>
