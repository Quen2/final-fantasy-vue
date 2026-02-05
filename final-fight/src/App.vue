<template>
  <div class="w-screen h-screen flex flex-col justify-center items-center">
    <div class="flex flex-col w-3/4 h-3/4 bg-gray-400">
      <div class="flex justify-between p-4">
        <PlayerPannel :max-hp="playerHp" :hp="playerHp" :name="playerName" />
        <PlayerPannel :max-hp="bossHp" :hp="bossHp" :name="bossName" />
      </div>
      <ActionButtons />
      <StatusMessage :message="message" />
    </div>
  </div>
</template>

<script>
  import PlayerPannel from "@/Components/PlayerPannel.vue";
  import ActionButtons from "@/Components/ActionButtons.vue";
  import StatusMessage from "@/Components/StatusMessage.vue";

  export default {
    components: {
      PlayerPannel,
      ActionButtons,
      StatusMessage
    },
    data() {
      return {
        playerHp: 50,
        playerName: "Cloud",
        bossHp: 50,
        bossName: "Sephiroth"
      }
    },
    computed: {
      message() {
        return this.playerName + " va commencer."
      }
    }
  }
</script>

<style scoped></style>
