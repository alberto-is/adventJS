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
// Soculión 3 estrellas
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
// 5 estrellas
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
// 4 estrellas
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
// 5 estrellas
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
// 4 estrellas
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
// 5 estrellas
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

## Día 7
El grinch 👹 ha pasado por el taller de Santa Claus! Y menudo desastre ha montado. Ha cambiado el orden de algunos paquetes, por lo que los envíos no se pueden realizar.

Por suerte, el elfo Pheralb ha detectado el patrón que ha seguido el grinch para desordenarlos. Nos ha escrito las reglas que debemos seguir para reordenar los paquetes. Las instrucciones que siguen son:

Recibirás un string que contiene letras y paréntesis.
Cada vez que encuentres un par de paréntesis, debes voltear el contenido dentro de ellos.
Si hay paréntesis anidados, resuelve primero los más internos.
Devuelve el string resultante con los paréntesis eliminados, pero con el contenido volteado correctamente.
Nos ha dejado algunos ejemplos:

```js
fixPackages('a(cb)de')
// ➞ "abcde"
// Volteamos "cb" dentro de los paréntesis

fixPackages('a(bc(def)g)h')
// ➞ "agdefcbh"
// 1º volteamos "def" → "fed", luego volteamos "bcfedg" → "gdefcb"

fixPackages('abc(def(gh)i)jk')
// ➞ "abcighfedjk"
// 1º volteamos "gh" → "hg", luego "defhgi" → "ighfed"

fixPackages('a(b(c))e')
// ➞ "acbe"
// 1º volteamos "c" → "c", luego "bc" → "cb"
```

```js 
// 3 estrella :C
function fixPackages(packages) {
  function invertParentheses(str) {
    const regex = /\(([^()]*)\)/;
    
    if (!regex.test(str)) {
      return str;
    }
    return invertParentheses(str.replace(regex, (_, content) => {
      return content.split('').reverse().join('');
    }));
  }
  
  return invertParentheses(packages).replace(/[()]/g, '');
}
```

```js
// 2 estrella :C
function fixPackages(packages) {
  let arr = []
  for(let i = 0; i<packages.length ;i++){
    let p = packages[i]
    if ( p ==='('){
      arr.push(i)
    }
    else if (p === ')'){
      let begin = arr.pop()
      packages = packages.slice(0,begin) + invest(packages.slice(begin,i+1))+ packages.slice(i+1)
    }
  }

  return packages.replaceAll('(','').replaceAll(')','')

  function invest(str){
    return [...str].reverse().join('')
  }
}
```

```js
// 4 estrellas :/
function fixPackages(packages) {
  let arr = []
  for(let i = 0; i<packages.length ;i++){
    let p = packages[i]
    if ( p ==='('){
      arr.push(i)
    }
    else if (p === ')'){
      let begin = arr.pop()
      let invest = [...packages.slice(begin,i+1)].reverse().join('')
      packages = packages.slice(0,begin) +invest+ packages.slice(i+1)
    }
  }

  return packages.replaceAll('(','').replaceAll(')','')
}
```

```js
// 4 estrellas :////
function fixPackages(packages) {
  let arr = []
  let packages_arr = [...packages]
  for(let i = 0; i<packages_arr.length ;i++){
    let p = packages_arr[i]
    if ( p ==='('){
      arr.push(i)
    }
    else if (p === ')'){
      let begin = arr.pop()
      let invest = packages_arr.slice(begin+1,i).reverse()
      packages_arr = packages_arr.slice(0,begin).concat(invest,packages_arr.slice(i+1))
      i = i-2
    }
  }

  return packages_arr.join('')
}
```


```js
// 4 estrellas ://///////
function fixPackages(packages) {
  let arr = []
  let packages_arr = [...packages]
  for(let i = 0; i<packages_arr.length ;i++){
    let p = packages_arr[i]
    if ( p ==='('){
      arr.push(i)
    }
    else if (p === ')'){
      let begin = arr.pop()
      let invest = packages_arr.slice(begin,i).reverse()
      packages_arr.splice(begin, i - begin , ...invest)
    }
  }

  return packages_arr.join('').replace(/[()]/g, '')
}
```

