---
category: general
date: 2026-05-22
description: Establece el ancho y la altura de la imagen al convertir un documento
  Word a PNG. Aprende a exportar un docx como imagen con renderizado de alta calidad
  en un tutorial paso a paso.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: es
og_description: Establece el ancho y la altura de la imagen al convertir un documento
  de Word a PNG. Este tutorial muestra cómo exportar un docx como imagen con configuraciones
  de alta calidad.
og_title: Establecer ancho y alto de la imagen al convertir Word a PNG – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Establecer ancho y alto de la imagen al convertir Word a PNG – Guía completa
url: /es/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer Ancho y Altura de Imagen al Convertir Word a PNG – Guía Completa

¿Alguna vez te has preguntado cómo **establecer el ancho y la altura de la imagen** mientras **conviertes Word a PNG**? No eres el único. Muchos desarrolladores se topan con un obstáculo cuando la exportación predeterminada produce una imagen borrosa o con dimensiones incorrectas, y luego pasan horas buscando una solución que realmente funcione.

En este tutorial recorreremos una solución limpia, de extremo a extremo, que muestra **cómo renderizar Word** documentos como imágenes PNG, permitiéndote **guardar docx como PNG** con control preciso de ancho‑alto y antialiasing de alta calidad. Al final tendrás un fragmento de código listo para ejecutar, una comprensión sólida de las opciones de la API y algunos consejos profesionales para evitar errores comunes.

## Lo que aprenderás

- Cargar un archivo `.docx` usando Aspose.Words for .NET.
- **Establecer ancho y altura de la imagen** con `ImageRenderingOptions`.
- **Exportar docx como imagen** (PNG) con antialiasing habilitado.
- Cómo **convertir word a png** para una sola página o todo el documento.
- Consejos para manejar documentos grandes, consideraciones de DPI y rutas del sistema de archivos.

Sin herramientas externas, sin complicados comandos de línea—solo código C# puro que puedes insertar en cualquier proyecto .NET.

---

## Requisitos previos

Antes de comenzar, asegúrate de tener lo siguiente:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0+** (or .NET Framework 4.7.2) | Aspose.Words es compatible con ambos, pero los entornos de ejecución más recientes ofrecen mejor rendimiento. |
| **Aspose.Words for .NET** NuGet package (`Install-Package Aspose.Words`) | Proporciona la clase `Document` y el motor de renderizado. |
| Un **documento Word** (`.docx`) que deseas convertir a PNG. | La fuente que vas a convertir. |
| Conocimientos básicos de C# – comprenderás las sentencias `using` y la inicialización de objetos. | Mantiene la curva de aprendizaje suave. |

Si te falta el paquete NuGet, ejecuta lo siguiente en la consola del Administrador de paquetes:

```powershell
Install-Package Aspose.Words
```

Eso es todo—una vez que el paquete esté instalado, estarás listo para comenzar a programar.

---

## Paso 1: Cargar el Documento Fuente

Lo primero que debes hacer es indicar a la biblioteca el archivo Word que deseas transformar.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Por qué es importante:** La clase `Document` lee todo el paquete Word en memoria, dándote acceso a páginas, estilos y todo lo demás. Si la ruta es incorrecta, obtendrás una `FileNotFoundException`, así que verifica que el archivo exista y que la ruta use barras invertidas escapadas (`\\`) o una cadena literal (`@`).  

> **Consejo profesional:** Envuelve la llamada de carga en un bloque `try/catch` si esperas que el archivo pueda faltar en tiempo de ejecución.

---

## Paso 2: Configurar Opciones de Renderizado de Imagen (Establecer Ancho y Altura de Imagen)

Ahora llega el corazón del tutorial: **cómo establecer el ancho y la altura de la imagen** para que el PNG resultante no se vea estirado o pixelado. La clase `ImageRenderingOptions` te brinda un control detallado sobre dimensiones, DPI y suavizado.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Explicación de las propiedades clave:**

