<template>
  <div class="results-container">
    <div class="results-content">
      <!-- Header -->
      <div class="results-header">
        <h1 class="results-title">🎉 Your Perfect PC Configuration</h1>
        <p class="results-subtitle">Based on your preferences, here's what we recommend</p>
      </div>

      <!-- Selected Criteria -->
      <div class="criteria-summary">
        <div class="criterion">
          <span class="criterion-label">Budget:</span>
          <span class="criterion-value">€{{ priceRange }}</span>
        </div>
        <div class="criterion">
          <span class="criterion-label">Usage:</span>
          <span class="criterion-value">{{ usageLabel }}</span>
        </div>
        <div class="criterion">
          <span class="criterion-label">Type:</span>
          <span class="criterion-value">{{ formFactorLabel }}</span>
        </div>
      </div>

      <!-- Recommended Configuration -->
      <div class="recommendation-card">
        <div class="card-header">
          <h2 class="card-title">{{ recommendation.name }}</h2>
          <div class="card-price">{{ recommendation.price }}</div>
        </div>

        <div class="card-content">
          <div class="specs-section">
            <h3 class="specs-title">📋 Specifications</h3>
            <div class="specs-grid">
              <div v-for="spec in recommendation.specs" :key="spec.label" class="spec-item">
                <div class="spec-icon">{{ spec.icon }}</div>
                <div class="spec-details">
                  <div class="spec-label">{{ spec.label }}</div>
                  <div class="spec-value">{{ spec.value }}</div>
                </div>
              </div>
            </div>
          </div>

          <div class="features-section">
            <h3 class="features-title">✨ Perfect for</h3>
            <ul class="features-list">
              <li v-for="feature in recommendation.features" :key="feature">
                <span class="check-icon">✓</span> {{ feature }}
              </li>
            </ul>
          </div>

          <div class="description-section">
            <p class="description">{{ recommendation.description }}</p>
          </div>
        </div>

        <div class="card-footer">
          <h3 class="buy-title">🛒 Where to Buy</h3>
          <div class="retailers-grid">
            <a 
              v-for="retailer in recommendation.retailers" 
              :key="retailer.name"
              :href="retailer.url"
              target="_blank"
              rel="noopener noreferrer"
              class="retailer-link"
            >
              <span class="retailer-name">{{ retailer.name }}</span>
              <span class="retailer-icon">→</span>
            </a>
          </div>
        </div>
      </div>

      <!-- Action Buttons -->
      <div class="action-buttons">
        <button class="btn btn-secondary" @click="goBack">
          ← Start Over
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()

// Get query parameters
const priceRange = computed(() => route.query.price as string || '800-1000')
const usage = computed(() => route.query.usage as string || 'office')
const formFactor = computed(() => route.query.formFactor as string || 'desktop')

// Labels for display
const usageLabels: Record<string, string> = {
  gaming: 'Gaming',
  office: 'Office & Media',
  creative: 'Creative Work',
  development: 'Development'
}

const formFactorLabels: Record<string, string> = {
  desktop: 'Desktop Tower',
  laptop: 'Laptop'
}

const usageLabel = computed(() => usageLabels[usage.value] || 'Unknown')
const formFactorLabel = computed(() => formFactorLabels[formFactor.value] || 'Unknown')

// Generate recommendation based on selections
const recommendation = computed(() => {
  const config = getConfiguration(priceRange.value, usage.value, formFactor.value)
  return config
})

// Types
interface Spec {
  icon: string
  label: string
  value: string
}

interface Retailer {
  name: string
  url: string
}

interface Configuration {
  name: string
  price: string
  specs: Spec[]
  features: string[]
  description: string
  retailers: Retailer[]
}

