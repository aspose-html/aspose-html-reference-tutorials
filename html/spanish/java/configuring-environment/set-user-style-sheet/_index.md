---
date: 2025-12-05
description: Aprenda a crear PDF a partir de HTML configurando una hoja de estilo
  de usuario personalizada en Aspose.HTML para Java y convierta fácilmente HTML a
  PDF con el Servicio de Agente de Usuario.
language: es
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Crear PDF a partir de HTML – Establecer hoja de estilo de usuario en Aspose.HTML
  para Java
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF a partir de HTML – Establecer hoja de estilo de usuario en Aspose.HTML para Java

## Introducción
En este tutorial aprenderá a **crear PDF a partir de HTML** usando Aspose.HTML para Java mientras aplica una hoja de estilo de usuario personalizada.  
¿Alguna vez ha querido ajustar la apariencia de sus documentos HTML con su propio estilo único? Imagine que está creando una página web y necesita que los encabezados destaquen con un color específico o que los párrafos se vean consistentes en todos los dispositivos. Aquí es donde una *hoja de estilo de usuario* y el **User Agent Service** entran en juego. Recorreremos cada paso —desde escribir un archivo HTML simple, configurar el agente de usuario, hasta finalmente **convertir HTML a PDF**— para que pueda ver el resultado al instante.

## Respuestas rápidas
- **¿Qué significa “crear PDF a partir de HTML”?** Significa renderizar un documento HTML (con CSS, imágenes, fuentes, etc.) y guardar la salida visual como un archivo PDF.  
- **¿Qué componente de Aspose se requiere?** La biblioteca Aspose.HTML for Java proporciona el motor de conversión y el User Agent Service.  
- **¿Necesito una licencia para pruebas?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo usar un archivo CSS externo?** Sí — puede enlazar hojas de estilo externas como en un navegador normal.  
- **¿Cuánto tiempo tarda la conversión?** Para un documento simple como el de esta guía, la conversión se completa en menos de un segundo.

## Requisitos previos
Antes de sumergirnos en el código, asegúrese de tener lo siguiente:

1. **Aspose.HTML for Java** – descargue el JAR más reciente desde la [página de lanzamientos de Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – asegúrese de que `java -version` muestre la versión 8 o superior.  
3. **IDE** – IntelliJ IDEA, Eclipse o NetBeans funcionarán bien.  
4. **Conocimientos básicos de HTML/CSS** – útiles pero no obligatorios.

## Importar paquetes
Para comenzar, importe las clases Java esenciales. La única importación explícita que necesita para este ejemplo es `java.io.IOException`; las clases de Aspose se referencian con nombres totalmente calificados más adelante.

```java
import java.io.IOException;
```

## Paso 1: Crear un documento HTML simple
Primero, escribiremos un archivo HTML mínimo (`document.html`) que servirá como origen para nuestra conversión a PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Consejo profesional:** Mantenga el archivo HTML en el mismo directorio que su código fuente Java para evitar problemas relacionados con rutas.

## Paso 2: Configurar Aspose.HTML
Cree un objeto `Configuration`. Este objeto actúa como contenedor para todos los servicios (incluido el User Agent Service) que usará más adelante.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Paso 3: Acceder al User Agent Service  
El **User Agent Service** le permite inyectar una hoja de estilo personalizada, establecer el conjunto de caracteres predeterminado y controlar otras opciones de renderizado.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Paso 4: Definir y aplicar la hoja de estilo de usuario  
Ahora proporcionamos las reglas CSS que estilizarán el HTML cuando se renderice. Aquí es donde **usamos el user agent service** para establecer la hoja de estilo.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Por qué es importante:** Al aplicar una hoja de estilo a nivel de agente de usuario, se asegura de que los estilos se respeten incluso si el HTML original no hace referencia a un archivo CSS.

## Paso 5: Cargar el documento HTML con la configuración personalizada  
Pase tanto la ruta del archivo como la instancia `Configuration` al constructor `HTMLDocument`. Esto vincula la hoja de estilo de usuario al documento.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Paso 6: Convertir HTML a PDF  
Con el documento completamente estilizado, invoque el método estático `convertHTML` para **convertir HTML a PDF**. El objeto `PdfSaveOptions` le permite ajustar finamente la salida (p. ej., tamaño de página, compresión).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Resultado:** `user-agent-stylesheet_out.pdf` contendrá el encabezado en marrón y el párrafo con un fondo GhostWhite, exactamente como se definió en la hoja de estilo.

## Paso 7: Liberar recursos  
Siempre libere los objetos de Aspose para liberar la memoria nativa.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| **Salida PDF en blanco** | No se aplicó la hoja de estilo o el documento no se cargó con la configuración. | Verifique que `configuration` se pase a `HTMLDocument` y que `setUserStyleSheet` se llame antes de cargar. |
| **Advertencia de propiedad CSS no compatible** | Aspose.HTML no admite algunas características avanzadas de CSS. | Utilice solo las propiedades CSS listadas en la documentación de Aspose.HTML o recurra a estilos más simples. |
| **FileNotFoundException** | Ruta incorrecta a `document.html`. | Use una ruta absoluta o coloque el archivo HTML en la raíz del proyecto. |

## Preguntas frecuentes

**P: ¿Puedo aplicar estilos diferentes para distintos elementos HTML?**  
R: ¡Absolutamente! Puede definir tantas reglas CSS como necesite dentro de la hoja de estilo de usuario.

**P: ¿Qué pasa si necesito cambiar la hoja de estilo dinámicamente?**  
R: Llame a `setUserStyleSheet` nuevamente antes de crear una nueva instancia de `HTMLDocument`; los nuevos estilos se aplicarán en la siguiente conversión.

**P: ¿Es posible usar archivos CSS externos con Aspose.HTML for Java?**  
R: Sí — puede enlazar una hoja de estilo externa en el HTML o cargar su contenido y pasarlo a `setUserStyleSheet`.

**P: ¿Cómo maneja Aspose.HTML las propiedades CSS no compatibles?**  
R: Las propiedades no compatibles se ignoran, permitiendo que el resto de la hoja de estilo se renderice sin errores.

**P: ¿Puedo convertir HTML a formatos diferentes de PDF?**  
R: Sí, Aspose.HTML admite la conversión a XPS, TIFF, PNG, JPEG y más usando la clase `SaveOptions` apropiada.

## Conclusión
Ahora ha visto cómo **crear PDF a partir de HTML** estableciendo una hoja de estilo de usuario personalizada con Aspose.HTML for Java. Este flujo de trabajo le brinda control total sobre la apariencia visual del PDF generado, lo que lo hace ideal para la generación automática de informes, la creación de facturas o cualquier escenario donde el estilo consistente sea crucial. Siéntase libre de experimentar con CSS más complejo, fuentes externas o formatos de conversión adicionales para ampliar esta base.

---

**Última actualización:** 2025-12-05  
**Probado con:** Aspose.HTML for Java 24.11 (última versión al momento de escribir)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}