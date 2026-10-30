<script setup lang="ts">
import { ref, watchEffect } from 'vue'

// TODO: replace placeholder URLs with real ones
const links = [
  { label: 'Portfolio', href: 'https://example.com' },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/in/your-handle' },
  { label: 'Instagram', href: 'https://www.instagram.com/your-handle' },
  { label: 'Email', href: 'mailto:you@example.com' },
]

const isDark = ref(false)

watchEffect(() => {
  document.documentElement.classList.toggle('dark', isDark.value)
})
</script>

<template>
  <main class="page">
    <button
      class="theme-toggle"
      type="button"
      :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
      @click="isDark = !isDark"
    >
      <svg v-if="isDark" viewBox="0 0 24 24" aria-hidden="true">
        <circle cx="12" cy="12" r="5" />
        <path
          d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"
        />
      </svg>
      <svg v-else viewBox="0 0 24 24" aria-hidden="true">
        <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
      </svg>
    </button>

    <section class="card">
      <div class="avatar" role="img" aria-label="Profile photo placeholder">SJ</div>
      <h1 class="name">Stephen Jablonsky</h1>
      <p class="tagline">Designer, developer &amp; maker of things.</p>

      <nav class="links">
        <a
          v-for="link in links"
          :key="link.label"
          class="link-btn"
          :href="link.href"
          :target="link.href.startsWith('mailto:') ? undefined : '_blank'"
          rel="noopener noreferrer"
        >
          {{ link.label }}
        </a>
      </nav>
    </section>
  </main>
</template>

<style scoped>
.page {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 4.5rem 1rem 2rem;
}

.card {
  width: 100%;
  max-width: 480px;
  padding: 2.5rem 1.5rem;
  background: var(--card-bg);
  border-radius: 24px;
  box-shadow: var(--shadow);
  text-align: center;
  transition: background-color 0.3s ease;
}

.avatar {
  width: 112px;
  height: 112px;
  margin: 0 auto 1.25rem;
  border-radius: 50%;
  background: var(--avatar-bg);
  color: var(--text-muted);
  display: grid;
  place-items: center;
  font-size: 2rem;
  font-weight: 600;
  letter-spacing: 0.05em;
}

.name {
  font-size: 1.75rem;
  font-weight: 700;
}

.tagline {
  margin-top: 0.25rem;
  color: var(--text-muted);
  font-size: 1rem;
}

.links {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.875rem;
}

.link-btn {
  display: block;
  padding: 0.95rem 1.25rem;
  border: 1px solid var(--btn-border);
  border-radius: 14px;
  background: var(--btn-bg);
  color: var(--text);
  font-weight: 600;
  text-decoration: none;
  transition:
    transform 0.25s ease,
    box-shadow 0.25s ease,
    background-color 0.25s ease,
    color 0.25s ease,
    border-color 0.25s ease;
}

.link-btn:hover,
.link-btn:focus-visible {
  transform: translateY(-3px) scale(1.02);
  background: var(--btn-hover-bg);
  color: var(--btn-hover-text);
  border-color: var(--btn-hover-bg);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  outline: none;
}

.link-btn:active {
  transform: translateY(-1px) scale(0.99);
}

.theme-toggle {
  position: fixed;
  top: 1rem;
  right: 1rem;
  width: 44px;
  height: 44px;
  display: grid;
  place-items: center;
  border: 1px solid var(--btn-border);
  border-radius: 50%;
  background: var(--card-bg);
  color: var(--text);
  cursor: pointer;
  transition:
    transform 0.25s ease,
    background-color 0.3s ease;
}

.theme-toggle:hover {
  transform: rotate(20deg) scale(1.08);
}

.theme-toggle svg {
  width: 20px;
  height: 20px;
  fill: none;
  stroke: currentColor;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

@media (min-width: 640px) {
  .card {
    padding: 3rem 2.5rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .link-btn,
  .theme-toggle {
    transition: none;
  }
}
</style>
