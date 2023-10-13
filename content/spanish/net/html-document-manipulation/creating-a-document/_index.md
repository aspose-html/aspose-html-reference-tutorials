---
title: Creando un documento en .NET con Aspose.HTML
linktitle: Crear un documento en .NET
second_title: Aspose.Slides API de manipulación HTML .NET
description: Libere el poder de Aspose.HTML para .NET. Aprenda a crear, manipular y optimizar documentos HTML y SVG con facilidad. Explore ejemplos paso a paso y preguntas frecuentes.
type: docs
weight: 14
url: /es/net/html-document-manipulation/creating-a-document/
---

En el mundo del desarrollo web en constante evolución, mantenerse a la vanguardia es esencial. Aspose.HTML para .NET proporciona a los desarrolladores un sólido conjunto de herramientas para trabajar con documentos HTML. Ya sea que esté comenzando desde cero, cargando desde un archivo, extrayendo de una URL o manejando documentos SVG, esta biblioteca ofrece la versatilidad que necesita.

En esta guía paso a paso, profundizaremos en los fundamentos del uso de Aspose.HTML para .NET, asegurándonos de que esté bien equipado para utilizar esta poderosa herramienta en sus proyectos de desarrollo web. Antes de profundizar en los detalles, repasemos los requisitos previos y los espacios de nombres necesarios para iniciar su viaje.

## Requisitos previos

Para seguir con éxito este tutorial y aprovechar el poder de Aspose.HTML para .NET, necesitará los siguientes requisitos previos:

- Una máquina Windows con .NET Framework o .NET Core instalado.
- Un editor de código como Visual Studio.
- Conocimientos básicos de programación en C#.

Ahora que ya tiene los requisitos previos establecidos, comencemos.

## Importando espacios de nombres

Antes de comenzar a usar Aspose.HTML para .NET, debe importar los espacios de nombres necesarios. Estos espacios de nombres contienen clases y métodos que son vitales para trabajar con documentos HTML. A continuación se muestra una lista de espacios de nombres que debe importar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Una vez importados estos espacios de nombres, ya está listo para sumergirse en los ejemplos paso a paso.

## Crear un documento HTML desde cero

### Paso 1: inicializar un documento HTML vacío

```csharp
// Inicialice un documento HTML vacío.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento de texto y agrégalo al documento.
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Guarde el documento en el disco.
    document.Save("document.html");
}
```

En este ejemplo, comenzamos creando un documento HTML vacío y agregando un "¡Hola mundo!" enviarle un mensaje de texto. Luego guardamos el documento en un archivo.

## Crear un documento HTML a partir de un archivo

### Paso 1: prepare un archivo 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Paso 2: cargar desde un archivo 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Escriba el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aquí preparamos un archivo con "¡Hola mundo!" contenido y luego cárguelo como un documento HTML. Imprimimos el contenido del documento en la consola.

## Crear un documento HTML a partir de una URL

### Paso 1: cargar un documento desde una página web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Escriba el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

En este ejemplo, cargamos un documento HTML directamente desde una página web y mostramos su contenido.

## Crear un documento HTML a partir de una cadena

### Paso 1: preparar un código HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Paso 2: inicializar el documento desde la variable de cadena

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Guarde el documento en el disco.
    document.Save("document.html");
}
```

Aquí, creamos un documento HTML a partir de una variable de cadena y lo guardamos en un archivo.

## Crear un documento HTML a partir de un MemoryStream

### Paso 1: crear un objeto de flujo de memoria

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Escriba el código HTML en el objeto de memoria.
    sw.Write("<p>Hello World!</p>");
    // Establecer la posición al principio.
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

### Paso 1: Inicialice el documento SVG a partir de una cadena

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Escriba el contenido del documento en el flujo de salida.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aquí, creamos y mostramos un documento SVG a partir de una cadena.

## Cargar un documento HTML de forma asincrónica

### Paso 1: crear la instancia del documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Paso 2: Suscríbete al evento 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Verifique el valor de la propiedad 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Paso 3: navegar de forma asincrónica en el Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

En este ejemplo, cargamos un documento HTML de forma asincrónica y manejamos el evento 'ReadyStateChange' para mostrar el contenido cuando se completa la carga.

## Manejo del evento 'OnLoad'

### Paso 1: crear la instancia del documento HTML

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

### Paso 3: navegar de forma asincrónica en el Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Este ejemplo demuestra la carga de un documento HTML de forma asincrónica y el manejo del evento 'OnLoad' para mostrar el contenido al finalizar.

## En conclusión

En el dinámico mundo del desarrollo web, tener las herramientas adecuadas a su disposición es crucial. Aspose.HTML para .NET le proporciona los medios para crear, manipular y procesar documentos HTML y SVG de manera eficiente. Esta guía completa lo ha guiado a través de los conceptos básicos, asegurando que pueda aprovechar el poder de Aspose.HTML para .NET en sus proyectos.

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para .NET?

R1: Aspose.HTML para .NET es una poderosa biblioteca .NET que permite a los desarrolladores trabajar con documentos HTML y SVG. Proporciona una amplia gama de funciones, desde la creación de documentos desde cero hasta el análisis y manipulación de archivos HTML y SVG existentes.

### P2: ¿Puedo usar Aspose.HTML para .NET con .NET Core?

R2: Sí, Aspose.HTML para .NET es compatible tanto con .NET Framework como con .NET Core, lo que lo convierte en una opción versátil para aplicaciones .NET modernas.

### P3: ¿Aspose.HTML para .NET es adecuado para el análisis y el scraping web?

R3: ¡Absolutamente! Aspose.HTML para .NET es una excelente opción para tareas de análisis y raspado web, gracias a su capacidad para cargar documentos HTML desde URL y cadenas. Puede extraer datos, realizar análisis y más.

### P4: ¿Cómo puedo acceder al soporte de Aspose.HTML para .NET?

 R4: Si encuentra algún problema o tiene preguntas mientras usa Aspose.HTML para .NET, puede visitar el[Foro Aspose](https://forum.aspose.com/) para el apoyo y asistencia de la comunidad y los expertos de Aspose.

### R5: ¿Dónde puedo encontrar documentación detallada y opciones de descarga?

R5: Para obtener documentación completa y acceso a opciones de descarga, puede consultar los siguientes enlaces:

- [Documentación](https://reference.aspose.com/html/net/)
- [Descargar](https://releases.aspose.com/html/net/)
- [Comprar](https://purchase.aspose.com/buy)
- [Prueba gratis](https://releases.aspose.com/)
- [Licencia Temporal](https://purchase.aspose.com/temporary-license/)