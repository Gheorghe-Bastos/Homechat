<template>
    <header>
        <div class="flex justify-center">
            <div class="bg-neutral-900 flex justify-between  shadow-[0px_10px_20px_#ffd50083]
                items-center mt-4 mr-4 ml-4 w-full h-22 rounded-lg">
                <div class="flex flex-col ml-2">
                    <h1 class="text-4xl text-neutral-200">HOMECHAT</h1>
                    <h1 class="text-neutral-200 text-lg">O Lar da Conversa</h1>
                </div>

                <div v-if="divChatAtivado">

                </div>

                <div v-else class="flex flex-col gap-0.5 mr-2">


                    <a href="https://github.com/Gheorghe-Bastos" class="group relative h-6 w-6">

                        <img src="../assets/github-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/github-amarelo.svg" class="absolute top-0 let-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">
                    </a>

                    <a href="www.linkedin.com/in/gheorghebastos" class="group relative h-6 w-6">

                        <img src="../assets/linkedin-logo-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/linkedin-logo-amarelo.svg" class="absolute top-0 let-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">

                    </a>

                    <a href="gheorghe.bastos.ofc@gmail.com" class="group relative h-6 w-6">
                        <img src="../assets/contato-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/contato-amarelo.svg" class="absolute top-0 let-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">
                    </a>

                </div>

            </div>
        </div>
    </header>
</template>

<script setup>

import loginEChat from './loginEChat.vue';

</script>