<template>

  <div class="">

  <headerHome/>

  <main class="flex items-center justify-center h-screen">
  <chat v-if="divChat"/>
  <login v-else/>
  </main>

  </div>
</template>

<script setup>

import { auth } from './service/firebase';
import { ref, provide } from 'vue';

import login from './components/login.vue';
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