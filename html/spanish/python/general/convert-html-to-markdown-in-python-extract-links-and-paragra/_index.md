---
category: general
date: 2026-09-26
description: Convertir HTML a Markdown con Python, extrayendo enlaces del HTML y guardando
  HTML como Markdown. Aprende cómo convertir HTML paso a paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: es
lastmod: 2026-09-26
og_description: Convierte HTML a Markdown con Python, extrayendo enlaces del HTML
  y guardando HTML como Markdown. Sigue esta guía completa.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Convertir HTML a Markdown en Python – extraer enlaces y párrafos
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Convertir HTML a Markdown en Python – extrae enlaces y párrafos fácilmente
url: /es/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to Markdown in Python – extract links and paragraphs easily

Si necesitas **convertir HTML a Markdown** conservando solo las partes útiles, esta guía te muestra cómo hacerlo con solo unas pocas líneas de Python. Ya sea que estés extrayendo publicaciones de blogs, archivando documentación o limpiando cuerpos de correos electrónicos, aprenderás una forma fiable de extraer enlaces de HTML y guardar HTML como Markdown.

El tutorial cubre todo, desde la instalación del paquete necesario hasta el manejo de casos límite como etiquetas `<a>` vacías o párrafos anidados. Al final tendrás un script listo‑para‑ejecutar que **convierte HTML a Markdown**, extrae enlaces de HTML y, incluso, extrae párrafos de HTML cuando los necesites.

---

## Prerequisites

Antes de comenzar, asegúrate de tener:

* Python 3.8 o superior instalado  
* Acceso al paquete Python `groupdocs-conversion` (la biblioteca que proporciona `HTMLDocument`, `MarkdownSaveOptions` y `Converter`)  
* Un archivo HTML local que quieras procesar (por ejemplo, `article.html`)

Puedes instalar la biblioteca con pip:

```bash
pip install groupdocs-conversion
```

> **Consejo:** Usa un entorno virtual (`python -m venv venv`) para mantener las dependencias aisladas.

---

## Step 1: Load the source HTML document

La primera operación es crear un objeto `HTMLDocument` que apunte a tu archivo fuente. Este objeto abstrae el HTML bruto y le da al convertidor un punto de entrada limpio.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Por qué es importante:* Cargar el documento de esta manera permite que la biblioteca analice el DOM una sola vez, de modo que las operaciones posteriores (como extraer enlaces o párrafos) sean rápidas y eficientes en memoria.

---

## Step 2: Create Markdown save options and select the features you need

`MarkdownSaveOptions` te permite decidir qué elementos HTML sobreviven a la conversión. La bandera `features` usa un OR a nivel de bits para combinar opciones.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Por qué es importante:* Al especificar `LINKS` y `PARAGRAPHS` **extraes enlaces de HTML** y **extraes párrafos de HTML** mientras descartas todo lo demás (estilos, scripts, imágenes). Si más tarde solo necesitas enlaces, reemplaza `MarkdownFeatures.PARAGRAPHS` por `0` (o elimínalo).

---

## Step 3: Convert the HTML to Markdown using the configured options

Ahora llama al método estático `convert_html`, pasando el documento fuente, la ruta de destino y las opciones que acabas de crear.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Por qué es importante:* La conversión se ejecuta en una sola pasada, aplicando el filtro de características que definiste. El archivo resultante (`article_links.md`) contiene solo enlaces y párrafos formateados en Markdown, que es exactamente lo que necesitas cuando deseas **guardar HTML como Markdown** para procesamiento posterior.

---

## Full script – everything together

A continuación tienes un script completo y ejecutable que puedes copiar‑pegar en un archivo llamado `html_to_md.py`. Ajusta las rutas para que coincidan con tu entorno.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Expected output

Ejecutar el script genera un archivo similar al siguiente (el contenido exacto depende del HTML de origen):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Solo aparecen el texto del enlace y el texto del párrafo; todos los demás elementos HTML se eliminan.

---

## Extract only links or only paragraphs (advanced variations)

A veces necesitas **cómo convertir HTML** en un archivo Markdown que contenga solo un tipo de elemento.

### 1. Extract only links

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extract only paragraphs

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Ambas variaciones reutilizan la misma llamada `convert_html`, por lo que no tienes que escribir lógica de conversión separada.

---

## Handling edge cases

| Situation                               | Recommended fix |
|----------------------------------------|-----------------|
| HTML file contains empty `<a>` tags    | The converter automatically skips empty links. If you see stray `[]()` entries, set `md_options.removeEmptyLinks = True`. |
| Nested paragraphs (`<p>` inside `<div>`) | The library flattens nested paragraphs, preserving the text order. No extra code needed. |
| Non‑ASCII characters in link titles    | Ensure your Python file is saved with UTF‑8 encoding and open the output file with `encoding="utf-8"` if you read it later. |
| Very large HTML files (≥ 50 MB)        | Process the file in chunks using `HTMLDocument(stream=io.BytesIO(...))` to avoid loading the entire file into memory. |

---

## Frequently asked questions

**P: ¿Esto funciona con fragmentos HTML (sin etiqueta `<html>` raíz)?**  
R: Sí. `HTMLDocument` acepta cualquier fragmento bien formado; el convertidor trata el fragmento como el cuerpo del documento.

**P: ¿Puedo mantener las imágenes con la sintaxis de imagen Markdown?**  
R: Añade `MarkdownFeatures.IMAGES` a la bandera `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**P: ¿Cómo convierto muchos archivos en un directorio?**  
R: Envuelve `convert_html_to_markdown` en un bucle que recorra el directorio con `os.listdir` o `pathlib.Path.rglob("*.html")`.

---

## Conclusion

Ahora sabes cómo **convertir HTML a Markdown** en Python mientras extraes selectivamente **enlaces de HTML** y **párrafos de HTML**. El script muestra el enfoque estándar: cargar el documento, configurar `MarkdownSaveOptions` y ejecutar `Converter.convert_html`. Con unos pocos ajustes también puedes **guardar HTML como Markdown** que contenga solo enlaces, solo párrafos o una representación fiel completa.

A continuación, podrías explorar:

* Añadir `MarkdownFeatures.HEADINGS` para preservar los títulos de sección.  
* Usar el Markdown resultante como entrada para generadores de sitios estáticos como MkDocs o Hugo.  
* Automatizar conversiones masivas para todo un repositorio de documentación.

¡Feliz conversión!

## What Should You Learn Next?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}