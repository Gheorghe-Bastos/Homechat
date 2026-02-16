<template>

    <div class="flex justify-center m-12 w-4xl h-full">
        <div v-if="divChat" class="flex flex-col justify-center m-6 h-full w-full">
            <div class="bg-neutral-800 flex justify-between p-2 w-full">
                <h1>oi</h1>
                <button class="text-2xl" href=""></button>
            </div>
        </div>
        <div v-else class="bg-neutral-900 flex flex-col justify-center items-center m-0 w-2xl 
        p-8 rounded-2xl shadow-[0px_0px_20px_#ffd500]">
            <h2 class="text-3xl mt-5">Login</h2>
            <h3 class="text-neutral-400 text-lg mb-3">Digite o seu nome de usuario e sua senha
            </h3>
            <form @submit.prevent="verificar" class="flex flex-col items-center w-lg">

                <div id="preencherUsuario" class="mb-2 mt-2 w-full">
                    <label for="userName" class="text-neutral-400 text-sm">Usuário:</label>
                    <input id="userName" class="focus:outline-none focus:ring-0 focus:border-1 focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                    bg-neutral-800 w-full text-neutral-200 rounded-sm"  placeholder="Digite seu usuário" v-model="userName"></input>
                </div>
                <div id="preencherSenha" class="mb-2 mt-2 w-full">
                    <label for="password" class="text-neutral-400 text-sm">Senha:</label>
                    <input id="password" type="password" class="focus:outline-none focus:ring-0 focus:border-1 focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                    bg-neutral-800 w-full text-neutral-200 rounded-sm" placeholder="Digite sua senha" v-model="password"></input>
                </div>
                <p v-if="senhaErro" class="text-sm text-red-700 absolute">{{ senhaErro }}</p>

                <buttonpadrao :acao-button="verificar" texto-button="Entrar" class="w-full mt-4 mb-6"/>

                
                <div class="flex w-full justify-center text-sm h-1 text-neutral-300">
                    <p>Powered by SALO - Hometech - © 2026</p>
                </div>
            </form>
        </div>
    </div>

</template>

<script setup>

import { ref } from 'vue';
import buttonpadrao from './buttonpadrao.vue';


const usuario = ref({
     nome: '', 
     senha: '' 
})


const userName = ref('');
const password = ref('');
const senhaErro = ref('');
const divChat = ref(false);

function verificar() {

    if(userName.value.trim() !== '' && password.value.trim() !== '') {
        senhaErro.value = '';

        usuario.value = {
            nome: userName.value,
            senha: password.value
        };
        
        divChat.value = true;

        console.log(usuario.value);
    }
    else {
        senhaErro.value = "Usuario e/ou senha incorretos!";
        divChat.value = false;
        userName.value = '';
        password.value = '';
        return;
    }
}

</script>