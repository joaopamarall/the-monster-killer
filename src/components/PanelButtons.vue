<template>
    <div class="panel buttons">
        <template v-if="running">
            <button @click="attack(false)"
                class="btn attack">Attack</button>
            <button @click="attack(true)"
                class="btn especial-attack">Special Attack</button>
            <button @click="healAndHurt"
                class="btn heal">Heal</button>
            <button @click="running = false"
                class="btn give-up">Quit</button>
        </template>
        <button v-else @click="startGame"
            class="btn new-game">Start Game</button>
    </div>
</template>

<script>
export default {
    props: {
        playerLife: Number,
        monsterLife: Number,
        running: Boolean
  },
    methods: {  
        startGame() {
            this.running = true;
            this.playerLife = 100;
            this.monsterLife = 100;
            this.logs = []
            this.$emit("emit-startGame", this.running);
        },
        attack(especial) {
            this.hurt('monsterLife', 5, 10, especial, 'Player', 'Monster', 'player')
            if(this.monsterLife > 0) {
            this.hurt('playerLife', 7, 12, false, 'Monster', 'Player', 'monster')
        }
    },
        healAndHurt() {
            this.$emit("emit-healAndHurt");
        },
    },
}
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
    color: #FFF;
}

.give-up {
    background-color: #BBB;
    color: #000;
}
</style>