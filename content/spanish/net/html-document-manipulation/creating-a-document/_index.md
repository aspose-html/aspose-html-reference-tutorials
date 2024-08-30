---
title: Creación de un documento en .NET con Aspose.HTML
linktitle: Creando un documento en .NET
second_title: Aspose.HTML .NET API de manipulación HTML
description: Descubra el poder de Aspose.HTML para .NET. Aprenda a crear, manipular y optimizar documentos HTML y SVG con facilidad. Explore ejemplos paso a paso y preguntas frecuentes.
type: docs
weight: 14
url: /es/net/html-document-manipulation/creating-a-document/
---

En el mundo del desarrollo web, que está en constante evolución, es fundamental mantenerse a la vanguardia. Aspose.HTML para .NET ofrece a los desarrolladores un conjunto de herramientas sólido para trabajar con documentos HTML. Ya sea que comience desde cero, cargue desde un archivo, extraiga desde una URL o gestione documentos SVG, esta biblioteca ofrece la versatilidad que necesita.

En esta guía paso a paso, profundizaremos en los aspectos básicos del uso de Aspose.HTML para .NET, lo que garantizará que esté bien equipado para utilizar esta poderosa herramienta en sus proyectos de desarrollo web. Antes de profundizar en los detalles, repasemos los requisitos previos y los espacios de nombres necesarios para comenzar su recorrido.

## Prerrequisitos

Para seguir con éxito este tutorial y aprovechar el poder de Aspose.HTML para .NET, necesitará los siguientes requisitos previos:

- Una máquina Windows con .NET Framework o .NET Core instalado.
- Un editor de código como Visual Studio.
- Conocimientos básicos de programación en C#.

Ahora que ya tienes los requisitos previos establecidos, comencemos.

## Importación de espacios de nombres

Antes de comenzar a utilizar Aspose.HTML para .NET, debe importar los espacios de nombres necesarios. Estos espacios de nombres contienen clases y métodos que son fundamentales para trabajar con documentos HTML. A continuación, se incluye una lista de los espacios de nombres que debe importar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Con estos espacios de nombres importados, ahora está listo para sumergirse en los ejemplos paso a paso.

## Creando un documento HTML desde cero

### Paso 1: Inicializar un documento HTML vacío

```csharp
// Inicializar un documento HTML vacío.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento de texto y agrégalo al documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Guarde el documento en el disco.
    document.Save("document.html");
}
```

En este ejemplo, comenzamos creando un documento HTML vacío y le agregamos el texto "¡Hola mundo!". Luego, guardamos el documento en un archivo.

## Crear un documento HTML a partir de un archivo

### Paso 1: Prepare un archivo 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Paso 2: Cargar desde un archivo 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Escribe el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aquí, preparamos un archivo con el contenido "Hola mundo" y luego lo cargamos como un documento HTML. Imprimimos el contenido del documento en la consola.

## Crear un documento HTML a partir de una URL

### Paso 1: Cargar un documento desde una página web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Escribe el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

En este ejemplo, cargamos un documento HTML directamente desde una página web y mostramos su contenido.

## Creación de un documento HTML a partir de una cadena

### Paso 1: Preparar un código HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Paso 2: Inicializar el documento desde la variable de cadena

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Guarde el documento en el disco.
    document.Save("document.html");
}
```

Aquí, creamos un documento HTML a partir de una variable de cadena y lo guardamos en un archivo.

## Creación de un documento HTML a partir de un MemoryStream

### Paso 1: Crear un objeto de flujo de memoria

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Escribe el código HTML en el objeto de memoria
    sw.Write("<p>Hello World!</p>");
    // Establezca la posición al principio
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Inicializar documento desde el flujo de memoria
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Guarde el documento en el disco.
        document.Save("document.html");
    }
}
```

En este ejemplo, creamos un documento HTML a partir de un flujo de memoria y lo guardamos en un archivo.

## Trabajar con documentos SVG

### Paso 1: Inicializar el documento SVG a partir de una cadena

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://<circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Escribe el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aquí, creamos y mostramos un documento SVG a partir de una cadena.

## Cargar un documento HTML de forma asincrónica

### Paso 1: Crear la instancia del documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Paso 2: Suscríbete al evento 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Verifique el valor de la propiedad 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Paso 3: Navegar de forma asincrónica en la Uri especificada

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

En este ejemplo, cargamos un documento HTML de forma asincrónica y manejamos el evento 'ReadyStateChange' para mostrar el contenido cuando se completa la carga.

## Manejo del evento 'OnLoad'

### Paso 1: Crear la instancia del documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Paso 2: Suscríbete al evento 'OnLoad'

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Paso 3: Navegar de forma asincrónica en la Uri especificada

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Este ejemplo demuestra cómo cargar un documento HTML de forma asincrónica y manejar el evento 'OnLoad' para mostrar el contenido una vez finalizado.

## En conclusión

En el dinámico mundo del desarrollo web, es fundamental contar con las herramientas adecuadas. Aspose.HTML para .NET le proporciona los medios para crear, manipular y procesar documentos HTML y SVG de manera eficiente. Esta guía completa le ha enseñado los aspectos básicos para que pueda aprovechar el poder de Aspose.HTML para .NET en sus proyectos.

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para .NET?

A1: Aspose.HTML para .NET es una potente biblioteca .NET que permite a los desarrolladores trabajar con documentos HTML y SVG. Ofrece una amplia gama de funciones, desde la creación de documentos desde cero hasta el análisis y la manipulación de archivos HTML y SVG existentes.

### P2: ¿Puedo usar Aspose.HTML para .NET con .NET Core?

A2: Sí, Aspose.HTML para .NET es compatible con .NET Framework y .NET Core, lo que lo convierte en una opción versátil para las aplicaciones .NET modernas.

### P3: ¿Aspose.HTML para .NET es adecuado para el raspado y análisis web?

A3: ¡Por supuesto! Aspose.HTML para .NET es una excelente opción para tareas de análisis y extracción de datos web, gracias a su capacidad para cargar documentos HTML desde URL y cadenas. Puede extraer datos, realizar análisis y mucho más.

### P4: ¿Cómo puedo acceder al soporte para Aspose.HTML para .NET?

 A4: Si encuentra algún problema o tiene preguntas mientras usa Aspose.HTML para .NET, puede visitar el[Foro de Aspose](https://forum.aspose.com/) para recibir apoyo y asistencia de la comunidad y de los expertos de Aspose.

### A5: ¿Dónde puedo encontrar documentación detallada y opciones de descarga?

A5: Para obtener documentación completa y acceder a las opciones de descarga, puede consultar los siguientes enlaces:

- [Documentación](https://reference.aspose.com/html/net/)
- [Descargar](https://releases.aspose.com/html/net/)
- [Comprar](https://purchase.aspose.com/buy)
- [Prueba gratuita](https://releases.aspose.com/)
- [Licencia temporal](https://purchase.aspose.com/temporary-license/)