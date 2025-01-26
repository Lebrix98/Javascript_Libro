## Capítulo 1

## Becoming Functional - Several Questions

La programación funcional (o PF) ha existido desde los primeros días de la computación y está pasando por una especie de renacimiento debido a su mayor uso con varios marcos y bibliotecas, especialmente en JavaScript (JS). En este capítulo, haremos lo siguiente:

- Introducir algunos conceptos de la PF para dar una pequeña muestra de lo que significa.
- Mostrar los beneficios (y problemas) que implica el uso de la PF y por qué deberíamos usarla.
- Comenzar a pensar por qué JavaScript puede considerarse un lenguaje apropiado para la PF.
- Repasar las características y herramientas del lenguaje que deberías conocer para aprovechar al máximo todo lo que se presenta en este libro.

Al final de este capítulo, tendrás las herramientas básicas que usaremos en el resto del libro, así que comencemos aprendiendo sobre programación funcional.

### Teoría versus práctica

En este libro, no abordaremos la PF de manera teórica. En cambio, nuestro objetivo es mostrarte cómo algunas de sus técnicas y principios pueden aplicarse con éxito a la programación común y diaria en JavaScript. Pero—y esto es importante—no lo haremos de manera dogmática, sino de una forma muy práctica. No descartaremos constructos útiles de JavaScript simplemente porque no cumplan con las expectativas académicas de la PF. Igualmente, no evitaremos características prácticas de JavaScript solo para encajar en el paradigma de la PF. De hecho, podríamos decir que estaremos haciendo **Programación Funcional Sorta** (SFP), ya que nuestro código será una mezcla de características de la PF, las clásicas imperativas y la programación orientada a objetos (OOP).

Ten cuidado, sin embargo: lo que acabamos de decir no significa que dejaremos toda la teoría a un lado. Seremos selectivos y tocaremos los puntos teóricos principales, aprenderemos algo de vocabulario y definiciones, y explicaremos los conceptos clave de la PF, pero siempre manteniendo en vista la idea de producir un código útil de JavaScript real, en lugar de intentar cumplir con algún criterio místico y dogmático de la PF.

OOP ha sido una forma de resolver la complejidad inherente a la escritura de programas y sistemas grandes, y desarrollar arquitecturas de aplicaciones limpias, extensibles y escalables. Sin embargo, debido a la escala de las aplicaciones web actuales, la complejidad de todos los códigos sigue creciendo. Además, las nuevas características de JavaScript hacen posible desarrollar aplicaciones que ni siquiera habrían sido posibles hace algunos años; piensa en las aplicaciones móviles (híbridas) hechas con Ionic, Apache Cordova o React Native, o aplicaciones de escritorio hechas con Electron o NW.js, por ejemplo. JavaScript también ha migrado al backend con Node.js, por lo que hoy el alcance de uso del lenguaje ha crecido de una manera seria, abarcando toda la complejidad añadida de los diseños modernos.

### Un enfoque diferente

La programación funcional es una forma diferente de escribir programas, y a veces puede ser difícil de aprender. En la mayoría de los lenguajes, la programación se realiza de manera imperativa: un programa es una secuencia de declaraciones, ejecutadas de manera prescrita, y el resultado deseado se logra creando objetos y manipulándolos, lo que generalmente significa modificar los objetos en sí mismos. La PF se basa en producir el resultado deseado evaluando expresiones construidas a partir de funciones que se componen entre sí. En la PF, es común pasar funciones de un lado a otro (como pasar parámetros a otras funciones o devolver funciones como resultado de un cálculo), no usar bucles (optando por recursión en su lugar), y evitar efectos secundarios (como modificar objetos o variables globales).

En otras palabras, la PF se enfoca en qué se debe hacer, más que en cómo hacerlo. En lugar de preocuparse por bucles o arreglos, se trabaja en un nivel más alto, considerando lo que debe hacerse. Después de acostumbrarte a este estilo, verás que tu código se vuelve más simple, corto y elegante, y será fácil de probar y depurar. Sin embargo, no caigas en la trampa de considerar que la PF es el objetivo. Piensa en la PF solo como un medio para un fin, como con todas las herramientas de software. El código funcional no es bueno solo por ser funcional, y escribir código malo es tan posible con PF como con cualquier otra técnica.

---

### Qué no es la programación funcional

Dado que hemos mencionado algunas cosas sobre lo que es la PF, también aclaremos algunos malentendidos comunes y veamos lo que NO es la PF:

- **La PF no es solo una cosa académica:** Es cierto que el cálculo lambda, sobre el cual se basa la PF, fue desarrollado por Alonzo Church en 1936 como una herramienta para probar un resultado importante en la teoría de la computación (¡más de 20 años antes de los lenguajes de programación modernos!). Sin embargo, los lenguajes de PF se están utilizando hoy en día para todo tipo de sistemas.

