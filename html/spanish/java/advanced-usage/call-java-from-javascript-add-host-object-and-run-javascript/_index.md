---
category: general
date: 2026-03-14
description: Aprende cómo llamar a Java desde JavaScript usando Aspose.HTML. Esta
  guía muestra cómo agregar un objeto host, ejecutar JavaScript en Java y registrar
  desde JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: es
og_description: Llama a Java desde JavaScript usando Aspose.HTML. Añade un objeto
  host, ejecuta JavaScript en Java y registra desde JavaScript en un único tutorial.
og_title: Llamar a Java desde JavaScript – Guía completa con objeto host
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Llamar a Java desde JavaScript – Añadir objeto host y ejecutar JavaScript en
  Java
url: /es/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

/products/products-backtop-button >}}

Make sure to keep them unchanged.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Llamar a Java desde JavaScript – Añadir objeto host y ejecutar JavaScript en Java

¿Alguna vez necesitaste **llamar a Java desde JavaScript** dentro de una aplicación Java? Tal vez estés construyendo un motor de informes HTML dinámico o simplemente quieras exponer un logger de Java a un script que controlas. En este tutorial verás exactamente cómo añadir un objeto host, ejecutar JavaScript en Java, e incluso **registrar desde JavaScript** de vuelta a la JVM, todo con Aspose.HTML.

Recorreremos un ejemplo completo y ejecutable que crea un documento HTML vacío, inyecta una clase Java `Logger` como objeto host, ejecuta un pequeño script y muestra el resultado en la consola. No se requiere un navegador externo, no hay “magia” misteriosa, solo código Java puro que puedes copiar‑pegar y ejecutar hoy.

## Requisitos previos

- Java 17 (o cualquier JDK reciente) instalado y configurado.  
- Biblioteca Aspose.HTML para Java (versión 23.10 o más reciente). Puedes obtenerla desde Maven Central o el sitio web de Aspose.  
- Un IDE sencillo o un editor de texto; el ejemplo también funciona desde la línea de comandos.

> **Consejo profesional:** Si usas Maven, agrega la siguiente dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

O, para Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Ahora que tenemos los conceptos básicos claros, vamos a sumergirnos en la solución paso a paso.

## Paso 1: Crear un proyecto Java mínimo

Primero, crea una nueva clase Java llamada `JsHostObjectDemo`. La clase contendrá nuestro método `main` y la definición del objeto host. Mantener todo en un solo archivo hace que el tutorial sea autocontenido y fácil de copiar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### ¿Por qué un `HTMLDocument`?

La clase `HTMLDocument` de Aspose.HTML crea un entorno de scripting totalmente compatible con HTML‑5. Aunque nunca carguemos ningún marcado, el objeto `window` del documento nos brinda acceso al motor JavaScript, que es donde ocurre la magia de **ejecutar JavaScript en Java**.

## Paso 2: Añadir el objeto host – “javaLogger”

La línea

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

realiza el trabajo pesado para el requisito de **añadir objeto host**. Al registrar la instancia de `Logger` bajo el nombre `"javaLogger"`, cualquier script evaluado en este documento puede llamar a `javaLogger.log(...)`. Este es el núcleo del concepto de **javascript host object**: un puente que permite a JavaScript acceder a la JVM.

### Problemas comunes

- **Colisiones de nombres** – Si ya tienes una variable global llamada `javaLogger` en tu script, el objeto host será sobrescrito. Elige un nombre único.  
- **Seguridad de subprocesos** – El objeto host se comparte entre ejecuciones de script en el mismo documento. Si planeas ejecutar scripts concurrentemente, haz que la clase host sea segura para subprocesos (por ejemplo, usando `synchronized` o primitivas de `java.util.concurrent`).

## Paso 3: Escribir y ejecutar JavaScript

El script que pasamos a `eval` es deliberadamente pequeño:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Cuando `document.getWindow().eval(script)` se ejecuta, el motor busca `javaLogger` en su ámbito global, encuentra el objeto Java que añadimos y llama a su método `log` con la cadena suministrada.

### Salida esperada

Ejecutar el método `main` imprime la siguiente línea en la consola:

