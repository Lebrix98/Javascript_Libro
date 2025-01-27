[Haz clic aquí para ir al Capítulo 2](./../capitulo_2/ThinkingFunctionally-AFirstExample.md)

# Empezando con Funciones - Un Concepto Central Capítulo 3

El punto que queremos destacar es que una función puede ser asignada a una variable y también puede ser reasignada si se desea. De manera similar, podemos definir funciones en el momento en que se necesitan. Incluso podemos hacer esto sin nombrarlas: al igual que con las expresiones comunes, si se usan solo una vez, entonces no es necesario nombrarlas ni almacenarlas en una variable.

## Un reducer de React-Redux

Podemos ver otro ejemplo que implica la asignación de funciones. Como mencionamos anteriormente en este capítulo, React-Redux funciona enviando acciones que son procesadas por un reducer. Por lo general, el reducer incluye código con un `switch`:

```javascript
function doAction(state = initialState, action) {
  let newState = {};
  switch (action.type) {
    case "CREATE":
      // actualizar el estado, generando newState,
      // dependiendo de los datos de la acción
      // para crear un nuevo elemento
      return newState;
    case "DELETE":
      // actualizar el estado, generando newState,
      // después de eliminar un elemento
      return newState;
    case "UPDATE":
      // actualizar un elemento,
      // y generar un estado actualizado
      return newState;
    default:
      return state;
  }
}
```

Proporcionar `initialState` como un valor predeterminado para `state` es una forma simple de inicializar el estado global la primera vez. No prestes atención a ese `default`; no es relevante para nuestro ejemplo, pero lo incluí solo por completitud.

Al aprovechar la posibilidad de almacenar funciones, podemos construir una tabla de despacho y simplificar el código anterior. Primero, inicializamos un objeto con el código de las funciones para cada tipo de acción.

```javascript
const dispatchTable = {
  CREATE: (state, action) => {
    // actualizar el estado, generando newState,
    // dependiendo de los datos de la acción
    // para crear un nuevo elemento
    return newState;
  },
  DELETE: (state, action) => {
    // actualizar el estado, generando newState,
    // después de eliminar un elemento
    return newState;
  },
  UPDATE: (state, action) => {
    // actualizar un elemento,
    // y generar un estado actualizado
    return newState;
  },
};
```

Almacenamos las diferentes funciones que procesan cada tipo de acción como atributos en un objeto que funcionará como una tabla de despacho. Este objeto se crea solo una vez y es constante durante la ejecución de la aplicación. Con él, ahora podemos reescribir el código de procesamiento de acciones en una sola línea de código:

```javascript
function doAction2(state = initialState, action) {
  return dispatchTable[action.type]
    ? dispatchTable[action.type](state, action)
    : state;
}
```

Analicémoslo: dada la acción, si `action.type` coincide con un atributo en el objeto de despacho, ejecutamos la función correspondiente tomada del objeto donde se almacenó. Si no hay coincidencia, simplemente devolvemos el estado actual como requiere Redux. Este tipo de código no sería posible si no pudiéramos manejar funciones (almacenarlas y recordarlas) como objetos de primera clase.

[ 57 ]

## Un error innecesario

Sin embargo, hay un error común (aunque de hecho, inofensivo) que suele cometerse. A menudo se ve código como este:

```javascript
fetch("some/remote/url").then(function (data) {
  processResult(data);
});
```

¿Qué hace este código? La idea es que se obtiene una URL remota, y cuando llegan los datos, se llama a una función, y esta función a su vez llama a `processResult` con `data` como argumento. Es decir, en la parte `then()`, queremos una función que, dado `data`, calcule `processResult(data)`. Pero, ¿no tenemos ya tal función?

Un poco de teoría: en términos de cálculo lambda, estamos reemplazando `λx.func x` con simplemente `func`. Esto se llama una conversión eta, o más específicamente, una reducción eta. (Si lo hicieras al revés, sería una abstracción eta). En nuestro caso, podría considerarse una (¡muy, muy pequeña!) optimización, pero su principal ventaja es un código más corto y compacto.

Básicamente, hay una regla que puedes aplicar cada vez que veas algo como lo siguiente:

```javascript
function someFunction(someData) {
  return someOtherFunction(someData);
}
```

Esta regla establece que puedes reemplazar el código que se asemeja al anterior con solo `someOtherFunction`. Entonces, en nuestro ejemplo, podemos escribir directamente lo siguiente:

```javascript
fetch("some/remote/url").then(processResult);
```

Este código es exactamente equivalente al método anterior que vimos (aunque es infinitesimalmente más rápido, ya que evitas una llamada a función), pero ¿es más simple de entender? Este estilo de programación se llama estilo pointfree o estilo tácito, y su principal característica es que nunca especificas los argumentos para cada aplicación de función. Una ventaja de esta forma de codificar es que ayuda al escritor (y a los futuros lectores del código) a pensar en las funciones mismas y sus significados en lugar de trabajar a un nivel bajo, pasando datos y trabajando con ellos. En la versión más corta del código, no hay detalles extraños o irrelevantes: si entiendes lo que hace la función llamada, entonces entiendes el significado de la pieza completa de código. En nuestro texto, a menudo (pero no necesariamente siempre) trabajaremos de esta manera.

