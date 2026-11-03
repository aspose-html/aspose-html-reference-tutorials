---
category: general
date: 2026-04-02
description: Aprende cómo establecer DPI, definir el tamaño del viewport y configurar
  el agente de usuario en Aspose.HTML Sandbox. Ejemplo paso a paso en Java con código
  completo y consejos.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: es
og_description: Domina cómo establecer el DPI, el tamaño del viewport y el agente
  de usuario en Aspose.HTML Sandbox con un ejemplo completo en Java.
og_title: Cómo establecer DPI en Aspose.HTML Sandbox – Tutorial de Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Cómo establecer DPI en Aspose.HTML Sandbox – Guía completa de Java
url: /es/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer DPI en Aspose.HTML Sandbox – Guía completa de Java

¿Alguna vez te has preguntado **cómo establecer DPI** al renderizar una página web con Aspose.HTML? No eres el único. En muchos escenarios de pruebas necesitas que el diseño coincida con una densidad de pantalla específica—piensa en PDFs listos para imprimir o capturas de pantalla de alta resolución. La buena noticia es que el sandbox de Aspose.HTML te permite controlar DPI, tamaño del viewport y hasta la cadena user‑agent en un solo paquete ordenado.

En este tutorial recorreremos un ejemplo práctico en Java que **establece DPI**, **establece el tamaño del viewport** y **establece el user agent** de una sola vez. Al final tendrás un programa ejecutable, sabrás por qué cada configuración es importante y estarás listo para ajustar el sandbox a tus propios proyectos.

---

## Lo que necesitarás

- **Java 17** (o cualquier JDK reciente; la API es compatible con Java 8+)
- **Aspose.HTML for Java** library (versión 23.12 o más reciente)
- Un IDE o editor de texto simple + compilación por línea de comandos
- Acceso a Internet para la URL de ejemplo (`https://example.com`)

No se requieren herramientas de compilación externas; el código se compila con `javac` y se ejecuta con `java`. Si prefieres Maven o Gradle, simplemente agrega la dependencia de Aspose.HTML—nada complicado.

---

## Paso 1: Crear un Sandbox que define el entorno de renderizado

El sandbox es donde le indicas a Aspose.HTML qué “pantalla” estás simulando. Aquí establecemos un **viewport de 1024 × 768**, un **DPI de 96**, y una cadena **user‑agent** personalizada.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Por qué esto importa:**  
- **DPI** influye en cómo las unidades CSS `pt` se traducen a píxeles; un DPI más alto produce un renderizado más nítido.  
- **Tamaño del viewport** determina los puntos de quiebre del diseño que el CSS responsivo alcanzará.  
- **User‑agent** puede activar variaciones de contenido del lado del servidor (móvil vs escritorio).

> **Consejo profesional:** Si vas a generar PDFs más adelante, ajusta el DPI a la resolución de impresión objetivo (p.ej., 300 dpi para impresiones de alta calidad).

---

## Paso 2: Cargar una página web dentro del Sandbox

Ahora apuntamos el sandbox a una URL. El constructor `HTMLDocument` acepta el sandbox, por lo que el motor de diseño respeta las configuraciones que acabamos de definir.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**¿Qué ocurre bajo el capó?**  
Aspose.HTML crea un contexto de renderizado aislado, similar a un navegador sin cabeza, pero sin la sobrecarga de una instancia completa de Chromium. Esto hace que la operación sea rápida y ligera en memoria—perfecta para procesamiento por lotes.

---

## Paso 3: Interactuar con el DOM – Leer el título de la página

Para la demostración extraeremos el título y lo imprimiremos. En un escenario real podrías tomar una captura de pantalla, exportar a PDF o extraer datos.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Salida esperada** (cuando `https://example.com` es accesible):

```
Title inside sandbox: Example Domain
```

Si el sitio devuelve un título diferente, verás ese en su lugar—no necesitas cambiar nada más.

---

## Paso 4: Verificar la configuración (Depuración opcional)