- `Width` y `Height` – Estas son las dimensiones exactas en píxeles que deseas. Al configurarlas, **estableces el ancho y la altura de la imagen** directamente, sobrescribiendo el tamaño de página predeterminado.
- `UseAntialiasing` – Habilita un suavizado de alta calidad para texto y gráficos vectoriales, lo cual es crucial cuando **conviertes word a png** y deseas bordes nítidos.
- `Resolution` – Un DPI más alto brinda más detalle, especialmente en diseños complejos. Vigila el uso de memoria; una imagen de 300 DPI puede ser grande.

> **¿Por qué no confiar solo en el tamaño predeterminado?** El predeterminado usa las dimensiones físicas de la página (p.ej., A4 a 96 DPI). Eso a menudo produce una imagen de 794 × 1123 píxeles—útil en algunos casos pero no cuando necesitas una miniatura de UI específica o una vista previa de tamaño fijo.

---

## Paso 3: Renderizar y Guardar como PNG (Exportar Docx como Imagen)

Con el documento cargado y las opciones configuradas, finalmente puedes **exportar docx como imagen**. El método `RenderToImage` realiza el trabajo pesado.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Si deseas renderizar **todo el documento** (todas las páginas) en archivos PNG separados, recorre la colección de páginas:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**¿Qué ocurre internamente?** El renderizador rasteriza cada página usando las dimensiones que proporcionaste, aplica antialiasing y escribe un flujo de bytes PNG en el disco. Como PNG es sin pérdida, mantienes la fidelidad completa del diseño original de Word.

**Salida esperada:** Un archivo PNG nítido de exactamente 1024 × 768 píxeles (o el tamaño que hayas configurado). Ábrelo en cualquier visor de imágenes y verás el contenido de Word renderizado exactamente como aparece en el documento original, pero ahora como una imagen bitmap.

---

## Consejos Avanzados y Variaciones

### 1. Conservar Fondos Transparentes

Si tu documento Word contiene formas con fondos transparentes y deseas conservar esa transparencia, establece `BackgroundColor` a `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Renderizar Solo un Rango Específico

A veces solo necesitas un párrafo o una tabla, no toda la página. Usa `DocumentVisitor` para extraer el nodo y renderizarlo por separado. Es un escenario más avanzado, pero muestra **cómo renderizar word** a nivel granular.

### 3. Ajustar DPI Dinámicamente

Si necesitas diferentes DPI por página (p.ej., alta resolución para la portada), modifica `Resolution` dentro del bucle:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Procesamiento por Lotes

Al convertir docenas de documentos, envuelve todo el flujo en un método y reutiliza la misma instancia de `ImageRenderingOptions`. Reutilizar el objeto de opciones reduce la sobrecarga de asignación.

---

## Problemas Comunes y Cómo Evitarlos

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| El PNG está borroso a pesar de DPI alto | `UseAntialiasing` dejado en `false` | Establecer `UseAntialiasing = true`. |
| El tamaño de salida no coincide con Ancho/Altura | DPI no considerado | Multiplica el tamaño deseado por `Resolution / 96` o ajusta `Resolution`. |
| Excepción de falta de memoria en documentos grandes | Renderizar todo el documento a 300 DPI | Renderiza una página a la vez, libera cada imagen después de guardarla. |
| El PNG muestra fondo blanco en imágenes transparentes | `BackgroundColor` no establecido | Establecer `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Ejemplo Completo Funcional

A continuación tienes un programa autónomo que puedes copiar y pegar en una aplicación de consola. Demuestra **convertir word a png**, **guardar docx como png**, y por supuesto **establecer ancho y altura de la imagen**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Ejecuta:** Compila el proyecto, coloca un `input.docx` válido en la ruta que especificaste y ejecuta. Deberías ver un `output.png` de exactamente **1024 × 768** píxeles, renderizado con bordes suaves.

## Tutoriales Relacionados

- [Cómo habilitar antialiasing al convertir DOCX a PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convertir docx a png – crear archivo zip tutorial c#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Cómo usar Aspose para renderizar HTML a PNG – Guía paso a paso](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}