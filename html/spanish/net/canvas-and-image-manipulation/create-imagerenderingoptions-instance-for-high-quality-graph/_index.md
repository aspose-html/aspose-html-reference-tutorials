---
category: general
date: 2026-10-09
description: Cree una instancia de ImageRenderingOptions para habilitar el antialiasing
  y mejorar la calidad del renderizado gráfico en aplicaciones .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: es
lastmod: 2026-10-09
og_description: Crea una instancia de ImageRenderingOptions para habilitar el antialiasing
  y lograr una renderización de gráficos más suave en .NET. Sigue la guía paso a paso.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Crear instancia de ImageRenderingOptions – mejorar la calidad gráfica en
  .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Crear instancia de ImageRenderingOptions para renderizado de gráficos de alta
  calidad
url: /es/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear instancia de ImageRenderingOptions para renderizado de gráficos de alta calidad

Si necesitas **crear una instancia de ImageRenderingOptions** para producir gráficos más suaves, esta guía te muestra exactamente cómo. Al configurar el antialiasing eliminas los bordes dentados y obtienes una salida de nivel profesional sin bibliotecas adicionales.

Aprenderás a instanciar `ImageRenderingOptions`, activar el antialiasing y adjuntar las opciones a un motor de renderizado como Aspose.Slides o System.Drawing. El tutorial asume que estás familiarizado con la sintaxis básica de C# y que tienes un entorno de desarrollo .NET listo.

## Requisitos previos

- .NET 6.0 o posterior (la API está disponible en .NET Standard 2.0+)
- Una referencia al ensamblado que contiene `ImageRenderingOptions` (p. ej., `Aspose.Slides.NET`)
- Un IDE como Visual Studio 2022 o VS Code con la extensión de C#
- Comprensión básica de los pipelines de renderizado gráfico

## Paso 1: Crear instancia de ImageRenderingOptions

La primera operación es asignar un nuevo objeto `ImageRenderingOptions`. Este objeto actúa como contenedor de todas las banderas relacionadas con el renderizado.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Crear la instancia te brinda control total sobre cómo se rasterizan los gráficos vectoriales. Más adelante podrás habilitar o deshabilitar características específicas como antialiasing, modo de renderizado de texto o compresión de imágenes.

## Paso 2: Habilitar antialiasing para mejorar el renderizado de gráficos

El antialiasing suaviza la transición entre colores de píxeles, reduciendo el efecto de escalones en líneas diagonales o curvas. La propiedad más antigua `SmoothingMode` está obsoleta; `UseAntialiasing` es el enfoque moderno y recomendado.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Establecer `UseAntialiasing` en `true` indica al motor de renderizado que aplique un filtro de alta calidad durante la rasterización. Esta bandera funciona tanto para formas vectoriales como para texto, garantizando una fidelidad visual consistente en la diapositiva.

### ¿Por qué no usar SmoothingMode?

`SmoothingMode` pertenece a `System.Drawing.Graphics` y solo afecta al dibujo GDI+. Cuando renderizas diapositivas o PDFs mediante Aspose.Slides, `ImageRenderingOptions.UseAntialiasing` es la única bandera que la biblioteca respeta. Usar la propiedad más reciente garantiza compatibilidad futura y elimina comportamientos inesperados en plataformas que no sean Windows.

## Paso 3: Aplicar las opciones a una operación de renderizado

Una vez que la instancia de `ImageRenderingOptions` está configurada, pásala al método que realiza el renderizado real. A continuación se muestra un ejemplo completo y ejecutable que carga una presentación, renderiza la primera diapositiva como PNG y guarda la imagen con antialiasing habilitado.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Explicación de las líneas clave**

- `new Presentation("sample.pptx")` carga el archivo fuente.  
- `GetThumbnail(2f, 2f, imgOptions)` crea un bitmap de la diapositiva al doble del DPI predeterminado mientras aplica las opciones de renderizado que configuraste.  
- El PNG resultante (`slide1_antialiased.png`) muestra curvas y texto suaves gracias a `UseAntialiasing = true`.

### Resultado esperado

Abre `slide1_antialiased.png` en cualquier visor de imágenes. En comparación con un renderizado que omite el antialiasing, notarás:

- Las esquinas redondeadas de las formas aparecen sin pasos dentados.  
- Los bordes del texto son nítidos pero suavizados, eliminando artefactos pixelados.  
- La calidad visual general coincide con lo que verías en la vista original de PowerPoint.

## Paso 4: Ajustes opcionales para renderizado gráfico avanzado

Aunque el antialiasing es la bandera más común, `ImageRenderingOptions` ofrece controles adicionales:

| Propiedad | Propósito | Valor típico |
|-----------|-----------|--------------|
| `UseHighQualityRendering` | Habilita renderizado subpíxel para texto | `true` |
| `PixelFormat` | Determina la profundidad de color del bitmap de salida | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Define el formato de imagen de destino (PNG, JPEG, etc.) | `Export.SaveFormat.Png` |

Puedes encadenar estas configuraciones:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Consejo profesional:** Al generar PDFs a gran escala o PNGs de alta resolución, mantén `UseAntialiasing` activado pero vigila el uso de memoria. El antialiasing añade sobrecarga de procesamiento, lo que puede notarse en máquinas de gama baja.

## Problemas comunes y cómo evitarlos

1. **Olvidar pasar las opciones** – Los métodos de renderizado que aceptan `ImageRenderingOptions` ignorarán el antialiasing si llamas a la sobrecarga sin el parámetro de opciones. Usa siempre el método `GetThumbnail` de tres parámetros o su equivalente.  
2. **Combinar SmoothingMode con ImageRenderingOptions** – Establecer `Graphics.SmoothingMode` no tiene efecto en el renderizado de Aspose.Slides. Depende únicamente de `UseAntialiasing`.  
3. **Usar una versión de biblioteca desactualizada** – `ImageRenderingOptions` se introdujo en Aspose.Slides 20.5. Asegúrate de que tu paquete NuGet esté actualizado; de lo contrario la clase puede faltar o no incluir la propiedad `UseAntialiasing`.

## Conclusión

Ahora sabes cómo **crear una instancia de ImageRenderingOptions**, habilitar antialiasing e integrar las opciones en un flujo de trabajo de renderizado. Este enfoque garantiza un renderizado de gráficos más suave, reemplaza la configuración heredada `SmoothingMode` y funciona de manera consistente en plataformas .NET.

A partir de aquí puedes explorar banderas de renderizado adicionales, experimentar con diferentes escalas de DPI o combinar la técnica con la exportación a PDF para obtener activos de calidad imprimible. Dominar `ImageRenderingOptions` es una piedra angular de la programación gráfica .NET de alta fidelidad.

---


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}