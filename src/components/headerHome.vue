<template>
    <header>
        <div class="flex fixed w-full justify-center">
            <div class="bg-neutral-900 flex justify-center
                items-center w-full pt-4 gap-3 pl-20 pr-20 h-25 shadow-lg shadow-[#ffd5003e]">

                <div class="flex justify-between items-center">

                    <button v-if="divChat === true" @click="voltar">
                        <Icon icon="tabler:arrow-back-up"
                            class="trasition duration-300 w-6 h-6 hover:drop-shadow-[0_0_5px_#ffd500]" />
                    </button>

                    <img src="../assets/faviconHomechat.png" class=" ml-4 h-20">

                    <div class="flex flex-col ml-2">
                        <h1 class="text-2xl sm:text-4xl text-neutral-200">HOMECHAT</h1>
                        <h1 class="text-neutral-200 text-sm sm:text-lg">O Lar da Conversa</h1>
                    </div>

                </div>
                <div class="flex flex-col gap-0.5 mr-13">


                    <a href="https://github.com/Gheorghe-Bastos" target="blank"
                        class="group relative xs:h-5 xs:w-5 sm:h-6 sm:w-6 flex">
                        <img src="../assets/github-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/github-amarelo.svg" class="absolute top-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">
                    </a>

                    <a href="https://www.linkedin.com/in/gheorghebastos" traget="blank"
                        class="group relative h-5 w-5 sm:h-6 sm:w-6">

                        <img src="../assets/linkedin-logo-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/linkedin-logo-amarelo.svg" class="absolute top-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">

                    </a>

                    <a href="mailto:gheorghe.bastos.ofc@gmail.com" target="blank"
                        class="group relative h-5 w-5 sm:h-6 sm:w-6">
                        <img src="../assets/contato-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/contato-amarelo.svg" class="absolute top-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">
                    </a>

                </div>

            </div>
        </div>
    </header>
</template>

<script setup>

import { Icon } from '@iconify/vue';
import { inject } from 'vue';

const { divChat } = inject('estadoChat');

function voltar() {
    divChat.value = false;
}

</script>