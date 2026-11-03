<script setup>
defineProps({ item: { type: Object, required: true } })
</script>

<template>
  <div class="item-image">
    <img class="cloth-photo" :src="item.image" alt="" />
  </div>
</template>