- **La PF no es lo opuesto a la programación orientada a objetos (OOP):** No se trata de elegir entre programación declarativa o imperativa. Puedes mezclar y combinar como más te convenga, y eso es lo que haremos a lo largo de este libro, reuniendo lo mejor de todos los mundos.

- **La PF no es excesivamente compleja de aprender:** Algunos de los lenguajes de PF son bastante diferentes de JavaScript, pero las diferencias son principalmente sintácticas. Una vez que aprendas los conceptos básicos, verás que puedes obtener los mismos resultados en JavaScript que con los lenguajes de PF.

También es relevante mencionar que varios marcos modernos, como la combinación React y Redux, incluyen ideas de PF.

Si retrocedemos en la historia de la computación, encontraremos que el segundo lenguaje de programación más antiguo que todavía se usa, Lisp, se basa en la PF. Desde entonces, ha habido muchos más lenguajes funcionales, y la PF ha sido aplicada de manera más amplia. Pero aun así, si le preguntas a la gente qué es la PF, probablemente recibirás dos respuestas muy diferentes. Por ejemplo, en React, se dice que la vista (lo que el usuario ve en un momento dado) es una función del estado actual. Usas una función para calcular qué HTML y CSS deben producirse en cada momento, pensando de manera "caja negra". De manera similar, en Redux tienes el concepto de acciones que son procesadas por reductores. Una acción proporciona algunos datos, y un reductor es una función que produce el nuevo estado de la aplicación de manera funcional a partir del estado actual y los datos proporcionados.

Así que, tanto por las ventajas teóricas (de las cuales hablaremos en la siguiente sección) como por las prácticas (como el hecho de que podemos usar los marcos y bibliotecas más recientes), tiene sentido considerar la programación funcional. Vamos a ello.

### ¿Por qué usar PF?

A lo largo de los años, ha habido muchos estilos y modas en la programación. Sin embargo, la PF ha demostrado ser bastante resistente y es de gran interés hoy en día. ¿Por qué querrías usar la PF? La pregunta debería ser primero: ¿qué quieres conseguir? Y solo después, ¿la PF te lleva allí? Vamos a responder estas importantes preguntas en las siguientes secciones.

#### Lo que necesitamos

Podemos estar de acuerdo en que la siguiente lista de preocupaciones es universal. Nuestro código debe tener las siguientes cualidades:

- **Modular:** La funcionalidad de tu programa debe dividirse en módulos independientes, cada uno de los cuales contiene lo necesario para realizar un aspecto de la funcionalidad del programa. Los cambios en un módulo o función no deberían afectar al resto del código.
- **Comprensible:** Un lector de tu programa debería poder discernir sus componentes, sus funciones y sus relaciones sin un esfuerzo indebido. Esto está estrechamente relacionado con el mantenimiento del código; tu código tendrá que ser mantenido en algún momento, ya sea para ser cambiado o para añadir nueva funcionalidad.
- **Testable (probable de probar):** Las pruebas unitarias intentan comprobar pequeñas partes de tu programa, verificando su comportamiento independientemente del resto del código. Tu estilo de programación debe favorecer escribir código que simplifique la tarea de escribir pruebas unitarias.
- **Extensible:** Es un hecho que tu programa algún día requerirá mantenimiento, posiblemente para añadir nueva funcionalidad. Esos cambios deberían impactar la estructura y el flujo de datos del código original lo mínimo posible (si es que lo hacen).
- **Reutilizable:** La reutilización del código tiene como objetivo ahorrar recursos, tiempo y dinero, y reducir la redundancia aprovechando el código ya escrito. Hay algunas características que ayudan a lograr este objetivo, como la modularidad (que ya hemos mencionado), la alta cohesión (todas las piezas en un módulo pertenecen juntas), el bajo acoplamiento (los módulos son independientes entre sí), la separación de preocupaciones (las partes de un programa deben superponerse en funcionalidad lo menos posible) y el ocultamiento de información (los cambios internos de un módulo no deberían afectar al resto del sistema).

---

### Lo que conseguimos

Entonces, ¿la programación funcional (PF) te da las cinco características que acabamos de listar en la sección anterior?

En la PF, el objetivo es escribir funciones independientes y separadas que se unen para producir los resultados finales.

Los programas que se escriben en un estilo funcional generalmente tienden a ser más limpios, más cortos y más fáciles de entender.

Las funciones pueden ser probadas de forma independiente, y el código en PF tiene ventajas al lograr esto.

Puedes reutilizar funciones en otros programas porque son independientes, no dependen del resto del sistema. La mayoría de los programas funcionales comparten funciones comunes, varias de las cuales consideraremos en este libro.

El código funcional está libre de efectos secundarios, lo que significa que puedes entender el objetivo de una función al estudiarla sin tener que considerar el resto del programa.

