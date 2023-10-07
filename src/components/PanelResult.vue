<template>
    <div v-if="hasResult" class="panel result">
      <div class="result-message" :class="{ win: isWin, lose: isLose }">
        {{ resultMessage }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      playerLife: Number,
      monsterLife: Number,
    },
    computed: {
      hasResult() {
        return this.playerLife === 0 || this.monsterLife === 0;
      },
      isWin() {
        return this.monsterLife === 0;
      },
      isLose() {
        return this.playerLife === 0;
      },
      resultMessage() {
        return this.isWin ? 'You WIN!!! :)' : 'You LOSE! :(';
      },
    },
    watch: {
      hasResult(value) {
        if (value) {
          this.$emit('game-over', this.isWin ? 'win' : 'lose');
        }
      },
    },
  };
  </script>
  
  <style>
  .result {
    display: flex;
    justify-content: center;
    font-size: 1.3rem;
    font-weight: 600;
  }
  
  .result-message {
    color: green; /* Default color for a win message */
  }
  
  .result-message.lose {
    color: red;
  }
  </style>
  