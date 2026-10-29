---
category: general
date: 2026-02-22
description: Establece la relación de píxeles del dispositivo en Java con el sandbox
  de Aspose.HTML. Aprende cómo configurar un agente de usuario personalizado, obtener
  el título de la página en Java y convertir HTML a PNG en un solo tutorial.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: es
og_description: Establecer la relación de píxeles del dispositivo en Java usando el
  sandbox de Aspose.HTML. Este tutorial muestra cómo establecer un agente de usuario
  personalizado, obtener el título de la página en Java y convertir HTML a PNG.
og_title: Establecer la relación de píxeles del dispositivo en Java – Guía completa
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Establecer la relación de píxeles del dispositivo en Java – Guía completa
url: /es/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer la relación de píxeles del dispositivo en Java – Guía completa

¿Alguna vez te has preguntado cómo **establecer la relación de píxeles del dispositivo** al renderizar una página web desde Java? No eres el único. Muchos desarrolladores necesitan emular pantallas móviles de alta‑DPI para que las capturas de pantalla se vean nítidas, especialmente cuando luego **guardan html como imagen** para informes o materiales de marketing. En este tutorial recorreremos un ejemplo práctico que hace exactamente eso, y también te mostraremos cómo **establecer un agente de usuario personalizado**, **obtener el título de la página java**, y **convertir html a png** usando Aspose.HTML.

Comenzaremos con una breve visión general de la API sandbox, luego profundizaremos en cada paso de configuración y, finalmente, produciremos un archivo PNG que reproduzca la pantalla real de un iPhone. Al final, tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto Java. No se requieren herramientas externas, solo Java puro y Aspose.HTML 7.x (o superior).

---

## Requisitos previos

- Java 17 o posterior (el código compila con versiones anteriores, pero se recomienda la 17).
- Biblioteca Aspose.HTML para Java (descárgala del sitio oficial de Aspose; coordenadas Maven: `com.aspose:aspose-html:23.10`).
- Un IDE o editor de texto de tu elección (IntelliJ IDEA, VS Code, Eclipse… todos funcionan).
- Acceso a Internet para la URL de demostración (`https://example.com/responsive.html`), o reemplázala con cualquier página HTML pública que poseas.

> **Consejo profesional:** Si estás detrás de un proxy, configura las propiedades del sistema `http.proxyHost` y `http.proxyPort` de la JVM antes de ejecutar el código.

---

## Paso 1: Establecer la relación de píxeles del dispositivo y otras opciones del sandbox

Lo primero que necesitamos es una instancia de **SandboxOptions** donde definimos el tamaño de pantalla virtual y la *relación de píxeles del dispositivo* (DPR). Piensa en el DPR como el factor que indica al navegador cuántos píxeles físicos corresponden a un píxel CSS. En un iPhone Retina, el DPR suele ser **2.0**, por eso usaremos ese valor.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Por qué es importante:** Sin establecer el DPR correcto, la imagen renderizada aparecerá borrosa o sobredimensionada porque el rasterizador asume una correspondencia 1:1 de píxeles.

---

## Paso 2: Establecer un agente de usuario personalizado

Los sitios web a menudo sirven un marcado diferente según el encabezado **User‑Agent**. Para asegurarnos de que nuestra página se comporte como lo haría en un iPhone real, inyectamos una cadena personalizada que imita Safari en iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Caso límite:** Algunos sitios también inspeccionan el encabezado `Accept-Language`. Si notas traducciones faltantes, agrega `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Paso 3: Cargar la página dentro del sandbox y obtener el título

Ahora iniciamos el sandbox con las opciones que acabamos de definir. El objeto **Sandbox** aísla el proceso de renderizado, garantizando que se respeten nuestras configuraciones de DPR y agente de usuario.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Una vez que la página se carga, obtener el título es tan simple como llamar a `getTitle()`. Esto satisface el requisito de **obtener el título de la página java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Salida esperada en consola**

```
Title: Responsive Demo – Mobile View
```

Si el título está vacío, verifica nuevamente la URL o asegúrate de que la página no esté bloqueada por políticas CORS.

---

## Paso 4: Convertir HTML a PNG y guardar HTML como imagen

Aspose.HTML te permite renderizar el DOM directamente a un archivo de imagen. Como ya hemos establecido el DPR en 2.0, el PNG resultante tendrá el doble de densidad de píxeles, produciendo una captura nítida.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

El método `save` detecta automáticamente la extensión del archivo y elige el renderizador apropiado. Si necesitas otro formato (JPEG, BMP), simplemente cambia el nombre del archivo en consecuencia.

> **¿Qué pasa si necesitas un tamaño de imagen específico?**  
> Usa `ImageSaveOptions` para controlar ancho, alto y color de fondo:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Ejemplo completo funcional

A continuación tienes el programa completo, listo para ejecutar, que une todos los pasos. Copia‑pega el código en un archivo `SandboxDemo.java`, agrega la dependencia de Aspose.HTML y ejecuta `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Al ejecutar el programa se generan dos archivos PNG:

| Archivo | Descripción |
|---------|-------------|
| `mobile_view.png` | Renderizado predeterminado usando el DPR configurado. |
| `mobile_view_custom.png` | Renderizado con ancho/alto explícitos (útil para recursos de tamaño fijo). |

Puedes abrir cualquiera de los archivos en cualquier visor de imágenes para verificar la salida de alta resolución.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si la página contiene JavaScript que modifica el DOM después de la carga?** | Aspose.HTML ejecuta scripts por defecto. Si necesitas una captura estática antes de la ejecución del script, establece `sandboxOptions.setEnableJavaScript(false)`. |
| **¿Puedo renderizar una página que requiere autenticación?** | Sí. Usa `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` o inyecta cookies mediante `sandboxOptions.getCookies().add(...)`. |
| **¿El DPR está limitado a 2.0?** | No. Puedes establecer cualquier número doble positivo (p. ej., 3.0 para dispositivos ultra‑alta‑DPI). Solo recuerda que un DPR mayor implica archivos de imagen más grandes. |
| **¿Cómo manejo páginas con recursos grandes (imágenes, fuentes)?** | Incrementa el límite de memoria del sandbox con `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). Esto evita errores de falta de memoria en páginas pesadas. |
| **¿Necesito cerrar el sandbox manualmente?** | El `Sandbox` implementa `AutoCloseable`. Envuélvelo en un bloque try‑with‑resources para una limpieza automática. |

---

## Conclusión

Hemos demostrado cómo **establecer la relación de píxeles del dispositivo** en un sandbox de Java, **establecer un agente de usuario personalizado**, **obtener el título de la página java** y **convertir html a png** (efectivamente **guardar html como imagen**) usando Aspose.HTML. El ejemplo completo muestra un flujo de trabajo práctico que puedes adaptar para generación automática de capturas, pruebas de regresión visual o cualquier escenario donde se requiera una representación pixel‑perfecta de una página web.

Siéntete libre de experimentar: cambia el DPR a 3.0, sustituye el agente de usuario por una cadena de Android, o apunta la URL a un archivo HTML local. El mismo patrón funciona para PDFs, SVGs o incluso renderizado multipágina.

Si encontraste útil esta guía, considera explorar temas relacionados como **generación de PDF con Aspose.HTML**, **alternativas a Chrome sin cabeza**, o **renderizado por lotes de múltiples URLs**. ¡Feliz codificación, y que tus capturas siempre sean ultra‑nítidas!

![establecer relación de píxeles del dispositivo en sandbox de Java](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}