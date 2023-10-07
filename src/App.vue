<template>
  <div id="app">
    <PanelScores
      :playerLife="playerLife"
      :monsterLife="monsterLife"
    />
    <PanelResult
      :playerLife="playerLife"
      :monsterLife="monsterLife"
    />
    <PanelButtons
      :running="running"
      :gameOver="gameOver"
      @emit-startGame="startGame"
      @emit-attack="handleAttack"
      @emit-healAndHurt="healAndHurt"
    />
    <PanelLogs :logs="logs" />
  </div>
</template>

<script>
import PanelScores from "./components/PanelScores.vue";
import PanelResult from "./components/PanelResult.vue";
import PanelButtons from "./components/PanelButtons.vue";
import PanelLogs from "./components/PanelLogs.vue";

export default {
  name: "App",
  components: {
    PanelScores,
    PanelResult,
    PanelButtons,
    PanelLogs,
  },
  data() {
    return {
      playerLife: 100,
      monsterLife: 100,
      running: false,
      logs: [],
      gameOver: false,
    };
  },
  methods: {
    handleAttack(especial) {
      if (this.isGameOver()) return;

      this.monsterHurt(especial);
      this.playerHurt();
    },
    monsterHurt(especial) {
      const damage = this.getRandom(5 + (especial ? 5 : 0), 10 + (especial ? 5 : 0));
      this.monsterLife = Math.max(this.monsterLife - damage, 0);
      this.registerLog(`Player atingiu Monster com ${damage}.`, "player");

      if (this.monsterLife === 0) {
        this.endGame();
        return;
      }
    },
    playerHurt() {
      const damage = this.getRandom(7, 12);
      this.playerLife = Math.max(this.playerLife - damage, 0);
      this.registerLog(`Monster atingiu Player com ${damage}.`, "monster");

      if (this.playerLife === 0) {
        this.endGame();
        return;
      }
    },
    startGame() {
      this.gameOver = false;
      this.running = true;
      this.playerLife = 100;
      this.monsterLife = 100;
      this.logs = [];
    },
    healAndHurt() {
      if (this.isGameOver()) return;

      this.healPlayer();
      this.playerHurt();
    },
    healPlayer() {
      const heal = this.getRandom(10, 15);
      const newPlayerLife = Math.min(this.playerLife + heal, 100);
      const actualHeal = newPlayerLife - this.playerLife;
      this.playerLife = newPlayerLife;
      this.registerLog(`Player ganhou força de ${actualHeal}.`, "player");
    },
    getRandom(min, max) {
      const value = Math.random() * (max - min) + min;
      return Math.round(value);
    },
    registerLog(text, cls) {
      this.logs.unshift({ text, cls });
    },
    endGame() {
      this.running = false;
      this.gameOver = true;
    },
    isGameOver() {
      return this.playerLife <= 0 || this.monsterLife <= 0;
    },
  },
};
</script>

<style>
#app {
  font-family: "Montserrat", sans-serif;
  display: flex;
  flex-direction: column;
}

.panel {
  margin: 10px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
}
</style>