Finalmente, una vez que te acostumbras al estilo de programación funcional, el código se vuelve más comprensible y más fácil de extender. ¡Así que parece que las cinco características pueden lograrse con PF!

---

### No todo es oro

Sin embargo, busquemos un poco de balance. Usar PF no es una bala de plata que mágicamente hará que tu código sea mejor. Algunas soluciones de PF son realmente complicadas, y hay desarrolladores que disfrutan mucho escribir código y luego preguntar, ¿qué hace esto? Si no tienes cuidado, tu código puede volverse "solo escribible" y prácticamente imposible de mantener; ahí se van la comprensibilidad, extensibilidad y reutilización.

Otra desventaja es que puede ser más difícil encontrar desarrolladores con experiencia en PF. (Pregunta rápida: ¿cuántos anuncios de trabajo para programadores funcionales has visto?) La gran mayoría del código web actual está escrito de manera imperativa y no funcional, y la mayoría de los programadores están acostumbrados a esa forma de trabajar. Para algunos, tener que cambiar de mentalidad y comenzar a escribir programas de una manera diferente puede resultar una barrera insuperable.

Finalmente, si intentas hacer todo completamente funcional, puedes encontrarte en desacuerdo con JavaScript, y las tareas simples pueden volverse más difíciles de lo esperado. Como dijimos al principio, optaremos por un enfoque de **Sorta FP**, por lo que no rechazaremos drásticamente ninguna característica del lenguaje que no sea 100% funcional. Después de todo, queremos usar PF para simplificar nuestro código, ¡no para hacerlo más complejo!

Así que, aunque me esforzaré por mostrarte las ventajas de hacer tu código más funcional, como con cualquier cambio, siempre habrá algunas dificultades. Sin embargo, estoy completamente convencido de que podrás superarlas y que tu organización desarrollará mejor código aplicando PF. ¡Atrévete a cambiar!

### ¿Es JavaScript funcional?

En este punto, hay otra pregunta importante que deberías estar haciéndote: ¿Es JavaScript un lenguaje funcional?

Por lo general, cuando se piensa en la programación funcional (PF), la lista de lenguajes que se menciona no incluye a JavaScript, pero sí a opciones menos comunes, como Clojure, Erlang, Haskell y Scala; sin embargo, no existe una definición precisa para los lenguajes funcionales ni un conjunto exacto de características que dichos lenguajes deberían incluir. 

El punto principal es que puedes considerar un lenguaje como funcional si soporta el estilo común de programación asociado con la PF. Empecemos por aprender por qué querríamos usar JavaScript y cómo el lenguaje ha evolucionado hasta su versión actual, para luego ver algunas de las características clave que utilizaremos para trabajar de manera funcional.


# Volviéndose funcional con JavaScript

JavaScript ha evolucionado a través de los años, y la versión que usaremos es (informalmente) llamada JS10, y (formalmente) ECMAScript 2019, generalmente abreviada como ES2019 o ES10; esta versión fue finalizada en junio de 2019. Las versiones anteriores fueron las siguientes:

ECMAScript 1, junio 1997

ECMAScript 2, junio 1998, que era básicamente igual que la versión anterior

ECMAScript 3, diciembre 1999, con varias funcionalidades nuevas

ECMAScript 5, diciembre 2009 (y no, nunca hubo un ECMAScript 4, porque fue abandonado)

ECMAScript 5.1, junio 2011

ECMAScript 6 (o ES6; posteriormente renombrado ES2015), junio 2015

ECMAScript 7 (también ES7, o ES2016), junio 2016

ECMAScript 8 (ES8 o ES2017), junio 2017

ECMAScript 9 (ES9 o ES2018), junio 2018

ECMAScript 10 (ES10 o ES2019), junio 2019

ECMAScript 11 (ES11 o ES2020), junio 2020

ECMAScript 12 (ES12 o ES2021), junio 2021

ECMAScript 13 (ES13 o ES2022), junio 2022

ECMAScript 14 (ES14 o ES2023), junio 2023

ECMAScript 15 (ES15 o ES2024), junio 2024

ECMA originalmente significaba European Computer Manufacturers Association, pero hoy en día el nombre no se considera más un acrónimo. La organización es responsable de más estándares además de JavaScript, incluyendo JSON, C#, Dart, y otros. Para más detalles, visite su sitio en www.ecma-international.org/.

Puede leer la especificación estándar del lenguaje en www.ecma-international.org/ecma-262/7.0/. Cuando nos referimos a JavaScript en el texto sin más especificación, ES10 (ES2019) es a lo que nos referimos; sin embargo, en términos de las características del lenguaje que se utilizan en el libro, si solo usara ES2015, entonces mayormente no tendría problemas con este libro.


### Características clave de JavaScript

