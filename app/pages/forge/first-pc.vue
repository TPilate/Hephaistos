<template>
  <div class="forge-container">
    <div class="forge-content">
      <h1 class="forge-title">🔨 Forger le PC fait pour vous</h1>
      <p class="forge-subtitle">Construisons ensemble le PC qui correspond à vos besoins.</p>

      <!-- Stepper Progress -->
      <div class="stepper">
        <div 
          v-for="(step, index) in steps" 
          :key="index"
          class="step-item"
          :class="{ 
            'active': currentStep === index, 
            'completed': currentStep > index 
          }"
        >
          <div class="step-circle">
            <span v-if="currentStep > index" class="check-icon">✓</span>
            <span v-else>{{ index + 1 }}</span>
          </div>
          <div class="step-label">{{ step.label }}</div>
          <div v-if="index < steps.length - 1" class="step-line"/>
        </div>
      </div>

      <!-- Step Content -->
      <div class="step-content">
        <!-- Step 1: Price Range -->
        <div v-if="currentStep === 0" class="step-section">
          <h2 class="step-title">💰 Quel est votre budget ?</h2>
          <p class="step-description">Choisissez une fourchette de prix adaptée à vos besoins</p>
          
          <div class="options-grid">
            <div 
              v-for="range in priceRanges" 
              :key="range.value"
              class="option-card"
              :class="{ 'selected': selectedPriceRange === range.value }"
              @click="selectedPriceRange = range.value"
            >
              <div class="option-icon">{{ range.icon }}</div>
              <div class="option-title">{{ range.label }}</div>
              <div class="option-description">{{ range.description }}</div>
            </div>
          </div>
        </div>

        <!-- Step 2: Usage Type -->
        <div v-if="currentStep === 1" class="step-section">
          <h2 class="step-title">🎯 Quelle sera votre utilisation ?</h2>
          <p class="step-description">Sélectionnez votre cas d'usage principal</p>
          
          <div class="options-grid">
            <div 
              v-for="usage in usageTypes" 
              :key="usage.value"
              class="option-card"
              :class="{ 'selected': selectedUsage === usage.value }"
              @click="selectedUsage = usage.value"
            >
              <div class="option-icon">{{ usage.icon }}</div>
              <div class="option-title">{{ usage.label }}</div>
              <div class="option-description">{{ usage.description }}</div>
            </div>
          </div>
        </div>

        <!-- Step 3: Form Factor -->
        <div v-if="currentStep === 2" class="step-section">
          <h2 class="step-title">🖥️ Choisissez votre format</h2>
          <p class="step-description">Ordinateur de bureau ou portable ?</p>
          
          <div class="options-grid">
            <div 
              v-for="factor in formFactors" 
              :key="factor.value"
              class="option-card large"
              :class="{ 'selected': selectedFormFactor === factor.value }"
              @click="selectedFormFactor = factor.value"
            >
              <div class="option-icon large">{{ factor.icon }}</div>
              <div class="option-title">{{ factor.label }}</div>
              <div class="option-description">{{ factor.description }}</div>
              <ul class="option-features">
                <li v-for="feature in factor.features" :key="feature">{{ feature }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <!-- Navigation Buttons -->
      <div class="navigation-buttons">
        <button 
          v-if="currentStep > 0"
          class="btn btn-secondary"
          @click="previousStep"
        >
          ← Précédent
        </button>
        <button 
          v-if="currentStep < steps.length - 1"
          :disabled="!canProceed"
          class="btn btn-primary"
          @click="nextStep"
        >
          Suivant →
        </button>
        <button 
          v-if="currentStep === steps.length - 1"
          :disabled="!canProceed"
          class="btn btn-success"
          @click="submitConfiguration"
        >
          🔥 Forger mon PC
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// Stepper state
const currentStep = ref(0)
const steps = [
  { label: 'Budget' },
  { label: 'Usage' },
  { label: 'Format' }
]

// User selections
const selectedPriceRange = ref<string | null>(null)
const selectedUsage = ref<string | null>(null)
const selectedFormFactor = ref<string | null>(null)

// Price ranges
const priceRanges = [
  {
    value: '800-1000',
    label: '800 € - 1 000 €',
    icon: '💚',
    description: 'Entrée de gamme - Idéal pour un usage quotidien'
  },
  {
    value: '1500-2000',
    label: '1 500 € - 2 000 €',
    icon: '💙',
    description: 'Milieu de gamme - Équilibre parfait entre puissance et prix'
  },
  {
    value: '2500-3000',
    label: '2 500 € - 3 000 €',
    icon: '💜',
    description: 'Haut de gamme - Performance maximale'
  }
]

// Usage types
const usageTypes = [
  {
    value: 'gaming',
    label: 'Jeux vidéo',
    icon: '🎮',
    description: 'FPS élevés, ray tracing, jeux AAA'
  },
  {
    value: 'office',
    label: 'Bureautique & Multimédia',
    icon: '📄',
    description: 'Documents, navigation, streaming'
  },
  {
    value: 'creative',
    label: 'Création',
    icon: '🎨',
    description: 'Montage photo/vidéo, modélisation 3D'
  },
  {
    value: 'development',
    label: 'Développement',
    icon: '💻',
    description: 'Programmation, VMs, conteneurs, multitâche'
  }
]

// Form factors
const formFactors = [
  {
    value: 'desktop',
    label: 'Tour de bureau',
    icon: '🖥️',
    description: 'Puissance et évolutivité maximales',
    features: [
      '✓ Meilleur rapport performance/prix',
      '✓ Facile à upgrader',
      '✓ Meilleur refroidissement',
      '✓ Composants plus puissants'
    ]
  },
  {
    value: 'laptop',
    label: 'Ordinateur portable',
    icon: '💻',
    description: 'Portabilité et praticité',
    features: [
      '✓ Emportez-le partout',
      '✓ Écran et batterie intégrés',
      '✓ Design compact',
      '✓ Solution tout-en-un'
    ]
  }
]

// Computed properties
const canProceed = computed(() => {
  if (currentStep.value === 0) return selectedPriceRange.value !== null
  if (currentStep.value === 1) return selectedUsage.value !== null
  if (currentStep.value === 2) return selectedFormFactor.value !== null
  return false
})

// Methods
const nextStep = () => {
  if (canProceed.value && currentStep.value < steps.length - 1) {
    currentStep.value++
  }
}

const previousStep = () => {
  if (currentStep.value > 0) {
    currentStep.value--
  }
}

const submitConfiguration = () => {
  if (canProceed.value) {
    // Navigate to results page with query parameters
    router.push({
      path: '/forge/results',
      query: {
        price: selectedPriceRange.value,
        usage: selectedUsage.value,
        formFactor: selectedFormFactor.value
      }
    })
  }
}
</script>

<style scoped>
.forge-container {
  min-height: 100vh;
  padding: 2rem;
}

.forge-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.forge-title {
  font-family: var(--font-heading);
  font-size: 3rem;
  font-weight: 800;
  text-align: center;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, var(--primary), oklch(0.8 0.2 45));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.forge-subtitle {
  font-family: var(--font-body);
  font-size: 1.25rem;
  text-align: center;
  color: var(--muted-foreground);
  margin-bottom: 3rem;
}

/* Stepper Styles */
.stepper {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 4rem;
  position: relative;
}

.step-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  flex: 1;
  max-width: 200px;
}

