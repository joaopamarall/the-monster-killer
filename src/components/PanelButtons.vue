<template>
    <div class="panel buttons">
      <template v-if="isRunning">
        <button
          @click="handleAttack(false)"
          class="btn attack"
          :disabled="!canPerformActions">
          Attack
        </button>
        <button
          @click="handleAttack(true)"
          :disabled="!canPerformActions"
          class="btn especial-attack">
          Special Attack
        </button>
        <button @click="healAndHurt" :disabled="!canPerformActions" class="btn heal">
          Heal
        </button>
        <button @click="endGame" class="btn give-up">Quit</button>
      </template>
      <button v-else @click="startGame" class="btn new-game">Start Game</button>
    </div>
</template>
  
<script>
  export default {
      props: {
          running: Boolean,
          gameOver: Boolean,
      },
      data() {
          return {
              isRunning: this.running,
          };
      },
      computed: {
          canPerformActions() {
              return this.isRunning && !this.gameOver;
          },
      },
      methods: {
          startGame() {
              this.isRunning = true;
              this.playerLife = 100;
              this.monsterLife = 100;
              this.logs = [];
              this.$emit("emit-startGame");
          },
          handleAttack(especial) {
              if (this.canPerformActions) {
                  this.$emit("emit-attack", especial);
              }
          },
          healAndHurt() {
              if (this.canPerformActions) {
                  this.$emit("emit-healAndHurt");
              }
          },
          endGame() {
              this.isRunning = false;
              this.gameOver = true;
          },
      },
  };
</script>
  
<style>
    .buttons {
        display: flex;
        justify-content: center;
    }

    .btn {
        padding: 5px 10px;
        margin: 0px 10px;
        border-radius: 5px;
        text-transform: uppercase;
        font-size: 1.1rem;
    }

    .new-game {
        background-color: #4253af;
        color: #fff;
    }

    .attack {
        background-color: #e51c23;
        color: #fff;
    }

    .especial-attack {
        background-color: #ff9800;
        color: #000;
    }

    .heal {
        background-color: #259b24;
        color: #fff;
    }

    .give-up {
        background-color: #bbb;
        color: #000;
    }
</style>
  