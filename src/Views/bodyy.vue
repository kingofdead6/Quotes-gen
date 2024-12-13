<template>
    <div class="app">
  <!-- Starry Background -->
  <canvas ref="starCanvas" class="absolute inset-0"></canvas>

  <!-- Content Area -->
  <div class="relative z-10 text-white text-center p-4 sm:p-8">
    <h1 class="text-3xl sm:text-5xl font-bold mb-4">Welcome to the Quotes Generator</h1>
    <p class="text-sm sm:text-lg">
      Discover inspirational quotes and let the stars guide your thoughts.
    </p>
    <!-- Moon Button -->
    <moonButton @quote-generated="generateQuote" />

    <!-- Display Generated Quote -->
    <div v-if="currentQuote" class="text-xl font-semibold mt-6 max-w-lg sm:max-w-xl mx-auto bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 p-6 rounded-xl shadow-xl transform transition-all hover:scale-105 hover:shadow-2xl">
      <p class="text-white text-center text-lg sm:text-2xl mb-4 italic">"{{ currentQuote.content }}"</p>
      <p class="text-white text-center text-sm sm:text-lg">— {{ currentQuote.author }}</p>
    </div>
  </div>
</div>

  </template>
  
  <script>
  import moonButton from '../components/MoonButton.vue';
  import { quotes } from '../components/quotes'; 
  
  export default {
    components: {
      moonButton,
    },
    data() {
      return {
        currentQuote: null,
        quotes: quotes, 
      };
    },
    methods: {
      generateQuote() {
        const randomIndex = Math.floor(Math.random() * this.quotes.length);
        this.currentQuote = this.quotes[randomIndex];
      },
      initStars() {
        const canvas = this.$refs.starCanvas;
        const ctx = canvas.getContext("2d");
  
        // Resize canvas to full viewport
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
  
        const stars = [];
        const maxStars = 150;
  
        // Mouse position
        const mouse = { x: 0, y: 0 };
  
        // Create star objects
        function createStar() {
          return {
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            radius: Math.random() * 2,
            speedX: (Math.random() - 0.5) * 0.2,
            speedY: (Math.random() - 0.5) * 0.2,
            twinkle: Math.random() * 0.5 + 0.5,
          };
        }
  
        // Initialize stars
        for (let i = 0; i < maxStars; i++) {
          stars.push(createStar());
        }
  
        // Draw stars
        function drawStars() {
          ctx.clearRect(0, 0, canvas.width, canvas.height);
  
          ctx.fillStyle = "white";
          stars.forEach((star) => {
            ctx.beginPath();
            ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
            ctx.globalAlpha = star.twinkle;
            ctx.fill();
          });
        }
  
        // Update stars' positions
        function updateStars() {
          stars.forEach((star) => {
            star.x += star.speedX + (mouse.x / canvas.width - 0.5) * 5;
            star.y += star.speedY + (mouse.y / canvas.height - 0.5) * 5;
  
            // Wrap around edges
            if (star.x < 0) star.x = canvas.width;
            if (star.x > canvas.width) star.x = 0;
            if (star.y < 0) star.y = canvas.height;
            if (star.y > canvas.height) star.y = 0;
  
            // Twinkle effect
            star.twinkle = 0.5 + Math.random() * 0.5;
          });
        }
  
        // Animate stars
        function animateStars() {
          updateStars();
          drawStars();
          requestAnimationFrame(animateStars);
        }
  
        // Mouse movement
        canvas.addEventListener("mousemove", (e) => {
          mouse.x = e.clientX;
          mouse.y = e.clientY;
        });
  
        // Start animation
        animateStars();
  
        // Resize canvas on window resize
        window.addEventListener("resize", () => {
          canvas.width = window.innerWidth;
          canvas.height = window.innerHeight;
        });
      },
    },
    mounted() {
      this.initStars();
    },
  };
  </script>
  
  <style>
  body {
    margin: 0;
    background: linear-gradient(to bottom, #0a0b1d, #000);
    overflow: hidden;
    font-family: "Arial", sans-serif;
  }
  
  canvas {
    display: block;
    position: fixed;
    top: 0;
    left: 0;
  }
  
  .app {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    text-align: center;
  }
  </style>
  