.step-circle {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: oklch(0.2 0.02 280);
  border: 3px solid oklch(0.3 0.05 280);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.25rem;
  color: var(--muted-foreground);
  transition: all 300ms ease;
  z-index: 2;
  position: relative;
}

.step-item.active .step-circle {
  background: var(--primary);
  border-color: var(--primary);
  color: white;
  box-shadow: 0 0 20px oklch(0.63 0.18 65 / 0.5);
  transform: scale(1.1);
}

.step-item.completed .step-circle {
  background: oklch(0.5 0.15 150);
  border-color: oklch(0.5 0.15 150);
  color: white;
}

.check-icon {
  font-size: 1.5rem;
}

.step-label {
  margin-top: 1rem;
  font-family: var(--font-body);
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--muted-foreground);
  text-align: center;
}

.step-item.active .step-label {
  color: var(--primary);
}

.step-item.completed .step-label {
  color: oklch(0.5 0.15 150);
}

.step-line {
  position: absolute;
  top: 25px;
  left: 50%;
  width: 100%;
  height: 3px;
  background: oklch(0.3 0.05 280);
  z-index: 1;
  transition: background 300ms ease;
}

.step-item.completed .step-line {
  background: oklch(0.5 0.15 150);
}

/* Step Content */
.step-content {
  min-height: 400px;
  margin-bottom: 3rem;
}

