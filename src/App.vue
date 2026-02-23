<template>

  <div class="">

  <headerHome/>

  <main class="flex items-center justify-center h-screen">
  <chat v-if="divChat"/>
  <loginEChat v-else/>
  </main>

  </div>
</template>

<script setup>

import { ref, provide } from 'vue';

import loginEChat from './components/loginEChat.vue';
import headerHome from './components/headerHome.vue';
import chat from './components/chat.vue';

const usuarioLogado = ref('');
const usuariosArray = ref([]);
const divChat = ref(false);

provide('estadoChat', {
usuarioLogado,
usuariosArray,
divChat

})

</script>