[ 58 ]

Los usuarios de Unix/Linux ya pueden estar acostumbrados a este estilo, porque trabajan de manera similar cuando usan tuberías para pasar el resultado de un comando como entrada a otro. Cuando escribes algo como `ls|grep doc|sort`, la salida de `ls` es la entrada de `grep`, y la salida de este último es la entrada de `sort`, pero los argumentos de entrada no se escriben en ningún lugar; están implícitos. Volveremos a esto en la sección Estilo Pointfree del Capítulo 8, Conectando Funciones - Tuberías y Composición.

## Trabajando con métodos

Sin embargo, hay un caso del que debes estar consciente: ¿qué sucede si estás llamando a un método de un objeto? Mira el siguiente código:

```javascript
fetch("some/remote/url").then(function (data) {
  myObject.store(data);
});
```

Si tu código original hubiera sido algo como el anterior, entonces el código transformado aparentemente obvio fallaría:

```javascript
fetch("some/remote/url").then(myObject.store);
```

¿Por qué? La razón es que en el código original, el método llamado está vinculado a un objeto (`myObject`), pero en el código modificado, no está vinculado y es solo una función libre. Podemos arreglarlo de manera simple usando `bind()`, de la siguiente manera:

```javascript
fetch("some/remote/url").then(myObject.store.bind(myObject));
```

Esta es una solución general. Cuando se trata de un método, no puedes simplemente asignarlo; debes usar `bind()` para que el contexto correcto esté disponible. Mira el siguiente código:

```javascript
function doSomeMethod(someData) {
  return someObject.someMethod(someData);
}
```

Siguiendo esta regla, el código como el anterior debería convertirse en lo siguiente:

```javascript
const doSomeMethod = someObject.someMethod.bind(someObject);
```

Lee más sobre `bind()` en https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind.

[ 59 ]

Esto parece bastante incómodo y no muy elegante, pero es necesario para que el método esté asociado con el objeto correcto. Veremos una aplicación de esto cuando promisifiquemos funciones en el Capítulo 6, Produciendo Funciones - Funciones de Orden Superior. Incluso si este código no es tan agradable a la vista, cada vez que tengas que trabajar con objetos (y recuerda, no dijimos que intentaríamos apuntar a un código completamente FP, y dijimos que aceptaríamos otras construcciones si facilitaban las cosas), tendrás que recordar vincular métodos antes de pasarlos como objetos de primera clase en estilo pointfree.

## Usando funciones de manera FP

Hay varios patrones de codificación comunes que en realidad aprovechan el estilo FP, incluso si no eras consciente de ello. En esta sección, los revisaremos y veremos los aspectos funcionales del código para que puedas acostumbrarte más a este estilo de codificación.

Luego, veremos en detalle el uso de funciones de manera FP considerando varias técnicas FP, como las siguientes:

- Inyección, que es necesaria para ordenar diferentes estrategias, así como otros usos
- Callbacks y promesas, introduciendo el estilo de paso de continuaciones
- Polyfilling y stubbing
- Esquemas de invocación inmediata

### Inyección - ordenándolo

El primer ejemplo de pasar funciones como parámetros es proporcionado por el método `Array.prototype.sort()`. Si tienes un array de cadenas y quieres ordenarlo, puedes simplemente usar el método `sort()`. Por ejemplo, para ordenar alfabéticamente un array con los colores del arcoíris, escribiríamos algo como lo siguiente:

```javascript
var colors = ["violet", "indigo", "blue", "green", "yellow", "orange", "red"];
colors.sort();
console.log(colors);
// ["blue", "green", "indigo", "orange", "red", "violet", "yellow"]
```

[ 60 ]

Nota que no tuvimos que proporcionar ningún parámetro a la llamada `sort()`, pero el array se ordenó perfectamente bien. Por defecto, este método ordena las cadenas según su representación interna ASCII. Entonces, si usas este método para ordenar un array de números, fallará, ya que decidirá que 20 debe estar entre 100 y 3, porque 100 precede a 20 (tomados como cadenas) y este último precede a 3, ¡así que esto necesita arreglarse! El siguiente código muestra el problema:

```javascript
var someNumbers = [3, 20, 100];
someNumbers.sort();
console.log(someNumbers);
// [100, 20, 3]
```

Pero olvidémonos de los números por un momento y sigamos ordenando cadenas. Queremos preguntarnos qué pasaría si quisiéramos ordenar algunas palabras en español (palabras) pero siguiendo las reglas de localización apropiadas. Estaríamos ordenando cadenas, pero los resultados no serían correctos:

