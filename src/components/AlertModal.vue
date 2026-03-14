<template>
  <!-- This is a global alert modal component -->
  <!-- We use v-if to determine whether to render this modal based on the value of isVisible -->
  <div v-if="isVisible" class="modal-overlay">
    <div class="modal-content">
      <!-- Red header of the modal -->
      <div class="modal-header">
        <span class="warning-icon">⚠</span>
        <h2>Danger Alert!</h2>
        <!-- When the close button is clicked, it triggers the 'close' event -->
        <button class="close-btn" @click="close">×</button>
      </div>
      <!-- Main body content of the modal -->
      <div class="modal-body">
        <p>UV level is VERY HIGH (9)! Your skin can burn in just 22 minutes. Take protective action NOW.</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // props are data received from the parent component (App.vue)
  // isVisible is a boolean value (true/false) used to control the display of the modal
  props: ['isVisible'],

  methods: {
    // This function is called when the user clicks the close button
    close() {
      // Emits an event named 'close' to notify the parent component to close the modal
      this.$emit('close');
    }
  }
}
</script>

<style scoped>
/* Gray semi-transparent background overlay for the modal */
.modal-overlay {
  position: fixed; /* Fixed positioning, covers the entire screen */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent black */
  display: flex;
  justify-content: center; /* Center horizontally */
  align-items: center;    /* Center vertically */
  z-index: 9999; /* Ensure it is on top of all content */
}

/* White container for the modal content */
.modal-content {
  background-color: white;
  border-radius: 8px;
  width: 90%; /* Width is 90% on small screens */
  max-width: 400px; /* Maximum width does not exceed 400px */
  overflow: hidden; /* Hide overflowing content (like rounded corners) */
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

/* Red header of the modal */
.modal-header {
  background-color: #DC3545; /* Red */
  color: white;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 10px;
}

.warning-icon {
  font-size: 1.5rem;
}

.modal-header h2 {
  flex-grow: 1; /* Allow the title to take up as much space as possible */
  margin: 0;
  font-size: 1.2rem;
}

.close-btn {
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

/* Main body part of the modal */
.modal-body {
  padding: 1.5rem;
  color: #333;
  font-size: 1rem;
  line-height: 1.5; /* Set line height to make text easier to read */
}
</style>
