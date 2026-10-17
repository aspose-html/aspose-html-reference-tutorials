---
category: general
date: 2026-03-18
description: Crea PDF a partir de HTML en Java rápidamente. Aprende cómo convertir
  HTML a PDF, simular la pantalla de iPhone y establecer el tamaño de pantalla para
  PDFs responsivos.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: es
og_description: Crear PDF a partir de HTML en Java. Esta guía muestra cómo convertir
  HTML a PDF, simular una pantalla de iPhone y establecer dimensiones de pantalla
  para PDFs responsivos perfectos.
og_title: Crear PDF a partir de HTML con viewport móvil – Tutorial de Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Crear PDF a partir de HTML con viewport móvil – Guía completa de Java
url: /es/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF a partir de HTML con Viewport móvil – Guía completa de Java

¿Alguna vez necesitaste **crear PDF a partir de HTML** pero la salida se veía como una página de escritorio en una pantalla de teléfono diminuta? No eres el único. Cuando conviertes un sitio web responsivo a PDF, el viewport predeterminado a menudo ignora los puntos de quiebre móviles, dejándote con un desastre apretado.  

¿La buena noticia? Puedes **convertir HTML a PDF** mientras **simulas una pantalla de iPhone**, todo desde código Java puro. En este tutorial recorreremos cada paso: cómo establecer el tamaño de pantalla, cómo ajustar el factor de escala del dispositivo y por qué esos ajustes son importantes para obtener un PDF pixel‑perfecto.

> **Consejo profesional:** Si ya has usado Aspose.HTML para conversiones simples, encontrarás los ajustes del viewport a solo unas pocas líneas adicionales.

---

## Lo que aprenderás

* Cómo **crear PDF a partir de HTML** usando Aspose.HTML para Java.  
* El código exacto para **simular una pantalla de iPhone** con dimensiones (375 × 667 px @ 2× densidad).  
* Dónde colocar las opciones de **cómo establecer la pantalla** en la canalización de conversión.  
* Errores comunes al convertir páginas responsivas y cómo evitarlos.  
* Un ejemplo completo, listo‑para‑ejecutar en Java que puedes copiar‑pegar en tu IDE.

### Requisitos previos

