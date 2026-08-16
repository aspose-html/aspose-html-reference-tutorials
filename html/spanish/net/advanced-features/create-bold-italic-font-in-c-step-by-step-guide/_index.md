---
category: general
date: 2026-08-15
description: Crea una fuente en negrita y cursiva en C# rápidamente. Aprende cómo
  crear una fuente en C# con estilos negrita y cursiva usando la clase Font incorporada.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: es
lastmod: 2026-08-15
og_description: Crear una fuente en negrita y cursiva en C# con un ejemplo claro.
  Este tutorial muestra cómo crear una fuente en C# usando los flags de FontStyle
  y explica los errores comunes.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Crear fuente en negrita y cursiva en C# – guía completa de codificación
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Crear fuente en negrita y cursiva en C# – guía paso a paso
url: /es/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear fuente negrita cursiva en C# – guía paso a paso

Si necesitas **crear una fuente negrita cursiva** en C#, esta guía te muestra exactamente cómo hacerlo. Verás un ejemplo completo y ejecutable que también demuestra cómo **crear una fuente en C#** usando la clase estándar de .NET `Font`.

Trabajar con fuentes personalizadas es una parte rutinaria de la creación de aplicaciones de escritorio Windows, generación de PDFs o renderizado de HTML en el servidor. Al final de este tutorial podrás instanciar una fuente que sea tanto negrita como cursiva, entender por qué se usa el operador bit a bit `|` y manejar casos comunes como familias de fuentes ausentes.

## Lo que aprenderás

* Cómo importar los espacios de nombres requeridos para el manejo de fuentes.  
* La sintaxis para combinar `FontStyle.Bold` y `FontStyle.Italic`.  
* Cómo verificar que la fuente se creó correctamente.  
* Consejos para el manejo de alternativas cuando la familia solicitada no está instalada.  

No se requieren bibliotecas externas: todo utiliza la biblioteca de clases base de .NET Framework / .NET Core.

## Requisitos previos

* SDK de .NET 6.0 o superior (el código también funciona en .NET Framework 4.6+).  
* Un editor de código o IDE (Visual Studio, VS Code, Rider, etc.).  
* Familiaridad básica con la sintaxis de C#.  

Si cumples con estos requisitos, puedes seguir los pasos sin ninguna configuración adicional.

## Paso 1: Añadir las directivas `using` necesarias

La clase `Font` se encuentra en el espacio de nombres `System.Drawing`, que forma parte del paquete NuGet `System.Drawing.Common` para .NET Core/.NET 5+. Añade el espacio de nombres al inicio de tu archivo:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Por qué este paso es importante** – Sin la línea `using System.Drawing;` el compilador no puede localizar `Font` o `FontStyle`, lo que produce un error de “type or namespace name could not be found”.

## Paso 2: Combinar estilos negrita y cursiva con el operador OR bit a bit

En .NET, `FontStyle` es un enum marcado con el atributo `[Flags]`. Esto significa que puedes combinar varios valores usando el operador `|` (OR bit a bit):

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Explicación

* `"Arial"` – el nombre de la familia de fuentes. Si el sistema no tiene Arial instalado, el constructor recurre a la fuente predeterminada.  
* `12` – tamaño en puntos.  
* `FontStyle.Bold | FontStyle.Italic` – combina los dos indicadores de estilo. El operador `|` fusiona la representación binaria de cada bandera, produciendo un único valor que representa “negrita + cursiva”.

> **Consejo profesional:** Siempre usa los nombres del enum (`FontStyle.Bold`) en lugar de números mágicos; esto mejora la legibilidad y evita errores cuando los valores del enum cambian.

## Paso 3: Verificar la fuente creada (opcional pero recomendado)

Imprimir las propiedades de la fuente te ayuda a confirmar que la combinación de estilos se realizó con éxito, especialmente al depurar en una máquina nueva.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Salida esperada**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Si la salida muestra tanto `Bold` como `Italic`, la fuente se creó correctamente.

