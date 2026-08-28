---
category: general
date: 2026-06-10
description: 'Cargar HTML en Python para extraer imágenes SVG de tus páginas: código
  paso a paso, consejos y manejo de casos límite.'
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: es
og_description: Carga HTML en Python y extrae imágenes SVG con un ejemplo claro y
  ejecutable. Aprende a buscar elementos SVG en HTML y a manejar casos límite.
og_title: Cargar HTML en Python – Extraer imágenes SVG de manera eficiente
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Cargar HTML en Python – Guía completa para extraer imágenes SVG
url: /es/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cargar HTML en Python – Guía completa para extraer imágenes SVG

¿Alguna vez necesitaste **cargar HTML en Python** solo para extraer cada gráfico SVG de una página? No eres el único. Ya sea que estés construyendo un web‑scraper, generando un informe de activos, o simplemente tengas curiosidad por los íconos que usa un sitio, saber cómo **extraer imágenes SVG** te ahorra mucho trabajo manual.

En este tutorial recorreremos una solución práctica, de extremo a extremo, que **carga HTML en Python**, luego **busca elementos HTML SVG**, **encuentra SVG en línea**, e incluso captura archivos SVG externos referenciados por etiquetas `<img>`. Al final tendrás un script reutilizable, varios consejos para los aspectos complicados y una visión clara de cómo se ve la salida.

## Qué obtendrás al finalizar

* Un script de Python completamente ejecutable que analiza un archivo HTML local (o una página obtenida) y enumera cada SVG que pueda encontrar.  
* Comprensión de la diferencia entre **inline SVG** (`<svg>…</svg>`) y **external SVG** (`<img src="… .svg">`).  
* Estrategias para manejar marcado malformado, archivos faltantes y peculiaridades de espacios de nombres.  
* Ideas para ampliar el código: guardar los SVG, convertirlos a PNG o insertarlos en una base de datos.

### Requisitos previos

* Python 3.8+ instalado.  
* Familiaridad básica con las librerías `requests` y `BeautifulSoup` de Python (las importaremos, no se necesita una inmersión profunda).  
* Un archivo HTML local o una URL que quieras escanear.  

Ahora, vamos a sumergirnos.

## Cargar HTML en Python – Configurando el analizador

El primer paso es **cargar HTML en Python**. Puedes leer un archivo del disco o obtener una página remota. A continuación se muestra un ayudante minimalista pero robusto que hace ambas cosas:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Por qué es importante:** Usar `BeautifulSoup` abstrae las peculiaridades del análisis de cadenas crudas, y la función maneja con elegancia tanto archivos locales como URLs remotas. También lanza una excepción si una solicitud de red falla, de modo que sabrás al instante cuándo algo salió mal.

## Extraer imágenes SVG – Encontrar elementos SVG en línea

Una vez que el documento está cargado, el siguiente paso lógico es **encontrar etiquetas SVG en línea**. El SVG en línea está incrustado directamente en el marcado HTML, lo que significa que puedes obtenerlo directamente del DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Consejo profesional:* Si la página usa espacios de nombres SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` aún encuentra la etiqueta porque ignora los espacios de nombres por defecto. Es una comodidad útil cuando solo estás **buscando HTML SVG**.

## Buscar HTML SVG – Manejo de referencias externas `<img>`

Muchos sitios no incrustan SVG directamente; hacen referencia a archivos externos mediante `<img src="icon.svg">`. Para capturarlos, necesitamos iterar sobre cada etiqueta `<img>`, comprobar su `src` y verificar si termina con `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Alerta de caso límite:** Algunas páginas usan cadenas de consulta (`icon.svg?v=2`) o fragmentos (`icon.svg#layer`). La comprobación `endswith(".svg")` sigue funcionando porque solo miramos la parte final en minúsculas de la cadena. Si necesitas una validación más estricta, considera usar `urllib.parse` para eliminar los parámetros primero.

## Encontrar SVG en línea – Informar los resultados

Ahora que tenemos dos listas —una para el marcado SVG en línea y otra para referencias a archivos externos— podemos combinarlas e informar el recuento total. Esto refleja el fragmento original que publicaste, pero agrega un poco más de contexto.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Juntándolo todo – Script completo

A continuación se muestra el programa completo, listo para ejecutarse. Guárdalo como `extract_svg.py` y apúntalo a un archivo HTML local o a una URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Salida esperada

Ejecutar el script contra un `sample.html` de ejemplo podría producir:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Si descomentas el bloque de descarga, el SVG externo

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [svg to png java – Convertir SVG a imagen con Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convertir SVG a imagen en .NET con Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Cómo convertir SVG a XPS con Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}