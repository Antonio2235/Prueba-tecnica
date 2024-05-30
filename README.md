# PruebaVue

Este pequeño proyecto es una prueba técnica.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
## Funcionalidades
### Añadir to-do items

La función que se usa para esto es "addItem"

Lo primero que hace es guardar los values de los inputs en unas variables, para poder utilizarlos posteriormente.
Lo siguiente es esta línea "event.preventDefault();" que impide el envío del formulario, ya que al haber un botón dentro de un formulario, entiende que es para que se haga submit, por lo que al escribir este método, de previene ese comportamiento.

Lo siguiente es crear la variable names, que guarda todos los nombres de la tabla, para posteriormente comprobar si ya existe.
También se crean un index = -1 y un booleano exist a false.
Estas dos variables servirán para determinar si existe o no el item que se quiere añadir.

Ahora recorre todos los nombres guardados en la variable names, de forma que si encuentra un nombre repetido tornará el booleano a true y guardará el index con el propósito de editar la fila en esa posición más tarde.

if name te comprueba si name está vacío o no, y en caso de que esté vacío saltará un alert.

Justo después comprobamos el booleano de si existe el item ya, para entonces llamar directamente a la función addTagToRow, de forma que solo añadirá la tag a la fila.

En caso de que el booleano sea falso, creará la fila y dentro de la fila las celdas que corresponden a la información, que son la celda del nombre, la de las tags, y la celda con el botón de eliminar la fila.

Ese botón coge el elemento que tenga la clase .delete-btn y hace un remove() de la fila que se ha añadido en ese evento.

Después se vacía el input diciendole que el value sea "".

## Función addTagRow

La función addTagToRow recibe como parámetro el índice de la fila que se quiere modificar y la tag que se añadirá, esta función en llamada en dos ocasiones, cuando se crea un elemento o cuando se añade una tag poniendo el nombre del item existente.

Funciona de la siguiente manera, crea la variable tagsRow que contiene el segundo hijo td del tr de el índice introducido de la fila exacta de un "array" de todas las filas.
De esta forma podremos editarla con el método innerHTML.

Diciendo que si la tag es diferente de "", que solo es igual a "" cuando se elige none, añadirá un span con una clase con el nombre de la tag para de esa manera darle el estilo que quiero.

En el contenido también se le dará el valor de la variable tag, y después creo un botón con la clase noStyleBtn para hacer un botón sin estilo que se usará para eliiminar la tag.

Debajo se les añade la funcionalidad a los botones de eliminar tags, diciendo que elimine el padre de el botón, que en este caso es el span.

## Función filterByTag

Recibe el nombre de tag que se quiera filtrar por parámetros, ya que todos los botones llaman a la función con su respectiva tag a filtrar.

Lo primero que hago es crear la variable rows, que contiene todas las filas.

Ahora hago un bucle for each en el que por cada fila guardaré las tags que tenga en una variable tags.

Recorro con otro foreach todas las tags que haya diciendo que si la tag contiene el nombre tagname introducido por parámetro el booleano hastag se tornará true.

Este booleano servirá para ahora determinar si se debe mostrar la fila con el método .style.display, para que en caso de que sea true o se haya pulsado "All" se muestre.

