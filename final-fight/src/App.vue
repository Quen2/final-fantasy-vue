<template>
  <div class="w-screen h-screen flex flex-col justify-center items-center">
    <div class="flex flex-col w-3/4 h-3/4 bg-gray-400">
      <div class="flex justify-between p-4">
        <PlayerPannel
            :max-hp="playerHp"
            :hp="playerHp"
            :name="playerName"
            :asset="playerAsset"
        />
        <PlayerPannel
            :max-hp="bossHp"
            :hp="bossHp"
            :name="bossName"
            :asset="bossAsset"
        />
      </div>
      <ActionButtons
          @lightStrike="lightStrike"
          @heavyStrike="heavyStrike"
          @healPlayer="healPlayer"
          :gameIsOver="gameIsOver"
      />
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
        playerAsset: "spritecloud.png",
        bossHp: 50,
        bossName: "Sephiroth",
        bossAsset: "spriteSephiroth.webp",
        message: "Cloud va commencer.",
        gameIsOver: false
      }
    },
    methods: {
      lightStrike(dmg) {
        this.bossHp -= dmg;
        this.message = this.playerName + " a frappé " + this.bossName + " pour " + dmg + " dégats.";
        this.checkGameState()
        this.enemyTurn()
      },
      heavyStrike(dmg) {
        this.bossHp -= dmg;
        this.message = this.playerName + " a frappé " + this.bossName + " pour " + dmg + " dégats.";
        this.checkGameState()
        this.enemyTurn()
      },
      healPlayer(amount) {
        this.playerHp += amount;
        this.message = this.playerName + " a récupéré " + amount + " pv.";
        this.checkGameState()
        this.enemyTurn()
      },
      enemyTurn() {
        const dmg = Math.floor(Math.random() * 15) + 1;
        this.message += "\n" + this.bossName + " a frappé " + this.playerName + " pour " + dmg + " dégats.";
        this.playerHp -= dmg;
        this.checkGameState()
      },
      checkGameState() {
        if (this.bossHp <= 0 || this.playerHp <= 0) {
          this.gameIsOver = true;
          this.message = this.bossHp <= 0 ? this.playerName + " a gagné." : this.bossName + " a gagné.";
        }
      }
    }
  }
</script>

<style scoped></style>
