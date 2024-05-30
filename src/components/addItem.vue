<template>
  <i class="bi bi-plus-lg addItem" @click="createItem"></i>
</template>
<script setup>

function createItem () {
    const ul = document.querySelector("ul");

    // <input type="checkbox" id="checkbox1" />
    //       <label for="checkbox1">comprar el pan</label>
    //       <div class="tags">
    //         <p>mañana</p>
    //         <p>fsdfasdfasdfasfd</p>
    //       </div>
    //       <hr />
}

</script>
<style scoped>
.addItem {
  font-size: 1.5rem;
  float: right;
  margin-right: 10px;
  margin-top: 10px;
}

.addItem:active {
  background-color: var(--lightgrey2);
  border-radius: 5px;
}
</style>
