<template>
  <div class="w-screen h-screen flex justify-center items-center bg-linear-to-br from-black to-gray-900">
    <div class="flex flex-col w-4/5 max-w-4xl bg-gray-700 rounded-2xl shadow-2xl overflow-hidden">

      <!-- Zone combat -->
      <div class="flex justify-between p-6">
        <PlayerPannel
            :max-hp="50"
            :hp="playerHp"
            :name="playerName"
            :asset="playerAsset"
        />
        <PlayerPannel
            :max-hp="50"
            :hp="bossHp"
            :name="bossName"
            :asset="bossAsset"
        />
      </div>
      <!-- Actions -->
      <ActionButtons
          @lightStrike="lightStrike"
          @heavyStrike="heavyStrike"
          @healPlayer="healPlayer"
          :gameIsOver="gameIsOver"
      />
      <!-- Message -->
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
          if (this.bossHp <= 0) { this.bossHp = 0 }
          if (this.playerHp <= 0) { this.playerHp = 0 }
          this.gameIsOver = true;
          this.message = this.bossHp <= 0 ? this.playerName + " a gagné." : this.bossName + " a gagné.";
        }
      }
    }
  }
</script>

<style scoped></style>
