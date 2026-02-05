<template>
  <div class="flex justify-around p-4 bg-gray-900">
    <button
        @click="lightStrike"
        :disabled="gameIsOver"
        class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded-lg disabled:opacity-50 disabled:cursor-not-allowed transition"
    >
      ⚔️ Attaque légère
    </button>

    <button
        @click="healPlayer"
        :disabled="gameIsOver"
        class="px-4 py-2 bg-green-500 hover:bg-green-600 text-white rounded-lg disabled:opacity-50 transition"
    >
      ✨ Se soigner
    </button>

    <button
        @click="heavyStrike"
        :disabled="gameIsOver"
        class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded-lg disabled:opacity-50 transition"
    >
      💥 Attaque lourde
    </button>
  </div>
</template>


<script>
  export default {
    name: "ActionButtons",
    methods: {
      lightStrike() {
        const dmg = Math.floor(Math.random() * 10) + 1;
        this.$emit("lightStrike", dmg);
      },
      heavyStrike() {
        const heavyDmg = Math.floor(Math.random() * 7) + 1;
        this.$emit("heavyStrike", (heavyDmg + 10));
      },
      healPlayer() {
        const healAmount = Math.floor(Math.random() * 10) + 1;
        this.$emit("healPlayer", healAmount);
      }
    },
    props: {
      gameIsOver: Boolean,
    }
  }
</script>

<style scoped>

</style>