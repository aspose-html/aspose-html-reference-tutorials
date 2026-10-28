---
category: general
date: 2026-10-28
description: Aprende cómo abrir enlaces en una nueva pestaña analizando HTML en Java,
  encontrando enlaces externos y añadiendo target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: es
lastmod: 2026-10-28
og_description: 'Abrir enlaces en una nueva pestaña usando Java: analizar HTML, encontrar
  enlaces externos, agregar target="_blank" y guardar el HTML modificado.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Abrir enlaces en una nueva pestaña con Java – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Cómo abrir enlaces en una nueva pestaña con Java
url: /es/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo abrir enlaces en una nueva pestaña con Java

Si necesitas **abrir enlaces en una nueva pestaña** desde un archivo HTML estático, esta guía te muestra exactamente cómo hacerlo. Aprenderás a **parsear HTML en Java**, **encontrar enlaces externos**, **añadir target blank** y **guardar HTML modificado** sin salir de tu IDE.

Abrir enlaces externos en una nueva pestaña del navegador mejora la experiencia del usuario y mantiene a los visitantes en la página original. La solución a continuación funciona con cualquier documento HTML, solo requiere la popular biblioteca jsoup y se ejecuta en Java 8 o superior.

## Prerequisites

Antes de comenzar, asegúrate de tener:

* JDK 8 + instalado  
* Una herramienta de construcción (Maven o Gradle) para obtener la dependencia **jsoup**  
* Un archivo HTML que contenga etiquetas de anclaje con la clase `external`

No necesitas un servidor web ni frameworks adicionales—jsoup maneja todo localmente.

## Step 1: Set up jsoup in your project

Añade jsoup como dependencia. Si usas Maven, coloca esto en `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Para Gradle, agrega la siguiente línea a `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Estas coordenadas descargan la última versión estable (a partir de octubre 2026). Después de sincronizar, podrás importar las clases de `org.jsoup` en tus archivos fuente Java.

## Step 2: Parse the HTML document

Parsear el archivo es el primer paso para **open links new tab**. El método `Jsoup.parse` lee el archivo en una estructura mutable similar a un DOM.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Why this matters*: `Document` te brinda selectores al estilo CSS, lo que hace trivial localizar los elementos que necesitas.

## Step 3: Find external links

Ahora localiza cada elemento `<a>` que tenga la clase `external`. Esto cumple con el requisito de **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` es una colección de nodos coincidentes. Si el selector devuelve un conjunto vacío, tu HTML carece de la clase o usa una convención de nombres diferente—ajusta el selector según corresponda.

## Step 4: Add `target="_blank"` to each link

Para cada nodo devuelto por **find external links**, establece el atributo `target` a `_blank`. Esto satisface el paso **add target blank** y asegura que los navegadores abran el enlace en una nueva pestaña.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

El método `attr` sobrescribe cualquier valor existente de `target`, garantizando un comportamiento consistente en todos los anclajes externos.

## Step 5: Save the modified HTML

Después de actualizar el DOM, escribe los cambios de vuelta a un archivo. Esto completa la parte de **save modified html** del tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializa todo el documento, preservando la indentación y el formato tal como jsoup lo analizó originalmente.

## Full working example

Unir todos los pasos genera un programa autocontenido que puedes copiar, pegar y ejecutar.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Expected output

Supongamos que `sample.html` contiene:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Después de ejecutar el programa, `updated.html` contendrá:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Solo el enlace externo recibió el atributo `target="_blank"`, lo que significa que los navegadores ahora lo abrirán en una nueva pestaña.

## Pro tips and common pitfalls

* **Pro tip:** Si necesitas tratar como externos los enlaces que comienzan con `http://` o `https://` aun sin una clase CSS, amplía el selector: `doc.select("a[href^=http]")`.
* **Edge case:** Algunas páginas ya especifican `target="_self"`; la llamada a `attr` lo sobrescribe, asegurando un comportamiento consistente.
* **Performance:** Para archivos HTML muy grandes, considera el parseo en streaming (`Jsoup.parse(File, String, String, Parser.htmlParser())`) para reducir el uso de memoria.
* **Testing:** Verifica el resultado abriendo `updated.html` en un navegador y examinando el enlace con las herramientas de desarrollo—busca el atributo `target`.

## Conclusion

Ahora tienes una solución completa y ejecutable para **open links in a new tab** usando Java. El tutorial cubrió cómo **parse html in java**, **find external links**, **add target blank** y **save modified html**, todo con la liviana biblioteca jsoup. 

A partir de aquí puedes:

* Extender el selector para manejar otros patrones de enlaces (p. ej., `rel="external"`).  
* Combinar esta lógica con un paso de compilación que procese todos los archivos HTML de un proyecto.  
* Integrar el código en una canalización de gestión de contenido más grande.

¡Siéntete libre de experimentar con diferentes selectores o formatos de salida, y comparte tus resultados con la comunidad!

## What Should You Learn Next?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}