// Configuration database
function getConfiguration(price: string, usageType: string, factor: string): Configuration {
  const configs: Record<string, Configuration> = {
    // Desktop configurations
    'desktop-800-1000-office': {
      name: 'Essential Office Desktop',
      price: '€850',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'AMD Ryzen 5 5600' },
        { icon: '💾', label: 'RAM', value: '16GB DDR4' },
        { icon: '💿', label: 'Storage', value: '512GB NVMe SSD' },
        { icon: '🎨', label: 'Graphics', value: 'Integrated Radeon' },
      ],
      features: [
        'Smooth multitasking',
        '4K video playback',
        'Fast boot times',
        'Quiet operation',
        'Energy efficient'
      ],
      description: 'Perfect for everyday computing tasks, web browsing, office work, and media consumption. This build offers excellent value and reliability.',
      retailers: [
        { name: 'Alternate.be', url: 'https://www.alternate.be' },
        { name: 'Coolblue', url: 'https://www.coolblue.be' },
        { name: 'Azerty', url: 'https://www.azerty.nl' }
      ]
    },
    'desktop-800-1000-gaming': {
      name: 'Budget Gaming Desktop',
      price: '€950',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'AMD Ryzen 5 5600' },
        { icon: '💾', label: 'RAM', value: '16GB DDR4' },
        { icon: '💿', label: 'Storage', value: '500GB NVMe SSD' },
        { icon: '🎨', label: 'Graphics', value: 'NVIDIA GTX 1660 Super' },
      ],
      features: [
        '1080p gaming at 60+ FPS',
        'E-sports titles at high settings',
        'Great entry point',
        'Upgradeable platform'
      ],
      description: 'An excellent starting point for PC gaming. Handles most modern games at 1080p with good frame rates.',
      retailers: [
        { name: 'Alternate.be', url: 'https://www.alternate.be' },
        { name: 'Megekko', url: 'https://www.megekko.nl' },
        { name: 'Azerty', url: 'https://www.azerty.nl' }
      ]
    },
    'desktop-1500-2000-gaming': {
      name: 'Performance Gaming Desktop',
      price: '€1,750',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'AMD Ryzen 7 5800X3D' },
        { icon: '💾', label: 'RAM', value: '32GB DDR4' },
        { icon: '💿', label: 'Storage', value: '1TB NVMe SSD' },
        { icon: '🎨', label: 'Graphics', value: 'NVIDIA RTX 4060 Ti' },
      ],
      features: [
        '1440p high-refresh gaming',
        'Ray tracing capable',
        'Streaming ready',
        'VR compatible',
        'Future-proof performance'
      ],
      description: 'A powerful gaming machine that handles AAA titles at high settings with ray tracing. Excellent for content creation too.',
      retailers: [
        { name: 'Alternate.be', url: 'https://www.alternate.be' },
        { name: 'Coolblue', url: 'https://www.coolblue.be' },
        { name: 'Megekko', url: 'https://www.megekko.nl' }
      ]
    },
    'desktop-2500-3000-gaming': {
      name: 'Ultimate Gaming Beast',
      price: '€2,850',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'AMD Ryzen 9 7900X' },
        { icon: '💾', label: 'RAM', value: '32GB DDR5' },
        { icon: '💿', label: 'Storage', value: '2TB NVMe Gen4 SSD' },
        { icon: '🎨', label: 'Graphics', value: 'NVIDIA RTX 4080' },
      ],
      features: [
        '4K gaming at 120+ FPS',
        'Maximum ray tracing',
        'Professional workloads',
        'Top-tier performance',
        'Premium components'
      ],
      description: 'The ultimate gaming and content creation powerhouse. No compromises, maximum performance in every scenario.',
      retailers: [
        { name: 'Alternate.be', url: 'https://www.alternate.be' },
        { name: 'Coolblue', url: 'https://www.coolblue.be' },
        { name: 'Informatique', url: 'https://www.informatique.be' }
      ]
    },
    // Laptop configurations
    'laptop-800-1000-office': {
      name: 'Essential Office Laptop',
      price: '€899',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'AMD Ryzen 5 5500U' },
        { icon: '💾', label: 'RAM', value: '16GB DDR4' },
        { icon: '💿', label: 'Storage', value: '512GB SSD' },
        { icon: '📺', label: 'Display', value: '15.6" Full HD IPS' },
      ],
      features: [
        'All-day battery life',
        'Lightweight design',
        'Perfect for remote work',
        'Comfortable keyboard',
        'Good webcam'
      ],
      description: 'Reliable laptop for everyday tasks, video calls, and productivity. Great battery life and portability.',
      retailers: [
        { name: 'Coolblue', url: 'https://www.coolblue.be' },
        { name: 'MediaMarkt', url: 'https://www.mediamarkt.be' },
        { name: 'Bol.com', url: 'https://www.bol.com' }
      ]
    },
    'laptop-1500-2000-gaming': {
      name: 'Gaming Laptop Pro',
      price: '€1,699',
      specs: [
        { icon: '🧠', label: 'Processor', value: 'Intel Core i7-12700H' },
        { icon: '💾', label: 'RAM', value: '16GB DDR5' },
        { icon: '💿', label: 'Storage', value: '1TB SSD' },
        { icon: '🎨', label: 'Graphics', value: 'NVIDIA RTX 4060' },
        { icon: '📺', label: 'Display', value: '15.6" 165Hz QHD' },
      ],
      features: [
        'High refresh gaming',
        'Portable powerhouse',
        'RGB keyboard',
        'Advanced cooling',
        'Great connectivity'
      ],
      description: 'A powerful gaming laptop that doesn\'t compromise on performance. Perfect for gamers on the go.',
      retailers: [
        { name: 'Coolblue', url: 'https://www.coolblue.be' },
        { name: 'Alternate.be', url: 'https://www.alternate.be' },
        { name: 'MediaMarkt', url: 'https://www.mediamarkt.be' }
      ]
    }
  }

  // Create config key
  const key = `${factor}-${price}-${usageType}`
  
  // Return matching config or default
  return configs[key] || configs[`${factor}-${price}-office`] || {
    name: 'Custom Configuration',
    price: `€${price.split('-')[0]}+`,
    specs: [
      { icon: '🧠', label: 'Processor', value: 'Optimized for your needs' },
      { icon: '💾', label: 'RAM', value: 'Sufficient capacity' },
      { icon: '💿', label: 'Storage', value: 'Fast SSD storage' },
    ],
    features: [
      'Tailored to your requirements',
      'Best value for budget',
      'Quality components'
    ],
    description: 'A custom configuration matching your specific needs and budget.',
    retailers: [
      { name: 'Alternate.be', url: 'https://www.alternate.be' },
      { name: 'Coolblue', url: 'https://www.coolblue.be' }
    ]
  }
}

