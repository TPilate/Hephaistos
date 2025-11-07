<template>
  <div class="forge-index-container">
    <div class="forge-index-content">
      <div class="hero-section">
        <h1 class="hero-title">⚒️ Bienvenue à la Forge</h1>
        <p class="hero-subtitle">
          Votre atelier personnel pour créer la configuration PC parfaite
        </p>
      </div>

      <div class="cards-grid">
        <NuxtLink to="/forge/first-pc" class="forge-card glass glass-hover">
          <div class="card-icon">🖥️</div>
          <h2 class="card-title">Construire votre premier PC</h2>
          <p class="card-description">
            Laissez-nous vous guider dans le choix de l'ordinateur parfait selon votre budget, votre utilisation et vos préférences.
          </p>
          <div class="card-features">
            <span class="feature-tag">Basé sur le budget</span>
            <span class="feature-tag">Personnalisé</span>
            <span class="feature-tag">Facile</span>
          </div>
          <div class="card-cta">
            Commencer la construction →
          </div>
        </NuxtLink>

        <div class="forge-card glass coming-soon">
          <div class="card-badge">Bientôt disponible</div>
          <div class="card-icon">🎨</div>
          <h2 class="card-title">Configuration personnalisée</h2>
          <p class="card-description">
            Choisissez chaque composant individuellement pour une configuration PC entièrement personnalisée selon vos spécifications exactes.
          </p>
          <div class="card-features">
            <span class="feature-tag">Avancé</span>
            <span class="feature-tag">Contrôle total</span>
            <span class="feature-tag">Expert</span>
          </div>
        </div>

        <div class="forge-card glass coming-soon">
          <div class="card-badge">Bientôt disponible</div>
          <div class="card-icon">🔧</div>
          <h2 class="card-title">Conseiller de mise à niveau</h2>
          <p class="card-description">
            Vous avez déjà un PC ? Obtenez des recommandations sur les composants à mettre à niveau pour le meilleur gain de performance.
          </p>
          <div class="card-features">
            <span class="feature-tag">Économique</span>
            <span class="feature-tag">Intelligent</span>
            <span class="feature-tag">Optimisation</span>
          </div>
        </div>
      </div>

      <div class="info-section">
        <div class="info-card glass">
          <h3 class="info-title">💡 Pourquoi utiliser la Forge ?</h3>
          <ul class="info-list">
            <li>Recommandations d'experts basées sur vos besoins spécifiques</li>
            <li>Prix transparents de revendeurs de confiance</li>
            <li>Aucune connaissance technique requise</li>
            <li>Configurations équilibrées pour des performances optimales</li>
            <li>Liens directs pour acheter tous les composants</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
.forge-index-container {
  min-height: 100vh;
  padding: 2rem;
}

.forge-index-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}

/* Hero Section */
.hero-section {
  text-align: center;
  margin-bottom: 4rem;
}

.hero-title {
  font-family: var(--font-heading);
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, var(--primary), oklch(0.8 0.2 45));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-family: var(--font-body);
  font-size: 1.5rem;
  color: var(--muted-foreground);
  max-width: 700px;
  margin: 0 auto;
  line-height: 1.6;
}

/* Cards Grid */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.forge-card {
  padding: 2.5rem;
  border-radius: 1.5rem;
  text-decoration: none;
  color: var(--foreground);
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  min-height: 400px;
}

.forge-card:not(.coming-soon) {
  cursor: pointer;
  transition: all 300ms ease;
}

.forge-card:not(.coming-soon):hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px oklch(0.63 0.18 65 / 0.3);
}

.forge-card.coming-soon {
  opacity: 0.7;
  cursor: not-allowed;
}

.card-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: var(--primary);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  font-family: var(--font-body);
  font-size: 0.85rem;
  font-weight: 600;
}

.card-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
}

.card-title {
  font-family: var(--font-heading);
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: var(--foreground);
}

.card-description {
  font-family: var(--font-body);
  font-size: 1.1rem;
  line-height: 1.6;
  color: var(--muted-foreground);
  margin-bottom: 1.5rem;
  flex: 1;
}

.card-features {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
}

.feature-tag {
  background: oklch(0.2 0.02 280);
  color: var(--primary);
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  font-family: var(--font-body);
  font-size: 0.9rem;
  font-weight: 600;
  border: 1px solid oklch(0.3 0.05 280);
}

.card-cta {
  font-family: var(--font-body);
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--primary);
  text-align: center;
  padding: 1rem;
  background: oklch(0.2 0.02 280);
  border-radius: 0.75rem;
  border: 2px solid var(--primary);
  transition: all 300ms ease;
}

.forge-card:not(.coming-soon):hover .card-cta {
  background: var(--primary);
  color: white;
  transform: scale(1.05);
}

/* Info Section */
.info-section {
  margin-top: 4rem;
}

.info-card {
  padding: 2.5rem;
  border-radius: 1.5rem;
  max-width: 800px;
  margin: 0 auto;
}

.info-title {
  font-family: var(--font-heading);
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: var(--foreground);
}

.info-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.info-list li {
  font-family: var(--font-body);
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--muted-foreground);
  padding: 0.75rem 0;
  padding-left: 2rem;
  position: relative;
}

.info-list li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: var(--primary);
  font-weight: bold;
  font-size: 1.3rem;
}

/* Responsive Design */
@media (max-width: 768px) {
  .forge-index-content {
    padding: 1rem;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .cards-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .forge-card {
    min-height: auto;
    padding: 2rem;
  }

  .card-icon {
    font-size: 3rem;
  }

  .info-card {
    padding: 2rem;
  }
}
</style>
