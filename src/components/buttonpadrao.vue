<template>

    <button @click="acaoButton" class="bg-yellow-400 text-black p-2 border-1 border-yellow-400 rounded transition duration-300
        hover:shadow-[0px_0px_15px_#ffd500] hover:text-black">
        {{ textoButton }}
      </button>

</template>

<script setup>

defineProps({
  textoButton: {
    type: String,
    default: "Clique aqui"
  },
  acaoButton: {
    type: Function,
    default: () => {}
  }
})

</script>