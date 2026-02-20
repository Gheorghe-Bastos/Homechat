<script setup>

import { ref } from 'vue';
import { nextTick } from 'vue';
import buttonpadrao from './buttonpadrao.vue';

const msgDeTerceirosArray = ref([]);
const mensagemArray = ref([]);
const usuarioLogado = ref([]);
const chatContainer = ref('');

const userName = ref('');
const password = ref('');
const alertaErro = ref('');
const divChat = ref(false);
const mensagem = ref('');
const usuarios = ref([
    {
        nome: 'gheorghe',
        senha: 'gheorghe2006',
        mensagens: mensagemArray,
        msgTerceiros: msgDeTerceirosArray
    },

    {
        mone: 'mathias',
        senha: 'eusougay123',
        mensagens: mensagemArray,
        msgTerceiros: msgDeTerceirosArray
    }
]);

function buscar(nomeBusca) {

    for (const u of usuarios.value) {
        if (u.nome == nomeBusca) {
            return u
        }
    }
    return null;
}

function verificar() {
    alertaErro.value = '';

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
        usuarios.value.push({
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

async function enviarMensagem() {
    if (mensagem.value.trim() === '') {
        return null
    }
    else {
        mensagemArray.value.push(
            mensagem.value
        )
        mensagem.value = '';
    };

    await nextTick();

    if (chatContainer.value) {
        chatContainer.value.scrollTop = chatContainer.value.scrollHeight
    }
};

</script>

<template>
    <div v-if="divChat" class="flex flex-col-reverse w-4xl min-h-full bg-neutral-900 rounded-2xl">
        <div class="flex flex-col p-4 w-full">
            <div class="flex flex-col w-full ">
                <div ref="chatContainer" class="h-159 overflow-scroll flex flex-col pr-2">
                    <!--<div v-for="(mensagem, index) in msgDeTerceirosArray" :key="index" 
                    class="flex flex-col mb-2">
                        <div class="ml-1">
                            
                        </div>            
                    </div>-->
                    <div v-for="(mensagem, index) in mensagemArray" :key="index" class="flex flex-col self-end mb-2">
                        <div class="self-end mr-1">
                            {{ usuarioLogado }}
                        </div>
                        <div class="bg-yellow-400 rounded-xl rounded-br-none text-black p-3 
                        w-fit min-w-16">
                            {{ mensagem }}
                        </div>
                    </div>
                </div>
                <form @submit.prevent="enviarMensagem" class="bg-neutral-800 flex items-stretch w-full rounded-md">
                    <div class="flex w-full h-full rounded-md  focus:outline.none justify-between ">
                        <input id="mensagem" class="focus:outline-none focus:ring-0 focus:border 
                        focus:border-yellow-400 transition duration-300 focus:shadow-[0px_0px_20px_#ffd500] 
                        border border-[#0000] pl-4 pr-4 font-extralight
                        w-full h-12 text-neutral-200 rounded-l-md" placeholder="Digite o que quiser!"
                        v-model=mensagem></input>

                        <buttonpadrao :acao-button="enviarMensagem" texto-button="Enviar"
                        class="w-23 h-12 rounded-r-md rounded-l-none" />
                    </div>
                </form>
            </div>
        </div>
    </div>
    <div v-else class="mb-12">
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
