<template>

  <div class="flex flex-col min-h-screen">

  <headerHome/>

  <main class="flex-grow flex items-center justify-center">
  <loginEChat/>
  
  </main>

  </div>
</template>

<script setup>
import loginEChat from './components/loginEChat.vue';
import headerHome from './components/headerHome.vue';

</script>