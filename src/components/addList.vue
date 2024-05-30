<script setup>
import { ref } from "vue";

const active = ref(false);
const newListName = ref("");

function addNewList() {
  active.value = true;
  focusInput();
}

function focusInput() {
  const input = document.getElementById("inputList");
  if (input) {
    input.focus();
  }
}

function enterNewList() {
  const input = document.getElementById("inputList");

  const newLiContent = input.value;
  if (newLiContent !== "") {
    const listsContainer = document.querySelector(".listsContainer");

    if (listsContainer) {
      const newLi = document.createElement("li");
      newLi.textContent = newLiContent;
      listsContainer.appendChild(newLi);

      const newPage = document.querySelector(".newPage");

      const newtittle = document.createElement("h1");
      const newUl = document.createElement("ul");

      newUl.className = input.value.trim();

      newtittle.textContent = input.value;

      newPage.appendChild(newtittle);
      newPage.appendChild(newUl);
      input.value = "";
      active.value = false;
    } else {
      console.error("listsContainer no encontrado");
    }
  }
}
</script>

<template>
  <input
    type="text"
    id="inputList"
    placeholder="List name"
    v-show="active"
    @keyup.enter="enterNewList"
  />
  <button class="container" @click="addNewList">
    <i class="bi bi-plus-circle icono"></i>
    <p>Add List</p>
  </button>
</template>

<style scoped>
.container {
  position: absolute;
  bottom: 20px;
  left: 20px;
  width: 150px;
  padding: 5px;
  display: flex;
  align-items: center;
  appearance: none;
  border: none;
  background-color: transparent;
  width: 100px;
}

.container:active {
  background-color: var(--lightgrey2);
  border-radius: 5px;
}

.container i {
  margin-right: 10px;
}

#inputList {
  margin-left: 20px;
  border-radius: 5px;
}
</style>
