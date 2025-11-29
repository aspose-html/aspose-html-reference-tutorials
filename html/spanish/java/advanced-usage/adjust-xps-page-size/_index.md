---
date: 2025-11-29
description: Aprende cómo convertir HTML a XPS y ajustar el tamaño de página XPS usando
  Aspose.HTML para Java. Controla fácilmente las dimensiones de salida.
language: es
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Convertir HTML a XPS y ajustar el tamaño de página XPS con Aspose.HTML para
  Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML a XPS y ajustar el tamaño de página XPS con Aspose.HTML para Java

En este tutorial descubrirá **cómo convertir HTML a XPS** y ajustar finamente el tamaño de página resultante usando Aspose.HTML para Java. Ya sea que esté generando informes imprimibles, facturas o documentos de archivo, controlar las dimensiones del XPS garantiza que la salida se vea exactamente como espera. Recorreremos cada paso—desde la configuración del entorno hasta la generación del archivo XPS final—para que pueda integrar esta capacidad en sus aplicaciones Java de inmediato.

## Respuestas rápidas
- **¿Qué significa “convertir HTML a XPS”?** Renderiza un documento HTML en un archivo XPS, preservando el diseño y el estilo.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Qué versión de Java es compatible?** Java 8 o superior (se recomienda JDK 11+).  
- **¿Puedo cambiar el tamaño de página?** Sí – Aspose.HTML le permite especificar dimensiones personalizadas antes de la generación.  
- **¿Cuánto tiempo lleva la conversión?** Normalmente menos de un segundo para páginas estándar; documentos más grandes pueden tardar más.

## ¿Qué es convertir HTML a XPS?
Convertir HTML a XPS significa tomar un archivo de marcado orientado a la web y producir un documento XPS (XML Paper Specification), un formato de diseño fijo y listo para imprimir similar al PDF. Esto es útil cuando necesita documentos de alta fidelidad e independientes del dispositivo para archivado o impresión desde aplicaciones Java.

## ¿Por qué ajustar el tamaño de página XPS?
Ajustar el tamaño de página le brinda control sobre las dimensiones físicas del documento final (p. ej., A4, Letter, etiquetas personalizadas). Evita escalados no deseados, asegura que el contenido encaje perfectamente y puede reducir el tamaño del archivo al eliminar espacios en blanco innecesarios.

## Requisitos previos

Antes de comenzar, asegúrese de tener los siguientes requisitos previos:

1. **Entorno de desarrollo Java** – Java Development Kit (JDK) instalado en su sistema.  
2. **Biblioteca Aspose.HTML para Java** – Descargue e incluya la biblioteca Aspose.HTML para Java en su proyecto. Puede encontrar la biblioteca [aquí](https://releases.aspose.com/html/java/).  
3. **Archivo HTML de entrada** – Prepare un archivo HTML que desea renderizar y ajustar el tamaño de página XPS. Puede usar su propio archivo HTML para este tutorial.

## Importar paquetes

Primero, importe las clases que necesitará. Estos paquetes le dan acceso a funcionalidades de manejo de documentos, renderizado y configuración de página.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Paso 1: Establecer el nombre del archivo de entrada

Lea el archivo HTML de origen usando un `FileInputStream`. Este flujo alimenta el HTML sin procesar al motor de Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Paso 2: Crear un documento HTML y establecer estilos

Cree una instancia de `HTMLDocument` que representa el contenido que va a renderizar. En este ejemplo también inyectamos un pequeño bloque CSS para demostrar el estilo—siéntase libre de reemplazarlo con su propio marcado.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## Paso 3: Crear opciones de renderizado XPS

Instancie `XpsRenderingOptions` para contener todas las configuraciones que afectan la conversión de HTML a XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Paso 4: Ajustar el tamaño de página

Defina un tamaño de página personalizado (ancho × alto en puntos) y indique al renderizador si debe expandirse automáticamente a la página más ancha. Configurar `adjustToWidestPage` a `false` preserva las dimensiones exactas que especifique.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Paso 5: Generar la salida

Finalmente, cree un `XpsDevice` con las opciones configuradas y renderice el documento HTML. El resultado es un archivo XPS completamente formado con las dimensiones de página personalizadas que estableció.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problemas comunes y soluciones

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Salida XPS en blanco** | Flujo de entrada no cerrado o HTMLDocument apunta al archivo incorrecto. | Asegúrese de que el `FileInputStream` esté correctamente envuelto en un bloque try‑with‑resources y que la ruta del archivo sea exacta. |
| **Tamaño de página no aplicado** | `adjustToWidestPage` quedó en `true`. | Establezca `pageSetup.setAdjustToWidestPage(false);` como se muestra en el Paso 4. |
| **CSS no compatible** | Aspose.HTML solo soporta un subconjunto de CSS. | Limítese a diseños básicos, fuentes y colores; evite selectores avanzados o CSS Grid. |
| **LicenseException** | Ejecutar sin una licencia válida en producción. | Aplique su licencia temporal o comprada antes de renderizar (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Preguntas frecuentes

**P: ¿Qué es Aspose.HTML para Java?**  
R: Aspose.HTML para Java es una biblioteca Java que permite a los desarrolladores manipular y convertir documentos HTML a varios formatos, como XPS, PDF e imágenes.

**P: ¿Dónde puedo descargar Aspose.HTML para Java?**  
R: Puede descargar la biblioteca Aspose.HTML para Java desde [este enlace](https://releases.aspose.com/html/java/).

**P: ¿Hay una prueba gratuita disponible para Aspose.HTML para Java?**  
R: Sí, puede obtener una prueba gratuita de Aspose.HTML para Java desde [aquí](https://releases.aspose.com/).

**P: ¿Cómo puedo obtener una licencia temporal para Aspose.HTML para Java?**  
R: Para obtener una licencia temporal para Aspose.HTML para Java, visite [esta página](https://purchase.aspose.com/temporary-license/).

**P: ¿Puedo obtener soporte para Aspose.HTML para Java?**  
R: Sí, puede buscar ayuda y soporte en la comunidad de Aspose en el [Foro de Aspose](https://forum.aspose.com/).

**P: ¿Puedo convertir HTML a XPS en un servidor sin interfaz gráfica?**  
R: Absolutamente. Aspose.HTML funciona en entornos sin GUI; solo asegúrese de que el runtime de Java esté configurado correctamente.

**P: ¿La biblioteca soporta márgenes de página personalizados?**  
R: Sí. Use `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., antes de asignar el `PageSetup` a las opciones de renderizado.

## Conclusión

Hemos recorrido todo el proceso de **convertir HTML a XPS** y ajustar el tamaño de página con Aspose.HTML para Java. Siguiendo estos pasos, podrá generar documentos XPS listos para imprimir que coincidan con sus requisitos de diseño exactos. Siéntase libre de experimentar con diferentes dimensiones de página, estilos, o incluso agregar encabezados y pies de página para adaptarse a las necesidades de su proyecto.

Si tiene alguna pregunta o necesita más ayuda, explore la [documentación de Aspose.HTML para Java](https://reference.aspose.com/html/java/) o únase a la conversación en el [Foro de Aspose](https://forum.aspose.com/).

**Última actualización:** 2025-11-29  
**Probado con:** Aspose.HTML for Java 24.11 (última versión al momento de escribir)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}