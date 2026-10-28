---
category: general
date: 2026-10-28
description: Cómo leer HTML en Java y extraer texto de archivos HTML. Aprende a convertir
  HTML a texto con Jsoup, cubriendo la lectura de HTML desde archivo y las técnicas
  de HTML a texto en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: es
lastmod: 2026-10-28
og_description: Cómo leer HTML en Java y extraer texto de archivos HTML. Este tutorial
  muestra una solución completa para convertir HTML a texto usando Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Cómo leer HTML y extraer texto en Java – guía rápida
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: 'Cómo leer HTML y extraer texto en Java: una guía paso a paso'
url: /es/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo leer HTML y extraer texto en Java – una guía paso a paso

Si necesitas **how to read html** desde un archivo local, esta guía ofrece una solución completa. Aprenderás a cargar un documento HTML, extraer el texto plano y, opcionalmente, convertir HTML a texto con control fino. Al final del tutorial podrás ejecutar el código de ejemplo y ver el texto extraído impreso en la consola.

Leer archivos HTML es una tarea común al procesar datos extraídos de la web, generar informes o limpiar contenido generado por usuarios. Los pasos a continuación cubren todo lo que necesitas, desde agregar la biblioteca requerida hasta manejar casos límite como marcado malformado o problemas de codificación de caracteres.

## Lo que necesitarás

- Java 17 o superior (el código también compila con versiones anteriores)
- Maven o Gradle para la gestión de dependencias, o el JAR de Jsoup añadido manualmente
- Un archivo HTML llamado `input.html` colocado en el directorio `src/main/resources` del proyecto (puedes cambiar la ruta más tarde)

## Configura la biblioteca Jsoup

Jsoup es una biblioteca ligera y bien documentada que analiza HTML en una estructura similar a DOM. Maneja HTML roto de forma elegante, lo que la hace ideal para tareas de **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Si prefieres una descarga manual, coloca el JAR en tu classpath e importa `org.jsoup.*` en tu archivo fuente.

## Cargar HTML desde un archivo

El primer paso programático es leer el archivo en un objeto `Document`. Jsoup ofrece un método estático `parse` que acepta un `File` y el nombre de un conjunto de caracteres.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Por qué es importante:** `Jsoup.parse(File, String)` lee los bytes crudos, los decodifica según el conjunto de caracteres proporcionado y construye un DOM limpio. Este enfoque es más seguro que leer el archivo en una cadena tú mismo porque Jsoup normaliza los finales de línea y corrige automáticamente errores comunes de marcado.

## Extraer texto plano del HTML

Una vez que tienes un `Document`, obtener el texto visible es una única llamada a método. El método `text()` concatena el contenido textual de todos los elementos mientras descarta etiquetas, scripts y estilos.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

La llamada `body()` limita la extracción al elemento `<body>`, que es el objetivo típico cuando **read html from file** para análisis de contenido. La cadena resultante contiene espacios en blanco colapsados a un solo espacio, imitando cómo un navegador renderizaría el texto.

### Salida esperada

Asumiendo que `input.html` contiene:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Ejecutar el programa imprime:

```
Extracted text:
Hello World This is a demo page.
```

## Convertir HTML a texto con opciones adicionales

A veces necesitas más control que el que ofrece `text()`, por ejemplo, preservar saltos de línea, mantener la numeración de listas o ignorar ciertas etiquetas. El `NodeTraversor` de Jsoup combinado con un `NodeVisitor` personalizado te brinda esa flexibilidad.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Reemplaza la simple llamada `doc.body().text()` con:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Por qué funciona:** El visitante recorre el DOM en profundidad, añadiendo un salto de línea antes de cada elemento de nivel bloque (p. ej., `<p>`, `<div>`, `<h1>`). Esto mantiene la separación de párrafos, lo cual es útil cuando **convert html to text** para legibilidad o pipelines de NLP posteriores.

## Errores comunes y buenas prácticas

| Issue | Why it occurs | Recommended fix |
|-------|---------------|-----------------|
| Conjunto de caracteres incorrecto | Los archivos guardados en ISO‑8859‑1 pero analizados como UTF‑8 generan caracteres distorsionados. | Detecta el conjunto de caracteres a partir de la etiqueta meta del archivo (`<meta charset="...">`) o pasa el nombre correcto a `Jsoup.parse`. |
| Archivos grandes | Cargar un archivo HTML muy grande en memoria puede provocar `OutOfMemoryError`. | Transmite el archivo con `Jsoup.parse(File, String, String baseUri)` y procesa los nodos de forma incremental, o aumenta el tamaño del heap de la JVM. |
| Texto no deseado de script/estilo | `text()` elimina el contenido de script y estilo, pero los visitantes personalizados pueden incluirlo sin querer. | Omite los nodos cuyo nombre de etiqueta sea `script` o `style` dentro del método `head` del visitante. |
| Preservar espacios en blanco | Colapsar los espacios puede perder el formato necesario para la conversión a markdown. | Utiliza `Element.wholeText()` para nodos de texto sin procesar, y luego procesa manualmente los espacios en blanco. |

Abordar estas cuestiones garantiza que tu solución **html to text java** funcione de manera fiable con entradas diversas.

## Ejemplo completo ejecutable

A continuación se muestra un programa autocontenido que demuestra todo el flujo de trabajo —desde la configuración de dependencias hasta la verificación de salida. Copia el código en un archivo llamado `HtmlToTextDemo.java`, coloca un archivo `input.html` junto a él y ejecuta `javac && java` como se muestra.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Ejecutando el programa

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

La consola muestra tanto la extracción simple como la detallada

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar XPath en Java – Leer HTML y extraer texto](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Cómo analizar HTML en Java – Extraer texto de artículos HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extraer texto de HTML con Java – Guía completa paso a paso](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}