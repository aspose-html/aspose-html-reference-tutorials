---
title: Ajuste el tamaño de la página PDF con Aspose.HTML para Java
linktitle: Ajustar el tamaño de la página PDF
second_title: Procesamiento HTML de Java con Aspose.HTML
description: Aprenda a ajustar el tamaño de la página PDF con Aspose.HTML para Java. Cree archivos PDF de alta calidad a partir de HTML sin esfuerzo. Controle las dimensiones de la página de forma eficaz.
type: docs
weight: 15
url: /es/java/advanced-usage/adjust-pdf-page-size/
---

En la era digital actual, la necesidad de generar archivos PDF de alta calidad a partir de contenido HTML va en aumento. Aspose.HTML para Java es una poderosa biblioteca de Java que le permite convertir documentos HTML a formato PDF sin esfuerzo. En este tutorial, nos centraremos en ajustar el tamaño de la página al convertir HTML a PDF usando Aspose.HTML para Java.

## Requisitos previos

Antes de comenzar, asegúrese de cumplir con los siguientes requisitos previos:

- Entorno de desarrollo de Java: asegúrese de tener el kit de desarrollo de Java (JDK) instalado en su sistema.
-  Aspose.HTML para Java: debe descargar e instalar Aspose.HTML para Java desde el sitio web[aquí](https://releases.aspose.com/html/java/).
- Documento HTML: debe tener un documento HTML listo para la conversión. De lo contrario, cree uno o utilice un archivo HTML existente.

## Importar paquetes

Para comenzar, necesita importar los paquetes necesarios para trabajar con Aspose.HTML para Java. El siguiente fragmento de código demuestra cómo hacer esto:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Ahora que cuenta con los requisitos previos y ha importado los paquetes necesarios, dividamos el proceso de ajuste del tamaño de la página PDF en varios pasos:

## Paso 1: leer contenido HTML

Primero, necesitas leer el contenido HTML que deseas convertir a PDF. En este ejemplo, leeremos el HTML de un archivo llamado "FirstFile.html".

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Paso 2: escribir contenido HTML

A continuación, escribirá el contenido HTML en un archivo llamado "FirstFileOut.html".

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Agregue estilos o contenido HTML personalizados aquí
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Paso 3: renderizar HTML a PDF

Ahora, renderizará el contenido HTML en un archivo PDF. Cubriremos dos escenarios: uno donde el tamaño de la página no se ajusta al ancho del contenido y otro donde sí se ajusta.

### Tamaño de página no ajustado

En este escenario, el tamaño de la página se establece en un ancho y alto fijos, lo que puede recortar el contenido si excede estas dimensiones.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Cree una instancia de HTMLDocument a partir del archivo HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Establecer opciones de renderizado de PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizar la salida
pdf_renderer.render(device, html_document);
```

### Tamaño de página ajustado al ancho del contenido

En este escenario, el tamaño de la página se ajusta según el ancho del contenido.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizar la salida
pdf_renderer.render(device, html_document);
```

## Conclusión

En este tutorial, hemos explorado cómo ajustar el tamaño de la página PDF al convertir HTML a PDF usando Aspose.HTML para Java. Aprendió los requisitos previos, importó los paquetes necesarios y siguió una guía paso a paso para realizar esta tarea. Con Aspose.HTML para Java, puede controlar fácilmente el tamaño de página de sus archivos PDF generados, asegurándose de que su contenido se muestre según lo previsto.

 Siéntase libre de experimentar con diferentes tamaños de página y configuraciones para satisfacer sus requisitos específicos. Si tiene algún problema o tiene más preguntas, no dude en buscar ayuda del[Aspose.HTML para la documentación de Java](https://reference.aspose.com/html/java/) o el[Aspose foro de soporte](https://forum.aspose.com/).

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para Java?

R1: Aspose.HTML para Java es una biblioteca de Java que le permite trabajar con documentos HTML, manipularlos, convertirlos y renderizarlos a varios formatos, incluido PDF.

### P2: ¿Cómo puedo ajustar el tamaño de la página PDF al convertir HTML a PDF con Aspose.HTML para Java?

 A2: Puede ajustar el tamaño de la página PDF utilizando el`PageSetup` clase y establecer el`AdjustToWidestPage` propiedad a`true` o "falso", según sus requisitos.

### P3: ¿Puedo personalizar el estilo del contenido HTML antes de convertirlo a PDF?

R3: Sí, puedes personalizar el estilo agregando elementos CSS y HTML a tu contenido HTML antes de convertirlo a PDF, como se demuestra en el tutorial.

### P4: ¿Dónde puedo encontrar la documentación de Aspose.HTML para Java?

 A4: Puede consultar la documentación.[aquí](https://reference.aspose.com/html/java/) para obtener información completa y ejemplos.

### P5: ¿Hay una prueba gratuita disponible para Aspose.HTML para Java?

 R5: Sí, puede acceder a una prueba gratuita de Aspose.HTML para Java desde[este enlace](https://releases.aspose.com/).