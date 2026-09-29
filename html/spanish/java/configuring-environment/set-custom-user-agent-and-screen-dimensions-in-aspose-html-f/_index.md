---
category: general
date: 2026-09-29
description: Establezca un agente de usuario personalizado en Aspose.HTML para Java
  y aprenda cómo definir el tamaño de pantalla virtual para una renderización precisa
  de HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: es
lastmod: 2026-09-29
og_description: Establezca un agente de usuario personalizado en Aspose.HTML para
  Java y aprenda cómo configurar el tamaño de pantalla virtual para una representación
  precisa de HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Establecer agente de usuario personalizado y dimensiones de pantalla en
  Aspose.HTML para Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Establecer agente de usuario y dimensiones de pantalla personalizados en Aspose.HTML
  para Java
url: /es/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer agente de usuario personalizado y dimensiones de pantalla en Aspose.HTML para Java

Si necesita **establecer agente de usuario personalizado** mientras renderiza HTML con Aspose.HTML para Java, esta guía le muestra exactamente cómo hacerlo. Al configurar un sandbox también obtiene la capacidad de **establecer el tamaño de pantalla virtual**, asegurando que el diseño coincida con el viewport de un navegador real.

Terminará este tutorial con un programa completo y ejecutable que **especifica el agente de usuario**, **establece el ancho de pantalla** y **establece la altura de pantalla**. No se requieren herramientas externas, solo Aspose.HTML para Java y un runtime de Java 8+.

## Lo que aprenderá

* Cómo crear un `SandboxConfiguration` para aislar el renderizado.
* Cómo **establecer agente de usuario personalizado** y por qué es importante para páginas responsivas.
* Cómo **establecer el tamaño de pantalla virtual** (ancho y altura de pantalla) para un diseño preciso.
* Cómo cargar un archivo HTML en el sandbox y guardar el resultado procesado.
* Problemas comunes y consejos de mejores prácticas para el renderizado en sandbox.

> **Requisitos previos** – Necesita una licencia válida de Aspose.HTML para Java, Java 8 o superior, y un IDE (IntelliJ IDEA, Eclipse o VS Code). El ejemplo usa un archivo local `input.html`, pero cualquier URL accesible funciona.

![Diagrama de flujo del sandbox](sandbox-flow.png "ejemplo de establecer agente de usuario personalizado en Java")

## Paso 1: Crear una configuración de sandbox (la base)

El sandbox aísla el entorno de renderizado de la JVM host, lo cual es esencial cuando desea **establecer agente de usuario personalizado** o cambiar el tamaño del viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*¿Por qué este paso?*  
`SandboxConfiguration` contiene todas las opciones de renderizado, incluyendo **dimensiones de pantalla** y cadenas **user‑agent**. Al configurarlo antes de cargar el documento, garantiza que el motor HTML respete esas configuraciones desde la primera solicitud.

## Paso 2: Establecer dimensiones de pantalla para imitar un dispositivo real

Los sitios responsivos a menudo leen `window.innerWidth` y `window.innerHeight`. Para hacer que el motor piense que se ejecuta en una pantalla de 1024 × 768, usted **establece el tamaño de pantalla virtual**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*¿Por qué es importante?* – Si omite **establecer dimensiones de pantalla**, el renderizador puede usar un viewport diminuto, haciendo que las consultas de medios CSS seleccionen el diseño móvil. Al **establecer explícitamente el ancho de pantalla** y **establecer la altura de pantalla**, controla qué reglas CSS se aplican.

## Paso 3: Especificar una cadena de user‑agent personalizada

Algunas páginas web entregan contenido diferente según el encabezado user‑agent. Para **especificar el agente de usuario** simplemente configúrelo en la configuración del sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*¿Por qué usar un agente de usuario personalizado?*  
Una cadena personalizada puede eludir la detección de bots, activar funciones solo de escritorio o probar cómo se comporta un sitio para una versión específica de navegador. El motor Aspose reenvía este valor con cada solicitud HTTP realizada al cargar recursos externos (CSS, imágenes, scripts).

## Paso 4: Cargar el documento HTML dentro del sandbox

