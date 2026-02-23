<script setup>

import { ref, inject } from 'vue';
import buttonpadrao from './buttonpadrao.vue';

const { divChat, usuarioLogado, usuariosArray } = inject('estadoChat');

const userName = ref('');
const password = ref('');
const alertaErro = ref('');

function buscar(nomeBusca) {

    for (const u of usuariosArray.value) {
        if (u.nome == nomeBusca) {
            return u
        }
    }
    return null;
}

function verificar() {

    const nomeInput = userName.value.trim();
    const senhaInput = password.value.trim();

    if (nomeInput === '') {

        alertaErro.value = 'Usuário é obrigatório.'
        return;
    }
    if (senhaInput === '') {

        alertaErro.value = 'Senha é obrigatória.'
        return;
    }

    const usuarioExiste = buscar(nomeInput);

    if (!usuarioExiste && senhaInput !== '') {
        usuariosArray.value.push({
            nome: nomeInput,
            senha: senhaInput
        });
        
        entrarNoChat(nomeInput);
    }

    else {
        if (usuarioExiste.senha === senhaInput) {

            entrarNoChat(nomeInput);
        }
        else {
            alertaErro.value = 'Senha incorreta para este usuário!';
        }
    }
}
function entrarNoChat(nome) {
    usuarioLogado.value = nome;
    userName.value = '';
    password.value = '';
    divChat.value = true;
    alertaErro.value = '';
}

</script>

<template>
    <div class="mb-12">
        <div class="flex flex-col justify-center items-center gap-5 mt-14 w-4xl">

            <h1 class="text-6xl">HOMECHAT | O Lar da Conversa</h1>

            <div class="bg-neutral-900 flex flex-col justify-center items-center mt-10 w-2xl 
            p-8 rounded-2xl shadow-[0px_0px_20px_#ffd500]">
                <h2 class="text-3xl mt-5">Login</h2>
                <h3 class="text-neutral-400 text-lg mb-3">Digite o seu nome de usuario e sua senha
                </h3>
                <form @submit.prevent="verificar" class="flex flex-col items-center w-lg">

                    <div id="preencherUsuario" class="mb-2 mt-2 w-full">
                        <label for="userName" class="text-neutral-400 text-sm">Usuário:</label>
                        <input id="userName" class="p-1 focus:outline-none focus:ring-0 focus:border-1
                        focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                        bg-neutral-800 w-full text-neutral-200 rounded-sm" placeholder="Digite seu usuário"
                            v-model="userName"></input>
                    </div>
                    <div id="preencherSenha" class="mb-2 mt-2 w-full">
                        <label for="password" class="text-neutral-400 text-sm">Senha:</label>
                        <input id="password" type="password" class="p-1 focus:outline-none focus:ring-0 focus:border-1
                        focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                        bg-neutral-800 w-full text-neutral-200 rounded-sm" placeholder="Digite sua senha"
                        v-model="password"></input>
                    </div>
                    <p v-if="alertaErro" class="text-sm text-red-700 m-1.5">{{ alertaErro }}</p>

                    <buttonpadrao :acao-button="verificar" texto-button="Entrar" class="w-full mt-4 mb-6" />

                    <div class="flex w-full justify-center text-sm h-1 text-neutral-300">
                        <p>Powered by SALO - Hometech - © 2026</p>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
