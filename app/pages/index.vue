<template>
  <div class="index-wrapper">
    <div class="hero-section">
      <h1 class="hero-title">Que Forgeons-nous aujourd'hui ?</h1>
      <p class="hero-subtitle">Explorez les créations de la forge</p>
    </div>

    <div class="cards-grid">
      <NuxtLink to="/forge/first-pc" class="forge-card glass glass-hover">
        <div class="card-icon">💻</div>
        <h2 class="card-title">Mon premier PC</h2>
        <p class="card-description">Découvrez comment construire votre première machine</p>
        <div class="card-shimmer"/>
      </NuxtLink>

      <NuxtLink to="/forge/upgrades" class="forge-card glass glass-hover">
        <div class="card-icon">⚡</div>
        <h2 class="card-title">Améliorations de mon PC</h2>
        <p class="card-description">Optimisez et améliorez votre configuration existante</p>
        <div class="card-shimmer"/>
      </NuxtLink>

      <NuxtLink to="/forge/peripherals" class="forge-card glass glass-hover">
        <div class="card-icon">🎮</div>
        <h2 class="card-title">Périphériques</h2>
        <p class="card-description">Sélectionnez les meilleurs périphériques pour votre setup</p>
        <div class="card-shimmer"/>
      </NuxtLink>
    </div>
  </div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
.index-wrapper {
  padding: 3rem 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

.hero-section {
  text-align: center;
  margin-bottom: 4rem;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, var(--primary), var(--secondary));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: var(--muted-foreground);
  font-weight: 400;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.forge-card {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 3rem 2rem;
  border-radius: 1.5rem;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
  transform: translateY(0);
  transition: all 400ms cubic-bezier(0.4, 0, 0.2, 1);
}

.forge-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(
    circle at var(--mouse-x, 50%) var(--mouse-y, 50%),
    oklch(0.63 0.18 65 / 0.15),
    transparent 50%
  );
  opacity: 0;
  transition: opacity 400ms ease;
  pointer-events: none;
}

.forge-card:hover::before {
  opacity: 1;
}

.forge-card:hover {
  transform: translateY(-8px);
  box-shadow: 
    0 20px 40px -10px oklch(0.63 0.18 65 / 0.3),
    0 0 0 1px oklch(0.63 0.18 65 / 0.5);
}

.card-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
  transition: transform 400ms cubic-bezier(0.4, 0, 0.2, 1);
  filter: drop-shadow(0 4px 12px oklch(0.63 0.18 65 / 0.3));
}

.forge-card:hover .card-icon {
  transform: scale(1.1) rotateZ(5deg);
}

.card-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--foreground);
  margin-bottom: 0.75rem;
  text-align: center;
  transition: color 300ms ease;
}

.forge-card:hover .card-title {
  color: var(--primary);
}

.card-description {
  font-size: 0.95rem;
  color: var(--muted-foreground);
  text-align: center;
  line-height: 1.6;
  max-width: 280px;
}

.card-shimmer {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    oklch(0.63 0.18 65 / 0.1),
    transparent
  );
  transition: left 600ms ease;
}

.forge-card:hover .card-shimmer {
  left: 100%;
}

/* Responsive design */
@media (max-width: 768px) {
  .index-wrapper {
    padding: 2rem 1rem;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.1rem;
  }

  .cards-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .forge-card {
    padding: 2.5rem 1.5rem;
  }

  .card-icon {
    font-size: 3rem;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }

  .card-title {
    font-size: 1.25rem;
  }
}
</style>