```
[JS] Hello from JavaScript!
```

Esa pequeña línea demuestra que hemos logrado **llamar a Java desde JavaScript**, y el **registro desde JavaScript** aparece exactamente donde aparecería un mensaje normal de `System.out` en Java.

## Paso 4: Extender el host – más que solo registrar

Si necesitas exponer funcionalidad adicional (por ejemplo, acceso a archivos, consultas a bases de datos), simplemente agrega más métodos a la clase `Logger` —o crea una clase host totalmente nueva. Aquí tienes un ejemplo rápido que también devuelve un valor:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Ahora la consola muestra:

```
[JS] 3+4=7
```

Esto demuestra la flexibilidad del patrón de **javascript host object**: puedes exponer cualquier API Java que necesites, siempre que los tipos de datos sean convertibles entre Java y JavaScript (primitivos, cadenas, arreglos, etc.).

## Paso 5: Liberar recursos

Cuando termines con el entorno de scripting, elimina el `HTMLDocument` para liberar recursos nativos:

```java
document.dispose(); // Important for long‑running applications
```

Omitir la eliminación puede provocar fugas de memoria, especialmente si creas muchos documentos dentro de un bucle.

## Ejemplo completo funcionando

A continuación se muestra el archivo fuente completo que puedes compilar y ejecutar de inmediato. Guárdalo como `JsHostObjectDemo.java`, asegura que el JAR de Aspose.HTML esté en tu classpath y ejecuta `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Ejecutar este programa produce:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Ese es todo el flujo de trabajo de **llamar a Java desde JavaScript** en unas pocas líneas.

## Preguntas frecuentes

### ¿Funciona esto en Android?

Aspose.HTML es una biblioteca pura de Java, por lo que se ejecuta en cualquier JVM, incluido Dalvik/ART de Android. Simplemente incluye el JAR y tendrás las mismas capacidades de objeto host.

### ¿Qué pasa si necesito pasar objetos complejos?

Puedes exponer POJOs (plain old Java objects) que contengan campos, getters y setters. El motor los mapeará automáticamente a objetos JavaScript. Para colecciones, usa `java.util.List` o arreglos; ambos son convertibles.

### ¿Cómo funciona el manejo de errores?

Si el script lanza un error de JavaScript, `eval` propagará una `ScriptException`. Envuelve la llamada en un bloque try‑catch para registrar o recuperarte:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### ¿Puedo ejecutar varios scripts secuencialmente?

Absolutamente. La misma instancia de `HTMLDocument` conserva su ámbito global, por lo que puedes llamar a `eval` repetidamente. Solo ten cuidado con posibles colisiones de nombres de variables entre scripts.

## Mejores prácticas y consejos

- **Nombra tus objetos host con claridad** —`javaLogger`, `javaUtils`, etc.— para evitar confusiones.  
- **Mantén los métodos host pequeños y sin efectos secundarios** siempre que sea posible; facilita la depuración.  
- **Elimina el documento** tan pronto como termines; libera la memoria nativa que Aspose.HTML asigna.  
- **Valida las entradas** provenientes de JavaScript, especialmente si los scripts provienen de fuentes no confiables. Trátalos como cualquier dato externo.

## Conclusión

Ahora tienes un ejemplo sólido y de extremo a extremo de cómo **llamar a Java desde JavaScript** mediante **añadir un objeto host**, **ejecutar JavaScript en Java** y **registrar desde JavaScript** usando Aspose.HTML. El patrón es poderoso: cualquier servicio Java puede exponerse a scripts, convirtiendo tu aplicación Java en una plataforma ligera de scripting.

A continuación, podrías explorar:

- Inyectar una página HTML completa y manipular el DOM desde JavaScript.  
- Usar el objeto host para transmitir datos de vuelta al lado Java (por ejemplo, serialización JSON).  
- Integrarte con otros motores de scripting como Nashorn o GraalVM para soporte de más lenguajes.

¡Pruébalo, modifica las clases `Logger` o `Utils`, y ve hasta dónde puedes llevar el concepto de **javascript host object** en tus propios proyectos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}