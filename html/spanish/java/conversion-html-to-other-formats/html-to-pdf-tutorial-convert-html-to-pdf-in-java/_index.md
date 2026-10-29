---
category: general
date: 2026-06-19
description: Aprende cómo generar PDF a partir de HTML usando un sencillo ejemplo
  en Java. Este tutorial de HTML a PDF te muestra cómo convertir un archivo HTML a
  PDF con OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: es
og_description: El tutorial de HTML a PDF te muestra cómo generar PDF a partir de
  HTML usando Java. Sigue los pasos para convertir rápidamente un archivo HTML a PDF.
og_title: 'tutorial de html a pdf: guía de conversión en Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'tutorial de html a pdf: Convertir HTML a PDF en Java'
url: /es/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial html a pdf – Convierte una página HTML en un PDF con Java

¿Alguna vez te has preguntado cómo convertir una página HTML estática en un elegante documento PDF sin salir de tu IDE? No estás solo. En este **html to pdf tutorial** recorreremos un ejemplo completo y listo‑para‑ejecutar en Java que **generate pdf from html** en solo unos minutos.

Cubriremos todo lo que necesitas: configuración del proyecto, agregar la biblioteca adecuada, escribir el código de conversión e incluso un consejo rápido para convertir una página web en vivo a PDF. Al final podrás **convert html file pdf** en tu propia máquina, y entenderás cómo **create pdf from html** para cualquier proyecto futuro.

## Lo que necesitarás

- Java 17 o superior (el código funciona con cualquier JDK reciente)
- Maven o Gradle (mostraremos el fragmento de Maven)
- Un pequeño archivo HTML que quieras convertir en PDF (crearemos uno al vuelo)
- Un IDE o un editor de texto simple—tú decides

Eso es todo. Sin servidores pesados, sin SDKs de pago, solo Java puro y una biblioteca gratuita de código abierto.

## Paso 1: tutorial html a pdf – Configura un proyecto Maven

Primero lo primero. Crea un nuevo proyecto Maven (o añádelo a uno existente). La única dependencia que realmente necesitas es **OpenHTMLtoPDF**, que se encarga de renderizar HTML y CSS en un PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Consejo profesional:** Si estás usando Gradle, las mismas dependencias pueden añadirse bajo `implementation` en `build.gradle`.  

Por qué este paso es importante: sin la biblioteca la JVM no sabe cómo traducir etiquetas HTML en comandos de dibujo PDF. OpenHTMLtoPDF es ligera, se mantiene activamente y funciona con CSS‑2.1, por lo que tu estilo permanece intacto.

## Paso 2: generar pdf desde html – Prepara un archivo HTML de muestra

Creemos un pequeño `input.html` justo al lado de nuestro código Java. Esto mantiene el ejemplo autocontenido y demuestra el flujo de trabajo **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Puedes reemplazar el contenido con cualquier cosa—tablas, imágenes, incluso JavaScript (aunque el renderizador ignora los scripts). Lo importante es que el archivo esté en el classpath para que el conversor pueda localizarlo.

## Paso 3: convertir archivo html a pdf – Escribe la utilidad de conversión

Ahora el corazón del **html to pdf tutorial**: una pequeña clase `HtmlToPdfConverter` que lee el HTML y escribe un PDF. El código a continuación es un ejemplo completo y ejecutable; cópialo y pégalo en `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Por qué funciona este código

1. **Flexibilidad de recursos** – el método primero verifica si la ruta suministrada apunta a un archivo real; si no, recurre a un recurso del classpath. Eso significa que puedes **convert webpage to pdf** más tarde proporcionando una cadena URL (simplemente reemplaza la llamada `withHtmlContent` por `withUri`).

2. **Creación automática de directorios** – `Files.createDirectories` garantiza que la carpeta `target/` exista, por lo que no obtendrás un error de “No such file or directory”.

3. **Conversión en una sola línea** – `PdfRendererBuilder` maneja CSS, fuentes y el diseño de página internamente. No es necesario gestionar manualmente las páginas PDF; la biblioteca lo hace por ti, manteniendo el ejemplo corto y centrado en el concepto **convert html file pdf**.

## Paso 4: crear pdf desde html – Ejecuta el programa y verifica

Abre una terminal en la raíz del proyecto y ejecuta:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Si todo está configurado correctamente verás:

```
✅ PDF successfully created at target/output.pdf
```

Abre `target/output.pdf` con cualquier visor de PDF. Deberías ver el encabezado estilizado “Monthly Sales Report”, el texto del párrafo y los mismos márgenes que definiste en el bloque `<style>` del HTML.

> **¿Qué pasa si no ves el estilo?**  
> Asegúrate de que el CSS esté en línea o ubicado en la misma carpeta que el HTML. OpenHTMLtoPDF resuelve URLs relativas basándose en el URI base que pasas a `withHtmlContent`. En el fragmento anterior pasamos `null`, lo que funciona para CSS en línea simple. Para hojas de estilo externas, proporciona la ruta del directorio como segundo argumento.

## Paso 5: convertir página web a pdf – Manejo de URLs remotas (opcional)

A veces necesitas **convert webpage to pdf** directamente desde internet—piensa en archivar un recibo en línea. La biblioteca soporta esto mediante `withUri`. Aquí tienes una adaptación rápida:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Llámalo así:



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo convertir HTML a PDF Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convertir HTML a PDF Java – Configurando el entorno en Aspose.HTML](/html/english/java/configuring-environment/)
- [Convertir HTML a PDF en Java – Guía paso a paso con configuración de tamaño de página](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}