A veces quieres verificar dos veces que el sandbox realmente respeta tu DPI y viewport. Aspose.HTML no expone esos valores directamente, pero puedes inferirlos midiendo las dimensiones de los elementos.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Si sabes que el CSS declara el elemento como `width: 200pt;`, a **96 dpi** deberías ver `200pt * (96/72) ≈ 267px`. Ajusta el DPI y vuelve a ejecutar para ver el número cambiar—prueba de que **cómo establecer dpi** realmente funciona.

---

## Código fuente completo en un solo bloque

Copia y pega lo siguiente en `SandboxExample.java`. Compila tal cual; solo asegúrate de que el JAR de Aspose.HTML esté en tu classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Compila y ejecuta:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Deberías ver el título impreso, confirmando que el sandbox está funcionando con el **dpi establecido**, **tamaño de viewport establecido**, y **user agent establecido** que proporcionaste.

---

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito un DPI diferente?

Simplemente cambia el segundo argumento de `DocumentSandbox`. Para PDFs listos para imprimir podrías usar `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Un DPI más alto produce dimensiones de píxel mayores para los mismos puntos CSS, lo que mejora la calidad raster pero consume más memoria.

### ¿Puedo cargar un archivo HTML local en lugar de una URL?

Absolutamente. Reemplaza la URL con una ruta de archivo:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Asegúrate de que la ruta sea absoluta y use el esquema `file:///`.

### ¿Cómo cambio el user‑agent después de crear el sandbox?

El sandbox es inmutable—una vez que lo pasas a `HTMLDocument`, las configuraciones quedan bloqueadas. Para usar un user‑agent diferente, instancia un nuevo `DocumentSandbox` con la cadena deseada.

### ¿Aspose.HTML soporta la ejecución de JavaScript?

Sí, el motor ejecuta la mayoría de los scripts del lado del cliente. Si un script modifica el DOM después de la carga, puedes esperar un poco:

```java
webDoc.waitForLoad();
```

O usa lógica similar a `setTimeout` dentro de la página antes de consultar los elementos.

---

## Confirmación visual (Imagen)

A continuación hay una captura de pantalla de la consola que muestra la ejecución exitosa. Observa que la salida del título coincide con la página, confirmando que el sandbox respetó nuestras configuraciones.

![Salida de consola mostrando cómo establecer dpi en Aspose.HTML Sandbox](/images/console-output.png)

*Texto alternativo:* *Salida de consola que demuestra cómo establecer dpi, establecer el tamaño del viewport y establecer el user agent en Aspose.HTML Sandbox.*

---

## Resumen y próximos pasos

Hemos cubierto **cómo establecer DPI** (96 dpi en el ejemplo), **establecer el tamaño del viewport** (1024 × 768), y **establecer el user agent** (cadena personalizada) usando la API sandbox de Aspose.HTML. El programa Java completo y ejecutable demuestra que estas configuraciones no son solo teóricas—afectan directamente al renderizado y la interacción con el DOM.

¿Listo para más?

- **Exportar a PDF:** Después de cargar la página, llama a `webDoc.save("output.pdf", SaveFormat.PDF);` para generar un PDF de alta resolución que refleje el DPI que estableciste.  
- **Tomar una captura de pantalla:** Usa `webDoc.renderToBitmap("screenshot.png");` para obtener imágenes pixel‑perfectas.  
- **Jugar con diseños responsivos:** Cambia las dimensiones del viewport para probar puntos de quiebre móviles sin un dispositivo real.  

Experimenta con diferentes valores de DPI, combinaciones de viewport y user‑agents para ver cómo reaccionan los servidores y el CSS. El sandbox es un entorno de pruebas ligero que te ahorra tener que iniciar navegadores completos.

---

### Sigue explorando

- **Documentación de Aspose.HTML** – profundiza en las opciones de `DocumentSandbox`.  
- **Consultas avanzadas de medios CSS** – aprende cómo el tamaño del viewport desencadena diferentes estilos.  
- **Suplantación de User‑Agent** – descubre cómo algunos sitios entregan marcado alternativo según la cadena del agente.

¿Tienes preguntas o un caso complicado? Deja un comentario y solucionemos juntos. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}