```js 
// 5 estrellas :D
function fixPackages(packages) {
  let regex = /\([a-z]+\)/g
  let loop = true

  while(loop){
    loop = false
    packages = packages.replace(regex,frame => {
        loop= true
        return frame.slice(1, -1).split('').reverse().join('')
    })
  }

    return packages
}
```
## Día 8
¡Es hora de seleccionar a los renos más rápidos para los viajes de Santa! 🦌🎄
Santa Claus ha organizado unas emocionantes carreras de renos para decidir cuáles están en mejor forma.

Tu tarea es mostrar el progreso de cada reno en una pista de nieve en formato isométrico.

La información que recibes:
- indices: Un array de enteros que representan el progreso de cada reno en la pista:
- 0: El carril está vacío.
- Número positivo: La posición actual del reno desde el inicio de la pista.
- Número negativo: La posición actual del reno desde el final de la pista.
- length: La longitud de cada carril.

Devuelve un string que represente la pista de la carrera:
- Cada carril tiene exactamente length posiciones llenas de nieve (~).
- Cada reno se representa con la letra r.
- Los carriles están numerados al final con /1, /2, etc.
- La vista es isométrica, por lo que los carriles inferiores están desplazados hacia la derecha.

```js
drawRace([0, 5, -3], 10)
/*
  ~~~~~~~~~~ /1
 ~~~~~r~~~~ /2
~~~~~~~r~~ /3
*/

drawRace([2, -1, 0, 5], 8)
/*
   ~~r~~~~~ /1
  ~~~~~~~r /2
 ~~~~~~~~ /3
~~~~~r~~ /4
*/

drawRace([3, 7, -2], 12)
/*
  ~~~r~~~~~~~~ /1
 ~~~~~~~~r~~~ /2
~~~~~~~~~r~~ /3
*/
```

```js
// 5 estrellas
function drawRace(indices, length) {
  let reply = []
  for (let r = 0; r < indices.length; r++){
    let track = '~'.repeat(length)
    if (indices[r]== 0){
      reply[r] = track
    }
    else if (indices[r] <0){
      let p = length + indices[r]
      reply[r] = track.substring(0,p ) + 'r' + track.substring( p + 1);
    }
    else{
      reply[r] = track.substring(0, indices[r]) + 'r' + track.substring(indices[r] + 1);
    }

    reply[r] = ' '.repeat(indices.length-r-1)+reply[r]+` /${r+1}`
  }
  return reply.join("\n")
}
```

## Día 9
Los elfos están jugando con un tren 🚂 mágico que transporta regalos. Este tren se mueve en un tablero representado por un array de strings.

El tren está compuesto por una locomotora (@), seguida de sus vagones (o), y debe recoger frutas mágicas (*) que le sirve de combustible. El movimiento del tren sigue las siguientes reglas:

Recibirás dos parámetros board y mov.

board es un array de strings que representa el tablero:

@ es la locomotora del tren.
o son los vagones del tren.
* es una fruta mágica.
· son espacios vacíos.
mov es un string que indica el próximo movimiento del tren desde la cabeza del tren @:

'L': izquierda
'R': derecha
'U': arriba
'D': abajo.
Con esta información, debes devolver una cadena de texto:

'crash': Si el tren choca contra los bordes del tablero o contra sí mismo.
'eat': Si el tren recoge una fruta mágica (*).
'none': Si avanza sin chocar ni recoger ninguna fruta mágica.

