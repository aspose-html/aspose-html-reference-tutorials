---
category: general
date: 2026-08-03
description: Convierte HTML a Markdown usando Python. Aprende cómo extraer enlaces
  de HTML y extraer párrafos de HTML en una única conversión eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: es
lastmod: 2026-08-03
og_description: Convertir HTML a Markdown en Python con un ejemplo conciso que muestra
  cómo extraer enlaces del HTML y extraer párrafos del HTML mientras se guarda el
  resultado como un archivo Markdown.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Convertir HTML a Markdown en Python – guía completa de extracción
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Convertir HTML a Markdown con Python – extraer enlaces y párrafos
url: /es/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML a Markdown con Python – extraer enlaces y párrafos

Si necesitas **convertir HTML a Markdown**, este tutorial te muestra una forma práctica de hacerlo en Python mientras extraes selectivamente **enlaces del HTML** y **párrafos del HTML**. Verás un ejemplo completo y ejecutable que guarda el contenido filtrado como un archivo Markdown limpio.

Convertir HTML a Markdown es un paso común cuando deseas documentación ligera, controlada por versiones, contenido para sitios estáticos o simplemente una representación en texto plano de una página web. Al final de esta guía tendrás un script que:

1. Carga un documento HTML desde el disco.  
2. Configura un conjunto de características que mantiene solo enlaces y elementos de párrafo.  
3. Realiza la conversión usando el GroupDocs Conversion SDK para Python.  
4. Escribe el resultado en un archivo `.md`.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

| Requisito | Por qué es importante |
|-----------|-----------------------|
| Python 3.9+ | El SDK está dirigido a versiones modernas de Python. |
| paquete `groupdocs-conversion` | Proporciona las clases `HTMLDocument`, `MarkdownSaveOptions` y `Converter` usadas en el ejemplo. |
| Un archivo HTML para probar (p. ej., `sample.html`) | La fuente que vas a convertir. |

Instala el SDK con pip:

```bash
pip install groupdocs-conversion
```

> **Consejo profesional:** Usa un entorno virtual (`python -m venv .venv`) para mantener las dependencias aisladas.

## Convertir HTML a Markdown con Python

El núcleo de la conversión se realiza en unos pocos pasos sencillos. Cada paso se explica a continuación, y el script completo aparece al final del artículo.

### Paso 1: Cargar el documento HTML que deseas convertir

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*¿Por qué este paso?*  
`HTMLDocument` analiza el archivo fuente y construye una representación DOM interna con la que el conversor puede trabajar. Sin cargar el documento primero, el SDK no tiene nada que procesar.

### Paso 2: Crear un conjunto de características que incluya solo los elementos que necesitas

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*¿Por qué añadimos estas características?*  
`MarkdownSaveOptions.Features` actúa como filtro. Al agregar `LINK` y `PARAGRAPH` le indicamos al conversor que **extraiga enlaces del HTML** y **extraiga párrafos del HTML**, ignorando imágenes, tablas, scripts y demás marcado que no necesites en el Markdown final.

### Paso 3: Adjuntar el conjunto de características a las opciones de guardado de Markdown

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*¿Por qué este paso?*  
`MarkdownSaveOptions` contiene todas las preferencias de conversión. Asignar el `selected_features` construido previamente garantiza que la conversión respete nuestra configuración de filtro.

### Paso 4: Ejecutar la conversión y guardar el resultado como archivo Markdown

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*¿Por qué llamamos a `convert_html`?*  
`Converter.convert_html` es el punto de entrada del SDK para transformaciones de HTML a Markdown. Lee el `HTMLDocument`, aplica `md_options` y escribe la salida filtrada en `output_path`.

#### Salida esperada

El archivo resultante `links_and_paragraphs.md` contendrá solo representaciones Markdown de hipervínculos y texto de párrafos, por ejemplo:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

Todos los demás elementos HTML como `<img>`, `<table>` o `<script>` se omiten, manteniendo el archivo ligero y fácil de editar.

## Extraer enlaces del HTML (profundización opcional)

Si tu objetivo es **solo extraer enlaces del HTML** descartando todo lo demás, puedes simplificar el conjunto de características:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Ejecutar la conversión con esta configuración produce un archivo Markdown donde cada enlace aparece en su propia línea, por ejemplo:

```markdown


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convertir HTML a Markdown en Aspose.HTML para Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convertir HTML a Markdown en .NET con Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Cómo convertir HTML a PDF en Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}