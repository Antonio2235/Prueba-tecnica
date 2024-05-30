<template>
    <button class="container">
     See all
    </button>
  </template>
  <script setup></script>
  <style scoped>
  .container {
    position: absolute;
    bottom: 20px;
    left: 220px;
    width: 150px; 
    padding: 5px;
    display: flex;
    align-items: center;
    appearance: none;
    border: none;
    background-color: transparent;
    width: 55px;
  }
  
  .container:active {
      background-color: var(--lightgrey2);
      border-radius: 5px;
  }
  
  .container i {
    margin-right: 10px;
  }
  </style>
  