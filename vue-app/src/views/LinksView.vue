<script setup lang="ts">
import { computed } from 'vue'
import { useTheme } from 'vuetify'
import LinkButton from '@/components/LinkButton.vue'

// TODO: replace placeholder URLs with real ones
const links = [
  { label: 'Portfolio', url: 'https://example.com', icon: 'mdi-briefcase-outline' },
  { label: 'LinkedIn', url: 'https://www.linkedin.com/in/your-handle', icon: 'mdi-linkedin' },
  { label: 'Instagram', url: 'https://www.instagram.com/your-handle', icon: 'mdi-instagram' },
  { label: 'Email', url: 'mailto:you@example.com', icon: 'mdi-email-outline' },
]

const theme = useTheme()
const isDark = computed(() => theme.global.current.value.dark)
</script>

<template>
  <v-main>
    <v-btn
      :icon="isDark ? 'mdi-weather-sunny' : 'mdi-weather-night'"
      :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
      variant="outlined"
      position="fixed"
      location="top right"
      class="ma-4"
      @click="theme.toggle()"
    />

    <v-container class="fill-height">
      <v-row justify="center" align="center">
        <v-col cols="12">
          <v-card max-width="480" class="mx-auto pa-6 pa-sm-10 text-center" rounded="xl" elevation="8">
            <v-avatar size="112" color="surface-variant" class="mb-5">
              <span class="text-h4 font-weight-bold">SJ</span>
            </v-avatar>

            <h1 class="text-h4 font-weight-bold">Stephen Jablonsky</h1>
            <p class="text-body-1 text-medium-emphasis mt-1">
              Designer, developer &amp; maker of things.
            </p>

            <div class="d-flex flex-column ga-3 mt-8">
              <LinkButton
                v-for="link in links"
                :key="link.label"
                :label="link.label"
                :url="link.url"
                :icon="link.icon"
              />
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>
