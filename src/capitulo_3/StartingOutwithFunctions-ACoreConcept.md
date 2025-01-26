# Iniciando con Funciones - Un Concepto Fundamental

## Introducción
En el Capítulo 2 (Pensando Funcionalmente - Un Primer Ejemplo) revisamos un ejemplo de pensamiento de Programación Funcional (FP), pero ahora veremos los fundamentos y revisaremos las funciones. En el Capítulo 1 mencionamos que dos características importantes de JavaScript eran las funciones: objetos de primera clase y closures.

## Temas a Cubrir
1. Funciones en JavaScript, incluyendo cómo definirlas, con enfoque particular en funciones flecha
2. Currying y funciones como objetos de primera clase
3. Varias formas de usar funciones al estilo FP

## Todo Sobre Funciones
Iniciemos con una breve revisión de funciones en JavaScript y su relación con conceptos de FP.

### Lambdas y Funciones
En términos de cálculo lambda, una función puede verse como `λx.2*x`. La interpretación es que:
- La variable después del carácter λ es el parámetro de la función
- La expresión después del punto es donde reemplazarías el valor pasado como argumento

### Nota sobre Parámetros vs Argumentos

Nemotécnico: Parámetros son Potenciales, Argumentos son Actuales.

Parámetros: placeholders para valores potenciales
Argumentos: valores actuales pasados a la función

### Aplicación de Funciones
- Aplicar una función significa proveer un argumento actual
- Se escribe usando paréntesis
- Ejemplo: `(λx.2*x)(3)` se calcularía como `6`

### Definición de Funciones en JavaScript
Existen múltiples formas de definir funciones, y no todas tienen el mismo significado. Para más información sobre las diferentes formas de definir funciones, métodos y más, puedes consultar "The Many Faces of Functions in JavaScript" por Leo Balter y Rick Waldron en `https://bocoup.com/blog/the-many-faces-of-functions-in-javascript`.