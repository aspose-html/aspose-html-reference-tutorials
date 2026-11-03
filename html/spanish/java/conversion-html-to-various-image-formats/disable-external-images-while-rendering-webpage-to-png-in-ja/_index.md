---
category: general
date: 2026-05-31
description: Desactiva las imágenes externas al renderizar una página web a PNG en
  Java usando Aspose HTML. Aprende a cargar la página web en un sandbox de forma segura
  y guardar el documento HTML como PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: es
og_description: Deshabilita las imágenes externas al renderizar una página web a PNG
  en Java. Esta guía paso a paso muestra cómo cargar una página web en un sandbox
  y guardar el documento HTML como PNG.
og_title: Desactivar imágenes externas al renderizar una página web a PNG en Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Desactivar imágenes externas al renderizar una página web a PNG en Java
url: /es/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Desactivar imágenes externas al renderizar una página web a PNG en Java

¿Alguna vez necesitaste **desactivar imágenes externas** al renderizar una página web a PNG en Java? Tal vez estés construyendo un servicio de miniaturas que debe permanecer aislado de Internet público, o simplemente quieras garantizar que no se filtren imágenes de terceros durante la conversión. De cualquier manera, has llegado al lugar correcto.

En este tutorial recorreremos la carga de una página web en un sandbox, desactivaremos la obtención de imágenes externas y, finalmente, guardaremos el documento HTML como un archivo PNG, todo con Aspose.HTML para Java. Al final tendrás un ejemplo listo para ejecutar, además de varios consejos prácticos para evitar los problemas habituales.

## Qué aprenderás

- **Cómo renderizar HTML a imagen Java** usando `Converter` de Aspose.HTML.
- Los pasos exactos para **cargar una página web en sandbox** con un viewport y DPI personalizados.
- La configuración necesaria para **desactivar imágenes externas** mientras se sigue renderizando la página.
- Cómo **guardar el documento HTML como PNG** (o cualquier otro formato compatible) en disco.
- Manejo de casos límite, sugerencias de rendimiento y consejos de solución de problemas.

### Requisitos previos

- Java 8 o superior instalado (el código también funciona con JDK 11+).
- Maven o Gradle para obtener la biblioteca Aspose.HTML para Java.
- Familiaridad básica con la sintaxis de Java y el manejo de excepciones.
- Una conexión a Internet para la carga inicial de la página (a menos que sirvas el HTML localmente).

> **Consejo profesional:** Si trabajas detrás de un proxy corporativo, establece las propiedades JVM `http.proxyHost` y `http.proxyPort` antes de ejecutar el ejemplo.

---

## Paso 1: Configura tu proyecto y agrega Aspose.HTML

Lo primero, agrega la dependencia de Aspose.HTML. Si usas Maven, inserta esto en tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Para Gradle, el equivalente es:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Una vez que la biblioteca esté en el classpath, estás listo para comenzar a programar.

---

## Paso 2: **Desactivar imágenes externas** con un entorno Sandbox

El corazón de la solución está en `DocumentSandbox`. Al pasar `false` para la bandera *allowExternalImages*, indicamos a Aspose.HTML que ignore cualquier etiqueta `<img>` que apunte a URLs fuera del sandbox. Este es el mecanismo exacto que **desactiva imágenes externas**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Por qué es importante:** Sin el sandbox, el renderizador intentaría descargar cada imagen referenciada por la página, lo que puede ser lento, poco fiable o incluso un riesgo de seguridad. Establecer la bandera a `false` garantiza una pasada de renderizado limpia y autocontenida.

---

## Paso 3: **Cargar página web en Sandbox**  

Ahora apuntamos Aspose.HTML a la URL que queremos capturar. El constructor `HTMLDocument` acepta la instancia del sandbox, aplicando automáticamente las restricciones que acabamos de definir.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Si la página depende mucho de scripts externos para el diseño, podrías notar contenido faltante porque también desactivamos los scripts. En ese caso, cambia la bandera `allowExternalScripts` a `true` manteniendo `allowExternalImages` en `false`.

---

## Paso 4: **Renderizar página web a PNG**  

Con el documento cargado, convertirlo a una imagen es una sola línea usando `Converter.convert`. El objeto `ImageSaveOptions` te permite elegir el formato de salida; aquí seleccionamos PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