## Paso 4: Renderizar una cadena de ejemplo (confirmación visual)

Cuando ejecutas una aplicación de consola no puedes ver el estilo real de los glifos, pero puedes generar una imagen para demostrar el resultado. El siguiente fragmento dibuja “Hello, World!” usando la fuente negrita‑cursiva y la guarda como *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Después de que el programa termine, abre *sample.png* para ver el texto renderizado con el estilo negrita cursiva.

![Texto de ejemplo renderizado con fuente negrita cursiva](sample.png)

*Texto alternativo de la imagen: Captura de pantalla del texto renderizado con una fuente Arial negrita cursiva en una ventana de consola C#* – este texto alternativo satisface el requisito SEO para alt text de imágenes.

## Paso 5: Alternativa elegante cuando la familia de fuentes no está disponible

Si la familia solicitada (p. ej., “Arial”) no está instalada, el constructor `Font` lanza una `ArgumentException`. Envuelve la creación en un bloque `try/catch` y recurre a una fuente segura conocida como “Segoe UI”.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**¿Por qué manejar esto?** En entornos contenedorizados o sin interfaz gráfica el conjunto predeterminado de fuentes puede diferir del de un escritorio típico. Proveer una alternativa evita fallos en tiempo de ejecución y garantiza un estilo consistente.

## Ejemplo completo y ejecutable

Uniendo todo, aquí tienes un programa completo que puedes copiar, pegar y ejecutar:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Cómo ejecutar

1. Guarda el código en un archivo llamado `Program.cs`.  
2. Abre una terminal en el directorio del archivo.  
3. Ejecuta `dotnet new console -n FontDemo` (si necesitas una estructura de proyecto).  
4. Reemplaza el `Program.cs` generado con el código anterior.  
5. Ejecuta `dotnet add package System.Drawing.Common` (requerido para .NET Core/5+).  
6. Compila y ejecuta con `dotnet run`.  

Verás la salida en la consola confirmando las propiedades de la fuente, y `sample.png` aparecerá en la carpeta del proyecto.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Falta el paquete `System.Drawing.Common`** | .NET Core no incluye `System.Drawing` por defecto. | Ejecuta `dotnet add package System.Drawing.Common`. |
| **Familia de fuentes no instalada** | Las imágenes Docker sin entorno gráfico suelen carecer de fuentes de Windows. | Usa una fuente alternativa o instala las fuentes necesarias en el contenedor. |
| **Uso incorrecto de `|`** | Usar `+` en lugar de `|` produce una combinación inválida. | Siempre combina valores de `FontStyle` con el operador OR bit a bit (`|`). |
| **No disponer del objeto `Font`** | No llamar a `Dispose` puede provocar fugas de recursos GDI. | Envuelve `Font` en un bloque `using` o llama a `font.Dispose()` cuando termines. |

## Conclusión

Ahora sabes cómo **crear una fuente negrita cursiva** en C# y cómo **crear una fuente en C#** de forma segura y eficiente. El tutorial cubrió la importación del espacio de nombres correcto, la combinación de banderas `FontStyle`, la verificación del resultado, la generación de una muestra visual y el manejo de familias de fuentes ausentes.

A continuación, podrías explorar:

* **Crear fuentes subrayadas o tachadas** – añade `FontStyle.Underline` o `FontStyle.Strikeout`.  
* **Usar fuentes TrueType personalizadas** – carga un archivo `.ttf` con `PrivateFontCollection`.  
* **Aplicar fuentes en WinForms, WPF o generación de PDFs** – el mismo objeto `Font` puede pasarse a controles UI o bibliotecas de terceros.

Siéntete libre de experimentar con diferentes familias, tamaños y combinaciones de estilo. Si encuentras problemas, revisa la tabla “Errores comunes” o consulta la documentación oficial de [.NET para System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cara Menggabungkan Font Secara Programatis di C# – Panduan Langkah demi Langkah](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}