```js
const board = ['·····', '*····', '@····', 'o····', 'o····']

console.log(moveTrain(board, 'U'))
// ➞ 'eat'
// Porque el tren se mueve hacia arriba y encuentra una fruta mágica

console.log(moveTrain(board, 'D'))
// ➞ 'crash'
// El tren se mueve hacia abajo y la cabeza se choca consigo mismo

console.log(moveTrain(board, 'L'))
// ➞ 'crash'
// El tren se mueve a la izquierda y se choca contra la pared

console.log(moveTrain(board, 'R'))
// ➞ 'none'
// El tren se mueve hacia derecha y hay un espacio vacío en la derecha
```

```js
// 1 estrella :C
function moveTrain(board, mov) {
  let engine = -1
    for(let i = 0; i < board.length; i++){
      if (board[i].includes('@')){
        engine = i
        break
      }
    }
  if(engine === -1){
    return NaN
  }
  let pos = board[engine].indexOf('@')
    switch(mov){
      case 'D':
        if(engine+1 >= board.length || board[engine+1][pos]=='o'){
          return 'crash'
        }
        else if(board[engine+1][pos]=='*'){
          return 'eat'
        }
        return 'none'

      case 'U':
        if(engine-1<0 || board[engine-1][pos]=='o'){
          return 'crash'
        }
        else if(board[engine-1][pos]=='*'){
          return 'eat'
        }
        return 'none'

      case 'L':
        if(pos-1<0 || board[engine][pos-1]=='o'){
          return 'crash'
        }
        else if(board[engine][pos-1]=='*'){
          return 'eat'
        }
        return 'none'

      case 'R':
        if(pos+1>=board[engine].length || board[engine][pos+1]=='o'){
          return 'crash'
        }
        else if(board[engine][pos+1]=='*'){
          return 'eat'
        }
        return 'none'

      
    }
  return 'none';
}
```

```js
// 3 estrellas :////
function moveTrain(board, mov) {
  let engine = -1, pos = -1
    for(let i = 0; i < board.length; i++){
      let col = board[i].indexOf('@')
      if (col !== -1){
        engine = i
        pos = col
        break
      }
    }
    const moves = { 
    'U': [-1,  0], 
    'D': [ 1,  0], 
    'L': [ 0, -1], 
    'R': [ 0,  1] 
    };

    const newRow = engine + moves[mov][0];
    const newCol = pos + moves[mov][1];
  
    if (newRow < 0 || newRow >= board.length || newCol < 0 || newCol >= board[0].length) {
      return 'crash';
    }
    
    if (board[newRow][newCol] === 'o') return 'crash';
    if (board[newRow][newCol] === '*') return 'eat';
    return 'none';
}
```

## Día 10

Los elfos programadores están creando un pequeño ensamblador mágico para controlar las máquinas del taller de Santa Claus.

Para ayudarles, vamos a implementar un intérprete sencillo que soporte las siguientes instrucciones mágicas:

- MOV x y: Copia el valor x (puede ser un número o el contenido de un registro) en el registro y
- INC x: Incrementa en 1 el contenido del registro x
- DEC x: Decrementa en 1 el contenido del registro x
- JMP x y: Si el valor del registro x es 0 entonces salta a la instrucción en el índice y y sigue ejecutándose el programa desde ahí.

Comportamiento esperado:
- Si se intenta acceder, incrementar o decrementar a un registro que no ha sido inicializado, se tomará el valor 0 por defecto.
- El salto con JMP es absoluto y lleva al índice exacto indicado por y.
- Al finalizar, el programa debe devolver el contenido del registro A. Si A no tenía un valor definido, retorna undefined.

Nota: Los registros que no han sido inicializados previamente se inicializan a 0.

