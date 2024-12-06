## Dia 1
Santa Claus 🎅 ha recibido una lista de números mágicos que representan regalos 🎁, pero algunos de ellos están duplicados y deben ser eliminados para evitar confusiones. Además, los regalos deben ser ordenados en orden ascendente antes de entregárselos a los elfos.

Tu tarea es escribir una función que reciba una lista de números enteros (que pueden incluir duplicados) y devuelva una nueva lista sin duplicados, ordenada en orden ascendente.

```js
const gifts1 = [3, 1, 2, 3, 4, 2, 5]
const preparedGifts1 = prepareGifts(gifts1)
console.log(preparedGifts1) // [1, 2, 3, 4, 5]

const gifts2 = [6, 5, 5, 5, 5]
const preparedGifts2 = prepareGifts(gifts2)
console.log(preparedGifts2) // [5, 6]

const gifts3 = []
const preparedGifts3 = prepareGifts(gifts3)
console.log(preparedGifts3) // []
// No hay regalos, la lista queda vacía
```

```js
function prepareGifts(gifts) {
  gifts = Array.from(new Set(gifts))
  gifts.sort((a,b)=>a - b)
  return gifts 
}
```


## Dia 2
Santa Claus 🎅 quiere enmarcar los nombres de los niños buenos para decorar su taller 🖼️, pero el marco debe cumplir unas reglas específicas. Tu tarea es ayudar a los elfos a generar este marco mágico.

Reglas:

Dado un array de nombres, debes crear un marco rectangular que los contenga a todos.
Cada nombre debe estar en una línea, alineado a la izquierda.
El marco está construido con * y tiene un borde de una línea de ancho.
La anchura del marco se adapta automáticamente al nombre más largo más un margen de 1 espacio a cada lado.
Ejemplo de funcionamiento:

```js
createFrame(['midu', 'madeval', 'educalvolpz'])

// Resultado esperado:
***************
* midu        *
* madeval     *
* educalvolpz *
***************

createFrame(['midu'])

// Resultado esperado:
********
* midu *
********

createFrame(['a', 'bb', 'ccc'])

// Resultado esperado:
*******
* a   *
* bb  *
* ccc *
*******

createFrame(['a', 'bb', 'ccc', 'dddd'])
```

```js
function createFrame(names) {
  const max_length = Math.max(...names.map(name => name.length));

  const topBorder = '*'.repeat(max_length + 4);

  const nameLines = names.map(name => 
    `* ${name}${' '.repeat(max_length - name.length)} *`
  );

  return [
    topBorder,
    ...nameLines,
    topBorder
  ].join('\n');
}
```


## Dia 3
Santa Claus 🎅 está revisando el inventario de su taller para preparar la entrega de regalos. Los elfos han registrado los juguetes en un array de objetos, pero la información está un poco desordenada. Necesitas ayudar a Santa a organizar el inventario.

Recibirás un array de objetos, donde cada objeto representa un juguete y tiene las propiedades:

name: el nombre del juguete (string).
quantity: la cantidad disponible de ese juguete (entero).
category: la categoría a la que pertenece el juguete (string).
Escribe una función que procese este array y devuelva un objeto que organice los juguetes de la siguiente manera:

Las claves del objeto serán las categorías de juguetes.
Los valores serán objetos que tienen como claves los nombres de los juguetes y como valores las cantidades totales de cada juguete en esa categoría.
Si hay juguetes con el mismo nombre en la misma categoría, debes sumar sus cantidades.
Si el array está vacío, la función debe devolver un objeto vacío {}.

```js
const inventary = [
  { name: 'doll', quantity: 5, category: 'toys' },
  { name: 'car', quantity: 3, category: 'toys' },
  { name: 'ball', quantity: 2, category: 'sports' },
  { name: 'car', quantity: 2, category: 'toys' },
  { name: 'racket', quantity: 4, category: 'sports' }
]

organizeInventory(inventary)

// Resultado esperado:
// {
//   toys: {
//     doll: 5,
//     car: 5
//   },
//   sports: {
//     ball: 2,
//     racket: 4
//   }

const inventary2 = [
  { name: 'book', quantity: 10, category: 'education' },
  { name: 'book', quantity: 5, category: 'education' },
  { name: 'paint', quantity: 3, category: 'art' }
]

organizeInventory(inventary2)

// Resultado esperado:
// {
//   education: {
//     book: 15
//   },
//   art: {
//     paint: 3
//   }
// }
```

```js
// Soculión 3 extrellas
function organizeInventory(inventory) {
  return inventory.reduce((result,{name,quantity, category})=>{
    if(!result[category]){
      result[category] = {};
    }
    if (result[category][name])
    {
      result[category][name] += quantity;
    }
    else{
      result[category][name] = quantity;
    }

    return result;
    },{});
}
```

```js
// aveces 4 aveces 3
function organizeInventory(inventory) {
  const result = {};

  for (const { name, quantity, category } of inventory) {
    if (!result[category]) {
      result[category] = {};
    }
    if (!result[category][name]) {
      result[category][name] = quantity;
    } else {
      result[category][name] += quantity;
    }
  }

  return result;
}
```

```js
// 5 extrellas
function organizeInventory(inventory) {
  const result = {};
  for (const { name, quantity, category } of inventory) {
    result[category] = result[category]||{};
    if (result[category][name]) {
      result[category][name] += quantity;
    } else {
      result[category][name] = quantity;
    }
  }

  return result;
}
```

