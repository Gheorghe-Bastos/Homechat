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

                <div v-else class="flex flex-col gap-0.5">
                    
                        <a href="https://github.com/Gheorghe-Bastos" class="transition-all duration-250 hover:text-yellow-400"><img src="../assets/github-branco.svg"></a>
                        <a href="www.linkedin.com/in/gheorghebastos" class="transition-all duration-300 hover:text-yellow-400 flex justify-between gap-1 mr-2" ><img src="../assets/linkedin-logo-branco.svg"></a>
                        <a href="gheorghe.bastos.ofc@gmail.com" class="transition-all duration-300 hover:text-yellow-400 "><img src="../assets/contato-branco.svg"></a>
                    
                </div>

            </div>
        </div>
    </header>
</template>

<script setup>

import loginEChat from './loginEChat.vue';

</script>