<template>
  <div class="relative overflow-hidden">
    <!-- Animated Stars -->
    

    <!-- Main Navigation -->
    <nav class="relative z-10 bg-[#000000] text-white p-4 flex justify-between items-center font-inkut">
      <div class="absolute inset-0 stars"></div>
      <!-- Logo/Title -->
      <h1 class="text-2xl font-bold ml-4">
        <slot name="logo">Quotes Generator</slot>
      </h1>
   
    </nav>
  </div>
</template>


<style scoped>

/* Stars Background */
.stars {
  width: 1000%;
  height: 100%;
  background: radial-gradient(white 1px, transparent 1px),
              radial-gradient(white 1px, transparent 1px),
              radial-gradient(white 1px, transparent 1px);
  background-size: 50px 50px, 75px 75px;
  background-position: 0 0, 15px 15px;
  animation: stars-move 100s linear infinite;
  opacity: 0.5;
  pointer-events: none;
}

/* Animation for Stars */
@keyframes stars-move {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>
