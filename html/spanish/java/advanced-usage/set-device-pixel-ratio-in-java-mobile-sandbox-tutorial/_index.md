---
category: general
date: 2026-02-10
description: establecer la relación de píxeles del dispositivo en Java usando el sandbox
  de Aspose.HTML. Aprende cómo establecer el ancho y la altura de la pantalla y obtener
  el título de la página en Java con un ejemplo completo y ejecutable.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: es
og_description: establecer la relación de píxeles del dispositivo en Java con el sandbox
  de Aspose.HTML. Esta guía muestra cómo configurar el ancho y la altura de la pantalla
  y obtener el título de la página en Java en unos pocos pasos sencillos.
og_title: Configurar la relación de píxeles del dispositivo en Java – Tutorial de
  Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Establecer la relación de píxeles del dispositivo en Java – Tutorial de Mobile
  Sandbox
url: /es/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# establecer la relación de píxeles del dispositivo en Java – Tutorial de Sandbox móvil

¿Alguna vez necesitaste **establecer la relación de píxeles del dispositivo** mientras probabas un sitio responsivo en Java? No eres el único. Muchos desarrolladores se topan con un problema cuando la página se ve perfecta en escritorio pero se rompe en teléfonos de alta DPI. ¿La buena noticia? Con el sandbox de Aspose.HTML puedes emular un iPhone X (o cualquier dispositivo) directamente desde tu código Java—sin necesidad de navegador.

En esta guía recorreremos **cómo establecer el ancho y alto de pantalla**, configurar la **relación de píxeles del dispositivo**, y finalmente **obtener el título de la página java** para verificar que todo se haya renderizado correctamente. Al final tendrás un programa autónomo que puedes insertar en cualquier proyecto y comenzar a probar diseños móviles al instante.

## Requisitos previos

- Java 8 o superior (el código también compila con JDK 11)  
- Biblioteca Aspose.HTML para Java (versión 23.7 o posterior) – puedes obtenerla de Maven Central  
- Un IDE o una configuración simple de línea de comandos `javac`  
- Acceso a Internet para la URL de demostración (`https://responsive.example.com`)

Sin frameworks adicionales, sin Selenium, solo Java puro y Aspose.HTML.

---

## Paso 1: Establecer ancho y alto de pantalla y relación de píxeles del dispositivo

Lo primero que necesitamos es un objeto `SandboxOptions` que indique al sandbox qué “dispositivo” estamos simulando. Aquí usaremos las dimensiones del iPhone X (375 × 812 píxeles CSS) y una **relación de píxeles del dispositivo** de 3.0, que replica la pantalla retina de alta DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Por qué es importante:**  
> La llamada `setDevicePixelRatio` escala todo—desde imágenes hasta el renderizado de fuentes—de modo que la página crea que está en un teléfono real. Si la omites, el diseño puede volver a usar consultas de medios CSS de estilo de escritorio, anulando el propósito de las pruebas móviles.

---

## Paso 2: Crear la instancia del sandbox

Ahora convertimos esas opciones en un sandbox activo. Piensa en el sandbox como un pequeño navegador sin cabeza que respeta las dimensiones y la relación de píxeles que acabamos de definir.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Consejo profesional:** Puedes reutilizar el mismo objeto `Sandbox` para cargar varias páginas; solo cambia la URL y el sandbox mantendrá las mismas características del dispositivo.

---

## Paso 3: Cargar la página dentro del sandbox

Con el sandbox listo, cargar una página es tan simple como construir un `HTMLDocument` y pasar el sandbox como segundo argumento. Esto obliga al documento a renderizarse usando el dispositivo virtual que configuramos antes.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Si la URL no es accesible o la página contiene errores, Aspose.HTML lanzará una excepción. En código de producción probablemente envolverías esto en un `try‑catch` y registrarías el fallo, pero para el tutorial lo mantenemos sencillo.

---

## Paso 4: Verificar con get page title java

La verificación rápida es leer el título del documento. Si el sandbox aplicó correctamente la **relación de píxeles del dispositivo**, el título será idéntico al que verías en un iPhone X real.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Salida esperada (ejemplo):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Si ves el título impreso, has establecido con éxito la **relación de píxeles del dispositivo**, el **ancho y alto de pantalla**, y has **obtenido el título de la página** usando Java.

---

## Ejemplo completo y ejecutable

A continuación tienes el programa completo que puedes copiar y pegar en un archivo llamado `SandboxDemo.java`. Asegúrate de que los JARs de Aspose.HTML estén en tu classpath (bandera `-cp`) antes de compilar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Compila y ejecuta:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Deberías ver el título impreso en la consola, confirmando que la página se renderizó con la **relación de píxeles del dispositivo** deseada.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo cambiar la relación de píxeles en tiempo de ejecución?** | Sí—simplemente crea un nuevo `SandboxOptions` con un valor diferente en `setDevicePixelRatio` e instancia un `Sandbox` nuevo. Reutilizar el mismo sandbox después de cambiar sus opciones no está soportado. |
| **¿Qué pasa si necesito probar varios dispositivos?** | Itera sobre una lista de `SandboxOptions` (p. ej., iPhone 8, Pixel 4) y ejecuta la misma lógica de carga y obtención de título para cada uno. |
| **¿Esto funciona con sitios HTTPS que tienen certificados autofirmados?** | Aspose.HTML respeta el almacén de confianza SSL predeterminado de Java. Añade el certificado al keystore de la JVM o desactiva la verificación solo para pruebas (no recomendado para producción). |
| **¿Cómo capturo una captura de pantalla en lugar de solo el título?** | La API `HTMLDocument` proporciona métodos `save` que pueden exportar la página renderizada a PNG o JPEG. Usa `htmlDoc.save("output.png", SaveFormat.PNG);` después de cargar. |
| **¿Es thread‑safe el sandbox?** | Cada instancia de `Sandbox` está aislada, pero deberías evitar compartir una única instancia entre varios hilos sin sincronización. |

---

## Visión general visual

![Diagrama que muestra la configuración de la relación de píxeles del dispositivo en sandbox móvil](https://example.com/images/sandbox-diagram.png "diagrama de la relación de píxeles del dispositivo")

*La ilustración anterior muestra el flujo desde la configuración de `SandboxOptions` (incluyendo **establecer ancho y alto de pantalla** y **establecer la relación de píxeles del dispositivo**) hasta la carga de una URL y la extracción del título.*

---

## Conclusión

Ahora sabes **cómo establecer la relación de píxeles del dispositivo** en Java, cómo **establecer ancho y alto de pantalla** para una emulación móvil precisa, y cómo **obtener el título de la página java** para confirmar que el renderizado se realizó con éxito. Este flujo de trabajo compacto elimina la necesidad de navegadores pesados durante las pruebas automatizadas de UI y encaja perfectamente en los pipelines de CI.

¿Listo para el siguiente paso? Intenta exportar la página renderizada como una imagen, o experimenta con la depuración de consultas de medios CSS alternando el `devicePixelRatio` entre 1.0 y 3.0. También podrías explorar las funciones de conversión a PDF de Aspose.HTML para capturar una versión imprimible de la vista móvil.

¡Feliz codificación, y que tus diseños móviles siempre se vean nítidos—sin importar la densidad de píxeles!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}