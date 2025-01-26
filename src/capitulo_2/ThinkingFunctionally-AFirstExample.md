[Haz clic aquí para ir al Capítulo 1](../capitulo_1/BecomingFunctional-SeveralQuestions.md)

### Capitulo 2

### Pensando Funcionalmente - Un Primer Ejemplo

En el Capítulo 1, Convertirse en Funcional - Varias Preguntas, repasamos qué es la Programación Funcional (FP), mencionamos algunas ventajas de aplicarla y listamos algunas herramientas que necesitaríamos en JavaScript. Pero ahora dejemos la teoría atrás y comencemos considerando un problema simple y cómo resolverlo de manera funcional.

En este capítulo, haremos lo siguiente:

- Analizar un problema simple y común relacionado con el comercio electrónico.
- Considerar varias formas comunes de resolverlo, con sus defectos asociados.
- Encontrar una manera de resolver el problema viéndolo de manera funcional.
- Idear una solución de orden superior que se pueda aplicar a otros problemas.
- Ver cómo llevar a cabo pruebas unitarias para soluciones funcionales.

En capítulos futuros, volveremos a algunos de los temas mencionados aquí, por lo que no entraremos en demasiados detalles. Simplemente mostraremos cómo la FP puede ofrecer una perspectiva diferente para nuestro problema y dejaremos los detalles más profundos para después. Al trabajar en este capítulo, habrás tenido una primera visión de un problema común y una forma de resolverlo pensando de manera funcional, como preludio para el resto de este libro.

### Nuestro problema: hacer algo solo una vez

Consideremos una situación simple pero común. Has desarrollado un sitio de comercio electrónico; el usuario puede llenar su carrito de compras y, al final, debe hacer clic en un botón de Facturarme para que se le cobre con su tarjeta de crédito. Sin embargo, el usuario no debe hacer clic dos veces (o más), o será facturado varias veces.

La parte de HTML de tu aplicación podría tener algo como esto en algún lugar:

```javascript
<button id="billButton" onclick="billTheUser(some, sales, data)">
  Facturarme
</button>
```

Y, entre los scripts, tendrías algo similar al siguiente código:

```javascript
function billTheUser(some, sales, data) {
  window.alert("Facturando al usuario...");
  // en realidad, facturar al usuario
}
```

Asignar el manejador de eventos directamente en HTML, como lo hice, no es recomendado. Más bien, de manera no intrusiva, deberías asignar el manejador a través del código. ¡Así que haz lo que digo, no lo que hago!

Esta es una explicación muy básica del problema y de tu página web, pero es suficiente para nuestros propósitos. Ahora, vamos a pensar en formas de evitar los clics repetidos en ese botón. ¿Cómo podemos evitar que el usuario haga clic más de una vez? Ese es un problema interesante, con varias posibles soluciones. ¡Empecemos mirando algunas malas soluciones!

¿Cuántas formas se te ocurren para resolver nuestro problema? Repasemos varias soluciones y analicemos su calidad.

### Solución 1 – ¡esperando lo mejor!

¿Cómo podemos resolver el problema? La primera solución podría parecer una broma: no hacer nada, decirle al usuario que no haga clic dos veces, ¡y esperar lo mejor! Tu página podría verse algo así:

![Solution One - Hoping for the best!](./img/solutionOne.png)

Esta es una forma de evadir el problema; he visto varios sitios web que simplemente advierten al usuario sobre los riesgos de hacer clic más de una vez (ver Figura 2.1) y en realidad no hacen nada para prevenir la situación: ¿el usuario fue facturado dos veces? ¡Les advertimos... es su culpa!

Tu solución podría verse simplemente así:

```javascript
<button id="billButton" onclick="billTheUser(some, sales, data)">Facturarme</button>
<b>ADVERTENCIA: ¡HAGA CLIC SOLO UNA VEZ, NO HAGA CLIC DE NUEVO!!</b>
```

Bueno, en realidad esto no es una solución; pasemos a propuestas más serias.
