<template>
  <div class="flex flex-col text-center">
    <p>{{ name }}</p>
    <p class="text-center"> {{ hp }} / {{ maxHp }} hp </p>
    <img :src="'../../public/assets/' + asset" :alt="name"
    class="w-1/2"/>
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
      },
      asset: {
        type: String,
        required: true
      }
    }
  }
</script>

<style scoped>

</style>