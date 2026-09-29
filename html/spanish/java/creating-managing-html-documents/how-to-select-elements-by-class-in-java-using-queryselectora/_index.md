---
category: general
date: 2026-09-29
description: Aprende a seleccionar elementos por clase, leer HTML desde un archivo
  y encontrar enlaces externos en Java. Esta guía paso a paso cubre la iteración eficiente
  de un NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: es
lastmod: 2026-09-29
og_description: Selecciona elementos por clase en Java, lee HTML desde un archivo
  y encuentra enlaces externos usando querySelectorAll. Sigue el ejemplo completo
  para iterar un NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Seleccionar elementos por clase en Java – guía completa con querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Cómo seleccionar elementos por clase en Java usando querySelectorAll
url: /es/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo seleccionar elementos por clase en Java usando querySelectorAll

Si necesitas **seleccionar elementos por clase** mientras procesas un archivo HTML en Java, esta guía te muestra exactamente cómo hacerlo. Aprenderás a leer HTML desde un archivo, usar `querySelectorAll` para encontrar enlaces externos y recorrer de forma segura el `NodeList` resultante.

Trabajar con HTML en Java a menudo se siente pesado, pero las bibliotecas modernas te ofrecen una API concisa basada en selectores CSS. El ejemplo a continuación usa **jsoup** (versión 1.17.2) porque implementa selectores al estilo `querySelectorAll` y devuelve una colección `Elements` que se comporta como un `NodeList`. Puedes adaptar la misma lógica a otras implementaciones DOM si lo necesitas.

## Prerequisites

Antes de comenzar, asegúrate de tener:

* JDK 17 o superior instalado.
* Maven o Gradle para la gestión de dependencias.
* Familiaridad básica con streams de Java y el modelo DOM.

Añade jsoup a tu proyecto:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Step 1: Read HTML from file

La primera tarea es cargar el documento HTML desde el disco. `Jsoup.parse(Path, Charset)` lee el archivo y construye un árbol DOM que puedes consultar.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Why this matters*: Cargar el archivo una sola vez evita I/O repetido mientras iteras sobre los elementos más adelante. El objeto `Document` mantiene todo el DOM, lo que permite consultas de selectores rápidas.

## Step 2: Use `querySelectorAll` to select elements by class

Ahora que el documento está en memoria, puedes **seleccionar elementos por clase** usando un selector CSS. El selector `"a.external"` coincide con etiquetas `<a>` que poseen la clase `external`, exactamente lo que necesitas para **encontrar enlaces externos**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Why this matters*: Usar un selector de clase es tanto expresivo como eficiente. La biblioteca traduce el selector a un recorrido optimizado, por lo que no necesitas escribir bucles manuales sobre cada nodo.

## Step 3: Iterate the NodeList (Elements) in Java

`Elements` implementa `Iterable<Element>`, lo que significa que puedes usar un bucle `for‑each` estándar para **iterar NodeList Java**. El bucle a continuación imprime el atributo `href` de cada enlace.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Why this matters*: La iteración directa mantiene el código legible y evita la sobrecarga de convertir la colección a un stream cuando solo necesitas una salida sencilla.

## Full working example

Unir los tres pasos produce un programa autocontenido que puedes ejecutar desde la línea de comandos.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Expected output

Suponiendo que `input.html` contiene:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Ejecutar el programa muestra:

```
External link: https://example.com
External link: https://openai.com
```

## Pro tips and common pitfalls

* **Encoding matters** – Siempre lee el archivo con UTF‑8 (o el charset que coincida con tu fuente). Un encoding incorrecto puede corromper caracteres en los valores de los atributos.
* **Multiple classes** – Si un elemento tiene varias clases (p. ej., `class="btn external"`), el selector `"a.external"` sigue coincidiendo porque los selectores de clase CSS verifican la presencia del token, no la cadena exacta.
* **Performance tip** – Si solo necesitas el atributo `href`, puedes solicitarlo directamente con `doc.select("a.external[href]").eachAttr("href")`. Esto evita crear objetos `Element` completos para cada coincidencia.
* **Null safety** – `link.attr("href")` devuelve una cadena vacía si el atributo falta, por lo que no necesitas una verificación de null antes de imprimir.

## Frequently asked questions

**Q: Does this work with HTML fragments that lack a `<html>` root?**  
A: Yes. `Jsoup.parse` trata la entrada como un fragmento y agrega automáticamente los elementos raíz que faltan, permitiendo que los selectores funcionen sobre el cuerpo del fragmento.

**Q: Can I use `querySelectorAll` without jsoup?**  
A: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`. Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods. The pattern shown here—load, select with CSS, iterate—remains the same.

**Q: What if I need to modify the links instead of just printing them?**  
A: After obtaining each `Element`, you can call `link.attr("href", "newUrl")` and then write the document back to disk with `Files.writeString`.

## Conclusion

Ahora sabes cómo **seleccionar elementos por clase**, **leer HTML desde un archivo**, **encontrar enlaces externos** y **iterar un NodeList en Java** usando selectores al estilo `querySelectorAll`. El ejemplo completo muestra un flujo de trabajo limpio y listo para producción que puedes integrar en pipelines de scraping o transformación más grandes.

A continuación, explora temas relacionados como **parsear contenido dinámico con HTMLUnit**, **escribir HTML modificado de vuelta al disco**, o **usar streams de Java para recopilar URLs de enlaces en una lista**. Cada uno de estos se basa en la técnica central de selección basada en clases demostrada aquí. ¡Feliz codificación!


## What Should You Learn Next?


Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}