```js
const instructions = [
  'MOV -1 C', // copia -1 al registro 'C',
  'INC C', // incrementa el valor del registro 'C'
  'JMP C 1', // salta a la instrucción en el índice 1 si 'C' es 0
  'MOV C A', // copia el registro 'C' al registro 'a',
  'INC A' // incrementa el valor del registro 'a'
]

compile(instructions) // -> 2

/**
 Ejecución paso a paso:
 0: MOV -1 C -> El registro C recibe el valor -1
 1: INC C    -> El registro C pasa a ser 0
 2: JMP C 1  -> C es 0, salta a la instrucción en el índice 1
 1: INC C    -> El registro C pasa a ser 1
 2: JMP C 1  -> C es 1, ignoramos la instrucción
 3: MOV C A  -> Copiamos el registro C en A. Ahora A es 1
 4: INC A    -> El registro A pasa a ser 2
 */
```
```js
// 5 estrellas :D
function compile(instructions) {
  instructions = instructions.map((x) => x.split(' '))
  const vars = {}

  for (let i = 0; i < instructions.length ;i++) {
    let inst = instructions[i]
    switch(inst[0]){
      case 'INC':
          vars[inst[1]] !== undefined? vars[inst[1]]+=1 : vars[inst[1]] = 1
        break

      case 'DEC':
          vars[inst[1]] !== undefined? vars[inst[1]]-=1 : vars[inst[1]]= -1
        break
      case 'MOV':
          isNaN(inst[1])
          ? vars[inst[2]] = vars[inst[1]]
          : vars[inst[2]] = Number(inst[1])
        break

        case 'JMP':
          if((vars[inst[1]] || 0) === 0){
            i = inst[2] - 1
          }
        break
    }

  }

  return vars['A']
}
```

## Día 11

El Grinch ha hackeado 🏴‍☠️ los sistemas del taller de Santa Claus y ha codificado los nombres de todos los archivos importantes. Ahora los elfos no pueden encontrar los archivos originales y necesitan tu ayuda para descifrar los nombres.

Cada archivo sigue este formato:

Comienza con un número (puede contener cualquier cantidad de dígitos).
Luego tiene un guion bajo _.
Continúa con un nombre de archivo y su extensión.
Finaliza con una extensión extra al final (que no necesitamos).
Ten en cuenta que el nombre de los archivos pueden contener letras (a-z, A-Z), números (0-9), otros guiones bajos (_) y guiones (-).

Tu tarea es implementar una función que reciba un string con el nombre de un archivo codificado y devuelva solo la parte importante: el nombre del archivo y su extensión.

```js
decodeFilename('2023122512345678_sleighDesign.png.grinchwa')
// ➞ "sleighDesign.png"

decodeFilename('42_chimney_dimensions.pdf.hack2023')
// ➞ "chimney_dimensions.pdf"

decodeFilename('987654321_elf-roster.csv.tempfile')
// ➞ "elf-roster.csv"
```

```js
// 5 estrellas :D
function decodeFilename(filename) {
  let res = filename.match(/[a-zA-Z][a-zA-Z-_]*\.[a-z]+/)
  return res[0]
}
```

## Día 12

Estás en un mercado muy especial en el que se venden árboles de Navidad 🎄. Cada uno viene decorado con una serie de adornos muy peculiares, y el precio del árbol se determina en función de los adornos que tiene.

- *: Copo de nieve - Valor: 1
- o: Bola de Navidad - Valor: 5
- ^: Arbolito decorativo - Valor: 10
- #: Guirnalda brillante - Valor: 50
- @: Estrella polar - Valor: 100
Normalmente se sumarían todos los valores de los adornos y ya está…

Pero, ¡ojo! Si un adorno se encuentra inmediatamente a la izquierda de otro de mayor valor, en lugar de sumar, se resta su valor.

```js
calculatePrice('***')  // 3   (1 + 1 + 1)
calculatePrice('*o')   // 4   (5 - 1)
calculatePrice('o*')   // 6   (5 + 1)
calculatePrice('*o*')  // 5  (-1 + 5 + 1) 
calculatePrice('**o*') // 6  (1 - 1 + 5 + 1) 
calculatePrice('o***') // 8   (5 + 3)
calculatePrice('*o@')  // 94  (-5 - 1 + 100)
calculatePrice('*#')   // 49  (-1 + 50)
calculatePrice('@@@')  // 300 (100 + 100 + 100)
calculatePrice('#@')   // 50  (-50 + 100)
calculatePrice('#@Z')  // undefined (Z es desconocido)
```

