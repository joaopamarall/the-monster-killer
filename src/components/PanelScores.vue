<template>
    <div class="panel scores">
      <ScoreCard title="Player" :life="playerLife" />
      <ScoreCard title="Monster" :life="monsterLife" />
    </div>
  </template>
  
  <script>
  import ScoreCard from './ScoreCard.vue';
  
  export default {
    props: {
      playerLife: Number,
      monsterLife: Number,
    },
    components: {
      ScoreCard,
    },
  };
  </script>
  
  <style>
  .scores {
    display: flex;
    justify-content: space-between;
  }
  </style>
  