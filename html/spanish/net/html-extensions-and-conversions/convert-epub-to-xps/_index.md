---
title: Convierta EPUB a XPS en .NET con Aspose.HTML
linktitle: Convertir EPUB a XPS en .NET
second_title: Aspose.HTML .NET API de manipulación HTML
description: Aprenda a convertir EPUB a XPS en .NET con Aspose.HTML para .NET. Siga nuestra guía paso a paso para realizar conversiones sin esfuerzo.
weight: 13
url: /es/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convierta EPUB a XPS en .NET con Aspose.HTML


¿Está buscando una forma sencilla de convertir archivos EPUB a formato XPS en sus aplicaciones .NET? Aspose.HTML para .NET ofrece una solución eficaz para lograrlo sin esfuerzo. En esta guía paso a paso, le explicaremos el proceso de conversión de EPUB a formato XPS con Aspose.HTML. ¡Comencemos!

## Prerrequisitos

Antes de sumergirse en el proceso de conversión de EPUB a XPS, deberá asegurarse de tener los siguientes requisitos previos:

### 1. Biblioteca Aspose.HTML para .NET

 Asegúrese de tener instalada la biblioteca Aspose.HTML para .NET en su proyecto. Si aún no lo ha hecho, puede obtenerla desde[Página de descarga de Aspose.HTML para .NET](https://releases.aspose.com/html/net/).

### 2. Introduzca el archivo EPUB

Necesitará un archivo EPUB que desee convertir a XPS. Asegúrese de tener un archivo EPUB disponible para la conversión.

### 3. Entorno de desarrollo .NET

Esta guía asume que tiene un entorno de desarrollo .NET funcional configurado en su máquina.

## Importar espacio de nombres

Para comenzar, debes importar el espacio de nombres necesario para Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Convertir EPUB a XPS

Analicemos el proceso de conversión de un archivo EPUB al formato XPS en varios pasos.

### Paso 1.1: Abra el archivo EPUB

Primero, abra el archivo EPUB existente para leerlo usando FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuar con el proceso de conversión
}
```

### Paso 1.2: Crear XpsSaveOptions

Cree una instancia de XpsSaveOptions. Este paso es fundamental para configurar la salida XPS:

```csharp
var options = new XpsSaveOptions();
```

### Paso 1.3: Convertir EPUB a XPS

Ahora, llamemos al método ConvertEPUB para convertir el EPUB a XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Especificar opciones XPS personalizadas

Puede personalizar aún más la salida XPS especificando opciones personalizadas como el tamaño de la página y el color de fondo.

### Paso 2.1: Tamaño de página personalizado y color de fondo

Cree una instancia de XpsSaveOptions con tamaño de página y color de fondo personalizados:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Paso 2.2: Convertir EPUB a XPS con opciones personalizadas

Ahora, llame al método ConvertEPUB para convertir el EPUB a XPS con las opciones personalizadas:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Utilice un proveedor de transmisión personalizado

En este paso, convertiremos EPUB a XPS utilizando un proveedor de transmisión personalizado, lo que le permitirá manipular los datos resultantes.

### Paso 3.1: Crear un MemoryStreamProvider

Cree una instancia de MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Continuar con el proceso de conversión
}
```

### Paso 3.2: Convertir EPUB a XPS con Stream Provider

Convierta EPUB a XPS utilizando MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Paso 3.3: Acceder y guardar el resultado

Recupere el flujo de memoria que contiene los datos convertidos y guárdelo en un archivo de salida:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Código fuente de la clase MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista de objetos MemoryStream creados durante la representación del documento
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Este método se llama cuando solo se requiere un flujo de salida, por ejemplo, para los formatos XPS, PDF o TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Este método se llama cuando se requiere la creación de múltiples flujos de salida. Por ejemplo, durante la representación de HTML en una lista de archivos de imagen (JPG, PNG, etc.).
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Aquí puede liberar el flujo lleno de datos y, por ejemplo, vaciarlo al disco duro.
            }
            public void Dispose()
            {
                // Liberación de recursos
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
¡Felicitaciones! Has convertido exitosamente un archivo EPUB al formato XPS usando Aspose.HTML para .NET.

## Conclusión

En este tutorial completo, exploramos cómo aprovechar Aspose.HTML para .NET para convertir archivos EPUB a formato XPS con varias opciones de personalización. Ya sea que sea un desarrollador experimentado o recién esté comenzando, Aspose.HTML simplifica el proceso y le permite realizar conversiones de EPUB a XPS con facilidad.

 ¿Tiene alguna pregunta o ha tenido problemas? Consulte la[Documentación de Aspose.HTML](https://reference.aspose.com/html/net/) Para obtener más información o buscar ayuda, comuníquese con el[Foro de la comunidad Aspose.HTML](https://forum.aspose.com/).

## Preguntas frecuentes

### ¿Qué es Aspose.HTML para .NET?
Aspose.HTML para .NET es una potente biblioteca que permite a los desarrolladores trabajar con documentos HTML, EPUB y XPS en aplicaciones .NET.

### ¿Dónde puedo descargar Aspose.HTML para .NET?
 Puede descargar Aspose.HTML para .NET desde[página de descarga](https://releases.aspose.com/html/net/).

### ¿Hay una prueba gratuita disponible para Aspose.HTML para .NET?
 Sí, puedes obtener una prueba gratuita desde[aquí](https://releases.aspose.com/).

### ¿Cómo puedo obtener una licencia temporal de Aspose.HTML para .NET?
 Para obtener una licencia temporal, visite el[página de licencia temporal](https://purchase.aspose.com/temporary-license/).

### ¿Dónde puedo encontrar más tutoriales y documentación sobre Aspose.HTML para .NET?
 Explore una amplia gama de tutoriales y documentación detallada sobre el[Documentación de Aspose.HTML](https://reference.aspose.com/html/net/) página.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