```js
// No critiques, estaba jugueteando con los maps :C
// 1 estrella.
function calculatePrice(ornaments) {
  return ornaments.split('').map(x =>{
  switch(x){
    case '*':
      return 1
    case 'o':
      return 5
    case '^':
      return 10
    case '#':
      return 50
    case '@':
      return 100
  }}).map((x,i,arr)=>{
    if (x<arr[i+1]&&i<arr.length-1){
      return -x
    }
    return x
  }).reduce((x,y) =>{
    return x+y
  } ) || undefined
}
```

```js
//5 estrellas
function calculatePrice(ornaments) {
    const values = {
        '*': 1,
        'o': 5,
        '^': 10,
        '#': 50,
        '@': 100
    };

    let total = 0;
    let prevValue = 0;

    for (let char of ornaments) {
        if (!(char in values)) return undefined; 
        let currentValue = values[char];
        
        if (currentValue > prevValue) {
            total -= prevValue;
        } else {
            total += prevValue;
        }
        
        prevValue = currentValue;
    }

    return total + prevValue;
}
```

## Día 13

Los elfos del Polo Norte han creado un robot 🤖 especial que ayuda a Papá Noel a distribuir regalos dentro de un gran almacén. El robot se mueve en un plano 2D y partimos desde el origen (0, 0).

Queremos saber si, tras ejecutar una serie de movimientos, el robot vuelve a estar justo donde empezó.

Las órdenes básicas del robot son:

- L: Mover hacia la izquierda
- R: Mover hacia la derecha
- U: Mover hacia arriba
- D: Mover hacia abajo

Pero también tiene ciertos modificadores para los movimientos:

- *: El movimiento se realiza con el doble de intensidad (ej: *R significa RR)
- !: El siguiente movimiento se invierte (ej: R!L se considera como RR)
- ?: El siguiente movimiento se hace sólo si no se ha hecho antes (ej: R?R significa R)

Nota: Cuando el movimiento se invierte con ! se contabiliza el movimiento invertido y no el original. Por ejemplo, !U?U invierte el movimiento de U, por lo que contabiliza que se hizo el movimiento D pero no el U. Así !U?U se traduce como D?U y, por lo tanto, se haría el movimiento U final.

Debes devolver:

- true: si el robot vuelve a estar justo donde empezó
- [x, y]: si el robot no vuelve a estar justo donde empezó, devolver la posición donde se detuvo

```js
isRobotBack('R')     // [1, 0]
isRobotBack('RL')    // true
isRobotBack('RLUD')  // true
isRobotBack('*RU')   // [2, 1]
isRobotBack('R*U')   // [1, 2]
isRobotBack('LLL!R') // [-4, 0]
isRobotBack('R?R')   // [1, 0]
isRobotBack('U?D')   // true
isRobotBack('R!L')   // [2,0]
isRobotBack('U!D')   // [0,2]
isRobotBack('R?L')   // true
isRobotBack('U?U')   // [0,1]
isRobotBack('*U?U')  // [0,2]
isRobotBack('U?D?U') // true

// Ejemplos paso a paso:
isRobotBack('R!U?U') // [1,0]
// 'R'  -> se mueve a la derecha 
// '!U' -> se invierte y se convierte en 'D'
// '?U' -> se mueve arriba, porque no se ha hecho el movimiento 'U'

isRobotBack('UU!U?D') // [0,1]
// 'U'  -> se mueve arriba
// 'U'  -> se mueve arriba
// '!U' -> se invierte y se convierte en 'D'
// '?D' -> no se mueve, ya que ya se hizo el movimiento 'D'
```

