<template>
  <div class="dashboard">
    <!-- Top location bar -->
    <div class="location-bar">
      <div class="location-info">
        <span class="location-icon">📍</span>
        <span class="city-name">{{ location }}</span>
        <span class="weather-info">Max forecast: UV {{ uvIndex }} ({{ getUvLevel() }})</span>
      </div>
      <button class="change-loc-btn" @click="$emit('changeLocation')">Change location</button>
    </div>

    <!-- Sub-navigation -->
    <nav class="sub-nav">
      <ul>
        <li>Understanding UV</li>
        <li>Understanding skin cancer</li>
        <li>Sun protection</li>
        <li>Resources</li>
      </ul>
    </nav>

    <!-- Main content area -->
    <main class="content-area">

      <!-- Hero Card: UV Index -->
      <!-- We use :class to dynamically assign a CSS class to this element -->
      <section class="hero-card" :class="getUvClass()">
        <div class="uv-ring-container">
          <div class="uv-ring">
            <span class="uv-number">{{ uvIndex }}</span>
            <span class="uv-label">{{ getUvLevel() }}</span>
          </div>
        </div>
        <div class="hero-details">
          <p>Sun protection recommended from 10:00 AM to 4:00 PM</p>
          <button class="graph-btn">See today's UV graph</button>
        </div>
      </section>

      <!-- Alert Card (Using v-if, only shows when uvIndex >= 8) -->
      <section v-if="uvIndex >= 8" class="alert-card">
        <div class="alert-header">
          <span class="alert-icon">⚠</span>
          <h3>Very High UV - This is serious!</h3>
        </div>
        <p>Unprotected skin can burn in minutes.</p>
      </section>

      <!-- Time to Burn Card -->
      <section class="info-card time-card">
        <h3>Time to skin damage</h3>
        <p class="big-stat">{{ getTimeToBurn() }} mins</p>
        <p class="small-text">for fair skin without protection</p>
      </section>

      <!-- Protection Tips Card -->
      <section class="info-card tips-card">
        <h3>Protection Tips</h3>
        <ul class="tips-list">
          <li>Slip on sun-protective clothing</li>
          <li>Slop on SPF 30+ sunscreen</li>
          <li>Slap on a broad-brimmed hat</li>
          <li>Seek shade</li>
          <li>Slide on sunglasses</li>
        </ul>
      </section>

      <!-- Clothing Recommendations Component -->
      <ClothingRecommendations />

    </main>
  </div>
</template>

<script>
import ClothingRecommendations from './ClothingRecommendations.vue';

export default {
  components: {
    ClothingRecommendations
  },
  // 'props' are data passed from the parent component (App.vue)
  props: ['location'],

  // 'data' holds the local state for this component
  data() {
    return {
      uvIndex: 9, // We simulate a UV index here
    }
  },

  // 'methods' contains functions we can call
  methods: {
    // This function returns the corresponding level string based on the UV index
    getUvLevel() {
      if (this.uvIndex <= 2) return 'LOW';
      if (this.uvIndex <= 5) return 'MODERATE';
      if (this.uvIndex <= 7) return 'HIGH';
      if (this.uvIndex <= 10) return 'VERY HIGH';
      return 'EXTREME';
    },

    // This function returns a CSS class name based on the UV level
    getUvClass() {
      // For example, 'VERY HIGH' becomes 'very-high'
      return this.getUvLevel().toLowerCase().replace(' ', '-');
    },

    // This function calculates the approximate minutes required for skin sunburn
    getTimeToBurn() {
      // This is a simplified estimation formula
      return Math.round(200 / this.uvIndex);
    }
  },

  // 'mounted' is a lifecycle hook, code here runs after the component is loaded onto the page
  mounted() {
    // Check if the UV index is too high, if so, emit an event to notify the parent component to show an alert
    if (this.uvIndex >= 9) {
      this.$emit('triggerAlert'); // $emit is used to send messages to the parent component
    }
  }
}
</script>

<style scoped>
/* 'scoped' means styles here only affect this component, and won't leak to others */

.dashboard {
  background-color: #f4f7fa; /* Light gray background for the page */
  min-height: 100vh; /* Minimum height is the full screen height */
  padding-bottom: 40px; /* Leave some space at the bottom */
}

.location-bar {
  background: white;
  padding: 15px 20px;
  display: flex; /* Use Flexbox layout */
  justify-content: space-between; /* Align child elements to opposite ends */
  align-items: center; /* Vertically center */
  border-bottom: 1px solid #eee;
  font-size: 0.9rem;
}

.location-info {
  display: flex;
  align-items: center;
  gap: 10px; /* Spacing between elements */
  font-weight: 500;
}

.change-loc-btn {
  background: none;
  border: 1px solid #ccc;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.8rem;
}

.sub-nav {
  background: #003366;
  color: white;
  padding: 10px 0;
  overflow-x: auto; /* Allow horizontal scrolling if content overflows */
}

.sub-nav ul {
  display: flex;
  list-style: none;
  padding: 0 20px;
  margin: 0;
  gap: 20px;
  white-space: nowrap; /* Prevent text from wrapping */
}

/* Main content area, we vertically stack all cards */
.content-area {
  padding: 20px;
  max-width: 800px; /* Maximum width of the content */
  margin-left: auto; /* These two lines center the content on the page */
  margin-right: auto;
}

/* Add 20px vertical spacing between each direct child element (card) */
.content-area > * {
  margin-bottom: 20px;
}

/* Hero Card */
.hero-card {
  background: linear-gradient(135deg, #0056b3, #004494);
  color: white;
  border-radius: 12px;
  padding: 30px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0,50,100,0.2);
}

.uv-ring {
  width: 150px;
  height: 150px;
  border-radius: 50%; /* 50% border-radius creates a perfect circle */
  border: 10px solid rgba(255,255,255,0.3);
  margin: 0 auto 20px;
  display: flex;
  flex-direction: column; /* Vertically stack internal elements */
  justify-content: center;
  align-items: center;
}

/* Change the ring color based on the UV level */
.hero-card.very-high .uv-ring { border-color: #e63946; } /* Red */
.hero-card.moderate .uv-ring { border-color: #ffb703; } /* Yellow */
.hero-card.low .uv-ring { border-color: #2a9d8f; } /* Green */

.uv-number {
  font-size: 3rem;
  font-weight: bold;
}

.uv-label {
  font-size: 1rem;
  text-transform: uppercase; /* Uppercase text */
}

.graph-btn {
  margin-top: 15px;
  background: rgba(255,255,255,0.2);
  border: 1px solid white;
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  cursor: pointer;
}

/* Alert Card */
.alert-card {
  background-color: #ffebee;
  border: 1px solid #ffcdd2;
  color: #b71c1c;
  padding: 15px;
  border-radius: 8px;
}

/* Standard Info Card */
.info-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.info-card h3 {
  margin-top: 0;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 15px;
}

.big-stat {
  font-size: 2.5rem;
  font-weight: bold;
  margin: 0;
}

.tips-list {
  padding-left: 20px;
  line-height: 1.6;
}
</style>