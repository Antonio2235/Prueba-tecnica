<script setup></script>

<template>
  <div id="container">
    
    <input type="text" name="search" id="search" placeholder="Search">
    <i class="bi bi-search searchIcon"></i>
  </div>
</template>

<style scoped>

#container {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    padding-bottom: 2rem;
}

input {
    width: 100%;
    padding: 0.25rem;
    padding-left: 2.5rem;
    border-radius: 5px;
}

.searchIcon {
    position: absolute;
    left: 0.75rem;
    color: grey;
    pointer-events: none;
}

</style>
