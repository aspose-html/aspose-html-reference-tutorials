---
category: general
date: 2026-05-31
description: Aprende cómo extraer SVG de HTML usando Python. Este tutorial paso a
  paso muestra cómo leer un documento HTML, guardar archivos SVG y guardar SVG en
  línea de manera eficiente.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: es
og_description: Cómo extraer SVG de HTML usando Python. Sigue este tutorial para leer
  documentos HTML, guardar archivos SVG y manejar SVG en línea sin esfuerzo.
og_title: Cómo extraer SVG de HTML con Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Cómo extraer SVG de HTML con Python – Guía completa
url: /es/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer SVG de HTML con Python – Guía completa

¿Alguna vez te has preguntado **cómo extraer SVG** de una página HTML desordenada sin volverte loco? No estás solo. Ya sea que estés construyendo un web‑scraper, una canalización de diseño, o simplemente necesites exportar íconos en lote, saber **cómo extraer SVG** es un truco útil que ahorra tiempo y dolores de cabeza.

En este tutorial te mostraremos exactamente **cómo extraer SVG** usando la biblioteca Aspose.HTML para Python. Leeremos el documento HTML, extraeremos tanto el marcado `<svg>` en línea **y** las referencias SVG externas, y luego **guardaremos archivos SVG** en disco—todo en un script ordenado y reutilizable. Al final tendrás una solución lista‑para‑ejecutar que podrás adaptar a tus propios proyectos.

> **Consejo profesional:** Si solo necesitas una inspección rápida de la página, `BeautifulSoup` también funciona, pero Aspose.HTML te brinda un DOM completo, lo que hace que la extracción de SVG en línea y vinculados sea pan comido.

## Lo que necesitarás

* Python 3.8+ (el código usa f‑strings, así que 3.6+ es el mínimo absoluto)
* `pip install aspose-html` – la biblioteca comercial que impulsa nuestro análisis HTML
* Una carpeta con un archivo `input.html` que contiene los SVG que deseas extraer
* Permiso de escritura en el directorio de salida (lo llamaremos `YOUR_DIRECTORY`)

Eso es todo—sin binarios extra, sin navegadores sin cabeza. Simple, ¿verdad?

## Paso 1: Leer documento HTML con Aspose.HTML

Lo primero que debes hacer es **leer el documento HTML** para poder recorrer su árbol DOM. Aspose.HTML te proporciona un objeto `HTMLDocument` que se comporta como el `document` de un navegador.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Por qué es importante:* Al cargar el HTML en un DOM adecuado, evitas las trampas del análisis basado en expresiones regulares y obtienes métodos como `get_elements_by_tag_name` y `query_selector_all` de forma gratuita.

## Paso 2: Recolectar todos los elementos <svg> en línea

Los SVG en línea son esos bloques `<svg>…</svg>` que están dentro del HTML. Para **guardar SVG en línea** solo necesitamos su HTML externo.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Observa que estamos añadiendo el marcado crudo directamente a `svg_contents`. Más adelante decidiremos si cada entrada es un marcado o una ruta de archivo.

## Paso 3: Encontrar referencias SVG externas (etiquetas img y object)

Muchas páginas enlazan a archivos SVG externos mediante `<img src="icon.svg">` o `<object data="logo.svg">`. Para **extraer SVG de HTML** también necesitamos capturar esas URLs.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Alerta de caso límite:* Si la URL del SVG es relativa, deberás combinarla con la ruta base del archivo HTML. Por brevedad asumimos que el HTML está junto a los archivos SVG.

## Paso 4: Escribir cada SVG en un archivo separado

Ahora que tenemos una lista mixta de cadenas de marcado y rutas de archivo, iteraremos y **guardaremos archivos SVG**. El script distingue automáticamente entre marcado en línea y una referencia a un archivo existente.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Lo que verás:** Después de que el script termine, `YOUR_DIRECTORY` contendrá archivos llamados `svg_0.svg`, `svg_1.svg`, … cada uno con el marcado en línea original o una copia del SVG externo.

### Salida esperada

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Si falta un archivo referenciado, el script muestra una advertencia pero continúa—de modo que un enlace roto no detendrá toda la extracción.

## Manejo de problemas comunes

| Problema | Por qué ocurre | Solución rápida |
|----------|----------------|-----------------|
| **Las URLs relativas se rompen** | El atributo `src` puede ser `"../assets/icon.svg"` | Usa `os.path.join(os.path.dirname(html_path), src)` para resolver. |
| **Nombres de archivo duplicados** | Dos SVG con el mismo nombre se sobrescriben | Incluye un hash del contenido en el nombre del archivo (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Los SVG en línea grandes causan picos de memoria** | Almacenar todo el marcado en una lista antes de escribir | Transmite cada elemento directamente a un archivo en lugar de usar un búfer. |
| **Imágenes no SVG se cuelan** | Algunas etiquetas `<img>` terminan con `.svg?version=1` | Elimina las cadenas de consulta antes de comprobar la extensión (`src.split('?')[0]`). |

## Script completo que puedes copiar y pegar

A continuación se muestra el programa completo, listo para ejecutar. Guárdalo como `extract_svg.py`, ajusta `YOUR_DIRECTORY` y ejecuta `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Recapitulación – Cómo extraer SVG en pocas palabras

* **Leer documento HTML** con `HTMLDocument`.
* **Recolectar `<svg>` en línea** mediante `get_elements_by_tag_name`.
* **Ubicar SVG externos** usando un selector CSS que termina en `.svg`.
* **Guardar cada pieza**—escribir el marcado directamente a un archivo o copiar el archivo referenciado.
* **Manejar casos límite** como rutas relativas, duplicados y archivos faltantes.

Esa es la respuesta completa a **cómo extraer SVG** de una página HTML, envuelta en un único script fácil de modificar.

## ¿Qué sigue?

Ahora que puedes **extraer SVG** de forma fiable, considera estas ideas de seguimiento:

* **Procesamiento por lotes:** Recorrer un directorio de archivos HTML para crear una biblioteca de íconos.
* **Optimización:** Ejecutar cada SVG guardado a través de SVGO (un optimizador Node.js) para reducir el tamaño del archivo.
* **Conversión:** Usar `cairosvg` o `svglib` para convertir los SVG en PNGs para navegadores heredados.
* **Extracción de metadatos:** Analizar etiquetas `<title>` o `<desc>` dentro de cada SVG para obtener etiquetas buscables.

Cada uno de esos temas toca nuestras palabras clave secundarias—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—por lo que encontrarás mucho material para explorar.

---

*¡Feliz hacking! Si encuentras algún problema, deja un comentario abajo o envíame un mensaje en GitHub. El mundo del SVG es amplio, pero con las herramientas adecuadas, extraerlos es pan comido.*

## ¿Qué deberías aprender a continuación?

- [Guardar documento SVG en Aspose.HTML para Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Cómo convertir SVG a XPS con Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Renderizar un documento SVG en formato PNG en .NET con Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}