* Java 17 o superior (el código compila con versiones anteriores, pero se recomienda la 17).  
* Biblioteca Aspose.HTML para Java – puedes obtener el último JAR desde el [Aspose website](https://products.aspose.com/html/java).  
* Un archivo HTML simple (`input.html`) que deseas convertir a PDF.  
* Familiaridad básica con Maven o Gradle (mostraremos un fragmento de Maven).

---

## Paso 1 – Añadir Aspose.HTML a tu proyecto

Lo primero, necesitas la biblioteca en tu classpath. Si usas Maven, agrega esta dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Por qué es importante:** Aspose.HTML se encarga del trabajo pesado—analizar HTML, aplicar CSS y rasterizar el diseño. Sin ella, tendrías que escribir un motor de navegador completo tú mismo, lo cual es un *montón* de trabajo.

Si prefieres Gradle, el equivalente es:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Paso 2 – Preparar opciones de carga y simular un viewport de iPhone

Ahora configuraremos los parámetros de **cómo establecer la pantalla**. La clase `HtmlLoadOptions` te permite indicar a Aspose qué tamaño y densidad de píxeles simular que tiene el navegador.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### ¿Por qué estos números?

* **375 × 667** coincide con las dimensiones lógicas de píxeles CSS de un iPhone 6/7/8 en modo vertical.  
* **DeviceScaleFactor = 2.0** indica al renderizador que cada píxel CSS corresponde a dos píxeles físicos, imitando la pantalla Retina.  

Si necesitas un dispositivo diferente—por ejemplo un iPhone 12 Pro Max—cambiarías el tamaño a `428 × 926` y mantendrías el factor de escala en `3.0`.

---

## Paso 3 – Ejecutar la conversión y verificar la salida

Compila y ejecuta la clase:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Después de que el programa termine, abre `output.pdf`. Deberías ver:

* Todas las consultas de medios que apuntan a `max-width: 375px` aplicadas correctamente.  
* Imágenes renderizadas nítidamente gracias al factor de escala 2×.  
* Texto que respeta la jerarquía de tamaños de fuente móvil que definiste en CSS.

Si el PDF aún se ve como una página de escritorio, verifica que tu HTML use metaetiquetas responsivas:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Sin esa etiqueta, incluso una configuración de viewport perfecta no activará la hoja de estilos móvil.

---

## Paso 4 – Manejo de recursos externos (Imágenes, Fuentes, CSS)

Cuando **conviertes HTML a PDF**, Aspose.HTML intenta obtener cada recurso enlazado. Si estás convirtiendo una página que reside en un sistema de archivos local, las URLs absolutas (`file:///…`) funcionan bien. Para recursos remotos podrías encontrarte con:

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Errores 404 para imágenes** | El HTML apunta a una URL que requiere autenticación. | Usa `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` para resolver rutas relativas, o incrusta imágenes como Base64. |
| **Fuentes web faltantes** | El motor PDF no puede descargar el archivo de fuente. | Descarga los archivos `.woff`/`.ttf` localmente y haz referencia a ellos con una ruta relativa. |
| **CSS no aplicado** | El archivo CSS está bloqueado por CORS. | Aloja el CSS en un servidor que permita solicitudes de origen cruzado, o incrusta el CSS en el HTML. |

Una forma rápida de probar la carga de recursos es envolver la llamada de conversión en un bloque try‑catch y imprimir el mensaje de `Exception`. Aspose.HTML proporciona registros detallados que indican la URL exacta que falló.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Paso 5 – Ajustes avanzados (Opcional)

### a) Cambiar el tamaño de página PDF

Por defecto Aspose.HTML crea una página PDF que coincide con el tamaño del viewport. Si prefieres A4 o Letter, agrega una configuración `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Añadir un encabezado/pie de página programáticamente

Puedes inyectar un encabezado/pie de página simple después de la conversión usando Aspose.PDF (una biblioteca separada). El flujo de trabajo es:

1. Convertir HTML → PDF (como se muestra).  
2. Abrir el PDF resultante con Aspose.PDF.  
3. Añadir objetos `HeaderFooter` a cada página.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Conversión por lotes

Si tienes una carpeta de archivos HTML, itera sobre ellos:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Preguntas frecuentes (FAQs)

**P: ¿Esto funciona con páginas cargadas de JavaScript?**  
R: Aspose.HTML soporta un subconjunto de JavaScript. La manipulación simple del DOM y los cambios de CSS suelen funcionar, pero los frameworks complejos (React, Angular) pueden necesitar una instantánea HTML estática pre‑renderizada.

**P: ¿Qué pasa si necesito convertir una página que usa reglas `@media print`?**  
R: La biblioteca respeta `@media print` automáticamente. Sin embargo, si también estableces un viewport móvil, la hoja de estilos `print` puede sobrescribir algunos estilos móviles. Prueba ambos escenarios.

**P: ¿Puedo establecer un DPI personalizado para el PDF?**  
R: Sí. Usa `PdfSaveOptions.setDpi(300)` antes de la conversión. Un DPI más alto produce archivos más grandes pero imágenes más nítidas.

---

## Captura de pantalla del resultado esperado

Below is an illustration of the final PDF page (mobile viewport simulated).  
![Captura de pantalla del PDF generado por la demostración de crear pdf a partir de html mostrando diseño de tamaño iPhone]  

*El texto alternativo de la imagen incluye la palabra clave principal para SEO.*

---

## Conclusión

Ahora tienes un flujo de trabajo sólido, **crear pdf a partir de html**, que respeta los puntos de quiebre móviles, simula una pantalla de iPhone y te brinda control total sobre las dimensiones de la página. Ajustando `HtmlLoadOptions` puedes responder “**cómo establecer la pantalla**” para cualquier dispositivo, y usando `Converter.convertDocument` has dominado **cómo convertir html** en Java.

¿Listo para el próximo desafío? Intenta combinar este enfoque con Aspose.PDF para añadir marcas de agua, combinar varios PDFs o proteger el documento con una contraseña. Y no olvides experimentar con otros dispositivos—simplemente cambia los valores `Size` y `DeviceScaleFactor` para que coincidan con la densidad de píxeles que necesites.

¡Feliz codificación, y que tus PDFs siempre se vean tan nítidos en papel como en la pantalla de un teléfono!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}