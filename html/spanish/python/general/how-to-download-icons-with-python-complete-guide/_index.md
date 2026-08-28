---
category: general
date: 2026-05-31
description: Aprende cómo descargar íconos usando Python. También cubriremos cómo
  extraer favicons, leer documentos HTML con Python y escribir archivos binarios en
  Python en un solo tutorial.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: es
og_description: Cómo descargar íconos usando Python explicado paso a paso. Aprende
  a extraer favicon, leer documentos HTML con Python y escribir archivos binarios
  en Python.
og_title: Cómo descargar íconos con Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Cómo descargar iconos con Python – Guía completa
url: /es/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo descargar íconos con Python – Guía completa

¿Alguna vez te has preguntado **cómo descargar íconos** de un sitio web sin tener que hacer clic derecho en cada uno? No eres el único. Ya sea que estés construyendo una herramienta de auditoría de marcas o simplemente quieras una copia local de cada favicon que encuentres, dominar esta tarea te ahorra tiempo y pulsaciones.

En este tutorial recorreremos **cómo descargar íconos** de un archivo HTML usando Python puro. También te mostraremos **cómo extraer favicon**, demostraremos **read html document python**, y explicaremos **write binary file python** para que termines con una carpeta ordenada de archivos .ico lista para cualquier proyecto.

---

## Lo que necesitarás

- Python 3.8+ (la biblioteca estándar es suficiente)
- Una copia local de la página HTML que deseas escanear (o una URL que puedas obtener)
- Familiaridad básica con la E/S de archivos en Python  
- No se requieren paquetes externos, pero `beautifulsoup4` puede facilitar las cosas si lo prefieres (opcional)

¿Los tienes? Genial—¡vamos a sumergirnos!

![Ejemplo de cómo descargar íconos](https://example.com/placeholder.png "ejemplo de cómo descargar íconos")

---

## Paso 1: Cargar el documento HTML en Python  

Lo primero, necesitamos **load html python** estilo—leer el archivo en memoria para poder inspeccionar sus etiquetas `<link>`. La forma más sencilla es abrir el archivo con la función incorporada `open` y leerlo como texto.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*¿Por qué este paso?*  
Leer el HTML nos brinda una cadena cruda que podemos analizar. Si omites esto y tratas de trabajar directamente con una ruta, el analizador no tendrá nada que examinar.

---

## Paso 2: Analizar el documento y encontrar enlaces de íconos  

Ahora necesitamos **read html document python** estilo. Aunque podrías usar expresiones regulares, un pequeño analizador HTML mantiene las cosas fiables. Python incluye `html.parser` que podemos subclasificar para nuestro propósito.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Explicación**  

- `handle_starttag` se dispara para cada etiqueta de apertura.  
- Filtramos los elementos `<link>` cuyo atributo `rel` contiene la palabra *icon*. Esto cubre tanto `rel="icon"` como el más antiguo `rel="shortcut icon"`.  
- Los valores `href` se almacenan en `icon_hrefs`, listos para el siguiente paso.

---

## Paso 3: Resolver rutas relativas (Opcional pero útil)

Si el HTML usa URLs relativas, debemos convertirlas en rutas absolutas del sistema de archivos. Aquí es donde el conocimiento de **load html python** se encuentra con `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*¿Por qué molestarse?*  
Cuando más tarde **write binary file python**, necesitas una ruta de archivo real. URLs relativas como `images/favicon.ico` de otro modo causarían un `FileNotFoundError`.

---

## Paso 4: Escribir cada ícono en un archivo binario local  

Este es el corazón de **how to download icons**. Iteraremos sobre las rutas resueltas, leeremos cada ícono como datos binarios y lo escribiremos en un nuevo archivo dentro de una carpeta dedicada `icons/`.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**¿Qué está pasando?**  

- `os.makedirs(..., exist_ok=True)` asegura que la carpeta de salida exista.  
- `shutil.copyfileobj` transmite los bytes del origen al destino, que es la forma más eficiente en memoria de **write binary file python**.  
- Nombramos cada archivo `icon_<index>.ico` para evitar colisiones.

**Salida esperada**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

Después de que el script termine, tendrás una colección limpia de archivos de íconos listos para cualquier tarea posterior.

---

## Paso 5: Bonus – Descargar íconos directamente desde una URL remota  

Si tu HTML está en la web en lugar de en el disco local, reemplaza la parte de lectura de archivos con una pequeña llamada `requests`. Esto demuestra **how to extract favicon** de cualquier página en vivo.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**¿Por qué añadir esto?**  
Muchos proyectos del mundo real necesitan extraer favicons de sitios en vivo. Este fragmento muestra que puedes extender la misma lógica de **how to download icons** a internet con solo un par de líneas adicionales.

---

## Errores comunes y consejos profesionales

- **Falta `rel="icon"`** – Algunos sitios incrustan íconos mediante etiquetas `<meta>` o CSS. Si los necesitas, amplía el analizador para buscar `<meta name="msapplication‑TileImage">` o URLs de `background-image` en CSS.  
- **Formatos que no son ICO** – Los favicons modernos a menudo usan `.png` o `.svg`. El código anterior funciona para cualquier imagen binaria; solo ajusta la extensión del archivo en `dest_path` si te importa preservar el formato original.  
- **Errores de permiso** – Al escribir archivos, asegúrate de que tu script se ejecute con permiso de escritura en la carpeta de destino. Usar `os.makedirs(..., exist_ok=True)` evita fallos de “directorio no encontrado”.  
- **Archivos HTML grandes** – Para páginas masivas, considera transmitir el archivo línea por línea en lugar de cargar toda la cadena en memoria. El `HTMLParser` incorporado puede manejar flujos incrementales.  

---

## Conclusión

Acabas de aprender **how to download icons** de un documento HTML usando Python puro. Al **reading html document python**, analizar las etiquetas `<link rel="icon">`, resolver cualquier ruta relativa y finalmente **write binary file python** para almacenar cada ícono localmente, ahora tienes un script reutilizable que funciona tanto para páginas locales como remotas.

¿Próximos pasos? Intenta ampliar el analizador para capturar íconos Apple touch (`rel="apple-touch-icon"`), o integra el script en una canalización de rastreo web más grande que recopile favicons para cientos de dominios. Los fundamentos cubiertos aquí—análisis HTML, resolución de rutas y manejo de archivos binarios—son bloques de construcción para muchas tareas de automatización web.

¿Tienes preguntas o quieres compartir un caso de uso interesante? Deja un comentario abajo, ¡y feliz caza de íconos!

## ¿Qué deberías aprender a continuación?

- [Cómo editar el árbol de documentos HTML en Aspose.HTML para Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Cómo convertir HTML a PDF Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Cómo convertir HTML a JPEG usando Aspose.HTML para Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}