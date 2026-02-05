<template>
  <div class="text-center text-xl">
    <p class="whitespace-pre">{{ message }}</p>
  </div>
</template>

<script>
  export default {
    name: "StatusMessage",
    props: {
      message: {
        type: String,
        required: true,
      }
    },
  }
</script>

<style scoped>

</style>