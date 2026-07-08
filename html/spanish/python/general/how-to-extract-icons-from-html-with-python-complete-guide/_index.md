---
category: general
date: 2026-07-02
description: Cómo extraer íconos de un archivo HTML usando Python. Aprende a leer
  archivos HTML con Python, analizar el documento HTML y extraer el atributo href
  para obtener las URLs de los favicons.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: es
og_description: Cómo extraer íconos de una página HTML usando Python. Este tutorial
  te muestra cómo leer un archivo HTML con Python, analizar el documento y extraer
  las URLs de los favicons.
og_title: Cómo extraer íconos de HTML – Guía de Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Cómo extraer íconos de HTML con Python – Guía completa
url: /es/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer íconos de HTML con Python – Guía completa

¿Alguna vez te has preguntado **cómo extraer íconos** de una página web sin abrir un navegador? Tal vez estés creando un catálogo de sitios, una herramienta de auditoría SEO, o simplemente tengas curiosidad por esos pequeños favicons que aparecen en las pestañas. La buena noticia es que puedes hacerlo en unas pocas líneas de Python—sin Selenium, sin Chrome sin cabeza, solo con un archivo HTML de texto plano.

En este tutorial recorreremos la lectura de un archivo HTML con Python, el análisis del documento HTML y, finalmente, **extraer el atributo href** de las etiquetas `<link rel="icon">` para obtener esas URLs de favicon. Al final tendrás un fragmento reutilizable que funciona con cualquier HTML estático que le pases, y también verás cómo manejar casos especiales como rutas relativas o múltiples declaraciones de íconos.

## Lo que aprenderás

- Cargar un archivo HTML local con Python (read html file python)  
- Usar un analizador ligero para **parse html document** de forma segura  
- Ubicar los elementos `<link>` que declaran un ícono  
- **Extract href attribute** y convertirlos en URLs absolutas  
- Recopilar e imprimir todas las **favicon URLs** descubiertas  

Sin servicios externos—solo la biblioteca estándar y el popular paquete **BeautifulSoup**.

---

![Captura de pantalla que muestra un script Python extrayendo íconos – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Texto alternativo de la imagen: "how to extract icons using a Python script"*

## Requisitos previos

- Python 3.8+ instalado  
- Biblioteca `beautifulsoup4` (`pip install beautifulsoup4`)  
- Un archivo HTML local que quieras escanear (p. ej., `sample.html`)  

Si ya tienes todo eso, vamos al grano.

## Paso 1: Leer archivo HTML con Python – Cargar el documento

Lo primero: necesitamos abrir el archivo y pasar su contenido a un analizador. Usar `with open(..., "r", encoding="utf‑8")` garantiza que el archivo se cierre automáticamente, y la codificación UTF‑8 maneja la mayoría de las páginas modernas.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Por qué es importante:** Abrir el archivo con la codificación correcta evita caracteres misteriosos `�` que podrían romper el analizador más adelante. Usar `Path` de la biblioteca estándar también hace que el código sea multiplataforma.

## Paso 2: Analizar documento HTML – Encontrar todos los enlaces de íconos

Ahora le entregamos el HTML crudo a **BeautifulSoup**, que construye un árbol navegable. Buscaremos cada etiqueta `<link>` cuyo atributo `rel` contenga la palabra `icon`. Ten en cuenta que `rel` puede ser una lista separada por espacios (`rel="shortcut icon"`), por lo que necesitamos una comprobación flexible.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Por qué este paso es crucial:** Un `soup.find_all("link", rel="icon")` ingenuo perdería variaciones como `rel="shortcut icon"` o `rel="apple-touch-icon"`. Nuestro ayudante `is_icon_link` cubre esos casos, haciendo la extracción robusta.

## Paso 3: Extraer atributo href – Obtener las URLs

Con las etiquetas relevantes recopiladas, ahora extraemos el atributo `href` de cada una. Algunas páginas pueden omitir `href` (raro, pero posible), así que nos protegemos contra `None`. Además, los favicons a menudo se especifican con URLs relativas, por lo que las resolveremos contra la URL base de la página si la conoces. Para un archivo local simplemente mantendremos la ruta tal cual.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Por qué eliminamos espacios en blanco:** Los autores de HTML a veces añaden accidentalmente espacios alrededor de las URLs, lo que rompería una solicitud posterior. Recortar garantiza que obtengamos cadenas limpias.

## Paso 4: Extraer URLs de favicon – Mostrar los resultados

Finalmente, imprimimos (o devolvemos) la lista de URLs descubiertas. En un script del mundo real podrías escribirlas en un CSV, descargar los íconos o enviarlas a otro servicio. Aquí tienes un bucle sencillo que muestra el resultado en la consola.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Manejo de casos especiales

- **Múltiples valores en rel:** Nuestra comprobación `is_icon_link` ya captura `rel="shortcut icon"` y `rel="apple-touch-icon"`.  
- **Rutas relativas:** Si más adelante necesitas URLs absolutas, usa `urllib.parse.urljoin(base_url, href)`.  
- **Falta href:** La condición `if href:` omite etiquetas mal formadas, evitando errores `NoneType`.  
- **Entradas duplicadas:** Puedes usar `icon_urls = list(dict.fromkeys(icon_urls))` para eliminar duplicados.

---

## Script completo – Solución todo en uno

Juntándolo todo, aquí tienes el programa completo, listo para ejecutar. Guárdalo como `extract_icons.py` y apunta `html_path` a cualquier archivo que desees.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Salida esperada** (suponiendo que `sample.html` contiene dos íconos):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Ejecuta `python extract_icons.py` y verás las URLs impresas en la consola.

---

## Preguntas frecuentes

**P: ¿Qué pasa si el HTML usa etiquetas `<meta>` para los íconos?**  
R: Algunos sitios incrustan íconos mediante `<meta itemprop="image">`. Amplía `is_icon_link` para también comprobar `meta` con `itemprop="image"` y extraer su atributo `content`.

**P: ¿Puedo descargar los íconos automáticamente?**  
R: Sí—simplemente pasa cada URL a `requests.get(url, stream=True)` y escribe el contenido en un archivo. Recuerda manejar las URLs relativas con `urljoin`.

**P: ¿Esto funciona con páginas remotas?**  
R: Claro. Sustituye el paso de lectura de archivo por `requests.get(page_url).text` y pasa la cadena HTML a BeautifulSoup. Solo ten en cuenta robots.txt y los límites de velocidad.

---

## Conclusión

Hemos cubierto **cómo extraer íconos** de cualquier HTML estático usando Python, desde la lectura del archivo hasta la impresión de cada URL de favicon. Las ideas clave—leer el archivo, analizar el documento, localizar las etiquetas correctas y extraer el atributo `href`—son patrones reutilizables que encontrarás en muchas tareas de web‑scraping.

¿Próximos pasos? Prueba a ampliar el script para:

- Resolver URLs relativas contra la URL base de la página  
- Descargar cada ícono y guardarlo localmente  
- Soportar formatos de ícono adicionales (`rel="mask-icon"` para Safari)  

¡Experimenta, y si encuentras algún detalle curioso, deja un comentario abajo! ¡Feliz análisis!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}