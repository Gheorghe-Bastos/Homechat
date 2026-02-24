<template>
    <header>
        <div class="flex fixed w-full justify-center">
            <div class="bg-neutral-900 flex justify-center
                items-center w-full pt-4 gap-3 pl-20 pr-20 h-25 shadow-lg shadow-[#ffd5003e]">

                <div class="flex justify-between items-center">
                    <div>
                        <img src="../assets/faviconHomechat.png" class=" ml-4 h-20">
                    </div>

                    <div class="flex flex-col ml-2">
                        <h1 class="text-4xl text-neutral-200">HOMECHAT</h1>
                        <h1 class="text-neutral-200 text-lg">O Lar da Conversa</h1>
                    </div>

                </div>
                <div class="flex flex-col gap-0.5 mr-13">


                    <a href="https://github.com/Gheorghe-Bastos" target="blank" class="group relative h-6 w-6 flex">
                        <img src="../assets/github-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/github-amarelo.svg" class="absolute top-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">
                    </a>

                    <a href="https://www.linkedin.com/in/gheorghebastos" traget="blank" class="group relative h-6 w-6">

                        <img src="../assets/linkedin-logo-branco.svg"
                            class="transition-opacity duration-300 group-hover:opacity-0">
                        <img src="../assets/linkedin-logo-amarelo.svg" class="absolute top-0 transition-opacity duration-300 
                            opacity-0 group-hover:opacity-100 group-hover:drop-shadow-[0_0_5px_#ffd500]">

                    </a>

                    <a href="mailto:gheorghe.bastos.ofc@gmail.com" target="blank" class="group relative h-6 w-6">
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

import login from './login.vue';

</script>