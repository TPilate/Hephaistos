<template>
  <div class="header-wrapper">
    <nav class="navbar glass">
      <NuxtLink to="/" class="logo-link">
        <NuxtImg src="logo.png" class="logo" alt="Hephaistos Logo" />
      </NuxtLink>
      <div class="nav-links">
        <NuxtLink to="/forge" class="nav-link">
          <span class="nav-icon">🔨</span>
          Forge
        </NuxtLink>
        <NuxtLink to="/vault" class="nav-link">
          <span class="nav-icon">🧰</span>
          Le Coffre
        </NuxtLink>
        <NuxtLink to="/contact" class="nav-link">
          <span class="nav-icon">✉️</span>
          Contact
        </NuxtLink>
      </div>
    </nav>
  </div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
.header-wrapper {
  position: sticky;
  top: 0;
  z-index: 1000;
  padding: 1rem 2rem;
  background: var(--background);
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  border-radius: 1rem;
  backdrop-filter: blur(var(--glass-backdrop-blur));
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  transition: all 300ms ease-out;
}

.navbar:hover {
  background: oklch(0.15 0.02 280 / 0.6);
  border-color: oklch(0.63 0.18 65 / 0.3);
  box-shadow: 0 10px 15px -3px oklch(0.63 0.18 65 / 0.2);
}

.logo-link {
  display: flex;
  align-items: center;
  text-decoration: none;
  transition: transform 300ms ease-out;
}

.logo-link:hover {
  transform: scale(1.05);
}

.logo {
  height: 48px;
  width: auto;
  object-fit: contain;
}

.nav-links {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.nav-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 1rem;
  color: var(--foreground);
  text-decoration: none;
  border-radius: 0.5rem;
  transition: all 300ms ease-out;
  position: relative;
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 2px;
  background: var(--primary);
  transform: translateX(-50%);
  transition: width 300ms ease-out;
}

.nav-link:hover {
  color: var(--primary);
  background: oklch(0.15 0.02 280 / 0.8);
}

.nav-link:hover::before {
  width: 80%;
}

.nav-link.router-link-active {
  color: var(--primary);
  background: oklch(0.18 0.02 280);
}

.nav-link.router-link-active::before {
  width: 80%;
  background: var(--primary);
}

.nav-icon {
  font-size: 1.25rem;
  transition: transform 300ms ease-out;
}

.nav-link:hover .nav-icon {
  transform: scale(1.2);
}

/* Responsive design */
@media (max-width: 768px) {
  .header-wrapper {
    padding: 0.5rem 1rem;
  }

  .navbar {
    padding: 0.75rem 1rem;
    flex-direction: column;
    gap: 1rem;
  }

  .nav-links {
    flex-direction: column;
    gap: 0.5rem;
    width: 100%;
  }

  .nav-link {
    width: 100%;
    justify-content: center;
  }
}
</style>
