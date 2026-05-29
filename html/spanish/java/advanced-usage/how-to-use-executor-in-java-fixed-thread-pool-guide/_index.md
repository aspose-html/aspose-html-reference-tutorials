---
category: general
date: 2026-05-28
description: cómo usar executor en Java con un pool de hilos fijo, extraer texto de
  HTML y acelerar el procesamiento – un ejemplo completo de pool de hilos en Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: es
og_description: cómo usar executor en Java con un pool de hilos fijo. aprende un ejemplo
  completo de pool de hilos en Java que extrae texto de archivos HTML de manera eficiente.
og_title: Cómo usar Executor en Java – Guía de pool de hilos fijo
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Cómo usar Executor en Java – Guía de pool de hilos fijo
url: /es/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar Executor en Java – Guía de Pool de Hilos Fijo

¿Alguna vez te has preguntado **cómo usar executor** para ejecutar muchas tareas a la vez sin agotar tu memoria? No estás solo. En muchas aplicaciones del mundo real necesitarás recorrer una carpeta de archivos HTML, extraer el texto del cuerpo y hacerlo rápido—exactamente el escenario que resuelve este tutorial.

Recorreremos una implementación **fixed thread pool java** que extrae texto de HTML, imprime el recuento de caracteres de cada archivo y se cierra de forma limpia. Al final tendrás un **java thread pool example** autónomo que puedes incorporar a cualquier proyecto, además de algunos consejos para personalizar el tamaño del pool y manejar casos límite.

> **Lo que necesitarás**  
> * Java 17 (o cualquier JDK reciente)  
> * Una pequeña biblioteca de análisis HTML – usaremos *jsoup* porque está probada en batalla y no requiere configuración.  
> * Un puñado de archivos *.html* de muestra en un directorio de tu elección.

---

## Cómo usar Executor con un Pool de Hilos Fijo

El corazón de cualquier programa Java con alta concurrencia es el `ExecutorService`. Al crear un **fixed thread pool** le indicamos a la JVM que mantenga exactamente N hilos de trabajo activos, lo que evita la sobrecarga de creación de hilos y limita el uso de recursos.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Por qué es importante:*  
Si lanzaras un nuevo `Thread` por cada archivo HTML, el SO tendría que programar decenas de hilos en un portátil modesto, lo que provocaría un exceso de cambios de contexto. Un pool fijo reutiliza los mismos cuatro hilos, dándote un uso de CPU predecible.

---

## Definir los archivos HTML a procesar – Pool de Hilos Fijo en Java

A continuación enumeramos los archivos que queremos pasar al pool. En una aplicación real probablemente recorrerías un árbol de directorios; aquí lo mantenemos simple.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Consejo:* `List.of` devuelve una lista inmutable, lo que es seguro compartir entre hilos sin sincronización adicional.

---

## Enviar una tarea separada para cada archivo HTML

Ahora entregamos cada ruta al executor. La lambda que enviamos se ejecutará **en paralelo** en uno de los cuatro hilos de trabajo.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Por qué envolvemos la lógica en un método** (`extractBodyText`) se aclarará en la siguiente sección—mantiene la lambda ordenada y nos permite reutilizar el código de extracción en otro lugar.

---

## Extraer texto de HTML – La lógica central

Aquí está el helper reutilizable que realmente **extrae texto de html** usando Jsoup. Abre el archivo, analiza el DOM y devuelve el texto plano del cuerpo.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*¿Por qué Jsoup?* Es liviano, maneja marcado malformado de forma elegante y no requiere un motor de navegador completo. El método lanza `IOException` para que el llamador pueda decidir cómo registrar o recuperarse—perfecto para un escenario de pool de hilos donde no deseas que un solo archivo defectuoso termine todo el executor.

---

## Apagar el Executor de forma segura – Crear Pool de Hilos Fijo

Después de haber enviado todos los trabajos, debemos indicarle al pool que deje de aceptar nuevo trabajo y que termine lo que ya está en cola.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explicación:* `shutdown()` evita nuevas entregas, mientras que `awaitTermination` bloquea hasta que cada trabajo de análisis termine (o expire el tiempo de espera). Si algo se cuelga, `shutdownNow()` intenta cancelar las tareas en ejecución. Este patrón es la forma recomendada de **create fixed thread pool** de manera segura.

---

## Ejemplo completo y ejecutable

Juntando todo, aquí tienes un único archivo que puedes compilar y ejecutar. Incluye las importaciones necesarias, el método `main` y el helper descrito arriba.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Salida esperada** (asumiendo que cada archivo contiene aproximadamente 1 200 caracteres de texto del cuerpo):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Si falta algún archivo o está malformado, verás una traza de pila impresa en `stderr`, pero las demás tareas continuarán sin problemas—exactamente lo que debería hacer un **java thread pool example** bien comportado.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si tengo más de cuatro archivos?* | El pool pondrá en cola las tareas extra y las ejecutará tan pronto como un hilo quede libre. No se necesita código adicional. |
| *¿Debería usar `newCachedThreadPool` en su lugar?* | `newCachedThreadPool` crea hilos bajo demanda y puede crecer sin límite, lo cual es arriesgado para trabajos intensivos en I/O. Un **fixed thread pool** te brinda un uso predecible de memoria y CPU. |
| *¿Cómo cambio el tamaño del pool según los núcleos de CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` es un patrón común. |
| *¿Qué pasa si el análisis falla para un archivo?* | El `catch (IOException e)` dentro de la lambda aísla la falla, la registra y permite que el resto del pool continúe trabajando. |
| *¿Puedo devolver el texto extraído al llamador?* | Sí—usa `Future<String>` en lugar de `submit(Runnable)`. El código quedaría así `Future<String> f = executor.submit(() -> extractBodyText(path));` y luego `String result = f.get();`. |

---

## Conclusión

Hemos cubierto **cómo usar executor** para crear un **fixed thread pool java** que procesa una colección de archivos HTML en paralelo, extrae su texto del cuerpo y reporta el recuento de caracteres. El **java thread pool example** completo demuestra una gestión adecuada de recursos, manejo de errores y un método de extracción reutilizable.

¿Próximos pasos? Prueba a cambiar la implementación de `extractBodyText` por un scraper más sofisticado, experimenta con un pool de mayor tamaño, o envía los resultados a una base de datos. También podrías explorar `CompletionService` para obtener resultados tan pronto como estén listos, lo cual es útil cuando los tamaños de los archivos varían mucho.

Siéntete libre de ajustar la ruta del directorio, agregar más archivos o integrar este fragmento en un marco de rastreo más grande. El patrón central—crear un pool, enviar tareas independientes y apagarlo de forma segura—permanece igual, sin importar cuán complejo sea tu carga de trabajo.

¡Feliz codificación, y que tus hilos siempre permanezcan activos (hasta que los apagues, por supuesto)!

## Tutoriales relacionados

- [Fixed thread pool java – Limpieza paralela de HTML con ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Cómo consultar HTML en Java – Tutorial completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Cómo usar Aspose.HTML para Java - Dominando la renderización de Canvas HTML5](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}