```js
// 3 estrellas
function isRobotBack(moves) {
  const values = {
    'L': [-1,0],
    'R': [1,0],
    'D': [0,-1],
    'U': [0, 1]
  }
  const invert = {
    'L': 'R',
    'R': 'L',
    'U': 'D',
    'D': 'U'
  }
  let pos = [0,0]

  for (let i = 0; i < moves.length; i++){
    let move = moves[i]

    if (move in values){
      pos = pos.map((num, index) => num + values[move][index])
    }
    else{
      if(move === '*'){
      pos = pos.map((num, index) => num + 2*values[moves[i+1]][index])
      }
      else if(move === '!'){
        let nextMove = moves[i+1];
        let invertedMove = invert[nextMove];
        moves = moves.slice(0, i+1) + invertedMove + moves.slice(i+2);
        pos = pos.map((num, index) => num + values[invertedMove][index]);
      }
      else if(move === '?'&& !moves.slice(0, i).includes(moves[i+1])){
        pos = pos.map((num, index) => num + values[moves[i+1]][index])
      }
      i++
    }

     premove = moves[i]
  }

  return pos[0] === 0 && pos[1] === 0 ? true:pos
}
```

```js
// 5 estrellas
function isRobotBack(moves) {
  const values = {
    'L': [-1, 0],
    'R': [1, 0],
    'D': [0, -1],
    'U': [0, 1]
  };
  const invert = {
    'L': 'R',
    'R': 'L',
    'U': 'D',
    'D': 'U'
  };
  let pos = [0, 0];
  let previousMoves = new Set();

  for (let i = 0; i < moves.length; i++) {
    let move = moves[i];

    if (move in values) {
      pos[0] += values[move][0];
      pos[1] += values[move][1];
      previousMoves.add(move);
    } else if (move === '*') {
      i++;
      let nextMove = moves[i];
      if (nextMove in values) {
        pos[0] += 2 * values[nextMove][0];
        pos[1] += 2 * values[nextMove][1];
        previousMoves.add(nextMove);
      }
    } else if (move === '!') {
      i++; 
      let nextMove = moves[i];
      if (nextMove in values) {
        let invertedMove = invert[nextMove];
        pos[0] += values[invertedMove][0];
        pos[1] += values[invertedMove][1];
        previousMoves.add(invertedMove);
      }
    } else if (move === '?') {
      i++;
      let nextMove = moves[i];
      if (nextMove in values && !previousMoves.has(nextMove)) {
        pos[0] += values[nextMove][0];
        pos[1] += values[nextMove][1];
        previousMoves.add(nextMove);
      }
    }
  }

  return pos[0] === 0 && pos[1] === 0 ? true : [pos[0], pos[1]];
}

```

## Día 14

Los renos necesitan moverse para ocupar los establos, pero no puede haber más de un reno por establo. Además, para que los renos estén cómodos, debemos minimizar la distancia total que recorren para acomodarse.

Tenemos dos parámetros:

reindeer: Un array de enteros que representan las posiciones de los renos.
stables: Un array de enteros que representan las posiciones de los establos.
Hay que mover cada reno, desde su posición actual, hasta un establo. Pero hay que tener en cuenta que sólo puede haber un reno por establo.

Tu tarea es calcular el mínimo número de movimientos necesarios para que todos los renos acaben en un establo.

Nota: Ten en cuenta que el array de establos siempre tendrá el mismo tamaño que el array de renos y que siempre los establos serán únicos.

```js
minMovesToStables([2, 6, 9], [3, 8, 5]) // -> 3
// Explicación:
// Renos en posiciones: 2, 6, 9
// Establos en posiciones: 3, 8, 5
// 1er reno: se mueve de la posición 2 al establo en la posición 3 (1 movimiento).
// 2do reno: se mueve de la posición 6 al establo en la posición 5 (1 movimiento)
// 3er reno: se mueve de la posición 9 al establo en la posición 8 (1 movimiento).
// Total de movimientos: 1 + 1 + 1 = 3 movimientos

minMovesToStables([1, 1, 3], [1, 8, 4])
// Explicación:
// Renos en posiciones: 1, 1, 3
// Establos en posiciones: 1, 8, 4
// 1er reno: no se mueve (0 movimientos)
// 2do reno: se mueve de la posición 1 al establo en la posición 4 (3 movimientos)
// 3er reno: se mueve de la posición 3 al establo en la posición 8 (5 movimientos)
// Total de movimientos: 0 + 3 + 5 = 8 movimientos
```


