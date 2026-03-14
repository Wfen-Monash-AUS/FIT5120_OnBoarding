<template>
  <!-- id="app" is the root container for the entire Vue application -->
  <div id="app">

    <!-- 1. Header component at the top of the page -->
    <!-- @goHome is a custom event listener. When the Header component emits a 'goHome' event, the 'resetToHome' method here is called -->
    <Header @goHome="resetToHome" />

    <!-- 2. Main content area -->
    <main class="main-content">

      <!-- Use v-if and v-else-if to determine which page component to display based on the value of currentView -->

      <!-- If currentView is 'home', display the HomeView component -->
      <HomeView
        v-if="currentView === 'home'"
        @location-selected="handleLocationSelected"
      />

      <!-- Otherwise, if currentView is 'dashboard', display the DashboardView component -->
      <DashboardView
        v-else-if="currentView === 'dashboard'"
        :location="selectedLocation"
        @changeLocation="resetToHome"
        @triggerAlert="showAlert = true"
      />
    </main>

    <!-- 3. Footer component at the bottom of the page -->
    <Footer />

    <!-- 4. Alert modal component -->
    <!-- :isVisible is a prop that passes the value of showAlert (true/false) to the AlertModal component to control its display -->
    <AlertModal
      :isVisible="showAlert"
      @close="showAlert = false"
    />
  </div>
</template>

<script>
// Import all the components we need from the './components/' folder
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import HomeView from './components/HomeView.vue'
import DashboardView from './components/DashboardView.vue'
import AlertModal from './components/AlertModal.vue'

export default {
  name: 'App',

  // Register the imported components here so we can use them in the <template>
  components: {
    Header,
    Footer,
    HomeView,
    DashboardView,
    AlertModal
  },

  // The data() function returns an object containing the state (data) managed internally by this component
  data() {
    return {
      currentView: 'home',      // Controls which page is currently displayed, 'home' or 'dashboard'
      selectedLocation: '',     // Stores the location selected by the user
      showAlert: false          // Controls whether the alert modal is displayed, true or false
    }
  },

  // The methods object contains functions we can call
  methods: {
    // This function is called after a location is selected in the HomeView component
    handleLocationSelected(location) {
      this.selectedLocation = location; // Save the location

      // Simulate a short loading delay to make it feel more realistic to the user
      setTimeout(() => {
        this.currentView = 'dashboard'; // Switch to the dashboard page
      }, 500); // 500 milliseconds = 0.5 seconds
    },

    // This function is used to return to the home page
    resetToHome() {
      this.currentView = 'home';
      this.selectedLocation = '';
      this.showAlert = false; // Also ensure the alert modal is closed
    }
  }
}
</script>

<style>
/* Styles here are global and will affect all components in the entire application */

/* Basic style reset to ensure consistent behavior across different browsers */
body {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Set a common sans-serif font */
  color: #2c3e50; /* Set the default text color */
  background-color: #f8f9fa; /* Set the page background color */
}

/* Make the app container stretch to the full screen height */
#app {
  display: flex;
  flex-direction: column; /* Vertically arrange child elements (Header, main, Footer) */
  min-height: 100vh; /* Minimum height is 100% of the viewport height */
}

/* Allow the main content area to automatically expand to fill all space between Header and Footer */
.main-content {
  flex-grow: 1;
}

/* This is a good practice to give all buttons a pointer cursor */
button {
  cursor: pointer;
}

/* The box-sizing rule makes layout easier to calculate */
* {
  box-sizing: border-box;
}
</style>
