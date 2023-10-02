<template>
  <div id="app">
    <PanelScores :playerLife="playerLife" :monsterLife="monsterLife" />
    <PanelResult :playerLife="playerLife" :monsterLife="monsterLife" :running="running" />
    <PanelButtons :running="running" @emit-startGame="startGame" @emit-attack="attack" @emit-healAndHurt="healAndHurt" />
    <PanelLogs :logs="logs" />
  </div>
</template>

<script>
import PanelScores from './components/PanelScores.vue';
import PanelResult from './components/PanelResult.vue';
import PanelButtons from './components/PanelButtons.vue';
import PanelLogs from './components/PanelLogs.vue';

export default {
  name: 'App',
  components: {
    PanelScores,
    PanelResult,
    PanelButtons,
    PanelLogs
  },
  data() {
    return {
      playerLife: 100,
      monsterLife: 100,
      running: false,
      logs: []
    }
  },
  computed: {
    hasResult() {
      return this.playerLife == 0 || this.monsterLife == 0
    }
  },
  methods: {
    startGame() {
      this.running = true;
      this.playerLife = 100;
      this.monsterLife = 100;
      this.logs = []
    },
    
    healAndHurt() {
      this.heal(10, 15)
      this.hurt('playerLife', 7, 12, false, 'Monster', 'Player', 'monster')
    },
    quitGame() {
      this.running = false;
    },
    hurt(prop, min, max, especial, source, target, cls) {
      const plus = especial ? 5 : 0
      const hurt = this.getRandom(min + plus, max + plus)
      this[prop] = Math.max(this[prop] - hurt, 0)
      this.registerLog(`${source} atingiu ${target} com ${hurt}.`, cls)
    },
    heal(min, max) {
      const heal = this.getRandom(min, max)
      this.playerLife = Math.min(this.playerLife + heal, 100)
      this.registerLog(`Jogador ganhou força de ${heal}.`, 'player')
    },
    getRandom(min, max) {
      const value = Math.random() * (max - min) + min
      return Math.round(value)
    },
    registerLog(text, cls) {
      this.logs.unshift({ text, cls })
    }
  },
  watch: {
    hasResult(value) {
      if(value) this.running = false
    }
  }
}
</script>

<style>
#app {
    font-family: 'Montserrat', sans-serif;
    display: flex;
    flex-direction: column;
}

.panel {
    margin: 10px;
    padding: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
}
</style>
