---
title: Ajuste el tamaño de la página XPS con Aspose.HTML para Java
linktitle: Ajustar el tamaño de página XPS
second_title: Procesamiento HTML de Java con Aspose.HTML
description: Aprenda a ajustar el tamaño de la página XPS con Aspose.HTML para Java. Controle fácilmente las dimensiones de salida de sus documentos XPS.
type: docs
weight: 16
url: /es/java/advanced-usage/adjust-xps-page-size/
---

En este tutorial, lo guiaremos a través del proceso de ajustar el tamaño de la página XPS usando Aspose.HTML para Java. Esta poderosa biblioteca le permite manipular documentos HTML y representarlos en varios formatos, incluido XPS. Ajustar el tamaño de la página es esencial cuando necesita controlar las dimensiones de salida de su documento XPS.

## Requisitos previos

Antes de comenzar, asegúrese de cumplir con los siguientes requisitos previos:

1. Entorno de desarrollo de Java: asegúrese de tener el kit de desarrollo de Java (JDK) instalado en su sistema.

2.  Biblioteca Aspose.HTML para Java: debe descargar e incluir la biblioteca Aspose.HTML para Java en su proyecto Java. Puedes encontrar la biblioteca.[aquí](https://releases.aspose.com/html/java/).

3. Archivo HTML de entrada: prepare un archivo HTML que desee representar y ajuste el tamaño de la página XPS. Puede utilizar su propio archivo HTML para este tutorial.

## Importar paquetes

Primero, necesita importar los paquetes necesarios para trabajar con Aspose.HTML para Java. Incluya estos paquetes al comienzo de su clase de Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Paso 1: establezca el nombre del archivo de entrada

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 En este paso, leemos su archivo de entrada HTML usando un`FileInputStream`.

## Paso 2: cree un documento HTML y establezca estilos

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

 Este paso implica crear un`HTMLDocument` y agregarle estilos.

## Paso 3: cree opciones de renderizado XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Aquí, creamos opciones de renderizado XPS para configurar el proceso de renderizado.

## Paso 4: ajuste el tamaño de la página

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Este paso implica configurar el tamaño de la página y especificar si se ajusta a la página más ancha.

## Paso 5: renderizar la salida

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

En el paso final, renderizamos la salida XPS usando las opciones configuradas.

## Conclusión

En este tutorial, le mostramos cómo ajustar el tamaño de la página XPS usando Aspose.HTML para Java. Puede controlar las dimensiones de salida de sus documentos XPS, asegurándose de que cumplan con sus requisitos específicos. Con el código y los pasos proporcionados, puede implementar fácilmente esta función en sus aplicaciones Java.

 Si tiene alguna pregunta o necesita más ayuda, no dude en visitar el[Aspose.HTML para la documentación de Java](https://reference.aspose.com/html/java/) o pedir ayuda en el[Foro Aspose](https://forum.aspose.com/).

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para Java?

R1: Aspose.HTML para Java es una biblioteca de Java que permite a los desarrolladores manipular y convertir documentos HTML a varios formatos, como XPS, PDF e imágenes.

### P2: ¿Dónde puedo descargar Aspose.HTML para Java?

 R2: Puede descargar la biblioteca Aspose.HTML para Java desde[este enlace](https://releases.aspose.com/html/java/).

### P3: ¿Hay una prueba gratuita disponible para Aspose.HTML para Java?

 R3: Sí, puede obtener una prueba gratuita de Aspose.HTML para Java desde[aquí](https://releases.aspose.com/).

### P4: ¿Cómo puedo obtener una licencia temporal de Aspose.HTML para Java?

 R4: Para obtener una licencia temporal de Aspose.HTML para Java, visite[esta página](https://purchase.aspose.com/temporary-license/).

### P5: ¿Puedo obtener soporte para Aspose.HTML para Java?

 R5: Sí, puede buscar ayuda y apoyo de la comunidad de Aspose en el[Foro Aspose](https://forum.aspose.com/).