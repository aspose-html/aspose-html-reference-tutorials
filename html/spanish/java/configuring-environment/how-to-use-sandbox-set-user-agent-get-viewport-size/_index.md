---
category: general
date: 2026-04-03
description: Aprende a usar sandbox en Aspose.HTML Java para establecer el agente
  de usuario, definir el tamaño y obtener el tamaño del viewport al instante. Código
  completo, explicaciones y consejos incluidos.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: es
og_description: Aprende a usar sandbox en Aspose.HTML Java para establecer el agente
  de usuario, definir el tamaño y obtener el tamaño del viewport al instante. Guía
  completa con código y mejores prácticas.
og_title: Cómo usar Sandbox – Configurar el agente de usuario y obtener el tamaño
  del viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Cómo usar Sandbox – Configurar el agente de usuario y obtener el tamaño del
  viewport
url: /es/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar Sandbox – Establecer User Agent y obtener el tamaño del Viewport

¿Alguna vez te has preguntado **cómo usar sandbox** al renderizar HTML con Aspose.HTML for Java? Tal vez te hayas topado con un obstáculo al intentar simular un tamaño de pantalla específico o necesites falsificar una cadena de user‑agent para que la página se comporte como si se visitara desde un navegador móvil.  

Lo bueno es que la API sandbox te permite hacer exactamente eso, y también puedes obtener el tamaño del viewport calculado después de que la página se cargue. En este tutorial recorreremos la creación de un sandbox, la configuración del tamaño, la configuración de un user agent personalizado, la carga de una página remota y, finalmente, la lectura de las dimensiones del viewport. Al final sabrás **cómo establecer el tamaño**, **cómo obtener el viewport**, y por qué estos pasos son importantes para un renderizado headless fiable.

> **Resultado rápido:** tendrás una clase Java ejecutable que imprime algo como `Viewport: 1280×800` en segundos.

---

## Lo que necesitarás

- **Aspose.HTML for Java** version 24.6 or newer (the API we use was introduced in 24.5).  
- Un kit de desarrollo Java 17+ (cualquier JDK reciente funciona).  
- Un IDE o un editor de texto simple—no se requieren complementos especiales.  
- Acceso a Internet si deseas cargar una URL externa como `https://example.com`.

Eso es todo. No es obligatorio usar Maven/Gradle; puedes colocar los JARs en el classpath manualmente si lo prefieres.  

---

## Cómo usar Sandbox – Visión general

El sandbox aísla el motor de renderizado del sistema operativo host, permitiéndote definir una pantalla virtual (ancho, alto, DPI) y una cadena **user agent** personalizada. Piensa en él como una ventana de navegador en miniatura que vive completamente en memoria. Cuando más tarde solicites a `HTMLDocument` su vista predeterminada, el motor informará el **tamaño del viewport** que calculó en base a la configuración del sandbox.  

A continuación se muestra un flujo de alto nivel:

1. **Crear** un `DocumentSandbox` y configurar ancho, alto, DPI y user‑agent.  
2. **Cargar** un `HTMLDocument` dentro de ese sandbox.  
3. **Consultar** la vista predeterminada del documento para obtener el tamaño del viewport.  

Vamos a profundizar en cada paso.

---

## Paso 1: Crear un Sandbox y establecer el tamaño

Primero, iniciamos un sandbox y le indicamos cuán grande debe ser la pantalla virtual. Aquí es donde respondes a la pregunta **cómo establecer el tamaño** para un renderizado headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Consejo profesional:** Si estás probando un diseño responsive, prueba un ancho estrecho como `360` para emular un teléfono, o uno amplio como `1920` para un escritorio. El sandbox respeta el DPI que configures, por lo que una pantalla de alta densidad (p. ej., 144 DPI) afectará a las media‑queries que usan `device-pixel-ratio`.

---

## Paso 2: Establecer User Agent para el Sandbox

¿Por qué molestarse con un **user agent** personalizado? Algunos sitios entregan un marcado o scripts diferentes según el navegador reportado. Al llamar a `setUserAgent` puedes engañar a la página haciéndole creer que está siendo visitada desde Chrome, Firefox o un dispositivo móvil.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Ahora la página pensará que se está renderizando en un iPhone. Si necesitas **restablecer el user agent** al predeterminado, simplemente reutiliza la cadena “AsposeHTML/24.6 …” anterior.

---

## Paso 3: Cargar un documento HTML dentro del Sandbox

Con el sandbox listo, podemos cargar cualquier URL o archivo HTML local. El constructor `HTMLDocument` toma el sandbox como segundo argumento, vinculando ambos.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

El bloque `try‑with‑resources` garantiza que el documento se libere correctamente, liberando los recursos nativos que Aspose.HTML asigna internamente.

---

## Paso 4: Obtener el tamaño del Viewport del documento

Este es el momento que has estado esperando: obtener el **tamaño del viewport** que el motor de renderizado calculó. Esto responde a **cómo obtener el viewport** después de que la página se haya dispuesto.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Al ejecutar el programa, deberías ver algo como:

```
Viewport: 1280×800
```

Si cambiaste las dimensiones del sandbox en el Paso 1, los números impresos reflejarán esos nuevos valores—perfecto para pruebas automatizadas que verifican los puntos de quiebre responsive.

---

## Ejemplo completo y funcional

A continuación se muestra la clase completa, lista para ejecutar, que reúne todas las piezas. Copia y pega el código en un archivo llamado `SandboxExample.java`, agrega los JARs de Aspose.HTML a tu classpath y ejecuta `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Salida esperada** (suponiendo la configuración del sandbox anterior):

```
Viewport: 1280×800
```

Si estableces un ancho/alto diferente en el sandbox, la salida cambiará en consecuencia—exactamente lo que necesitas al probar diseños responsive.

---

## Casos límite y preguntas frecuentes

### ¿Qué pasa si la página usa `window.innerWidth` en lugar de media queries CSS?

El tamaño de pantalla virtual del sandbox influye tanto en el layout CSS como en `window.innerWidth/innerHeight` de JavaScript. Por lo tanto, **cómo obtener el viewport** mediante JavaScript devolverá los mismos números que ves en la consola Java.

### ¿Puedo ejecutar varios sandboxes en paralelo?

Sí. Cada instancia de `DocumentSandbox` es independiente, por lo que puedes crear un pool de hilos, asignar a cada hilo su propio sandbox con diferentes dimensiones y renderizar decenas de páginas simultáneamente. Solo recuerda que los JARs son seguros para hilos (lo son).

### ¿Afecta la configuración de DPI al escalado de imágenes?

Absolutamente. Un DPI más alto hace que un píxel CSS se mapee a más píxeles de dispositivo, lo que puede hacer que las imágenes de alta resolución se vean más nítidas. Si estás probando recursos estilo retina, prueba `sandbox.setDeviceDpi(144)`.

### ¿Cómo manejo certificados HTTPS que son auto‑firmados

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}