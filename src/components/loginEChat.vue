<template>

    <div v-if="divChat" class="flex justify-center m-12 w-4xl">
        <div class="flex flex-col m-6 h-full w-full">
            <div class="flex flex-col justify-between">
                <div v-for="(mensagem, index) in mensagemArray"
                :key="index" class="bg-yellow-400 rounded-xl text-black p-3 m-2
                 w-fit max-w">
                    {{ mensagem }}
                </div>
                <form @submit.prevent="enviarMensagem" class="bg-neutral-900 flex items-stretch w-full p-[1px] rounded-md">
                    <div class="flex w-full h-full rounded-md  focus:outline.none justify-between ">
                        <input id="mensagem" class="focus:outline-none focus:ring-0 focus:border-1 
                             focus:border-yellow-400 transition duration-300 focus:shadow-[0px_0px_20px_#ffd500] 
                             border-1 border-[#0000] pl-4 pr-4 font-extralight
                            w-full h-12 text-neutral-200 rounded-l-md" 
                            placeholder="Digite o que quiser!" v-model=mensagem></input>

                        <buttonpadrao :acao-button="enviarMensagem" texto-button="Enviar"
                            class="w-23 h-12 rounded-r-md rounded-l-[0px]" />
                    </div>
                </form>
            </div>
        </div>
    </div>
    <div v-else class="mb-12">
        <div class="flex flex-col justify-center items-center gap-5 mt-0 m-12 w-4xl">
            
            <h1 class="text-6xl">HOMECHAT | O Lar da Conversa</h1>
            
            <div class="bg-neutral-900 flex flex-col justify-center items-center mt-10 w-2xl 
            p-8 rounded-2xl shadow-[0px_0px_20px_#ffd500]">
                <h2 class="text-3xl mt-5">Login</h2>
                <h3 class="text-neutral-400 text-lg mb-3">Digite o seu nome de usuario e sua senha
                </h3>
                <form @submit.prevent="verificar" class="flex flex-col items-center w-lg">

                    <div id="preencherUsuario" class="mb-2 mt-2 w-full">
                        <label for="userName" class="text-neutral-400 text-sm">Usuário:</label>
                        <input id="userName" class="focus:outline-none focus:ring-0 focus:border-1
                        focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                        bg-neutral-800 w-full text-neutral-200 rounded-sm" placeholder="Digite seu usuário"
                            v-model="userName"></input>
                    </div>
                    <div id="preencherSenha" class="mb-2 mt-2 w-full">
                        <label for="password" class="text-neutral-400 text-sm">Senha:</label>
                        <input id="password" type="password" class="focus:outline-none focus:ring-0 focus:border-1
                        focus:border-yellow-400 border-1 border-[#0000] pl-1 pr-1 font-extralight
                        bg-neutral-800 w-full text-neutral-200 rounded-sm" placeholder="Digite sua senha"
                            v-model="password"></input>
                    </div>
                    <p v-if="alertaErro" class="text-sm text-red-700 fixed">{{ alertaErro }}</p>

                    <buttonpadrao :acao-button="verificar" texto-button="Entrar" class="w-full mt-4 mb-6" />

                    <div class="flex w-full justify-center text-sm h-1 text-neutral-300">
                        <p>Powered by SALO - Hometech - © 2026</p>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue';
import buttonpadrao from './buttonpadrao.vue'; 

const usuarios = ref([
    {
        nome: 'gheorghe',
        senha: 'gheorghe2006'
    }
]);
const mensagemArray = ref([]);
const usuarioLogado = ref([]);

const userName = ref('');
const password = ref('');
const alertaErro = ref('');
const divChat = ref(false);
const mensagem = ref('');

function buscar(nomeBusca) {
    
    for (const u of usuarios.value) {        
        if (u.nome == nomeBusca) {
            return u
        } 
    } 
    return null;
}

function verificar() {
    const nomeInput = userName.value.trim();
    const senhaInput = password.value.trim();

    if (nomeInput === '' || senhaInput === '')  {

        alertaErro.value = 'Preencha todos os campos'
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
            password.value = '';
            alertaErro.value = 'Senha incorreta para este usuário!';
        }
    }
}
function entrarNoChat(nome) {
    usuarioLogado.value = nome;
    userName.value = '';
    password.value = ''; 
    divChat.value = true;
    alertaErro.value ='';
}

function enviarMensagem() {
    if (mensagem.value.trim() === '') {
        return null
    }
    else {
    mensagemArray.value.push(
        mensagem.value
    )};
    mensagem.value = '';
};

</script>