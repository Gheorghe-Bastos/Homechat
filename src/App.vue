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
import { ref, provide, onMounted } from 'vue';
import { onAuthStateChanged } from 'firebase/auth';

import login from './components/login.vue';
import headerHome from './components/headerHome.vue';
import chat from './components/chat.vue';

const usuarioLogado = ref('');
const usuariosArray = ref([]);
const divChat = ref(false);

onMounted(() => {
  onAuthStateChanged(auth, (user) => {
    if (user) {
      usuarioLogado.value = user.email.split('@')[0];
      divChat.value = true;
    } else {
      usuarioLogado.value = '';
      divChat.value = false;
    }
  });
});

provide('estadoChat', {
usuarioLogado,
usuariosArray,
divChat

})

</script>