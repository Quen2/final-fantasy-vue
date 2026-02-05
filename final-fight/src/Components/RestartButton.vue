<template>
  <button @click="restartGame"
          class="px-4 py-2 bg-gray-800 hover:bg-gray-900 text-white rounded-lg disabled:opacity-50 transition"
  >
    Rejouer
  </button>
</template>

<script>
  export default {
    name: 'RestartButton',
    methods: {
      restartGame() {
        this.$emit('restartGame')
      }
    }
  }
</script>

<style scoped>

</style>