---
category: general
date: 2026-06-19
description: Cómo iniciar un hilo en Java con un Runnable reutilizable, iniciar varios
  hilos, imprimir el nombre del hilo y analizar HTML con Java. Ejemplo paso a paso.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: es
og_description: Cómo iniciar un hilo en Java usando Runnable, ejecutar varios hilos,
  imprimir el nombre del hilo y analizar HTML con Java en un único ejemplo ejecutable.
og_title: Cómo iniciar un hilo en Java – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Cómo iniciar un hilo en Java – Guía completa
url: /es/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo iniciar un hilo en Java – Guía completa

¿Alguna vez te has preguntado **cómo iniciar un hilo** en Java sin ahogarte en código repetitivo? No eres el único. Ya sea que estés construyendo un rastreador web, un actualizador de UI, o simplemente necesites delegar un cálculo pesado, dominar la creación de hilos es una habilidad imprescindible para cualquier desarrollador Java.

En este tutorial recorreremos un escenario práctico: **analizar HTML con Java**, imprimir el nombre del hilo actual y **iniciar varios hilos** que compartan la misma lógica. Al final sabrás **cómo usar Runnable**, lanzar varios workers y ver la salida que esperas, todo en un ejemplo autocontenido que puedes copiar‑pegar ahora mismo.

## Lo que aprenderás

- Los pasos exactos **cómo iniciar un hilo** usando la clase `Thread` y un `Runnable`.
- Cómo **iniciar varios hilos** que ejecuten la misma tarea sin duplicar código.
- La forma más sencilla de **imprimir el nombre del hilo** junto a tus resultados de procesamiento.
- Un método limpio para **analizar HTML con Java** usando un ayudante ligero `HTMLDocument` (o cualquier parser que prefieras).
- Por qué **cómo usar runnable** es importante para un código reutilizable y testeable.

No se requieren bibliotecas externas para el ejemplo principal, pero indicaremos dónde podrías sustituir Jsoup u otro parser si necesitas más potencia.

---

## Paso 1: Definir una tarea reutilizable – **cómo usar runnable**

Lo primero que necesitas saber **cómo usar runnable** es encapsular el trabajo que cada hilo debe realizar. Un `Runnable` es simplemente una interfaz funcional con un único método `run()`, lo que lo hace perfecto para expresiones lambda.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Por qué es importante:** Al mantener la lógica dentro de un `Runnable`, puedes entregarla a cualquier número de objetos `Thread`, a un pool de hilos o incluso a un servicio de ejecutores más adelante. Esto mantiene tu código DRY y testeable.

---

## Paso 2: **Cómo iniciar un hilo** – crear el primer worker

Ahora que tenemos un `Runnable`, lanzar un hilo es tan fácil como llamar al constructor de `Thread`. La pregunta **cómo iniciar hilo** se responde en una sola línea:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Observa el segundo argumento, `"Worker-1"`. Ese nombre aparecerá cuando más adelante **imprimamos el nombre del hilo**, facilitando mucho la depuración.

---

## Paso 3: **Iniciar varios hilos** – reutilizar el mismo Runnable

¿Quieres procesar varios archivos HTML a la vez? Simplemente crea otro `Thread` con el mismo `Runnable`. Esto demuestra **iniciar varios hilos** sin copiar el código de la tarea:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Tanto `Worker-1` como `Worker-2` ejecutarán el bloque definido en `extractTextLength` de forma concurrente. Como la tarea es sin estado (solo lee un archivo), no hay condiciones de carrera de las que preocuparse.

---

## Paso 4: **Imprimir el nombre del hilo** mientras se analiza HTML

Dentro del `Runnable` ya llamamos a `Thread.currentThread().getName()`. Esa es la forma canónica de **imprimir el nombre del hilo**. La salida se verá algo así (suponiendo que el cuerpo del HTML contenga 1 234 caracteres):

```
Worker-1: 1234
Worker-2: 1234
```

Si ejecutas el programa con un archivo más grande, cada línea mostrará la misma longitud porque ambos hilos leen el mismo archivo. Cambia la ruta o pasa el nombre del archivo como parámetro para ver resultados diferentes.

---

## Paso 5: Ejemplo completo y ejecutable – de la importación a la ejecución

A continuación tienes el programa completo, **autocontenido**, que puedes colocar en un archivo llamado `HtmlThreadDemo.java`. Incluye un pequeño stub `HTMLDocument` para que el código compile aunque no tengas un parser real a mano. Sustituye el stub por Jsoup o cualquier librería que prefieras para uso en producción.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Salida esperada

Suponiendo que `page.html` contiene 2 567 caracteres dentro de su etiqueta `<body>`, verás algo como:

```
Worker-1: 2567
Worker-2: 2567
```

Si el archivo no se puede leer, se imprimirá el stack trace—gracias al bloque `catch`.

---

## Problemas comunes y consejos profesionales

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Archivo no encontrado** | La ruta `"YOUR_DIRECTORY/page.html"` es relativa al directorio desde donde lanzas la JVM. | Usa una ruta absoluta o `Paths.get("").toAbsolutePath()` para depurar. |
| **Condiciones de carrera** | Si el `Runnable` modifica estado compartido, los hilos pueden chocar. | Mantén la tarea sin estado, o sincroniza el acceso a objetos compartidos. |
| **Demasiados hilos** | Crear decenas de `Thread`s puede agotar los recursos del SO. | Cambia a un `ExecutorService` con un pool limitado después de dominar lo básico. |
| **Parseo HTML incorrecto** | El stub `HTMLDocument` es simplista; páginas complejas fallan. | Sustitúyelo por Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Extender el ejemplo

Ahora que sabes **cómo iniciar un hilo**, podrías querer:

- **Analizar diferentes archivos** pasando el nombre del archivo al `Runnable` (usa un constructor o una lambda que capture una variable).
- **Recopilar resultados** con un `ConcurrentLinkedQueue<Integer>` en lugar de solo imprimir.
- **Aprovechar un pool de hilos** (`Executors.newFixedThreadPool(4)`) para mejor escalabilidad.
- **Cambiar el parser** por Jsoup, HtmlUnit, o cualquier biblioteca que se ajuste a las necesidades de tu proyecto.

Todos esos pasos siguen basándose en la idea central que cubrimos: definir una tarea reutilizable, entregarla a uno o varios hilos y observar qué hilo está trabajando mediante **imprimir el nombre del hilo**.

---

## Conclusión

Hemos cubierto **cómo iniciar un hilo** en Java, demostrado **cómo usar runnable** para trabajo reutilizable, mostrado cómo **iniciar varios hilos**, e ilustrado una forma sencilla de **analizar HTML con Java** mientras **imprimes el nombre del hilo** para cada worker. El fragmento de código completo arriba está listo para ejecutarse, y los conceptos escalan a aplicaciones más complejas y de nivel producción.

Siéntete libre de experimentar: cambia la ruta del archivo, aumenta el número de workers, o conecta un parser HTML real. Los fundamentos siguen siendo los mismos, y ahora tienes una base sólida para cualquier proyecto Java multihilo.

¿Tienes preguntas sobre seguridad de hilos, servicios de ejecutores o bibliotecas de parseo HTML? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Pool de hilos fijo en Java – Limpieza paralela de HTML con ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Cómo editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cómo convertir HTML a PDF en Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}