.step-section {
  animation: fadeIn 400ms ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.step-title {
  font-family: var(--font-heading);
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 0.5rem;
  color: var(--foreground);
}

.step-description {
  font-family: var(--font-body);
  font-size: 1.1rem;
  text-align: center;
  color: var(--muted-foreground);
  margin-bottom: 3rem;
}

/* Options Grid */
.options-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.option-card {
  background: oklch(0.15 0.02 280 / 0.6);
  backdrop-filter: blur(10px);
  border: 2px solid oklch(0.25 0.05 280);
  border-radius: 1rem;
  padding: 2rem;
  cursor: pointer;
  transition: all 300ms ease;
  text-align: center;
}

.option-card:hover {
  transform: translateY(-5px);
  border-color: var(--primary);
  box-shadow: 0 10px 30px oklch(0.63 0.18 65 / 0.2);
}

.option-card.selected {
  background: oklch(0.2 0.02 280);
  border-color: var(--primary);
  box-shadow: 0 0 30px oklch(0.63 0.18 65 / 0.4);
}

.option-card.large {
  padding: 2.5rem;
}

.option-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.option-icon.large {
  font-size: 4rem;
}

.option-title {
  font-family: var(--font-heading);
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--foreground);
  margin-bottom: 0.5rem;
}

.option-description {
  font-family: var(--font-body);
  font-size: 1rem;
  color: var(--muted-foreground);
  margin-bottom: 1rem;
}

.option-features {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0 0;
  text-align: left;
}

.option-features li {
  font-family: var(--font-body);
  font-size: 0.95rem;
  color: var(--muted-foreground);
  padding: 0.5rem 0;
  border-top: 1px solid oklch(0.25 0.05 280);
}

/* Navigation Buttons */
.navigation-buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 2rem;
}

.btn {
  padding: 1rem 2rem;
  font-family: var(--font-body);
  font-size: 1.1rem;
  font-weight: 600;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: all 300ms ease;
  min-width: 150px;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-primary {
  background: var(--primary);
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: oklch(0.7 0.2 65);
  transform: translateY(-2px);
  box-shadow: 0 10px 20px oklch(0.63 0.18 65 / 0.3);
}

.btn-secondary {
  background: oklch(0.25 0.05 280);
  color: var(--foreground);
}

.btn-secondary:hover {
  background: oklch(0.3 0.05 280);
  transform: translateY(-2px);
}

.btn-success {
  background: linear-gradient(135deg, var(--primary), oklch(0.8 0.2 45));
  color: white;
  font-size: 1.2rem;
}

.btn-success:hover:not(:disabled) {
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 15px 30px oklch(0.63 0.18 65 / 0.4);
}

/* Responsive Design */
@media (max-width: 768px) {
  .forge-content {
    padding: 1rem;
  }

  .forge-title {
    font-size: 2rem;
  }

  .stepper {
    flex-direction: column;
    gap: 1rem;
  }

  .step-line {
    display: none;
  }

  .options-grid {
    grid-template-columns: 1fr;
  }

  .navigation-buttons {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>
