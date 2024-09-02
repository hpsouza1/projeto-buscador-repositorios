<template>
    <div class="info">
      <h1>{{ title }}</h1>
      <h2>{{ text }}</h2>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Info',
    props: {
      title: String,
      text: String
    }
  }
  </script>
  
  <style scoped>
  .info {
  margin-bottom: 10px;
  background-color: transparent;
  
}
  
  .info h1 {
    font-size: 25px;
    margin: 0;
    padding: 0;
    position: relative;
    top: -10px;
    color: var(--neutral-text);
  }
  
  .info h2 {
    font-size: 13px;
    color: #F3BF99; 
    margin-top: -5px; 
    margin-bottom: 20px; 
  
  }
  </style>
  