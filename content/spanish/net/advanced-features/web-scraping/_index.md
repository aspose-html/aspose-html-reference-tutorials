---
title: Web Scraping en .NET con Aspose.HTML
linktitle: Raspado web en .NET
second_title: Aspose.HTML .NET API de manipulación de HTML
description: Aprenda a manipular documentos HTML en .NET con Aspose.HTML. Navegue, filtre, consulte y seleccione elementos de manera efectiva para mejorar el desarrollo web.
type: docs
weight: 13
url: /es/net/advanced-features/web-scraping/
---

En la era digital actual, manipular y extraer información de documentos HTML es una tarea común para los desarrolladores. Aspose.HTML para .NET es una poderosa herramienta que simplifica el procesamiento y manipulación de HTML en aplicaciones .NET. En este tutorial, exploraremos varios aspectos de Aspose.HTML para .NET, incluidos requisitos previos, espacios de nombres y ejemplos paso a paso para ayudarlo a aprovechar todo su potencial.

## Requisitos previos

Antes de sumergirse en el mundo de Aspose.HTML para .NET, necesitará algunos requisitos previos:

1. Entorno de desarrollo: asegúrese de tener un entorno de desarrollo funcional configurado con Visual Studio o cualquier otro IDE compatible para el desarrollo .NET.

2.  Aspose.HTML para .NET: descargue e instale la biblioteca Aspose.HTML para .NET desde[enlace de descarga](https://releases.aspose.com/html/net/). Puede elegir entre la versión de prueba gratuita o una con licencia según sus necesidades.

3. Conocimiento básico de HTML: la familiaridad con la estructura y los elementos HTML es esencial para utilizar Aspose.HTML de forma eficaz para .NET.

## Importando espacios de nombres

Para comenzar, necesita importar los espacios de nombres necesarios en su proyecto C#. Estos espacios de nombres brindan acceso a Aspose.HTML para clases y funcionalidades de .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Con los requisitos previos implementados y los espacios de nombres importados, analicemos algunos ejemplos clave paso a paso para ilustrar cómo usar Aspose.HTML para .NET de manera efectiva.

## Navegando a través de HTML

En este ejemplo, navegaremos por un documento HTML y accederemos a sus elementos paso a paso.

```csharp
public static void NavigateThroughHTML()
{
    // Preparar un código HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Inicializar un documento a partir del código preparado
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Obtener la referencia al primer hijo (primer SPAN) del BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Salida: Hola

        // Obtener la referencia al espacio en blanco entre elementos HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Producción: ' '

        // Obtener la referencia al segundo elemento SPAN.
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Salida: ¡Mundo!
    }
}
```

 En este ejemplo, creamos un documento HTML, accedemos a su primer hijo (un`SPAN` elemento), el espacio en blanco entre elementos, y el segundo`SPAN` elemento, que demuestra la navegación básica.

## Usar filtros de nodo

Los filtros de nodo le permiten procesar selectivamente elementos específicos dentro de un documento HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Preparar un código HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inicializar un documento basado en el código preparado.
    using (var document = new HTMLDocument(code, "."))
    {
        // Cree un TreeWalker con un filtro personalizado para elementos de imagen
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Salida: imagen1.png
                // Salida: imagen2.png
            }
        }
    }
}
```

 Este ejemplo demuestra cómo utilizar un filtro de nodo personalizado para extraer elementos específicos (en este caso,`IMG` elementos) del documento HTML.

## Consultas XPath

Las consultas XPath le permiten buscar elementos en un documento HTML según criterios específicos.

```csharp
public static void XPathQueryUsageExample()
{
    // Preparar un código HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Inicializar un documento basado en el código preparado.
    using (var document = new HTMLDocument(code, "."))
    {
        // Evaluar una expresión XPath para seleccionar elementos específicos
        var result = document.Evaluate("//*[@class='feliz']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iterar sobre los nodos resultantes.
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Salida: Hola
            // Salida: ¡Mundo!
        }
    }
}
```

Este ejemplo muestra el uso de consultas XPath para localizar elementos en el documento HTML en función de sus atributos y estructura.

## Selectores CSS

Los selectores CSS proporcionan una forma alternativa de seleccionar elementos en un documento HTML, similar a cómo las hojas de estilo CSS apuntan a los elementos.

```csharp
public static void CSSSelectorUsageExample()
{
    // Preparar un código HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Inicializar un documento basado en el código preparado.
    using (var document = new HTMLDocument(code, "."))
    {
        //Utilice un selector CSS para extraer elementos según la clase y la jerarquía
        var elements = document.QuerySelectorAll(".happy span");
        
        // Iterar sobre la lista de elementos resultante
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Salida: Hola
            // Salida: ¡Mundo!
        }
    }
}
```

Aquí, demostramos cómo usar selectores CSS para apuntar a elementos específicos en el documento HTML.

Con estos ejemplos, ha adquirido una comprensión básica de cómo navegar, filtrar, consultar y seleccionar elementos en documentos HTML utilizando Aspose.HTML para .NET.

## Conclusión

 Aspose.HTML para .NET es una biblioteca versátil que permite a los desarrolladores de .NET trabajar de manera eficiente con documentos HTML. Con sus potentes funciones de navegación, filtrado, consulta y selección de elementos, puede manejar diversas tareas de procesamiento HTML sin problemas. Siguiendo este tutorial y explorando la documentación en[Aspose.HTML para documentación .NET](https://reference.aspose.com/html/net/), puede desbloquear todo el potencial de esta herramienta para sus aplicaciones .NET.

## Preguntas frecuentes

### P1. ¿Aspose.HTML para .NET es de uso gratuito?

R1: Aspose.HTML para .NET ofrece una versión de prueba gratuita, pero para uso en producción, deberá adquirir una licencia. Puede encontrar detalles y opciones de licencia en[Aspose.HTML Compra](https://purchase.aspose.com/buy).

### P2. ¿Cómo puedo obtener una licencia temporal de Aspose.HTML para .NET?

 R2: Puede obtener una licencia temporal para fines de prueba en[Licencia temporal Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### P3. ¿Dónde puedo buscar ayuda o soporte para Aspose.HTML para .NET?

 R3: Si tiene algún problema o tiene preguntas, puede visitar el[Foro Aspose.HTML](https://forum.aspose.com/) para asistencia y apoyo comunitario.

### P4. ¿Existen recursos adicionales para aprender Aspose.HTML para .NET?

 R4: Junto con este tutorial, puede explorar más tutoriales y documentación sobre el[Página de documentación de Aspose.HTML para .NET](https://reference.aspose.com/html/net/).

### P5. ¿Aspose.HTML para .NET es compatible con las últimas versiones de .NET?

R5: Aspose.HTML para .NET se actualiza periódicamente para garantizar la compatibilidad con las últimas versiones y tecnologías de .NET.