---
category: general
date: 2026-01-14
description: cómo establecer dpi al convertir una URL a PNG. Aprende a renderizar
  HTML a PNG, establecer el tamaño del viewport y guardar HTML como PNG usando Aspose.HTML
  en Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: es
og_description: cómo establecer dpi al convertir una URL a PNG. Guía paso a paso para
  renderizar HTML a PNG, controlar el tamaño del viewport y guardar HTML como PNG
  usando Aspose.HTML.
og_title: Cómo establecer DPI – Renderizar HTML a PNG con AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: Cómo establecer DPI – Renderizar HTML a PNG con AsposeHTML
url: /es/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo establecer dpi – Renderizar HTML a PNG con AsposeHTML

¿Alguna vez te has preguntado **cómo establecer dpi** para una imagen similar a una captura de pantalla generada a partir de una página web? Tal vez necesites un PNG de 300 DPI para impresión, o una miniatura de baja resolución para una aplicación móvil. En cualquier caso, el truco consiste en indicar al motor de renderizado el DPI lógico que deseas, y luego dejar que haga el trabajo pesado.  

En este tutorial tomaremos una URL en vivo, la renderizaremos a un archivo PNG, **estableceremos el tamaño del viewport**, ajustaremos el DPI y, finalmente, **guardaremos HTML como PNG**—todo con Aspose.HTML para Java. Sin navegadores externos, sin herramientas complicadas de línea de comandos—solo código Java limpio que puedes incorporar a cualquier proyecto Maven o Gradle.

> **Consejo profesional:** Si solo buscas una miniatura rápida, puedes mantener el DPI en 96 DPI (el valor predeterminado para la mayoría de pantallas). Para recursos listos para impresión, aumentalo a 300 DPI o más.

![ejemplo de cómo establecer dpi](https://example.com/images/how-to-set-dpi.png "ejemplo de cómo establecer dpi")

## Lo que necesitarás

- **Java 17** (o cualquier JDK reciente).  
- **Aspose.HTML for Java** 24.10 o más reciente. Puedes obtenerlo de Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Una conexión a internet para obtener la página objetivo (el ejemplo usa `https://example.com/sample.html`).  
- Permiso de escritura en la carpeta de salida.

Eso es todo—sin Selenium, sin Chrome sin cabeza. Aspose.HTML realiza el renderizado en el proceso, lo que significa que permaneces dentro de la JVM y evitas la sobrecarga de lanzar un navegador.

## Paso 1 – Cargar el documento HTML desde una URL

Primero creamos una instancia de `HTMLDocument` que apunta a la página que queremos capturar. El constructor descarga automáticamente el HTML, lo analiza y prepara el DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Por qué es importante:* Al cargar el documento directamente, evitas la necesidad de un cliente HTTP separado. Aspose.HTML respeta redirecciones, cookies e incluso autenticación básica si incrustas credenciales en la URL.

## Paso 2 – Construir un sandbox con el DPI y viewport deseados

Un **sandbox** es la forma en que Aspose.HTML imita un entorno de navegador. Aquí le indicamos que simule una pantalla de 1280 × 720 y, lo que es crucial, establecemos el **DPI del dispositivo**. Cambiar el DPI modifica la densidad de píxeles de la imagen renderizada sin alterar el tamaño lógico.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Por qué podrías ajustar estos valores:*

- **Viewport size** controla cómo se comportan las consultas de medios CSS (`@media (max-width: …)`).
- **Device DPI** influye en el tamaño físico de la imagen al imprimir. Una imagen de 96 DPI se ve bien en pantallas; una imagen de 300 DPI mantiene la nitidez en papel.

Si necesitas una miniatura cuadrada, simplemente cambia `setViewportSize(500, 500)` yén el DPI bajo.

## Paso 3 – Elegir PNG como formato de salida

Aspose.HTML admite varios formatos raster (PNG, JPEG, BMP, GIF). PNG es sin pérdida, lo que lo hace perfecto para capturas de pantalla donde deseas que cada píxel se conserve.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

También puedes ajustar el nivel de compresión (`pngOptions.setCompressionLevel(9)`) si te preocupa el tamaño del archivo.

## Paso 4 – Renderizar y guardar la imagen

Ahora indicamos al documento que **guarde** como una imagen. El método `save` recibe una ruta de archivo y las opciones configuradas previamente.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Cuando el programa termine, encontrarás un archivo PNG en `YOUR_DIRECTORY/sandboxed.png`. Ábrelo—si estableciste el DPI a 300, los metadatos de la imagen lo reflejarán, aunque las dimensiones en píxeles sigan siendo 1280 × 720.

## Paso 5 – Verificar el DPI (Opcional pero útil)

Si deseas verificar el DPI realmente se aplicó, puedes leer los metadatos PNG con una biblioteca ligera como **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Deberías ver `300` (o el valor que hayas establecido) impreso en la consola. Este paso no es necesario para el renderizado, pero es una rápida verificación, especialmente cuando generas recursos para un flujo de trabajo de impresión.

## Preguntas comunes y casos límite

### “¿Qué pasa si la página usa JavaScript para cargar contenido?”

Aspose.HTML ejecuta un **subconjunto limitado** de JavaScript. Para la mayoría de los sitios estáticos funciona de inmediato. Si la página depende en gran medida de frameworks del lado del cliente (React, Angular, Vue), podrías necesitar pre‑renderizar la página o usar un navegador sin cabeza en su lugar. Sin embargo, la configuración del DPI funciona de la misma manera una vez que el DOM está listo.

### “¿Puedo renderizar un PDF en lugar de PNG?”

Claro. Cambia `ImageSaveOptions` por `PdfSaveOptions` y modifica la extensión de salida a `.pdf`. La configuración del DPI sigue influyendo en la apariencia rasterizada de cualquier imagen incrustada.

### “¿Qué pasa con capturas de alta resolución para pantallas retina?”

Simplemente duplica las dimensiones del viewport manteniendo el DPI en 96 DPI, o conserva el viewport y aumenta el DPI a 192. El PNG resultante contendrá el doble de píxeles, dándote esa nitidez característica de retina.

### “¿Necesito limpiar los recursos?”

`HTMLDocument` implementa `AutoCloseable`. En una aplicación de producción, envuélvelo en un bloque‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Eso garantiza que los recursos nativos se liberen rápidamente.

## Ejemplo completo funcional (listo para copiar y pegar)

A continuación se muestra el programa completo, listo para ejecutar. Reemplaza `YOUR_DIRECTORY` con una carpeta real en tu máquina.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Ejecuta la clase y obtendrás un PNG que respeta la configuración **cómo establecer dpi** que especificaste.

## Conclusión

Hemos recorrido **cómo establecer dpi** al **renderizar HTML a PNG**, cubierto el paso de **establecer el tamaño del viewport**, y te mostramos cómo **guardar HTML como PNG** usando Aspose.HTML para Java. Los puntos clave son:

- Utiliza un **sandbox** para controlar el DPI y el viewport.  
- Elige las **ImageSaveOptions** adecuadas para una salida sin pérdida.  
- Verifica los metadatos DPI si necesitas garantizar la calidad de impresión.  

Desde aquí puedes experimentar con diferentes valores de DPI, viewports más grandes, o incluso procesar por lotes una lista de URLs. ¿Quieres convertir todo un sitio web en miniaturas PNG? Simplemente recorre un arreglo de URLs y reutiliza la misma configuración de sandbox.

¡Feliz renderizado, y que tus capturas de pantalla siempre sean perfectas al píxel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}