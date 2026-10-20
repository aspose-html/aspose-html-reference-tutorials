---
category: general
date: 2026-04-06
description: Aprende cómo habilitar el antialiasing, establecer el ancho y la altura
  de la imagen, y guardar el documento como PNG en C# – una guía rápida para exportar
  el documento a imagen.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: es
og_description: Cómo habilitar el antialiasing al exportar un documento a una imagen.
  Esta guía muestra cómo establecer el ancho de la imagen, la altura de la imagen
  y guardar el documento como PNG.
og_title: Cómo habilitar el antialiasing – Exportar documento a imagen
tags:
- C#
- ImageRendering
- Antialiasing
title: Cómo habilitar el antialiasing – Exportar documento a imagen con C#
url: /es/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo habilitar el antialiasing – Exportar documento a imagen en C#

¿Alguna vez te has preguntado **cómo habilitar el antialiasing** al convertir un documento en una imagen? Tal vez intentaste una llamada rápida a `Save` y el resultado se veía dentado, especialmente en líneas diagonales. La buena noticia es que no necesitas ser un mago de los gráficos, solo unas pocas líneas de C# y las opciones correctas.

En este tutorial recorreremos cómo establecer el ancho de la imagen, cómo establecer la altura de la imagen y, finalmente, **guardar documento como PNG** para que puedas **exportar documento a imagen** con bordes suaves. Al final tendrás un fragmento listo‑para‑ejecutar que produce un PNG nítido de 800 × 600 con antialiasing activado.

## Prerrequisitos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.7+)
- Una referencia a una biblioteca de renderizado que admita `ImageRenderingOptions` (p. ej., Aspose.Words, Syncfusion o cualquier API que exponga propiedades similares)
- Un conocimiento básico de la sintaxis de C#

Sin configuraciones complicadas: solo agrega el paquete NuGet y estarás listo para comenzar.

## Paso 1: Instalar la biblioteca de renderizado

Primero, agrega el paquete a tu proyecto. Si estás usando Aspose.Words, ejecuta:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Mantén la versión de la biblioteca actualizada; la última versión (a partir de abril 2026) incluye mejoras de rendimiento para el antialiasing.

## Paso 2: Crear el objeto Document

Carga o crea el documento que deseas renderizar. Aquí tienes un ejemplo mínimo que construye un documento de una página con un párrafo simple:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

La clase `Document` es el punto de entrada; todo lo que renderizas proviene de ella. En proyectos reales probablemente cargarás un .docx existente:

```csharp
// Document doc = new Document("input.docx");
```

## Paso 3: Definir opciones de renderizado (Ancho, Altura, Antialiasing)

Ahora respondemos la pregunta central: **cómo habilitar el antialiasing**. El objeto `ImageRenderingOptions` te permite alternar el suavizado y controlar las dimensiones.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Observa los comentarios: mencionan explícitamente **set image width**, **set image height** y **UseAntialiasing**, los tres controles que más importan cuando deseas un PNG pulido.

### Por qué el antialiasing es importante

Sin antialiasing, las líneas diagonales y curvas aparecen en forma de escalones porque el renderizador trata cada píxel como encendido o apagado. Al habilitarlo, se mezclan los píxeles de los bordes, produciendo un suavizado visual que imita lo que verías en un editor de fotos. El compromiso es un pequeño aumento en el tiempo de procesamiento, pero para la mayoría de exportaciones orientadas a UI es insignificante.

## Paso 4: Guardar documento como PNG (Exportar documento a imagen)

Con las opciones listas, finalmente **guardamos documento como PNG**. El método `Save` recibe la ruta del archivo y las opciones que acabamos de configurar.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Eso es todo: tu documento ahora es un PNG de 800 × 600 con antialiasing aplicado. Si abres `output.png` verás texto limpio, líneas suaves y sin artefactos dentados.

### Verificando el resultado

Puedes comprobar rápidamente el archivo en cualquier visor de imágenes. Busca:

- Dimensiones correctas (800 × 600)  
- No haya bordes escalonados visibles en el texto o en cualquier forma  
- Un fondo transparente si tu documento no contenía color de fondo (la mayoría de las bibliotecas usan blanco por defecto)

Si la imagen se ve dentada, verifica que `UseAntialiasing = true` no esté siendo sobrescrito en otro lugar.

## Paso 5: Casos límite y variaciones

### Cambiar el formato de salida

¿Quieres un JPEG en lugar de PNG? Simplemente cambia la extensión del archivo y, opcionalmente, ajusta la compresión:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Exportar varias páginas

Cuando el documento de origen tiene varias páginas, el renderizador crea archivos de imagen separados por página de forma predeterminada. Puedes iterar sobre las páginas:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Guardar en un Stream (p. ej., respuesta HTTP)

Si estás construyendo una API web, quizá quieras devolver el PNG directamente:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar y pegar, que incorpora cada paso descrito:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Ejecutar este programa genera `output.png` en la carpeta del ejecutable. Ábrelo y verás un PNG suave de 800 × 600, exactamente lo que nos propusimos lograr.

## Preguntas frecuentes y solución de problemas

- **¿Qué pasa si la imagen se ve borrosa?**  
  La borrosidad puede ocurrir al escalar una página de origen pequeña. Mantén el tamaño de la página de origen cercano a las dimensiones objetivo, o incrementa la DPI mediante `imageOptions.Resolution` (p. ej., `Resolution = 300`).

- **¿Esto funciona en .NET Framework?**  
  Sí. La misma API está disponible en el framework clásico; solo debes referenciar el DLL correspondiente.

- **¿Puedo controlar el color de fondo?**  
  Por supuesto. Configura `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` antes de guardar.

- **¿El antialiasing está acelerado por hardware?**  
  La mayoría de las bibliotecas realizan antialiasing por software. Si necesitas aceleración GPU, busca un motor de renderizado que lo soporte explícitamente.

## Conclusión

Hemos cubierto **cómo habilitar el antialiasing** al **exportar documento a imagen**, repasado **set image width** y **set image height**, y mostrado los pasos exactos para **guardar documento como PNG**. El fragmento anterior está listo para producción, y ahora puedes adaptarlo a JPEG, PDFs multipágina o incluso transmitir la imagen directamente a un cliente.

A continuación, podrías explorar agregar marcas de agua, ajustar la DPI para una salida de calidad de impresión o integrar esta lógica en un endpoint de ASP.NET Core. Los mismos principios se aplican: solo cambia la ruta del archivo por un stream de respuesta.

¡Feliz codificación y disfruta de esas imágenes nítidas y antialiasadas!

![PNG renderizado con antialiasing habilitado](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}