## Dia 4
¡Es hora de poner el árbol de Navidad en casa! 🎄 Pero este año queremos que sea especial. Vamos a crear una función que recibe la altura del árbol (un entero positivo entre 1 y 100) y un carácter especial para decorarlo.

La función debe devolver un string que represente el árbol de Navidad, construido de la siguiente manera:
- El árbol está compuesto de triángulos de caracteres especiales.
- Los espacios en blanco a los lados del árbol se representan con guiones bajos _.
- Todos los árboles tienen un tronco de dos líneas, representado por el carácter #.
- El árbol siempre debe tener la misma longitud por cada lado.
- Debes asegurarte de que el árbol tenga la forma correcta usando saltos de línea \n para cada línea.

```js
const tree = createXmasTree(5, '*')
console.log(tree)
/*
____*____
___***___
__*****__
_*******_
*********
____#____
____#____
*/

const tree2 = createXmasTree(3, '+')
console.log(tree2)
/*
__+__
_+++_
+++++
__#__
__#__
*/

const tree3 = createXmasTree(6, '@')
console.log(tree3)
/*
_____@_____
____@@@____
___@@@@@___
__@@@@@@@__
_@@@@@@@@@_
@@@@@@@@@@@
_____#_____
_____#_____
*/
```

```js
// 4 extrellas
function createXmasTree(height, ornament) {
  let border = '_'.repeat(height-1)
  let tree = border + ornament + border +'\n'
  for(let i = 0; i < height ;i++){
    tree += '_'.repeat(height-1-i) + ornament.repeat(i)+ ornament + ornament.repeat(i)+ '_'.repeat(height-1-i) +'\n'
  }

  tree += `${border}#${border}\n`+`${border}#${border}`
  return tree
}
```

```js
// 5 extrellas
function createXmasTree(height, ornament) {
  const border = '_'.repeat(height - 1);
  const trunk = `${border}#${border}`;
  let tree = [];

  for (let i = 0; i < height; i++) {
    const padding = '_'.repeat(height - 1 - i);
    const layer = ornament.repeat(2 * i + 1);
    tree.push(`${padding}${layer}${padding}`);
  }

  return tree.join('\n') + `\n${trunk}\n${trunk}`;
```

## Dia 5

Los elfos 🧝🧝‍♂️ de Santa Claus han encontrado un montón de botas mágicas desordenadas en el taller. Cada bota se describe por dos valores:

- *type* indica si es una bota izquierda (I) o derecha (R).
- *size* indica el tamaño de la bota.

Tu tarea es ayudar a los elfos a emparejar todas las botas del mismo tamaño que tengan izquierda y derecha. Para ello, debes devolver una lista con los tamaños disponibles después de emparejar las botas.

```js
onst shoes = [
  { type: 'I', size: 38 },
  { type: 'R', size: 38 },
  { type: 'R', size: 42 },
  { type: 'I', size: 41 },
  { type: 'I', size: 42 }
]

organizeShoes(shoes)
// [38, 42]

const shoes2 = [
  { type: 'I', size: 38 },
  { type: 'R', size: 38 },
  { type: 'I', size: 38 },
  { type: 'I', size: 38 },
  { type: 'R', size: 38 }
]
// [38, 38]

const shoes3 = [
  { type: 'I', size: 38 },
  { type: 'R', size: 36 },
  { type: 'R', size: 42 },
  { type: 'I', size: 41 },
  { type: 'I', size: 43 }
]

organizeShoes(shoes3)
// []
```

```js
// 5 estrelllas
function organizeShoes(shoes) {
  let pares = [];
  let nopares = new Set();
  
  for (let shoe of shoes) {
    let need = `${shoe.type === 'R' ? 'I' : 'R'} ${shoe.size}`
    let save = `${shoe.type} ${shoe.size}`;
    
    if (nopares.has(need)) {
      nopares.delete(need);
      pares.push(parseInt(save.split(' ')[1]));
    } else {
      nopares.add(save);
    }
  }

  return pares;
}
```


## Día 6

Ya hemos empaquetado cientos de regalos 🎁… pero a un elfo se le ha olvidado revisar si el regalo, representado por un asterisco *, está dentro de la caja.

La caja tiene un regalo (*) y cuenta como dentro de la caja si:
- Está rodeada por # en los bordes de la caja.
- El * no está en los bordes de la caja.

Ten en cuenta entonces que el * puede estar dentro, fuera o incluso no estar. Y debemos devolver true si el * está dentro de la caja y false en caso contrario.

```js
inBox([
  "###",
  "#*#",
  "###"
]) // ➞ true

inBox([
  "####",
  "#* #",
  "#  #",
  "####"
]) // ➞ true

inBox([
  "*####",
  "#   #",
  "#  #*",
  "####"
]) // ➞ false

inBox([
  "#####",
  "#   #",
  "#   #",
  "#   #",
  "#####"
]) // ➞ false
```

```js
// 4 extrellas
function inBox(box) {

  for (let i = 1; i<box.length-1; i++){
    let line = box[i].split('')
    if(line.some((s)=> s === '*')){
      return line[0]=='#' && line[line.length-1]== '#' ? true: false
    }
  }
  return false
}
```

```js
// 5 extrellas
function inBox(box) {
  for (let i = 1; i<box.length-1; i++){
    let index = box[i].indexOf('*');
    if(index >0  && index < box[i].length-1){
      return  true
    }
  }
  return false
}
```