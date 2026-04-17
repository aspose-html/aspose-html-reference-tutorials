---
category: general
date: 2026-03-26
description: Ejemplo de top‑level await que muestra await delay en JavaScript, clase
  de contador incremental y campos de clase públicos en JavaScript en una demo en
  vivo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: es
og_description: Ejemplo de top‑level await que muestra await delay en JavaScript,
  una clase de contador incremental y campos de clase públicos en JavaScript en un
  tutorial conciso.
og_title: Ejemplo de await de nivel superior – Usando await delay en JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Ejemplo de await de nivel superior – Usando await delay en JavaScript
url: /es/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ejemplo de top level await – Usando await delay en JavaScript

¿Alguna vez te has preguntado cómo pausar la ejecución de un módulo sin envolver todo en una IIFE async? Eso es exactamente lo que permite un **ejemplo de top level await**. En este tutorial recorreremos una pequeña página web que usa `await delay javascript` para diferir el trabajo, y luego crea una `increment counter class` que aprovecha **public class fields javascript**. Al final tendrás un fragmento completo, listo para copiar y pegar, que se ejecuta en cualquier navegador moderno.

Cubriremos todo, desde definir una clase con un campo público hasta conectar un sencillo helper de retraso basado en promesas. Sin bibliotecas externas, sin paso de compilación—solo HTML puro, un `<script type="module">` y las características más recientes de ECMAScript. Si ya te sientes cómodo con funciones async, verás por qué top‑level await se siente como una extensión natural. Si eres nuevo en la sintaxis de **javascript class public field**, no te preocupes—explicamos el porqué de cada línea.

## Lo que aprenderás

- Cómo funciona un **ejemplo de top level await** dentro de un script de módulo.
- El patrón para un helper `await delay javascript` que imita `setTimeout` con promesas.
- Cómo escribir una **increment counter class** que usa un campo público (`count`) y un bloque de inicialización estático.
- Salida esperada en la consola y cómo verificar que el bloque estático se ejecuta antes que el resto del script.
- Consejos para solucionar problemas comunes, como navegadores antiguos que no soportan top‑level await.

> **Consejo profesional:** Los navegadores modernos (Chrome 106+, Firefox 102+, Edge 106+) ya soportan top‑level await. Si necesitas soportar entornos más antiguos, considera empaquetar con una herramienta como Vite o Babel.

## Paso 1 – Definir una clase con un campo público y un bloque estático

La primera pieza de nuestra demo es una clase que almacena un contador numérico. Observa la línea `count = 0;`—esta es la sintaxis de **public class fields javascript** introducida en ES2022. Crea una propiedad de instancia sin un constructor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**¿Por qué un bloque estático?** Permite ejecutar lógica de inicialización única (como registro) en el momento en que se analiza el módulo, *antes* de que se ejecute cualquier top‑level await. Esto garantiza que el mensaje aparezca primero en la consola, demostrando que la clase se evaluó temprano.

## Paso 2 – Crear un helper `await delay javascript`

A continuación necesitamos una pequeña función de retraso basada en promesas. Es esencialmente un contenedor alrededor de `setTimeout`, pero devolver una promesa la hace awaitable.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Caso límite:** Si `ms` es negativo o no es un número, `setTimeout` lo trata como `0`. Podrías añadir validación, pero para una demo la línea única mantiene las cosas legibles.

## Paso 3 – Usar Top‑Level Await para pausar la ejecución

Ahora llega la estrella del espectáculo: top‑level await. Debido a que nuestro script es un módulo (`type="module"`), podemos colocar `await` directamente en el ámbito superior. Esto pausa el módulo hasta que la promesa se resuelva, permitiéndonos controlar el orden de los efectos secundarios.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Pregunta frecuente:** “¿Puedo usar top‑level await en una etiqueta `<script>` normal?” No—solo los scripts de módulo lo soportan. Si olvidas `type="module"`, obtendrás un error de sintaxis.

## Paso 4 – Instanciar la clase, incrementar y registrar el resultado

Finalmente juntamos todo: crear una instancia, llamar a `increment()`, y mostrar el recuento final. Esto demuestra la **increment counter class** en acción.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Salida esperada en la consola

```
Counter class initialized
Final count: 1
```

Si abres la página en DevTools, deberías ver el mensaje del bloque estático aparecer **antes** de que finalice el retraso, confirmando que la clase se evaluó primero.

## Paso 5 – ¿Por qué usar campos públicos de clase en lugar de un constructor?

Podrías preguntarte por qué no escribimos:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Ambos enfoques funcionan, pero **public class fields javascript** te brindan una sintaxis más limpia y declarativa. El campo se define una sola vez, no dentro de cada llamada al constructor, lo que puede ser más fácil de leer cuando la clase crece. Además, los bloques estáticos no pueden colocarse dentro de un constructor, por lo que separar la lógica de inicialización se vuelve más natural.

## Paso 6 – Adaptar el ejemplo para aplicaciones del mundo real

En producción a menudo necesitarás más que un solo contador. Aquí tienes algunas ideas rápidas:

- **Múltiples contadores:** Almacénalos en un `Map` indexado por identificador.
- **Estado persistente:** Reemplaza `console.log` con escrituras en `localStorage`.
- **Inicialización async:** Usa el bloque estático para obtener la configuración de un servidor antes de crear cualquier instancia.

Todos estos patrones siguen beneficiándose de top‑level await, porque puedes obtener datos una vez al cargar el módulo y garantizar que estén listos para cada consumidor.

## Preguntas frecuentes

**P: ¿El top‑level await bloquea otros módulos?**  
R: No. Cada módulo se ejecuta de forma independiente. Sólo el módulo que contiene el await se pausa; los demás módulos continúan cargándose en paralelo.

**P: ¿Qué pasa si la promesa de retraso se rechaza?**  
R: Un rechazo no manejado abortará la evaluación del módulo y aparecerá como un error en la consola. Envuelve el await en un `try…catch` si necesitas una solución alternativa elegante.

**P: ¿Es necesario la palabra clave `static`?**  
R: No para el contador en sí, pero el bloque estático es una forma práctica de demostrar que el código se ejecuta *una sola vez* al cargar—ideal para registro o detección de características.

## Conclusión

Acabas de crear un **ejemplo de top level await** que muestra `await delay javascript`, una **increment counter class**, y el poder de **public class fields javascript**. El fragmento completo y ejecutable está arriba, y la salida de la consola demuestra que el bloque estático se ejecuta antes que el código retrasado.

Desde aquí puedes experimentar con flujos async más complejos, cambiar el retraso por una llamada real a una API, o ampliar la clase con métodos adicionales. Recuerda, el JavaScript moderno te permite tratar los módulos como entidades async de primera clase—sin envoltorios extra.

¡Feliz codificación, y siéntete libre de compartir tus variaciones en los comentarios! Si encontraste útil esta guía, compártela con un compañero que aún esté luchando con patrones async.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}