JavaScript no es un lenguaje puramente funcional, pero tiene todas las características que necesitamos para que funcione como si lo fuera. Las características principales del lenguaje que utilizaremos son las siguientes:

- Funciones como objetos de primer nivel
- Recursión
- Funciones flecha
- Cerraduras (Closures)
- Spread

Veamos algunos ejemplos de cada una de estas características y descubramos por qué serán útiles para nosotros. Ten en cuenta, sin embargo, que hay más características de JavaScript que utilizaremos; las secciones siguientes solo destacan las más importantes en términos de lo que vamos a usar para la programación funcional.

---

#### Funciones como objetos de primer nivel (Ordeden Superior)

Decir que las funciones son **objetos de primer nivel** (también llamadas **ciudadanos de primer nivel**) significa que puedes hacer todo con las funciones que puedes hacer con otros objetos. Por ejemplo, puedes almacenar una función en una variable, pasarla a otra función, imprimirla, entre otros.

Esto es realmente clave para hacer programación funcional; a menudo estaremos pasando funciones como parámetros (a otras funciones) o devolviendo una función como el resultado de una llamada a función.

Este fragmento explica cómo se usan los **callbacks** en las llamadas Ajax, un concepto clave en JavaScript para manejar operaciones asíncronas. También muestra un ejemplo usando jQuery.

```javascript
$.get("some/url", someData, function(result, status) {
  // Verificar el estado, y hacer algo
  // con el resultado
});
```

La función `$.get()` recibe una función de **callback** como parámetro y la llama después de que se obtiene el resultado.

Dado que las funciones pueden almacenarse en variables, también podrías escribir algo como lo siguiente. Presta atención a cómo usamos la variable `doSomething` en la llamada a `$.get(...)`:

```javascript
var doSomething = function(result, status) {
  // Verificar el estado, y hacer algo
  // con el resultado
};

$.get("some/url", someData, doSomething);
```

# Recursión

La recursión es la herramienta más potente para desarrollar algoritmos y una gran ayuda para resolver grandes clases de problemas. La idea es que una función puede, en cierto punto, llamarse a sí misma, y cuando esa llamada termina, continuar trabajando con cualquier resultado que haya recibido. Esto suele ser bastante útil para ciertas clases de problemas o definiciones. El ejemplo más citado es la función factorial (el factorial de n se escribe como n!) según se define para valores enteros no negativos:

Si n es 0, entonces n! = 1

Si n es mayor que 0, entonces n! = n * (n-1)!

```javascript
function fact(n) {
if (n === 0) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
}
console.log(fact(5)); // 120
```

La recursión será una gran ayuda para el diseño de algoritmos. Al usar la recursión, se puede prescindir de los bucles while o for. No es que queramos hacerlo, pero es interesante que podamos hacerlo. Dedicaremos la totalidad del Capítulo 9, Diseño de funciones: recursión, a diseñar algoritmos y escribir funciones de forma recursiva.


# Closures

Los closures son una forma de implementar el ocultamiento de datos (con variables privadas), lo que conduce a módulos y otras características interesantes. El concepto clave de los closures es que cuando defines una función, esta puede referirse no solo a sus propias variables locales, sino también a todo lo que está fuera del contexto de la función. Podemos escribir una función de conteo que mantendrá su propio contador mediante un closure:

```javascript
function newCounter() {
   let count = 0; // ambito lexico
   return function() {
       count++;
       return count;
   };
}

const nc = newCounter();
console.log(nc()); // 1
console.log(nc()); // 2
console.log(nc()); // 3
```

> *Documentación de Closures y Callbacks en JavaScript*
> 
> *Un closure es una función que mantiene acceso a variables de su scope exterior incluso después de que la función que la contiene haya terminado de ejecutarse. Los closures son fundamentales para la encapsulación de datos y la creación de funciones con estado.*
>
> *Ejemplo de un closure:*
> ```javascript
> function crearGestorCarrito() {
>     let items = [];
>     let descuentoActivo = null;
>     
>     return {
>         agregarProducto: function(producto) {
>             items.push({
>                 id: producto.id,
>                 nombre: producto.nombre,
>                 precio: producto.precio,
>                 cantidad: 1
>             });
>         },
>         calcularTotal: function() {
>             return items.reduce((total, item) => 
>                 total + (item.precio * item.cantidad), 0);
>         }
>     };
> }
> ```
>
> *Un callback, por otro lado, es una función que se pasa como argumento a otra función para ser ejecutada en un momento posterior. Los callbacks son esenciales para manejar operaciones asíncronas.*
>
> *Ejemplo de un callback:*
> ```javascript
> function descargarDatos(callback) {
>     setTimeout(() => {
>         const datos = { usuario: 'Juan' };
>         callback(datos);
>     }, 1000);
> }
> ```





[Haz clic aquí para ir al Capítulo 2](./../capitulo_2/ThinkingFunctionally-AFirstExample.md)