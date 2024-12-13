<template>
    <button
      class="moon-button p-4 sm:p-5 bg-[#240345] rounded-full shadow-lg text-3xl sm:text-4xl text-white hover:scale-110 focus:outline-none transition-all"
      @click="generateQuote"
    >
      Generate Quote
    </button>
  </template>
  
  
  <script>
  export default {
    methods: {
      generateQuote() {
        this.$emit('quote-generated'); 
      },
    },
  };
  </script>
  
  <style scoped>
  .moon-button {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .moon-button:hover {
    transform: scale(1.1);
    box-shadow: 0 0 30px rgba(255, 255, 255, 0.6);
  }
  
  .moon-button:active {
    transform: scale(0.95);
  }
  </style>
  