// Methods
const goBack = () => {
  router.push('/forge/first-pc')
}
</script>

<style scoped>
.results-container {
  min-height: 100vh;
  padding: 2rem;
}

.results-content {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
}

/* Header */
.results-header {
  text-align: center;
  margin-bottom: 3rem;
}

.results-title {
  font-family: var(--font-heading);
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, var(--primary), oklch(0.8 0.2 45));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.results-subtitle {
  font-family: var(--font-body);
  font-size: 1.2rem;
  color: var(--muted-foreground);
}

/* Criteria Summary */
.criteria-summary {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.criterion {
  background: oklch(0.15 0.02 280 / 0.6);
  backdrop-filter: blur(10px);
  border: 1px solid oklch(0.25 0.05 280);
  border-radius: 0.75rem;
  padding: 1rem 1.5rem;
  display: flex;
  gap: 0.5rem;
}

.criterion-label {
  font-family: var(--font-body);
  font-weight: 600;
  color: var(--muted-foreground);
}

.criterion-value {
  font-family: var(--font-body);
  font-weight: 700;
  color: var(--primary);
}

/* Recommendation Card */
.recommendation-card {
  background: oklch(0.15 0.02 280 / 0.8);
  backdrop-filter: blur(10px);
  border: 2px solid oklch(0.25 0.05 280);
  border-radius: 1.5rem;
  overflow: hidden;
  margin-bottom: 2rem;
  box-shadow: 0 20px 60px oklch(0 0 0 / 0.3);
}

.card-header {
  background: linear-gradient(135deg, oklch(0.2 0.05 280), oklch(0.18 0.03 260));
  padding: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid var(--primary);
}

.card-title {
  font-family: var(--font-heading);
  font-size: 2rem;
  font-weight: 700;
  color: var(--foreground);
}

.card-price {
  font-family: var(--font-heading);
  font-size: 2rem;
  font-weight: 800;
  color: var(--primary);
}

.card-content {
  padding: 2rem;
}

/* Specs Section */
.specs-section {
  margin-bottom: 2rem;
}

.specs-title {
  font-family: var(--font-heading);
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--foreground);
  margin-bottom: 1.5rem;
}

