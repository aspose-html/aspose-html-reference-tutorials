---
category: general
date: 2026-11-20
description: Aprende a guardar HTML usando un ResourceHandler personalizado en C#
  y también a guardar HTML en archivos zip con código conciso y listo para producción.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: es
lastmod: 2026-11-20
og_description: 'Cómo guardar HTML usando un ResourceHandler personalizado en C# y,
  opcionalmente, guardar HTML en archivos zip: guía completa y ejecutable para desarrolladores
  .NET.'
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Cómo guardar HTML con un controlador de recursos personalizado en C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Cómo guardar HTML con un controlador de recursos personalizado en C#
url: /es/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo guardar HTML con un controlador de recursos personalizado en C#

Si necesitas saber **cómo guardar HTML** a partir de una cadena en memoria o de un documento analizado, esta guía muestra una solución completa. Usar un `ResourceHandler` personalizado te permite controlar el flujo de destino, lo que significa que puedes **guardar HTML en zip** sin escribir archivos temporales.

Verás por qué un `ResourceHandler` se prefiere sobre el enfoque más antiguo `IOutputStorage`, cómo configurarlo y cómo ampliarlo para compresión zip. Al final de este tutorial podrás incrustar el código en cualquier proyecto .NET 6+ y adaptarlo a tus propios requisitos de almacenamiento.

## Lo que construirás

* Un `ResourceHandler` mínimo que devuelve un `MemoryStream`.
* Un `HtmlDocument` creado con **HtmlAgilityPack**.
* Una llamada a `doc.Save` que escribe el HTML en el flujo proporcionado por el controlador.
* Un contenedor opcional que comprime el HTML resultante en un archivo zip.

Requisitos previos:

* SDK .NET 6 o posterior.
* Paquete NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Familiaridad básica con flujos de C#.

## Paso 1: Crear un controlador de recursos personalizado (forma principal de **cómo guardar html**)

La clase base `ResourceHandler` (disponible a partir de la versión 24.2 del SDK del visor) define un único método abstracto, `HandleResource`. Implementar este método te brinda control total sobre dónde se escribe el HTML.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Por qué es importante:** Al devolver un `MemoryStream`, evitas I/O de disco, reduces la latencia y mantienes el código determinista para pruebas unitarias. El controlador se invoca automáticamente mediante el método `Save`, por lo que nunca necesitas pasar un flujo explícitamente.

## Paso 2: Cargar o crear el documento HTML

`HtmlAgilityPack` ofrece una práctica clase `HtmlDocument` que puede analizar una cadena, un archivo o un flujo. En este ejemplo cargamos un literal simple, pero el mismo código funciona con cualquier fuente HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Por qué es importante:** Mantener el documento en memoria se alinea con el enfoque basado en flujos del controlador personalizado. También te permite manipular el DOM antes de guardarlo, como inyectar scripts o corregir etiquetas mal formadas.

## Paso 3: Guardar el documento usando el controlador personalizado

Llamar a `doc.Save` con una instancia de `MyHandler` activa el método `HandleResource`. El HTML se escribe directamente en el flujo que devolviste.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Después de que `Save` finaliza, el `MemoryStream` dentro de `MyHandler` contiene el HTML serializado. Puedes recuperarlo así:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Resultado:** La consola imprime el HTML exacto que pasaste a `LoadHtml`. Esto demuestra que ahora entiendes **cómo guardar HTML** con un controlador personalizado.

## Paso 4: Extender el controlador para **guardar HTML en zip**

Si deseas archivar el HTML, modifica `MyHandler` para escribir en un `ZipArchiveEntry`. El espacio de nombres .NET `System.IO.Compression` hace esto sencillo.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Ahora usa el nuevo controlador:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Por qué funciona:** El método `HandleResource` crea una entrada zip llamada `document.html`. Cuando `doc.Save` escribe en el flujo devuelto, los datos se comprimen automáticamente. Como el zip se construye en memoria, puedes devolverlo desde una API web, adjuntarlo a un correo electrónico o almacenarlo en una base de datos sin tocar el sistema de archivos.

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito varios archivos HTML en el mismo zip?

Crea una nueva entrada para cada llamada a `HandleResource`. El argumento `resourceName` normalmente contiene el nombre del archivo, por lo que puedes usarlo directamente:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### ¿Cómo manejar documentos grandes sin agotar la memoria?

Reemplaza `MemoryStream` por un `FileStream` que apunte a un archivo temporal. El controlador entonces devuelve el flujo de archivo, y puedes eliminar el archivo posteriormente después de que se haya creado el zip.

### ¿Este enfoque funciona con .NET Core en Linux?

Sí. Todas las API usadas (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) son multiplataforma. Asegúrate de que el framework objetivo sea al menos .NET 6 para la mejor compatibilidad.

### ¿Puedo encriptar el archivo zip?

`ZipArchive` solo admite cifrado basado en contraseña mediante bibliotecas de terceros (p. ej., `SharpZipLib`). Si se requiere cifrado, envuelve los bytes de salida con una biblioteca que proporcione cifrado AES antes de enviarlos al cliente.

## Consejos profesionales

* **Reutiliza el controlador** al procesar muchos documentos en lote; crear un nuevo `ZipArchive` para cada archivo añade sobrecarga innecesaria.
* **Establece `LeaveOpen: true`** en el constructor de `ZipArchive` si necesitas leer los bytes del zip mientras el archivo está abierto.
* **Valida el HTML** antes de guardarlo llamando a `doc.OptionCheckSyntax = true;` – esto detecta etiquetas mal formadas temprano.
* **Registra el tamaño** del zip generado; una salida inusualmente grande a menudo indica recursos duplicados o falta de compresión.

## Ejemplo completo funcional

A continuación hay un solo archivo que puedes pegar en un proyecto de consola (`dotnet new console`) y ejecutar. Demuestra tanto el guardado de HTML simple como la compresión zip.



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo guardar HTML en C# con controlador de recursos personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Cómo usar ZipArchive – Guardar HTML y recursos en un archivo ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [guardar html como zip con un controlador de recursos personalizado – guía paso a paso](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}