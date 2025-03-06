---
title: Cómo guardar un documento en .NET con Aspose.HTML
linktitle: Guardar un documento en .NET
second_title: Aspose.HTML .NET API de manipulación HTML
description: Descubra el poder de Aspose.HTML para .NET con nuestra guía paso a paso. Aprenda a crear, manipular y convertir documentos HTML y SVG
weight: 16
url: /es/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo guardar un documento en .NET con Aspose.HTML


En la era digital actual, crear y manipular documentos HTML y SVG es esencial para muchos desarrolladores de software y empresas. Aspose.HTML para .NET es una potente biblioteca que simplifica estas tareas y ofrece varias funcionalidades para trabajar con HTML, SVG y más. En esta guía completa, profundizaremos en los aspectos esenciales de Aspose.HTML para .NET y desglosaremos cada ejemplo en pasos fáciles de seguir. Tanto si es un desarrollador experimentado como si recién está comenzando, esta guía le resultará invaluable para aprovechar las capacidades de Aspose.HTML.

## Prerrequisitos

Antes de emprender este viaje, asegurémonos de que tienes todo lo que necesitas:

- Entorno de desarrollo: asegúrese de tener Visual Studio o cualquier otro entorno de desarrollo .NET instalado en su computadora.

- Aspose.HTML para .NET: Necesita obtener la biblioteca Aspose.HTML para .NET. Puede descargarla desde[aquí](https://releases.aspose.com/html/net/).

- Conocimiento de C#: es conveniente estar familiarizado con el lenguaje de programación C#, pero no es obligatorio. Esta guía está diseñada para principiantes.

## Importar espacio de nombres

Para comenzar a utilizar Aspose.HTML para .NET, deberá importar los espacios de nombres necesarios en su proyecto. En su código C#, incluya el siguiente espacio de nombres:

### Paso 1: Importar el espacio de nombres Aspose.HTML
```csharp
using Aspose.Html;
```

Este espacio de nombres le otorgará acceso a varias capacidades de manipulación de HTML y SVG.

## HTML a archivo

### Paso 1: Inicializar un documento HTML vacío
```csharp
// Inicializar un documento HTML vacío.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento de texto y agrégalo al documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Guarde el HTML en el archivo en el disco.
    document.Save("document.html");
}
```

En este ejemplo, creamos un documento HTML y le agregamos un texto simple que diga "¡Hola mundo!". Luego, guardamos el HTML en un archivo en el disco.

## HTML sin archivo vinculado

### Paso 1: Prepare un archivo HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Aquí, creamos un archivo HTML básico con un enlace de ancla a otro archivo.

### Paso 2: Cargar 'document.html' en la memoria
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Crear una instancia de Opciones de guardado
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Establezca la profundidad máxima de manejo en 0 para cortar los archivos HTML vinculados.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Guardar el documento
    document.Save(@".\html-to-file-example\document.html", options);
}
```

En este ejemplo, cargamos un documento HTML en la memoria, establecemos la profundidad máxima de manejo para cortar los archivos vinculados y guardamos el documento. 

## HTML a MHTML

### Paso 1: Prepare un archivo HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Al igual que en el Ejemplo 2, creamos un archivo HTML básico con un enlace de ancla a otro archivo.

### Paso 2: Cargue 'document.html' en la memoria y guárdelo como MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Guardar el documento como MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Aquí, cargamos el documento HTML en la memoria y lo guardamos en formato MHTML.

## HTML a Markdown

### Paso 1: Preparar un código HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 En este paso, definimos un fragmento de código HTML que contiene un`<H2>` elemento.

### Paso 2: Inicializar el documento desde el código HTML y guardarlo como Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Guarde el documento como un archivo Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Creamos un documento HTML a partir del fragmento de código y lo guardamos como un archivo Markdown.

## SVG a archivo

### Paso 1: Preparar un código SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' altura='80' anchura='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Aquí, creamos un código SVG que dibuja un gráfico simple y colorido.

### Paso 2: Inicializar un documento SVG desde el código y guardarlo en el disco
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Guarde el archivo SVG en el disco
    document.Save("document.svg");
}
```

En este paso, creamos un documento SVG a partir del código y lo guardamos como un archivo SVG.

## Conclusión

Aspose.HTML para .NET es una biblioteca versátil que simplifica el manejo de documentos HTML y SVG en sus aplicaciones .NET. En esta guía, hemos cubierto cinco ejemplos esenciales, desglosados en instrucciones paso a paso. Ya sea que esté creando, manipulando o convirtiendo documentos, Aspose.HTML lo tiene cubierto. Si sigue estos pasos, estará en el camino correcto para dominar esta poderosa herramienta.

## Preguntas frecuentes

### P1: ¿Qué es Aspose.HTML para .NET?

A1: Aspose.HTML para .NET es una biblioteca .NET que proporciona una amplia gama de funciones para trabajar con documentos HTML y SVG, incluida la creación, manipulación y conversión.

### P2: ¿Dónde puedo descargar Aspose.HTML para .NET?

 A2: Puede descargar Aspose.HTML para .NET desde[aquí](https://releases.aspose.com/html/net/).

### P3: ¿Aspose.HTML para .NET es adecuado para principiantes?

A3: Sí, Aspose.HTML para .NET puede ser utilizado tanto por principiantes como por desarrolladores experimentados. Los ejemplos de esta guía están diseñados para que sean fáciles de usar para principiantes.

### P4: ¿Puedo convertir HTML a otros formatos usando Aspose.HTML para .NET?

A4: Sí, Aspose.HTML para .NET admite la conversión a varios formatos, incluidos MHTML y Markdown, como se muestra en los ejemplos.

### Q5: ¿Dónde puedo obtener soporte para Aspose.HTML para .NET?

 A5: Puede encontrar ayuda y respuestas a sus preguntas en el foro de la comunidad Aspose.HTML[aquí](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
