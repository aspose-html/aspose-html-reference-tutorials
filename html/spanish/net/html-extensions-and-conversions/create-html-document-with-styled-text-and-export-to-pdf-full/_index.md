---
category: general
date: 2025-12-29
description: Crear documento HTML en C# y aprender cómo establecer la familia tipográfica,
  establecer el tamaño de fuente, luego guardar el HTML como PDF o convertir HTML
  a PDF usando Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: es
og_description: Crea un documento HTML en C# y ve al instante cómo establecer la familia
  de fuentes, establecer el tamaño de fuente, luego guarda el HTML como PDF o convierte
  HTML a PDF con Aspose.HTML.
og_title: Crear documento HTML – Texto con estilo y exportación a PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Crear documento HTML con texto con estilo y exportar a PDF – Guía completa
url: /es/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento HTML con texto con estilo y exportar a PDF

¿Alguna vez necesitaste **crear un documento HTML** sobre la marcha y convertirlo en PDF sin salir de tu código C#? Tal vez estés construyendo un motor de informes, un generador de facturas o simplemente una vista previa rápida para los usuarios. La buena noticia es que puedes hacerlo en unas pocas líneas usando Aspose.HTML, y tendrás control total familia de fuentes, el tamaño de fuente e incluso el estilo negrita‑cursiva.

En este tutorial recorreremos todo el proceso —desde crear un documento HTML en memoria hasta guardarlo como archivo PDF. Al final sabrás exactamente cómo **establecer la familia de fuentes**, **establecer el tamaño de fuente** y **guardar HTML como PDF** (también conocido como **convertir HTML a PDF**) con un ejemplo de código limpio y listo para producción.

## Lo que necesitarás

- .NET 6+ (la API funciona tanto con .NET Core como con .NET Framework)  
- Paquete NuGet Aspose.HTML for .NET (`Aspose.Html`) – instalar vía `dotnet add package Aspose.Html`  
- Una carpeta en disco donde se pueda escribir el PDF generado  

Sin plantillas HTML adicionales, sin convertidores externos, solo C# puro.

![ilustración de crear documento html](/images/create-html-document.png){alt="ejemplo de crear documento html"}

## Paso 1: Crear el documento HTML

Primero, necesitamos un objeto de documento HTML vacío. Piensa en él como un lienzo fresco donde después pintarás tu párrafo con estilo.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Por qué es importante:** `HTMLDocument` te brinda una estructura tipo DOM que puedes manipular programáticamente. No necesitas tocar cadenas crudas ni I/O de archivos hasta el final.

## Paso 2: Añadir un párrafo y establecer familia y tamaño de fuente

Ahora crearemos un elemento `<p>`, insertaremos texto y definiremos explícitamente la familia y el tamaño de la fuente. Aquí es donde entran en juego las palabras clave **set font family** y **set font size**.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Consejo profesional:** Si necesitas una alternativa segura para la web, puedes proporcionar una lista separada por comas como `"Arial, Helvetica, sans-serif"`; el navegador (o Aspose) elegirá la primera fuente disponible.

## Paso 3: Aplicar estilo negrita y cursiva con banderas WebFontStyle

Aspose.HTML expone un práctico enum `WebFontStyle` que permite combinar estilos con un OR a nivel de bits. Hagamos que el texto sea tanto negrita **como** cursiva.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**¿Qué ocurre tras bambalinas?** La propiedad `FontStyle` se traduce a declaraciones CSS `font-weight` y `font-style`. Al combinar las banderas evitamos escribir dos líneas separadas de CSS.

## Paso 4: Convertir el HTML a PDF (Guardar HTML como PDF)

El paso final es la conversión propiamente dicha. Con una única llamada a `Save`, Aspose.HTML renderiza el DOM y escribe un archivo PDF en disco. Esto satisface tanto los requisitos de **save html as pdf** como de **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Resultado esperado:** Abre `styled.pdf` y verás un solo párrafo que dice “Bold & Italic text” en Arial de 18 px, renderizado en negrita y cursiva. Las dimensiones del PDF coinciden con una página A4 estándar, y el texto es seleccionable —gracias al renderizado vectorial.

## Ejemplo completo y funcional

Juntando todo, aquí tienes el programa completo listo para ejecutarse:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Ejecutar el código

1. Instala el paquete NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Reemplaza `C:\Temp\styled.pdf` por una carpeta donde tengas permiso de escritura.  
3. Compila y ejecuta: `dotnet run`.  

Deberías ver un mensaje en la consola confirmando la ubicación del archivo, y el PDF contendrá el párrafo con estilo.

## Preguntas frecuentes y casos especiales

- **¿Qué pasa si necesito una fuente web personalizada?**  
  Carga la fuente con `HTMLFontFaceRule` o referencia un archivo CSS remoto `@font-face` antes de crear el párrafo.

- **¿Puedo añadir imágenes antes de convertir?**  
  Por supuesto. Usa `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` y asigna `img.Source` a una ruta local o a un data URI.

- **¿Y los PDFs de varias páginas?**  
  Añade más elementos (tablas, divs, etc.) y Aspose.HTML paginará automáticamente cuando el contenido supere la altura de la página.

- **¿Hay forma de controlar los metadatos del PDF?**  
  Pasa una instancia de `PdfSaveOptions` y configura propiedades como `Author`, `Title` o `PdfAConformanceLevel`.

## Recapitulación

Hemos cubierto cómo **crear documento HTML** en C#, **establecer la familia de fuentes**, **establecer el tamaño de fuente**, aplicar estilos negrita‑cursiva y finalmente **guardar HTML como PDF**, convirtiendo efectivamente **HTML a PDF** con Aspose.HTML. El fragmento es lo suficientemente corto como para insertarlo en cualquier proyecto .NET, pero lo bastante completo como para servir de base sólida para escenarios de informes más complejos.

## Próximos pasos

- Experimenta con clases CSS para estilos reutilizables.  
- Combina varios párrafos, tablas e imágenes para crear PDFs más ricos.  
- Explora la conformidad PDF/A si necesitas documentos de grado archivístico.  

Siéntete libre de ajustar la fuente, el tamaño o los colores —no hay límite a lo que puedes generar programáticamente. ¡Feliz codificación, y que tus PDFs siempre se rendericen exactamente como lo imaginas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}