```js
// 4 estrellas
// Pasa los test pero sinceramente no creo que este del todo bien
function minMovesToStables(reindeer, stables) {
  let movs = 0
  for(rein of reindeer){
   let index = 0
   movs += stables.reduce((x,y,i)=>{
      let dif = Math.abs(y-rein)
      if(dif<x){
        index = i
        return dif
      }
      return x

    },Infinity)

   stables.splice(index,1)
  }
  return movs
}
```

```js
// 5 estrellas

function minMovesToStables(reindeer, stables) {
  const used = new Array(stables.length).fill(false);
  let totalMoves = 0;
  
  for (const position of reindeer) {
    let minDistance = Infinity;
    let bestStableIndex = 0;
    
    for (let i = 0; i < stables.length; i++) {
      if (!used[i]) {
        const distance = Math.abs(stables[i] - position);
        if (distance < minDistance) {
          minDistance = distance;
          bestStableIndex = i;
        }
      }
    }
    
    used[bestStableIndex] = true;
    totalMoves += minDistance;
  }
  
  return totalMoves;
}
```

## Día 15

l Polo Norte ha llegado ChatGPT y el elfo Sam Elfman está trabajando en una aplicación de administración de regalos y niños.

Para mejorar la presentación, quiere crear una función drawTable que reciba un array de objetos y lo convierta en una tabla de texto.

La tabla dibujada debe representar los datos del objeto de la siguiente manera:

Tiene una cabecera con el nombre de la columna.
- El nombre de la columna pone la primera letra en mayúscula.
- Cada fila debe contener los valores de los objetos en el orden correspondiente.
- Cada valor debe estar alineado a la izquierda.
- Los campos dejan siempre un espacio a la izquierda.
- Los campos dejan a la derecha el espacio necesario para alinear la caja.

Mira el ejemplo para ver cómo debes dibujar la tabla:

```js
drawTable([
  { name: 'Alice', city: 'London' },
  { name: 'Bob', city: 'Paris' },
  { name: 'Charlie', city: 'New York' }
])
// +---------+-----------+
// | Name    | City      |
// +---------+-----------+
// | Alice   | London    |
// | Bob     | Paris     |
// | Charlie | New York  |
// +---------+-----------+

drawTable([
  { gift: 'Doll', quantity: 10 },
  { gift: 'Book', quantity: 5 },
  { gift: 'Music CD', quantity: 1 }
])
// +----------+----------+
// | Gift     | Quantity |
// +----------+----------+
// | Doll     | 10       |
// | Book     | 5        |
// | Music CD | 1        |
// +----------+----------+
```


```js
function drawTable(data) {
  
  let [key1, key2] = Object.keys(data[0]);
  let max_length1 = Math.max(key1.length, ...data.map(person => person[key1].length));
  let max_length2 = Math.max(key2.length, ...data.map(person => person[key2].length));

  let tb = `+` + `-`.repeat(max_length1 + 2) + `+` + `-`.repeat(max_length2 + 2) + `+`;
  let header = `| ${key1}` + ' '.repeat(max_length1 - key1.length + 1) +
               `| ${key2}` + ' '.repeat(max_length2 - key2.length + 1) + `|\n`;

  let rows = data.map(person => {
    let first = person[key1];
    let second = person[key2];
    
    return `| ${first}` + ' '.repeat(max_length1 - first.length + 1) +
           `| ${second}` + ' '.repeat(max_length2 - second.length + 1) + `|`;
  }).join('\n');

  return tb +'\n'+ header + tb +'\n'+ rows + '\n' + tb;
}
```
