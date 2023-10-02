<template>
          <div v-if="logs.length"
          class="panel logs">
            <ul>
                <li v-for="(log, i) in logs" :key="i"
                    class="log"
                    :class="logs.cls">{{ log.text }}</li>
            </ul>
        </div>
</template>

<script>
export default {
}
</script>

<style>
.logs ul {
    display: flex;
    flex-direction: column;
    list-style: none;
    padding: 0;
    margin: 0;
}

.logs ul li {
    display: flex;
    justify-content: center;
    margin: 4px 0px;
    padding: 3px 0px;
    font-weight: 600;
    font-size: 1.1rem;
    text-transform: uppercase;
    border-radius: 3px;
}

.player {
    background-color: #4253afaa;
    color: #fff;
}

.monster {
    background-color: #e51c23aa;
    color: #fff;
}
</style>