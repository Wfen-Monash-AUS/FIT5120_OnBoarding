<template>
  <!-- This is the footer component -->
  <footer class="app-footer">
    <!-- Top part of the footer containing logo and menus -->
    <div class="footer-top">
      <!-- Logo and tagline -->
      <div class="footer-col brand-col">
        <div class="logo">
          <span class="sun-icon">☀</span>
          <span class="brand-name">UV Shield</span>
        </div>
        <p class="tagline">your skin from UV radiation</p>
      </div>
      <!-- Menu columns -->
      <div class="footer-col">
        <h4>Understanding UV</h4>
        <ul>
          <li>What is UV radiation?</li>
          <li>UV Index explained</li>
          <li>Myths about UV</li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Sun Protection</h4>
        <ul>
          <li>How to protect yourself</li>
          <li>Sunscreen guide</li>
          <li>UPF clothing</li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Resources</h4>
        <ul>
          <li>UV forecast</li>
          <li>Glossary of terms</li>
          <li>Scientific research</li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>About</h4>
        <ul>
          <li>About UV Shield</li>
          <li>Our data sources</li>
          <li>Contact us</li>
        </ul>
      </div>
    </div>
    <!-- Bottom part of the footer containing copyright info -->
    <div class="footer-bottom">
      <p>&copy; 2026 UV Shield. All rights reserved. | Data powered by World Weather Online.</p>
    </div>
  </footer>
</template>

<style scoped>
/* Overall footer styles */
.app-footer {
  background-color: #003366; /* Deep blue background */
  color: white;
  padding-top: 3rem;
  padding-bottom: 3rem;
  padding-left: 2rem;
  padding-right: 2rem;
  font-size: 0.9rem;
}

/* Container for the top part of the footer, uses Flexbox layout */
.footer-top {
  display: flex;
  flex-wrap: wrap; /* Allows wrapping to adapt to small screens */
  gap: 2rem; /* Spacing between columns */
  justify-content: space-between; /* Evenly distribute space between columns */
  border-bottom: 1px solid rgba(255,255,255,0.2); /* Semi-transparent divider line */
  padding-bottom: 2rem;
  max-width: 1200px; /* Maximum width of content */
  margin-left: auto; /* Center horizontally */
  margin-right: auto;
}

/* Specific styles for the brand column */
.brand-col {
  flex-basis: 250px; /* Base width */
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.sun-icon {
  font-size: 1.8rem;
  color: #FDB813; /* Yellow sun */
}

.tagline {
  margin: 0;
  color: #add8e6; /* Light blue */
  font-style: italic; /* Italic text */
}

/* Titles for menu columns */
.footer-col h4 {
  margin-top: 0;
  margin-bottom: 1rem;
  font-weight: 600;
  color: #add8e6;
}

/* Menu lists */
.footer-col ul {
  list-style: none; /* Remove default bullets */
  padding: 0;
  margin: 0;
}

/* Menu items */
.footer-col li {
  margin-bottom: 0.6rem;
  color: #ccc;
  cursor: pointer;
  transition: color 0.2s; /* Transition effect for color changes */
}

.footer-col li:hover {
  color: white; /* Turn white on mouse hover */
  text-decoration: underline; /* Add underline */
}

/* Copyright info at the bottom of the footer */
.footer-bottom {
  margin-top: 2rem;
  text-align: center;
  color: #88aacc;
  font-size: 0.8rem;
}
</style>