El archivo resultante, `sandboxed.png`, contiene una captura de la página **sin ninguna imagen externa**—solo permanecen los SVG inline o los gráficos codificados en base64, si los hay.

---

## Paso 5: Verifica la salida y depura problemas comunes

Después de ejecutar el programa, abre `sandboxed.png` con cualquier visor de imágenes. Deberías ver el diseño de la página, el texto y el estilo CSS, pero todos los elementos `<img src="http://…">` aparecerán en blanco (a menudo renderizados como un rectángulo blanco o omitidos por completo).

### Problemas típicos y cómo solucionarlos

| Síntoma | Causa probable | Solución |
|---|---|---|
| Página en blanco | La URL de destino bloqueó la solicitud (p. ej., Cloudflare) | Añade encabezados adecuados al user‑agent del sandbox o usa un proxy. |
| Fuentes faltantes | Los archivos de fuentes están alojados externamente | Instala las fuentes localmente o incrústalas como `@font-face` con URIs de datos. |
| Desplazamiento del diseño | Las hojas de estilo CSS hacen referencia a recursos externos que fueron bloqueados | Establece `allowExternalScripts` a `true` *solo* para la carga de CSS, luego vuelve a ejecutar. |
| `java.lang.OutOfMemoryError` | Renderizando una página muy grande a alta DPI | Reduce el tamaño del viewport o la DPI, o incrementa el heap de JVM (`-Xmx2g`). |

---

## Paso 6: Extender el ejemplo – Guardar en otros formatos

El mismo código funciona para JPEG, BMP o incluso PDF. Solo cambia el enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Si necesitas un PDF, reemplaza `ImageSaveOptions` por `PdfSaveOptions` y ajusta la extensión del archivo en consecuencia.

---

## Ejemplo completo (listo para copiar y pegar)

A continuación tienes el **programa completo y ejecutable**. Crea una nueva clase Java, pega el código, asegúrate de que exista el directorio `output` y ejecútalo.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Salida esperada** (consola):

```
PNG image saved to: output/sandboxed.png
```

Abre `sandboxed.png` – verás la página renderizada **sin ninguna imagen externa**.

---

## Preguntas frecuentes

**P: ¿Puedo seguir mostrando imágenes que están incrustadas dentro del HTML?**  
R: Sí. Los URIs `data:` inline o las imágenes codificadas en base64 se consideran parte del documento y aparecerán en el PNG.

**P: ¿Qué pasa si necesito mantener algunas imágenes externas pero bloquear otras?**  
R: El sandbox funciona como un interruptor todo‑o‑nada. Para un control más fino, descarga tú mismo las imágenes permitidas, incrústalas como URIs de datos y luego renderiza.

**P: ¿Este enfoque funciona en servidores sin cabeza (headless)?**  
R: Absolutamente. Aspose.HTML es una biblioteca pura de Java; no requiere un servidor de pantalla ni un motor de navegador.

**P: ¿En qué se diferencia de usar Selenium o Puppeteer?**  
R: Selenium controla un navegador real, lo que es pesado y más difícil de aislar. Aspose.HTML renderiza HTML directamente en memoria, ofreciéndote un rendimiento determinista y controles de seguridad más sencillos como **desactivar imágenes externas**.

---

## Conclusión

Ahora dispones de una receta sólida, de extremo a extremo, para **desactivar imágenes externas mientras renderizas una página web a PNG en Java**. Al aprovechar `DocumentSandbox`, obtienes un control estricto sobre qué recursos externos están permitidos, garantizando tanto seguridad como reproducibilidad. Desde aquí puedes experimentar con diferentes tamaños de viewport, configuraciones de DPI o formatos de salida—cada ajuste abre una nueva vía para generar miniaturas, vistas previas o instantáneas de archivo.

¿Listo para el siguiente desafío? Prueba a renderizar un lote de URLs en paralelo, o integra esta lógica en un microservicio Spring Boot que devuelva PNG bajo demanda. El cielo es el límite cuando combinas la flexibilidad de Aspose.HTML con las herramientas de concurrencia de Java.

¡Feliz codificación, y no olvides compartir tus historias de éxito en los comentarios!

## ¿Qué deberías aprender a continuación?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}