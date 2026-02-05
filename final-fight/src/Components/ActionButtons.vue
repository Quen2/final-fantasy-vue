<template>
  <div class="flex justify-between p-4">
    <div>
      <button @click="lightStrike" :disabled="gameIsOver">Attaque légère</button>
    </div>
    <div>
      <button @click="healPlayer" :disabled="gameIsOver">Se soigner</button>
    </div>
    <div>
      <button @click="heavyStrike" :disabled="gameIsOver">Attaque lourde</button>
    </div>
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