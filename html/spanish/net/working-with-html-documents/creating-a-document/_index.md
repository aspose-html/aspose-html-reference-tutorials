---
title: Creación de un documento HTML en .NET con Aspose.HTML
linktitle: Creación de un documento HTML en .NET
second_title: Aspose.HTML .NET API de manipulación HTML
description: Aprenda a crear documentos HTML en .NET con Aspose.HTML, desde cero o a partir de URL. Un tutorial completo para desarrolladores web.
weight: 10
url: /es/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creación de un documento HTML en .NET con Aspose.HTML


En el ámbito del desarrollo web y la manipulación de datos, es indispensable contar con una herramienta potente para crear, modificar y trabajar con documentos HTML. Aspose.HTML para .NET es una de esas herramientas que puede simplificar las tareas relacionadas con HTML. En este completo tutorial, exploraremos cómo crear documentos HTML utilizando Aspose.HTML para .NET paso a paso. Antes de profundizar en los ejemplos, veamos algunos requisitos previos.

## Prerrequisitos

Antes de emprender este viaje, asegúrese de tener los siguientes requisitos previos:

1. Visual Studio: asegúrese de tener Visual Studio instalado en su sistema.

2. Aspose.HTML para .NET: Descargue e instale la biblioteca Aspose.HTML para .NET. Puede encontrar el enlace de descarga[aquí](https://releases.aspose.com/html/net/).

3. Conocimientos básicos de C#: Familiarícese con los conceptos básicos del lenguaje de programación C#.

Ahora que cubrimos los requisitos previos, comencemos a crear documentos HTML.

## Importación de espacios de nombres

En primer lugar, debe importar los espacios de nombres necesarios para utilizar Aspose.HTML en su proyecto de C#. Agregue las siguientes directivas using a su archivo de código:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Creación de un documento SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Realice acciones en el documento SVG aquí...
    }
}
```

 En este ejemplo, creamos un documento SVG proporcionando el contenido SVG y una URL base.`SVGDocument` La clase de Aspose.HTML para .NET le permite manipular documentos SVG sin esfuerzo.

## Creando un documento HTML desde cero

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Realice acciones en el documento HTML aquí...
    }
}
```

 Este ejemplo demuestra cómo crear un documento HTML desde cero.`HTMLDocument`La clase proporciona un lienzo en blanco para su contenido HTML.

## Creación de un documento HTML a partir de un archivo local

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Realice acciones en el documento HTML aquí...
    }
}
```

 Si tiene un archivo HTML existente en su sistema local, puede cargarlo usando el`HTMLDocument` clase, como se muestra en este ejemplo.

## Creación de un documento HTML desde una URL remota

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://tu.sitio.com/"))
    {
        // Realice acciones en el documento HTML aquí...
    }
}
```

En ocasiones, es posible que necesite trabajar con contenido HTML alojado en un servidor remoto. Este ejemplo demuestra cómo crear un documento HTML desde una URL remota.

## Creación de un documento HTML desde una URL remota (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://tu.sitio.com/")))
    {
        // Realice acciones en el documento HTML aquí...
    }
}
```

Este enfoque alternativo también muestra cómo crear un documento HTML desde una URL remota utilizando un constructor diferente.

## Creación de un documento HTML a partir de contenido HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Realice acciones en el documento HTML aquí...
    }
}
```

Si tiene contenido HTML en formato de cadena, puede crear un documento HTML con él, como se muestra en este ejemplo.

## Creación de un documento HTML a partir de una secuencia

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Realice acciones en el documento HTML aquí...
        }
    }
}
```

En este ejemplo, mostramos cómo crear un documento HTML a partir de datos en un flujo de memoria. Esto puede resultar útil cuando se tiene contenido HTML en un flujo y se desea manipularlo.

## Conclusión

Aspose.HTML para .NET ofrece un potente conjunto de herramientas para crear y trabajar con documentos HTML en sus aplicaciones .NET. Con los ejemplos que se ofrecen en este tutorial, puede comenzar fácilmente a crear documentos HTML, ya sea desde cero, desde archivos locales, URL remotas o desde contenido HTML existente.

 ¿Tiene preguntas o necesita ayuda? Visite el foro de la comunidad Aspose.HTML para obtener ayuda en[https://forum.aspose.com/](https://forum.aspose.com/).

## Preguntas frecuentes

### P1: ¿Aspose.HTML para .NET es de uso gratuito?
 A1: Aspose.HTML para .NET ofrece una versión de prueba gratuita, pero para utilizarlo en su totalidad, deberá adquirir una licencia. Puede encontrar más detalles en[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### P2: ¿Cómo puedo obtener una licencia temporal de Aspose.HTML para .NET?
 A2: Si necesita una licencia temporal, puede obtenerla en[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### P3: ¿Dónde puedo encontrar documentación de Aspose.HTML para .NET?
A3: La documentación se puede encontrar en[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### P4: ¿Existen otras bibliotecas Aspose para el desarrollo .NET?
 A4: Sí, Aspose ofrece una variedad de bibliotecas para distintos formatos de archivos y tareas de manipulación de documentos. Consulta sus ofertas en[https://productos.aspose.com/](https://products.aspose.com/).

### Q5: ¿Puedo utilizar Aspose.HTML para .NET en mis aplicaciones web?
A5: Sí, Aspose.HTML para .NET es compatible con aplicaciones web, lo que lo convierte en una opción versátil tanto para proyectos de escritorio como basados en la web.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
