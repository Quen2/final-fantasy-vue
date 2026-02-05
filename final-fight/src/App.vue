<template>
  <div class="w-screen h-screen bg-black flex flex-col justify-center items-center">
    <div class="flex flex-col w-3/4 h-3/4 bg-gray-600">
      <div class="flex justify-between p-4">
        <PlayerPannel max-hp="50" hp="50" name="Quentin" />
        <PlayerPannel max-hp="60" hp="60" name="LARRY" />
      </div>
    </div>
  </div>
</template>

<script>
  import PlayerPannel from "@/Components/PlayerPannel.vue";
  export default {
    components: {
      PlayerPannel,
    }
  }
</script>

<style scoped></style>
