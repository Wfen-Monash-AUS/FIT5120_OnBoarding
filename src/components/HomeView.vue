<template>
  <!-- This is the container for the home page -->
  <div class="home-container">
    <!-- The white card in the center -->
    <div class="card">
      <h1 class="title">Real-Time UV Protection</h1>
      <p class="subtitle">Know exactly when UV radiation becomes dangerous</p>

      <!-- "Use My Current Location" button area -->
      <div class="input-group">
        <label>Set Your Location</label>
        <!-- @click is an event listener, when the button is clicked, it calls the 'useCurrentLocation' method -->
        <button class="current-loc-btn" @click="useCurrentLocation">
          <span>📍</span> Use My Current Location
        </button>
      </div>

      <!-- The "or" divider in the middle -->
      <div class="divider">
        <span class="or-text">or</span>
      </div>

      <!-- City search area -->
      <div class="search-group">
        <!-- v-model="city" creates two-way binding between the input value and the 'city' variable in data -->
        <input
          type="text"
          placeholder="Enter city name..."
          v-model="city"
        />
        <button class="search-btn" @click="searchCity">Search</button>
      </div>

      <!-- Explanatory text at the bottom -->
      <div class="info-text">
        <p>UV levels change rapidly throughout the day.</p>
        <p>Get accurate, localized data to protect your skin.</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // data() returns the data specific to this component
  data() {
    return {
      city: '' // Used to store the city name entered by the user in the input box
    }
  },
  methods: {
    // Called when the user clicks the "Use My Current Location" button
    useCurrentLocation() {
      // Emits an event named 'location-selected' and passes a value
      // The parent component (App.vue) will listen for this event
      this.$emit('location-selected', 'Current Location');
    },
    // Called when the user clicks the "Search" button
    searchCity() {
      // Ensure the user has entered something
      if (this.city) {
        this.$emit('location-selected', this.city);
      }
    }
  }
}
</script>

<style scoped>
/* Home container, uses Flexbox to center the card vertically and horizontally */
.home-container {
  display: flex;
  justify-content: center; /* Center horizontally */
  align-items: center;    /* Center vertically */
  min-height: 80vh; /* Minimum height is 80% of the viewport height */
  background-color: #f0f4f8;
  padding: 20px;
}

/* Styles for the center white card */
.card {
  background-color: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  text-align: center;
  max-width: 500px;
  width: 100%;
}

.title {
  color: #003366;
  margin-bottom: 10px;
}

.subtitle {
  color: #666;
  margin-bottom: 30px;
}

.input-group, .search-group {
  margin-bottom: 20px;
}

.current-loc-btn {
  width: 100%;
  padding: 12px;
  background-color: #007BFF;
  color: white;
  border-style: none; /* Remove border */
  border-radius: 6px;
  font-size: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  transition: background-color 0.3s; /* Transition effect for background color change */
}

.current-loc-btn:hover {
  background-color: #0056b3; /* Color when mouse hovers */
}

/* Divider styles */
.divider {
  position: relative; /* Used for positioning pseudo-elements */
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

/* This is the gray horizontal line */
.divider::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  height: 1px;
  background-color: #ddd;
}

/* Style for the "or" text, it covers the line */
.or-text {
  background-color: white;
  padding-left: 10px;
  padding-right: 10px;
  color: #999;
  position: relative; /* Ensure it is above the horizontal line */
}

.search-group {
  display: flex;
  gap: 10px;
}

.search-group input {
  flex-grow: 1; /* Input box takes up most of the space */
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.search-btn {
  padding: 10px 20px;
  background-color: #007BFF;
  color: white;
  border-style: none;
  border-radius: 6px;
}

.info-text {
  margin-top: 30px;
  font-size: 0.9rem;
  color: #888;
}
</style>
