<template>
    <div class="score">
      <h1>{{ title }}</h1>
      <div class="life-bar">
        <div
          class="life"
          :class="{ danger: life < 20 }"
          :style="{ width: life + '%' }"
        ></div>
      </div>
      <div>{{ life }}%</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      title: String,
      life: Number,
    },
  };
  </script>
  
  <style scoped>
  .score {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  
  .score h1 {
    font-weight: 300;
    font-size: 1.6rem;
  }
  
  .life-bar {
    width: 80%;
    height: 20px;
    border: 1px solid #aaa;
  }
  
  .life-bar .life {
    display: flex;
    justify-content: center;
    height: 100%;
    background-color: green;
  }
  
  .life-bar .life.danger {
    background-color: red;
  }
  </style>
  