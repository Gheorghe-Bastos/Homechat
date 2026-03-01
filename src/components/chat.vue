<script setup>

import { db, auth } from '../service/firebase';
import { collection, addDoc, serverTimestamp, query, orderBy, onSnapshot, limitToLast } from 'firebase/firestore'
import { Timestamp } from 'firebase/firestore';

import login from './login.vue';
import buttonpadrao from './buttonpadrao.vue'
import { ref, inject, nextTick, onMounted, onUnmounted } from 'vue';

const { usuarioLogado, divChat } = inject('estadoChat');

const mensagem = ref('');
const mensagemArray = ref([]);
const chatContainer = ref(null);

let unsubscribe = null;

onMounted(() => {
    const q = query(
        collection(db, "mensagens"),
        orderBy("horario", "asc"),
        limitToLast(50)
    );

    unsubscribe = onSnapshot(q, (snapshot) => {
        mensagemArray.value = snapshot.docs.map(doc => ({
            id: doc.id,
            ...doc.data()
        }));

        nextTick(() => {
            if (chatContainer.value) {
                chatContainer.value.scrollTop = chatContainer.value.scrollHeight;
            }
        });
    });
});

onUnmounted(() => {
    if (unsubscribe) unsubscribe();
});

async function enviarMensagem() {
    if (!mensagem.value.trim()) return;

    await addDoc(collection(db, "mensagens"), {
        mensagem: mensagem.value,
        usuario: auth.currentUser?.email?.split('@')[0],
        horario: serverTimestamp(),
        uid: auth.currentUser?.uid || null
    });
    mensagem.value = '';

    await nextTick();

    if (chatContainer.value) {
        chatContainer.value.scrollTop = chatContainer.value.scrollHeight
    }
};

</script>

<template>
    <div v-if="divChat" class="flex flex-col-reverse 
    w-4xl min-h-full bg-neutral-900 border-1 border-2 border-[#ffffff4b] rounded-2xl">
        <div class="flex flex-col p-4 w-full">
            <div class="flex flex-col w-full ">
                <div ref="chatContainer" class="h-159 overflow-scroll flex flex-col pr-2">
                    <!--<div v-for="(mensagem, index) in msgDeTerceirosArray" :key="index" 
                    class="flex flex-col mb-2">
                        <div class="ml-1">
                            
                        </div>            
                    </div>-->
                    <div v-for="(mensagem, index) in mensagemArray" :key="mensagem.id"
                        class="flex flex-col self-end mb-2">
                        <div class="self-end mr-1">
                            {{ mensagem.usuario }}
                        </div>
                        <div class="bg-yellow-400 rounded-xl rounded-br-none text-black p-3 
                        w-fit min-w-16">
                            {{ mensagem.mensagem }}
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
</template>
