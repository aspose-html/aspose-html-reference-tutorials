---
title: Convierta EPUB a PDF en .NET con Aspose.HTML
linktitle: Convertir EPUB a PDF en .NET
second_title: Aspose.HTML .NET API de manipulación de HTML
description: Aprenda cómo convertir EPUB a PDF usando Aspose.HTML para .NET. Esta guía paso a paso cubre opciones de personalización, preguntas frecuentes y más para una conversión de documentos perfecta.
type: docs
weight: 12
url: /es/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

En este tutorial, exploraremos cómo usar Aspose.HTML para .NET para convertir archivos EPUB a PDF. Aspose.HTML es una poderosa biblioteca .NET que proporciona varias funcionalidades para trabajar con documentos HTML y EPUB. Cubriremos los requisitos previos, importaremos los espacios de nombres necesarios y desglosaremos varios ejemplos, explicando cada paso en detalle.

## Requisitos previos

Antes de comenzar, asegúrese de cumplir con los siguientes requisitos previos:

1. Aspose.HTML para .NET: asegúrese de tener Aspose.HTML para .NET instalado en su proyecto .NET. Puedes descargarlo desde[aquí](https://releases.aspose.com/html/net/).

2. Su directorio de datos: necesitará un directorio de datos donde se almacenen sus archivos EPUB.

Ahora, profundicemos en el proceso paso a paso de convertir EPUB a PDF usando Aspose.HTML para .NET.

## Convertir EPUB a PDF

### Paso 1: Inicialice su proyecto

Asegúrese de tener un proyecto .NET configurado y Aspose.HTML para .NET esté instalado.

### Paso 2: importar los espacios de nombres necesarios

En su archivo de código C#, importe los espacios de nombres necesarios:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Paso 3: abra el archivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continúe con el siguiente paso...
}
```

-  Reemplazar`"Your Data Directory"` con el directorio real donde se encuentra su archivo EPUB.
- Este código abre el archivo EPUB para su lectura.

### Paso 4: configurar las opciones de PDF y realizar la conversión

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Crear una instancia de`PdfSaveOptions` para especificar la configuración de conversión de PDF.
-  Utilizar el`Converter.ConvertEPUB` Método para convertir EPUB a PDF con las opciones dadas.
- Guarde el PDF resultante como "output.pdf".

## Especificar opciones para guardar PDF

### Paso 1: Inicialice su proyecto

Asegúrese de tener un proyecto .NET configurado y Aspose.HTML para .NET instalado.

### Paso 2: importar los espacios de nombres necesarios

Importe los espacios de nombres necesarios en su código C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Paso 3: abra el archivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continúe con el siguiente paso...
}
```

-  Reemplazar`"Your Data Directory"` con el directorio real de su archivo EPUB.
- Abra el archivo EPUB para leerlo.

### Paso 4: Personaliza las opciones de PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Crear una instancia de`PdfSaveOptions` y personalizarlo según sus necesidades.
- En este ejemplo, configuramos el tamaño de la página en 3000 píxeles de ancho y 1000 píxeles de alto, y el color de fondo en Alice Blue.

### Paso 5: realizar la conversión

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Utilizar el`Converter.ConvertEPUB` Método para convertir EPUB a PDF con las opciones personalizadas.
- Guarde el PDF resultante como "output.pdf".

## Utilice un proveedor de transmisión personalizado

### Paso 1: Inicialice su proyecto

Configure un proyecto .NET e instale Aspose.HTML para .NET.

### Paso 2: importar los espacios de nombres necesarios

En su código C#, importe los espacios de nombres necesarios:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Paso 3: abra el archivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continúe con el siguiente paso...
}
```

-  Reemplazar`"Your Data Directory"` con el directorio real de su archivo EPUB.
- Abra el archivo EPUB para leerlo.

### Paso 4: utilice un proveedor de transmisión personalizado

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Continúe con el siguiente paso...
}
```

-  Crear un`MemoryStreamProvider` para gestionar el resultado de la conversión como un flujo de memoria.
-  Utilizar el`Converter.ConvertEPUB` método con el proveedor de flujo personalizado.

### Paso 5: guarde el resultado

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Acceda al flujo de memoria que contiene los datos convertidos.
- Establezca la posición de la transmisión al principio.
- Cree un archivo PDF de salida y copie el contenido del flujo de memoria en él.

### Código fuente de la clase MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista de objetos MemoryStream creados durante la representación del documento
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Se llama a este método cuando se requiere un único flujo de salida, por ejemplo para formatos XPS, PDF o TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Este método se llama cuando se requiere la creación de múltiples flujos de salida. Por ejemplo, durante el renderizado HTML para listar los archivos de imagen (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Aquí puede liberar el flujo lleno de datos y, por ejemplo, descargarlo en el disco duro.
            }
            public void Dispose()
            {
                // Liberando recursos
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Ahora ha aprendido cómo convertir archivos EPUB a PDF usando Aspose.HTML para .NET con varias opciones y posibilidades de personalización. Aspose.HTML simplifica el proceso, brindando flexibilidad y control sobre la conversión de su documento.

## Conclusión

Aspose.HTML para .NET es una herramienta versátil para convertir archivos EPUB a PDF, que ofrece opciones de personalización para adaptar el documento PDF resultante a sus necesidades. Ya sea que necesite conversiones simples o personalización avanzada, Aspose.HTML lo tiene cubierto.

 Si aún no lo ha hecho, puede descargar Aspose.HTML para .NET desde[sitio web](https://releases.aspose.com/html/net/) y comience a usarlo en sus aplicaciones .NET hoy.

---

## Preguntas frecuentes

### ¿Aspose.HTML para .NET es de uso gratuito?
    Aspose.HTML para .NET es un producto comercial, pero hay una prueba gratuita disponible[aquí](https://releases.aspose.com/).

### ¿Puedo personalizar la apariencia del PDF convertido?
   Sí, puedes personalizar la apariencia del PDF ajustando opciones como el tamaño de página y el color de fondo, como se muestra en el Ejemplo 2.

### ¿Cómo puedo obtener soporte para Aspose.HTML para .NET?
    Puede encontrar apoyo y recursos en el[Foro Aspose.HTML](https://forum.aspose.com/).

### ¿Existen otros formatos que pueda convertir con Aspose.HTML para .NET?
   Sí, Aspose.HTML para .NET admite varios formatos de documentos, incluidos HTML, EPUB y más.

### ¿Aspose.HTML para ..NET es adecuado para la conversión de documentos a gran escala?
   Aspose.HTML para .NET está diseñado para manejar conversiones de documentos a gran escala de manera eficiente, lo que lo hace adecuado para una amplia gama de aplicaciones.

