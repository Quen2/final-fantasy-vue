<template>
  <div class="w-screen h-screen flex justify-center items-center bg-linear-to-br from-black to-gray-900">
    <div class="flex flex-col w-4/5 max-w-4xl bg-gray-700 rounded-2xl shadow-2xl overflow-hidden">

      <div class="flex justify-between p-6">
        <PlayerPannel
            :max-hp="50"
            :hp="playerHp"
            :name="playerName"
            :asset="playerAsset"
        />
        <div v-if="winAmount !== 0 || loseAmount !== 0">
          <p>{{ winAmount }} w / {{ loseAmount }} d </p>
        </div>
        <PlayerPannel
            :max-hp="50"
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
      <div v-if="gameIsOver" class="flex justify-center p-2">
        <RestartButton
            @restartGame="restartGame"
        />
      </div>
    </div>
  </div>
</template>


<script>
  import PlayerPannel from "@/Components/PlayerPannel.vue";
  import ActionButtons from "@/Components/ActionButtons.vue";
  import StatusMessage from "@/Components/StatusMessage.vue";
  import RestartButton from "@/Components/RestartButton.vue";

  export default {
    components: {
      PlayerPannel,
      ActionButtons,
      StatusMessage,
      RestartButton,
    },
    data() {
      return {
        playerHp: 50,
        playerMaxHp:50,
        playerName: "Cloud",
        playerAsset: "spritecloud.png",
        bossHp: 50,
        bossMaxHp: 50,
        bossName: "Sephiroth",
        bossAsset: "spriteSephiroth.webp",
        message: "Cloud va commencer.",
        gameIsOver: false,
        winAmount: 0,
        loseAmount: 0
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
        if (this.gameIsOver) return;
        if (this.bossHp <= 0 || this.playerHp <= 0) {
          if (this.bossHp <= 0) { this.bossHp = 0; this.winAmount++; }
          if (this.playerHp <= 0) { this.playerHp = 0; this.loseAmount++; }
          this.gameIsOver = true;
          this.message = this.bossHp <= 0 ? this.playerName + " a gagné." : this.bossName + " a gagné.";

        }
      },
      restartGame() {
        this.gameIsOver = false;
        this.message = "Cloud va commencer.";
        this.bossHp = this.bossMaxHp;
        this.playerHp = this.playerMaxHp;
      }
    }
  }
</script>

<style scoped></style>
