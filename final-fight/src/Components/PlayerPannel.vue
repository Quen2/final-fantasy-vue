<template>
  <div class="flex flex-col">
    <p>{{ name }}</p>
    <div class="flex">
      {{ hp }} / {{ maxHp }} hp
    </div>
  </div>
</template>

<script>
  export default {
    name: 'PlayerPannel',
    props: {
      name: {
        type: String,
        required: true
      },
      hp: {
        type: Number,
        required: true
      },
      maxHp: {
        type: Number,
        required: true
      }
    }
  }
</script>

<style scoped>

</style>