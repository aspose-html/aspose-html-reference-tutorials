---
title: Ajuste del tamaño de página XPS con Aspose.HTML para Java
linktitle: Ajuste del tamaño de página XPS
second_title: Procesamiento de HTML en Java con Aspose.HTML
description: Aprenda a ajustar el tamaño de las páginas XPS con Aspose.HTML para Java. Controle las dimensiones de salida de sus documentos XPS fácilmente.
weight: 16
url: /es/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuste del tamaño de página XPS con Aspose.HTML para Java


En este tutorial, le guiaremos a través del proceso de ajuste del tamaño de página XPS utilizando Aspose.HTML para Java. Esta potente biblioteca le permite manipular documentos HTML y convertirlos en varios formatos, incluido XPS. Ajustar el tamaño de página es esencial cuando necesita controlar las dimensiones de salida de su documento XPS.

## Prerrequisitos

Antes de comenzar, asegúrese de tener los siguientes requisitos previos:

1. Entorno de desarrollo de Java: asegúrese de tener Java Development Kit (JDK) instalado en su sistema.

2.  Biblioteca Aspose.HTML para Java: debe descargar e incluir la biblioteca Aspose.HTML para Java en su proyecto Java. Puede encontrar la biblioteca[aquí](https://releases.aspose.com/html/java/).

3. Archivo HTML de entrada: Prepare un archivo HTML que desee renderizar y ajuste el tamaño de la página XPS. Puede utilizar su propio archivo HTML para este tutorial.

## Importar paquetes

En primer lugar, debe importar los paquetes necesarios para trabajar con Aspose.HTML para Java. Incluya estos paquetes al comienzo de su clase Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Paso 1: Establezca el nombre del archivo de entrada

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 En este paso, leemos su archivo de entrada HTML usando un`FileInputStream`.

## Paso 2: Crear un documento HTML y establecer estilos

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Este paso implica crear un`HTMLDocument` y añadiéndole estilos.

## Paso 3: Crear opciones de renderizado XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Aquí, creamos opciones de renderizado XPS para configurar el proceso de renderizado.

## Paso 4: Ajustar el tamaño de la página

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Este paso implica establecer el tamaño de la página y especificar si se debe ajustar a la página más ancha.

## Paso 5: Renderizar la salida

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

En el paso final, renderizamos la salida XPS utilizando las opciones configuradas.

## Conclusión

En este tutorial, le mostramos cómo ajustar el tamaño de página XPS con Aspose.HTML para Java. Puede controlar las dimensiones de salida de sus documentos XPS, asegurándose de que cumplan con sus requisitos específicos. Con el código y los pasos proporcionados, puede implementar fácilmente esta función en sus aplicaciones Java.

 Si tiene alguna pregunta o necesita más ayuda, no dude en visitar el[Documentación de Aspose.HTML para Java](https://reference.aspose.com/html/java/) o pedir ayuda en el[Foro de Aspose](https://forum.aspose.com/).

## Preguntas frecuentes

### Q1: ¿Qué es Aspose.HTML para Java?

A1: Aspose.HTML para Java es una biblioteca Java que permite a los desarrolladores manipular y convertir documentos HTML en varios formatos, como XPS, PDF e imágenes.

### P2: ¿Dónde puedo descargar Aspose.HTML para Java?

 A2: Puede descargar la biblioteca Aspose.HTML para Java desde[Este enlace](https://releases.aspose.com/html/java/).

### P3: ¿Hay una prueba gratuita disponible de Aspose.HTML para Java?

 A3: Sí, puede obtener una prueba gratuita de Aspose.HTML para Java desde[aquí](https://releases.aspose.com/).

### P4: ¿Cómo puedo obtener una licencia temporal de Aspose.HTML para Java?

 A4: Para obtener una licencia temporal de Aspose.HTML para Java, visite[Esta página](https://purchase.aspose.com/temporary-license/).

### Q5: ¿Puedo obtener soporte para Aspose.HTML para Java?

 A5: Sí, puede buscar ayuda y apoyo de la comunidad Aspose en el[Foro de Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
