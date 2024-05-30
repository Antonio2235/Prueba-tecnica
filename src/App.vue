<script setup>
  // Toda esta información está más detallada en el readme


  // Función para cuando se pulsa el boton add
  // Esta función tiene varias utilidades, ya que de esta forma se puede aprovechar el botón add.
  // Este botón recibe el evento de click del botón, se guarda los values de los inputs e imprime filas
  // en la tabla según lo escrito en los inputs.
  // Tienes la posibilidad de añadir un item sin tag, pero siempre tendrás que poner un nombre, para que funcione
  // el botón, si no saltará un alert.
  // Este botón también sirve para añadir etiquetas nuevas a items ya existentes.
  // Para hacerlo deberás poner el nombre de el item en cuestión y darle la etiqueta que quieras, de esta forma
  // el código comprueba si el nombre existe y entonces añade la nueva etiqueta a la fila de ese item.
  // Debajo de los inputs también tienes los botones de filtrado, que al pulsar uno, ejecuta la función filterByTag
  // que recibe como parámetro el nombre de la tag a filtrar, de esa forma recorre todas las filas y dentro de las filas
  // te recorre todas las tags, de esta forma si encuentra alguna tag que corresponda a la metida por parámetro
  // el booleano hasTag se tornará a true y entonces se mostrará la fila 


  function addItem(event) {
    let name = document.getElementById("name").value;
    let tag = document.getElementById("tag").value;
    event.preventDefault();
    let names = document.querySelectorAll("#tableBody tr td:nth-child(1)");
    let index = -1;
    let exist = false;

    for (let i = 0; i < names.length; i++) {
      if (names[i].textContent === name) {
        index = i;
        exist = true;
        break;
      }
    }

    if (name) {
      if (exist) {
        addTagToRow(index, tag);
      } else {
        let pbody = document.getElementById("tableBody");

        let newRow = pbody.insertRow();
        let nameCell = newRow.insertCell();
        let tagCell = newRow.insertCell();
        let buttonCell = newRow.insertCell();

        nameCell.innerHTML = name;
        addTagToRow(newRow.rowIndex - 1, tag);
        buttonCell.innerHTML = '<button class="delete-btn">Done</button>';

        let deleteButton = buttonCell.querySelector(".delete-btn");
        deleteButton.addEventListener("click", function () {
          newRow.remove();
        });
      }

      document.getElementById("name").value = "";
    } else {
      alert("You must write a name");
    }
  }

  function addTagToRow(rowIndex, tag) {
    let tagsRow = document
      .querySelectorAll("#tableBody tr")
      [rowIndex].querySelector("td:nth-child(2)");
    tagsRow.innerHTML +=
      tag != ""
        ? `<span class="${tag} tag">${tag} <button class="noStyleBtn">X</button></span>`
        : ``;

    let deleteButtons = tagsRow.querySelectorAll(".noStyleBtn");
    deleteButtons.forEach((button) => {
      button.addEventListener("click", function () {
        button.parentNode.remove();
      });
    });
  }

  function filterByTag(tagName) {
    let rows = document.querySelectorAll("#tableBody tr");
    rows.forEach((row) => {
      let tags = row.querySelectorAll(".tag");
      let hasTag = false;
      tags.forEach((tag) => {
        if (tag.classList.contains(tagName)) {
          hasTag = true;
        }
      });
      if (hasTag || tagName === "All") {
        row.style.display = "table-row";
      } else {
        row.style.display = "none";
      }
    });
  }
</script>

<template>
  <div class="container">
    <h2>To-do List</h2>
    <form>
      <input type="text" id="name" placeholder="Name" />
      <select name="tag" id="tag">
        <option value="">None</option>
        <option value="low">Low</option>
        <option value="medium">Medium</option>
        <option value="high">High</option>
        <option value="to-do">To-do</option>
        <option value="buy">Buy</option>
        <option value="important">Important</option>
      </select>
      <button class="addBtn" @click="addItem">Add</button>
    </form>
    
    <div>
      <button class="filterTag" @click="filterByTag('All')">All</button>
      <button class="filterTag" @click="filterByTag('low')">Low</button>
      <button class="filterTag" @click="filterByTag('medium')">Medium</button>
      <button class="filterTag" @click="filterByTag('high')">High</button>
      <button class="filterTag" @click="filterByTag('to-do')">To-do</button>
      <button class="filterTag" @click="filterByTag('buy')">Buy</button>
      <button class="filterTag" @click="filterByTag('important')">Important</button>
    </div>
    <table id="Table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Tags</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody id="tableBody"></tbody>
    </table>
  </div>
</template>


<style>
.low {
  background-color: lightgreen;
  margin-right: 5px;
}

.medium {
  background-color: lightblue;
  margin-right: 5px;
}

.high {
  background-color: lightcoral;
  margin-right: 5px;
}

.to-do {
  background-color: lightpink;
  margin-right: 5px;
}

.buy {
  background-color: lightseagreen;
  margin-right: 5px;
}

.important {
  background-color: red;
  margin-right: 5px;
}
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f4f4f4;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px;
}
form {
  margin-bottom: 20px;
}
input[type="text"],
input[type="number"],
select {
  padding: 10px;
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 200px;
}
.addBtn {
  padding: 10px;
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 200px;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
}
table {
  border-collapse: collapse;
  width: 100%;
}
th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}
th {
  background-color: #f2f2f2;
}
th:nth-child(1),
td:nth-child(1) {
  max-width: 30%;
  width: 30%;
}

td:nth-child(2),
th:nth-child(2) {
  max-width: 30%;
  width: 30%;
}

td:nth-child(3),
th:nth-child(3) {
  max-width: 10%;
  width: 10%;
}
td:nth-child(4),
th:nth-child(4) {
  max-width: 13%;
  width: 13%;
}

.tag {
  border-radius: 5px;
  padding: 3px;
  width: fit-content;
}

.delete-btn {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 8px 12px;
  cursor: pointer;
}

.noStyleBtn {
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.filterTag {
  padding: 3px;
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100px;
  background-color: white;
  cursor: pointer;
  margin-bottom: 20px;
}

.filterTag:focus {
  background-color: #4caf50;}
</style>
