---
category: general
date: 2026-08-15
description: Crea un manejador de recursos personalizado en C# para gestionar recursos
  HTML como imágenes y CSS. Aprende sobre HTMLLoadOptions, flujos de memoria y la
  carga de HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: es
lastmod: 2026-08-15
og_description: Crea un controlador de recursos personalizado en C# para controlar
  cómo se transmiten los recursos HTML. Este tutorial muestra la configuración de
  HTMLLoadOptions, el manejo de streams de memoria y la carga de HTMLDocument con
  lógica personalizada.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Crear controlador de recursos personalizado en C# – guía completa para la
  gestión de recursos HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Crear controlador de recursos personalizado en C# para cargar HTML
url: /es/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear un manejador de recursos personalizado en C# para la carga de HTML

Si necesitas **crear un manejador de recursos personalizado** para archivos HTML, esta guía te muestra exactamente cómo. Aprenderás a interceptar imágenes, CSS y otros recursos al cargar un documento HTML, usando `HTMLLoadOptions` y un flujo basado en memoria.

El tutorial cubre todo lo necesario para implementar un manejador reutilizable, configurar las opciones de carga y verificar que los recursos se capturan correctamente. No se necesita documentación externa, solo el código a continuación y las explicaciones.

## Requisitos previos

- .NET 6.0 o posterior
- Familiaridad básica con C#
- Una referencia a la biblioteca de procesamiento HTML que proporcione `HTMLDocument`, `HtmlLoadOptions` y `ResourceHandler` (p. ej., GroupDocs.Viewer for .NET)

## Visión general de la solución

Vamos a:

1. **Crear un manejador de recursos personalizado** mediante la subclase de `ResourceHandler`.
2. Configurar `HTMLLoadOptions` para usar el manejador.
3. Cargar un archivo HTML con `HTMLDocument` mientras el manejador suministra un flujo para cada recurso.
4. (Opcional) Almacenar los recursos recibidos en disco para verificación.

Cada paso incluye el código fuente completo y el razonamiento detrás de él.

## Paso 1: Definir la clase del manejador de recursos personalizado

Crear un manejador personalizado significa sobrescribir `HandleResource` para que la biblioteca pueda escribir los bytes del recurso en un flujo que tú controlas. Usar un `MemoryStream` mantiene los datos en memoria, lo que es ideal para pruebas o procesamiento posterior.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Por qué es importante:**  
Sobrescribir `HandleResource` te brinda control total sobre dónde se envían los datos del recurso. Si más adelante necesitas almacenar en caché imágenes, transformar CSS o registrar el uso de recursos, puedes reemplazar el `MemoryStream` por cualquier implementación de flujo personalizada.

## Paso 2: Configurar `HTMLLoadOptions` para usar el manejador

`HTMLLoadOptions` te permite conectar el manejador en la cadena de carga. Asignar la propiedad `ResourceHandler` indica al visor que invoque `MyHandler` para cada activo externo.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Por qué es importante:**  
Sin asignar `ResourceHandler`, el visor escribiría los recursos en su ubicación predeterminada (a menudo una carpeta temporal). Al especificar tu propio manejador, **creas un manejador de recursos personalizado** que se alinea con la estrategia de almacenamiento de tu aplicación.

## Paso 3: Cargar el documento HTML con las opciones configuradas

Ahora carga el archivo HTML. El visor llamará a `MyHandler.HandleResource` por cada recurso que encuentre.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

En este punto el contenido HTML se ha analizado y todos los recursos externos se han transmitido a los búferes de memoria suministrados por `MyHandler`.

## Paso 4 (opcional): Acceder a los recursos capturados

Si necesitas inspeccionar o persistir los recursos, puedes modificar `MyHandler` para almacenar cada `MemoryStream` en un diccionario indexado por el nombre del recurso.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Después de la carga, puedes iterar sobre `handler.Resources` y escribir cada uno en disco:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Por qué es importante:**  
Almacenar los recursos permite el post‑procesamiento, como optimización de imágenes, minificación de CSS o archivado. También proporciona una verificación tangible de que la lógica de **crear un manejador de recursos personalizado** funciona como se espera.

## Paso 5: Limpieza

Tanto `HTMLDocument` como cualquier flujo deben disponerse para liberar recursos no administrados.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Ejemplo completo ejecutable

A continuación se muestra un programa autocontenido que demuestra todos los pasos, desde la definición de la clase hasta la extracción de recursos.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Salida esperada**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

La consola enumera cada recurso que el visor transmitió a través de tu manejador personalizado, confirmando que el flujo de **crear un manejador de recursos personalizado** se completó con éxito.

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si un recurso es grande (p. ej., una imagen de alta resolución)?* | Reemplaza `MemoryStream` por un `FileStream` que apunte a una carpeta temporal. Esto evita un consumo excesivo de memoria. |
| *¿Puedo filtrar recursos por tipo?* | Dentro de `HandleResource`, inspecciona `info.MimeType` o `info.Extension` y devuelve `null` para los tipos no deseados. Devolver `null` indica al visor que omita el recurso. |
| *¿Se requiere seguridad en hilos?* | Si la misma instancia del manejador se usa en múltiples cargas concurrentes, protege el diccionario `Resources` con un bloqueo o utiliza una colección concurrente. |
| *¿Cómo admito URLs relativas?* | `ResourceInfo` contiene la URL original; puedes combinarla con la ruta base del archivo HTML para resolver referencias relativas antes de almacenarlas. |

## Conclusión

Ahora sabes cómo **crear un manejador de recursos personalizado** en C# para la carga de HTML, configurar `HTMLLoadOptions`, capturar los activos transmitidos y limpiar de forma responsable. Este patrón te brinda control total sobre la gestión de recursos, habilitando escenarios como procesamiento de imágenes en tiempo real, reescritura de CSS o almacenamiento seguro.

A continuación, explora temas relacionados como la **carga de HTMLDocument** con diferentes opciones de renderizado, o extiende el manejador a implementaciones de **manejador de recursos en C#** que escriban directamente en almacenamiento en la nube. Experimenta con el método `HandleResource` del manejador para adaptarlo al flujo de recursos específico de tu proyecto.

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}