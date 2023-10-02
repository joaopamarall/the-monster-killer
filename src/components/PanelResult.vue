<template>
  <div v-if="hasResult" class="panel result">
            <div class="win" v-if="monsterLife == 0">You WIN!!! :)</div>
            <div class="lose" v-else>You LOSE! :(</div>
        </div>
</template>

<script>
export default {
    props: {
        playerLife: Number,
        monsterLife: Number,
        running: Boolean
  }
}
</script>

<style>
.result {
    display: flex;
    justify-content: center;
    font-size: 1.3rem;
    font-weight: 600;
}

.result .win {
    color: green;
}

.result .lose {
    color: red;
}
</style>