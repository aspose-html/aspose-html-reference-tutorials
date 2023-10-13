---
title: Guardar un documento en .NET con Aspose.HTML
linktitle: Guardar un documento en .NET
second_title: Aspose.Slides API de manipulación HTML .NET
description: Desbloquee el poder de Aspose.HTML para .NET con nuestra guía paso a paso. Aprenda a crear, manipular y convertir documentos HTML y SVG
type: docs
weight: 16
url: /es/net/html-document-manipulation/saving-a-document/
---

En la era digital actual, crear y manipular documentos HTML y SVG es esencial para muchos desarrolladores de software y empresas. Aspose.HTML para .NET es una poderosa biblioteca que simplifica estas tareas y ofrece varias funcionalidades para trabajar con HTML, SVG y más. En esta guía completa, profundizaremos en los conceptos básicos de Aspose.HTML para .NET, dividiendo cada ejemplo en pasos fáciles de seguir. Si es un desarrollador experimentado o recién está comenzando, esta guía le resultará invaluable para aprovechar las capacidades de Aspose.HTML.

## Requisitos previos

Antes de embarcarnos en este viaje, asegurémonos de que tiene todo lo que necesita:

- Entorno de desarrollo: asegúrese de tener Visual Studio o cualquier otro entorno de desarrollo .NET instalado en su computadora.

-  Aspose.HTML para .NET: Debe obtener la biblioteca Aspose.HTML para .NET. Puedes descargarlo desde[aquí](https://releases.aspose.com/html/net/).

- Conocimiento de C#: la familiaridad con el lenguaje de programación C# es beneficiosa pero no obligatoria. Esta guía está diseñada para que sea fácil de usar para principiantes.

## Importar espacio de nombres

Para comenzar a usar Aspose.HTML para .NET, deberá importar los espacios de nombres necesarios a su proyecto. En su código C#, incluya el siguiente espacio de nombres:

### Paso 1: Importar el espacio de nombres Aspose.HTML
```csharp
using Aspose.Html;
```

Este espacio de nombres le otorgará acceso a varias capacidades de manipulación de HTML y SVG.

## HTML a archivo

### Paso 1: inicializar un documento HTML vacío
```csharp
// Inicialice un documento HTML vacío.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento de texto y agrégalo al documento.
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Guarde el HTML en el archivo del disco.
    document.Save("document.html");
}
```

En este ejemplo, creamos un documento HTML y agregamos un simple "¡Hola mundo!" enviarle un mensaje de texto. Luego guardamos el HTML en un archivo en el disco.

## HTML sin archivo vinculado

### Paso 1: prepare un archivo HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Aquí, creamos un archivo HTML básico con un enlace ancla a otro archivo.

### Paso 2: cargue 'document.html' en la memoria
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Crear instancia de Opciones de guardado
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    // Establezca la profundidad máxima de manejo en 0 para cortar los archivos HTML vinculados.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // guardar el documento
    document.Save(@".\html-to-file-example\document.html", options);
}
```

En este ejemplo, cargamos un documento HTML en la memoria, configuramos la profundidad máxima de manejo para cortar archivos vinculados y guardamos el documento. 

## HTML a MHTML

### Paso 1: prepare un archivo HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Al igual que en el Ejemplo 2, creamos un archivo HTML básico con un enlace ancla a otro archivo.

### Paso 2: cargue 'document.html' en la memoria y guárdelo como MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Guarde el documento como MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Aquí, cargamos el documento HTML en la memoria y lo guardamos en formato MHTML.

## HTML a rebajas

### Paso 1: preparar un código HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 En este paso, definimos un fragmento de código HTML que contiene un`<H2>` elemento.

### Paso 2: Inicialice el documento desde el código HTML y guárdelo como Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Guarde el documento como un archivo Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Creamos un documento HTML a partir del fragmento de código y lo guardamos como un archivo Markdown.

## SVG a archivo

### Paso 1: preparar un código SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' altura='80' ancho='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Aquí, creamos un código SVG que dibuja un gráfico simple y colorido.

### Paso 2: Inicialice un documento SVG desde el código y guárdelo en el disco
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Guarde el archivo SVG en el disco
    document.Save("document.svg");
}
```

En este paso, creamos un documento SVG a partir del código y lo guardamos como un archivo SVG.

## Conclusión

Aspose.HTML para .NET es una biblioteca versátil que simplifica el manejo de documentos HTML y SVG en sus aplicaciones .NET. En esta guía, cubrimos cinco ejemplos esenciales, dividiendo cada uno en instrucciones paso a paso. Ya sea que esté creando, manipulando o convirtiendo documentos, Aspose.HTML lo tiene cubierto. Si sigue estos pasos, estará en el camino correcto para dominar esta poderosa herramienta.

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para .NET?

R1: Aspose.HTML para .NET es una biblioteca .NET que proporciona una amplia gama de funciones para trabajar con documentos HTML y SVG, incluida la creación, manipulación y conversión.

### P2: ¿Dónde puedo descargar Aspose.HTML para .NET?

 R2: Puede descargar Aspose.HTML para .NET desde[aquí](https://releases.aspose.com/html/net/).

### P3: ¿Aspose.HTML para .NET es adecuado para principiantes?

R3: Sí, Aspose.HTML para .NET puede ser utilizado tanto por desarrolladores principiantes como experimentados. Los ejemplos de esta guía están diseñados para que sean aptos para principiantes.

### P4: ¿Puedo convertir HTML a otros formatos usando Aspose.HTML para .NET?

R4: Sí, Aspose.HTML para .NET admite la conversión a varios formatos, incluidos MHTML y Markdown, como se muestra en los ejemplos.

### P5: ¿Dónde puedo obtener soporte para Aspose.HTML para .NET?

 R5: Puede encontrar soporte y respuestas a sus preguntas en el foro de la comunidad Aspose.HTML.[aquí](https://forum.aspose.com/).