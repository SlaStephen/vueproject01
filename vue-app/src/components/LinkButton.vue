<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  label: string
  url: string
  icon: string
}>()

const isMailto = computed(() => props.url.startsWith('mailto:'))
</script>

<template>
  <v-btn
    :href="url"
    :target="isMailto ? undefined : '_blank'"
    rel="noopener noreferrer"
    :prepend-icon="icon"
    block
    size="x-large"
    variant="outlined"
    rounded="lg"
    class="link-btn text-none font-weight-bold"
  >
    {{ label }}
  </v-btn>
</template>

<style scoped>
/* Vuetify has no built-in lift effect */
.link-btn {
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.link-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

@media (prefers-reduced-motion: reduce) {
  .link-btn {
    transition: none;
  }
}
</style>