.specs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.spec-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: oklch(0.2 0.02 280);
  border: 1px solid oklch(0.25 0.05 280);
  border-radius: 0.75rem;
  padding: 1rem;
}

.spec-icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.spec-details {
  flex: 1;
}

.spec-label {
  font-family: var(--font-body);
  font-size: 0.9rem;
  color: var(--muted-foreground);
  margin-bottom: 0.25rem;
}

.spec-value {
  font-family: var(--font-body);
  font-size: 1rem;
  font-weight: 600;
  color: var(--foreground);
}

/* Features Section */
.features-section {
  margin-bottom: 2rem;
}

.features-title {
  font-family: var(--font-heading);
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--foreground);
  margin-bottom: 1rem;
}

.features-list {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 0.75rem;
}

.features-list li {
  font-family: var(--font-body);
  font-size: 1rem;
  color: var(--foreground);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.check-icon {
  color: oklch(0.5 0.15 150);
  font-weight: bold;
  font-size: 1.2rem;
}

/* Description Section */
.description-section {
  margin-top: 2rem;
  padding-top: 2rem;
  border-top: 1px solid oklch(0.25 0.05 280);
}

.description {
  font-family: var(--font-body);
  font-size: 1.1rem;
  line-height: 1.6;
  color: var(--muted-foreground);
}

/* Card Footer */
.card-footer {
  background: oklch(0.18 0.02 280);
  padding: 2rem;
  border-top: 1px solid oklch(0.25 0.05 280);
}

.buy-title {
  font-family: var(--font-heading);
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--foreground);
  margin-bottom: 1rem;
}

.retailers-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.retailer-link {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: oklch(0.2 0.02 280);
  border: 2px solid oklch(0.25 0.05 280);
  border-radius: 0.75rem;
  padding: 1rem 1.5rem;
  text-decoration: none;
  color: var(--foreground);
  font-family: var(--font-body);
  font-weight: 600;
  transition: all 300ms ease;
}

.retailer-link:hover {
  background: oklch(0.25 0.05 280);
  border-color: var(--primary);
  transform: translateX(5px);
}

.retailer-icon {
  color: var(--primary);
  font-size: 1.5rem;
  transition: transform 300ms ease;
}

.retailer-link:hover .retailer-icon {
  transform: translateX(5px);
}

/* Action Buttons */
.action-buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
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
  min-width: 200px;
}

.btn-primary {
  background: var(--primary);
  color: white;
}

.btn-primary:hover {
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

/* Responsive Design */
@media (max-width: 768px) {
  .results-content {
    padding: 1rem;
  }

  .results-title {
    font-size: 1.8rem;
  }

  .criteria-summary {
    flex-direction: column;
    gap: 1rem;
  }

  .card-header {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }

  .specs-grid,
  .features-list {
    grid-template-columns: 1fr;
  }

  .retailers-grid {
    grid-template-columns: 1fr;
  }

  .action-buttons {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>
