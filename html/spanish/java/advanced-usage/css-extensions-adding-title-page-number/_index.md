---
date: 2025-12-05
description: Aprenda cómo establecer los márgenes de página HTML en Java usando Aspose.HTML
  y añada números de página y títulos a sus documentos.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Cómo establecer los márgenes de una página HTML en Java con Aspose.HTML
url: /es/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer márgenes de página HTML en Java con Aspose.HTML

En este tutorial descubrirá **cómo establecer márgenes de página HTML en Java**‑style usando Aspose.HTML para Java. Recorreremos la creación de márgenes de página personalizados, la inserción de números de página y la adición de un título de documento, todo con código claro, paso a paso, que puede copiar en su propio proyecto.

## Respuestas rápidas
- **¿Qué biblioteca se necesita?** Aspose.HTML for Java  
- **¿Puedo controlar los márgenes programáticamente?** Sí, mediante una regla CSS `@page` en la hoja de estilo del usuario  
- **¿Qué formatos de salida admiten márgenes?** XPS, PDF y otros formatos rasterizados  
- **¿Necesito una licencia para producción?** Se requiere una licencia válida de Aspose.HTML para uso que no sea de prueba  
- **¿Es compatible con Java 11+?** Absolutamente – la biblioteca funciona con versiones modernas de Java  

## ¿Qué es “establecer márgenes de página HTML en Java”?
Establecer márgenes de página HTML en Java significa configurar el motor de renderizado (proporcionado por Aspose.HTML) para aplicar propiedades CSS de caja de página antes de que el documento se convierta a un formato imprimible como XPS o PDF. Al definir una regla `@page` personalizada controla el área imprimible, los números de página y el contenido de encabezado/pie de página.

## ¿Por qué usar Aspose.HTML para el control de márgenes?
- **Diseño preciso** – CSS `@page` le brinda control píxel a píxel sobre márgenes, encabezados y pies de página.  
- **Consistencia entre formatos** – Las mismas definiciones de margen funcionan para XPS, PDF y salidas de imagen.  
- **Sin dependencia del navegador** – El renderizado ocurre del lado del servidor, por lo que no necesita un navegador sin cabeza.  

## Requisitos previos

Antes de comenzar, asegúrese de contar con los siguientes requisitos:

1. **Entorno de desarrollo Java** – JDK 11 o posterior instalado.  
2. **Aspose.HTML for Java** – Descargue e instale la biblioteca desde [here](https://releases.aspose.com/html/java/).  

## Importar paquetes

Para comenzar, importe las clases necesarias de Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Cómo establecer márgenes de página HTML en Java – Guía paso a paso

### Paso 1: Inicializar la configuración y definir márgenes de página personalizados

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

En este bloque creamos un objeto `Configuration`, obtenemos el `IUserAgentService` e inyectamos una regla CSS `@page` que define los márgenes, un contador de página en la esquina inferior derecha y un título del documento centrado en la parte superior.

### Paso 2: Crear el documento HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Aquí instanciamos un `HTMLDocument` con un fragmento simple “Hello World”. La misma configuración del Paso 1 se aplica, de modo que los márgenes personalizados se respetan al renderizar el documento.

### Paso 3: Renderizar a un archivo XPS (o cualquier salida compatible)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Este paso crea un `XpsDevice` que escribe las páginas renderizadas en `output.xps`. Los márgenes, números de página y título que definió anteriormente aparecerán en el archivo final.

## Problemas comunes y consejos

- **Los márgenes aparecen sin cambios** – Asegúrese de que la regla `@page` no sea sobrescrita por otras hojas de estilo. La llamada `setUserStyleSheet` la fuerza con la máxima prioridad.  
- **Los números de página muestran “NaN”** – Verifique que esté usando Aspose.HTML versión 23.10 o posterior; versiones anteriores carecen de la función `currentPageNumber()`.  
- **El archivo de salida está en blanco** – Confirme que la ruta `Resources.output` se resuelva correctamente y que tenga permisos de escritura.  

## Preguntas frecuentes

### Q1: ¿Qué es Aspose.HTML for Java?

**A:** Aspose.HTML for Java es una biblioteca Java que proporciona herramientas potentes para trabajar con documentos HTML en aplicaciones Java, incluyendo conversión, renderizado y manipulación.

### Q2: ¿Puedo personalizar aún más los márgenes de página?

**A:** Sí, simplemente edite el CSS dentro de `setUserStyleSheet`. Puede cambiar cualquiera de los valores `margin-*` o añadir cajas `@top-*` / `@bottom-*` adicionales.

### Q3: ¿Cómo puedo agregar más contenido al documento HTML?

**A:** Reemplace la cadena en `new HTMLDocument("<div>Hello World!!!</div>", …)` con su propio marcado HTML, o cargue un archivo externo usando el constructor `HTMLDocument(String url, …)`.

### Q4: ¿Aspose.HTML for Java es compatible con otros formatos de documento?

**A:** Absolutamente. El mismo `HTMLDocument` puede renderizarse a PDF, XPS, imágenes o incluso EPUB cambiando el dispositivo de salida (p. ej., `PdfDevice`, `PngDevice`).

### Q5: ¿Necesito una licencia para usar Aspose.HTML for Java?

**A:** Sí, se requiere una licencia para uso en producción. Puede obtener una versión de prueba o comprar una licencia desde [here](https://purchase.aspose.com/buy) o [here](https://releases.aspose.com/).

### Q6: ¿Cómo establezco diferentes márgenes para páginas impares y pares?

**A:** Use las pseudo‑clases `@page :left` y `@page :right` dentro de su hoja de estilo para definir márgenes distintos para páginas izquierda (pares) y derecha (impares).

### Q7: ¿Puedo incrustar fuentes personalizadas en el documento renderizado?

**A:** Sí. Añada reglas `@font-face` a la hoja de estilo del usuario y haga referencia a las fuentes en su contenido HTML.

## Conclusión

Ahora domina **cómo establecer márgenes de página HTML en Java** usando Aspose.HTML, y sabe cómo agregar números de página y un título para que sus documentos luzcan profesionales. Siéntase libre de experimentar con cajas `@page` adicionales, fuentes personalizadas o diferentes formatos de salida para adaptarse a las necesidades de su proyecto.

Si encuentra algún desafío, la documentación oficial de [Aspose.HTML for Java](https://reference.aspose.com/html/java/) y el [foro de soporte de Aspose](https://forum.aspose.com/) son excelentes lugares para obtener ayuda.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Última actualización:** 2025-12-05  
**Probado con:** Aspose.HTML for Java 23.12  
**Autor:** Aspose  

---