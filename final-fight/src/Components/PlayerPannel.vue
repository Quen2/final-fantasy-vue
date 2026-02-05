<template>
  <div class="flex flex-col items-center bg-gray-800 text-white p-4 rounded-xl w-1/3 shadow-lg">
    <p class="text-xl font-bold mb-2">{{ name }}</p>

    <!-- Barre de vie -->
    <div class="w-full bg-gray-600 rounded-full h-4 mb-2 overflow-hidden">
      <div
          class="h-full bg-green-500 transition-all duration-300"
          :style="{ width: (hp / maxHp) * 100 + '%' }"
      ></div>
    </div>

    <p class="text-sm mb-2">{{ hp }} / {{ maxHp }} HP</p>

    <img
        :src="'../../public/assets/' + asset"
        :alt="name"
        class="w-32 h-32 object-contain"
    />
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