Ahora que el sandbox está completamente configurado, cargue el archivo HTML. El constructor que recibe una ruta de archivo y un `SandboxConfiguration` aplica automáticamente todas las configuraciones que definimos.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Si necesita cargar desde una URL remota, reemplace la ruta del archivo con la cadena URL—Aspose.HTML seguirá respetando el **agente de usuario personalizado establecido** y las **dimensiones de pantalla**.

## Paso 5: Guardar la salida procesada

Después de que el documento termine de cargarse, puede guardarlo en cualquier formato compatible. Aquí escribimos un archivo HTML en sandbox que refleja cualquier cambio en el DOM causado por la configuración personalizada.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

El archivo guardado contendrá el mismo marcado, pero cualquier script que haya consultado `navigator.userAgent` o inspeccionado `window.innerWidth` ahora verá los valores que usted proporcionó.

## Ejemplo completo y ejecutable

Al combinar todos los pasos obtiene un programa autónomo que puede copiar, pegar y ejecutar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Salida esperada

Ejecutar el programa crea `sandboxed_output.html`. Si lo abre en un navegador e inspecciona `navigator.userAgent` mediante la consola, verá **AsposeHTML/1.0**. De manera similar, `window.innerWidth` reportará **1024**, confirmando que **establecer dimensiones de pantalla** funcionó como se esperaba.

## Preguntas comunes y manejo de casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si la página carga recursos adicionales de un dominio diferente?** | El sandbox reenvía el **agente de usuario personalizado** con cada solicitud, pero las políticas de origen cruzado siguen aplicándose. Use `sandboxConfig.setAllowCrossDomain(true)` si necesita relajar esas restricciones. |
| **¿Puedo cambiar el tamaño de pantalla después de que el documento se haya cargado?** | No. Las dimensiones de pantalla se leen durante la pasada inicial de diseño. Para renderizar con un tamaño diferente, cree una nueva `SandboxConfiguration` y vuelva a cargar el documento. |
| **¿Necesito llamar a `document.close()`?** | El `HTMLDocument` implementa `AutoCloseable`. Usar un bloque try‑with‑resources garantiza una limpieza adecuada, pero el `close()` explícito es opcional en scripts simples. |
| **¿En qué se diferencia esto de establecer un user‑agent en un cliente HTTP?** | Establecer el user‑agent en el sandbox afecta **todas** las solicitudes de recursos realizadas por el motor HTML, no solo la obtención inicial del HTML. Esto imita más de cerca a un navegador real. |
| **¿Es seguro el sandbox para HTML no confiable?** | Sí. El sandbox aísla el acceso al sistema de archivos y limita las llamadas de red según la configuración, reduciendo el riesgo de que scripts maliciosos afecten su JVM host. |

## Consejos profesionales

* **Reutilizar configuraciones** – Si renderiza muchas páginas con el mismo viewport, cree un único `SandboxConfiguration` y reutilícelo para evitar la sobrecarga de creación de objetos.
* **Depurar con registro** – Active el registro de Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) para ver qué recursos se obtuvieron con el agente de usuario personalizado.
* **Combinar con consultas de medios CSS** – Al ajustar **establecer ancho de pantalla** puede probar cómo se comporta su diseño responsivo en tablets, teléfonos o escritorios grandes sin abrir un navegador real.

## Conclusión

Ahora sabe cómo **establecer un agente de usuario personalizado** y **establecer dimensiones de pantalla** al renderizar HTML con Aspose.HTML para Java. Al configurar un sandbox, aísla el entorno, controla el viewport y asegura que los recursos externos vean los encabezados exactos que especifica. Esta técnica es esencial para probar diseños responsivos, eludir bloqueos de bots o reproducir funciones solo de escritorio en pipelines automatizados.

A continuación, podría explorar **cómo establecer cookies personalizadas** o **capturar capturas de pantalla renderizadas** usando la API de renderizado de Aspose.HTML—ambos conceptos se basan en el mismo patrón de configuración de sandbox que acaba de dominar.

¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Renderizado de alta DPI en Java – Capturar capturas de pantalla de páginas web con agente de usuario personalizado](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Cómo cargar HTML, establecer DPI del dispositivo y leer el color de fondo](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Crear archivo HTML Java y configurar el servicio de red (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}