```javascript
var palabras = ["ñandú", "oasis", "mano", "natural", "mítico", "musical"];
palabras.sort();
console.log(palabras);
// ["mano", "musical", "mítico", "natural", "oasis", "ñandú"] -- ¡resultado incorrecto!
```

Para los aficionados al idioma o la biología, "ñandú" en inglés es rhea, un ave corredora algo similar a los avestruces. ¡No hay muchas palabras en español que comiencen con ñ, y resulta que tenemos estas aves en mi país, Uruguay, así que esa es la razón de la palabra extraña!

¡Ups! En español, ñ viene entre n y o, pero "ñandú" se ordenó al final. Además, "mítico" (en inglés, mythical; nota la í acentuada) debería aparecer entre "mano" y "musical" porque la tilde debería ignorarse. La forma apropiada de resolver esto es proporcionando una función de comparación a `sort()`. En este caso, podemos usar el método `localeCompare()` de la siguiente manera:

```javascript
palabras.sort((a, b) => a.localeCompare(b, "es"));
console.log(palabras);
// ["mano", "mítico", "musical", "natural", "ñandú", "oasis"]
```

La llamada `a.localeCompare(b,"es")` compara las cadenas `a` y `b` y devuelve un valor negativo si `a` precede a `b`, un valor positivo si `a` sigue a `b`, y 0 si `a` y `b` son iguales, pero según las reglas de ordenación en español ("es").

[ 61 ]

¡Ahora las cosas están bien! Y el código podría hacerse más claro introduciendo una nueva función, `spanishComparison()`, para realizar la comparación de cadenas requerida:

```javascript
const spanishComparison = (a, b) => a.localeCompare(b, "es");
palabras.sort(spanishComparison);
// ordena el array palabras según las reglas del español:
// ["mano", "mítico", "musical", "natural", "ñandú", "oasis"]
```

En los próximos capítulos, discutiremos cómo FP te permite escribir código de una manera más declarativa, produciendo un código más comprensible, y este tipo de pequeño cambio ayuda: cuando los lectores del código llegan al `sort`, deducirán inmediatamente lo que se está haciendo, incluso si el comentario no estuviera presente.

Esta forma de cambiar la forma en que funciona la función `sort()` inyectando diferentes funciones de comparación es en realidad un caso del patrón de diseño de estrategia. Aprenderemos más sobre esto en el Capítulo 11, Implementando Patrones de Diseño - La Manera Funcional.

Proporcionar una función de ordenación como parámetro (¡de una manera muy FP!) también puede ayudar con varios otros problemas, como los siguientes:

- `sort()` solo funciona con cadenas. Si quieres ordenar números (como intentamos hacer anteriormente), debes proporcionar una función que compare numéricamente. Por ejemplo, escribirías algo como `myNumbers.sort((a,b) => a-b)`.
- Si quieres ordenar objetos por un atributo dado, usarás una función que compare con él. Por ejemplo, podrías ordenar personas por edad con algo como `myPeople.sort((a,b) => a.age - b.age)`.

Para más información sobre las posibilidades de `localeCompare()`, consulta https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare. Puedes especificar qué reglas de localización aplicar, en qué orden colocar letras mayúsculas/minúsculas, si ignorar la puntuación y mucho más. Pero ten cuidado: no todos los navegadores pueden admitir los parámetros adicionales requeridos.

Este es un ejemplo simple que probablemente has usado antes, pero es un patrón FP, después de todo. Pasemos a un uso aún más común de funciones como parámetros cuando realizas llamadas Ajax.

[ 62 ]

## Callbacks, promesas y continuaciones

Probablemente el ejemplo más utilizado de funciones pasadas como objetos de primera clase tiene que ver con callbacks y promesas. En Node, leer un archivo se logra de manera asíncrona con algo como el siguiente código:

```javascript
const fs = require("fs");
fs.readFile("someFile.txt", (err, data) => {
  if (err) {
    console.error(err); // o lanzar un error, o manejar el problema de otra manera
  } else {
    console.log(data.toString()); // hacer algo con los datos
  }
});
```

La función `readFile()` requiere un callback, en este ejemplo una función anónima, que se llamará cuando se complete la operación de lectura del archivo.

Una mejor manera es usar promesas; lee más en https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise. Con esto, al realizar una llamada a un servicio web Ajax usando la función más moderna `fetch()`, podrías escribir algo como lo siguiente:

```javascript
fetch("some/remote/url")
  .then((data) => {
    // Hacer algún trabajo con los datos devueltos
  })
  .catch((error) => {
    // Procesar todos los errores aquí
  });
```

Nota que si hubieras definido las funciones apropiadas `processData(data)` y `processError(error)`, el código podría haberse acortado a `fetch("some/remote/url").then(processData).catch(processError)` siguiendo las líneas que vimos anteriormente.

Finalmente, también deberías considerar usar `async/await`; lee más sobre esto en https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function y https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await.

[Haz clic aquí para ir al Capítulo 4](./../capitulo_4/Behaving_Properly-Pure_Functions.md)
