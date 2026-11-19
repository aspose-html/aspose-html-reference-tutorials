---
category: general
date: 2026-06-26
description: Aprende cómo obtener el favicon cargando HTML desde una URL y extrayendo
  el href de las etiquetas <link>. Código Python paso a paso para obtener los íconos
  de sitios web rápidamente.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: es
og_description: 'Cómo obtener el favicon rápidamente: cargar HTML desde la URL, buscar link rel=''icon''
  y extraer href de las etiquetas link usando Python.'
og_title: Cómo obtener el favicon – Tutorial de Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Cómo obtener el favicon – Guía completa de Python para extraer íconos de sitios
url: /es/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo obtener el favicon – Guía completa en Python para extraer íconos de sitios

¿Alguna vez te has preguntado **how to get favicon** de cualquier sitio web sin tener que rebuscar manualmente en el código fuente? No eres el único: desarrolladores, profesionales de SEO e incluso diseñadores suelen necesitar ese pequeño ícono que representa a un sitio. En este tutorial te mostraremos una forma limpia, centrada en Python, para cargar HTML desde una URL, localizar las etiquetas `<link rel="icon">` y extraer las URLs de los íconos. Al final, sabrás exactamente **how to get favicon** para cualquier dominio y tendrás un script reutilizable listo para tus proyectos.

Cubrirémos todo, desde la obtención del HTML hasta el manejo de casos especiales como URLs relativas y múltiples formatos de íconos. No se requieren servicios externos, solo la biblioteca estándar `requests` y un parser HTML ligero. ¿Listo para comenzar? Vamos allá.

## Prerrequisitos

- Python 3.8+ instalado (el código también funciona en 3.10)  
- Familiaridad básica con `requests` y comprensiones de listas  
- Acceso a Internet para el sitio objetivo  

Si ya cuentas con esto, perfecto—pasa al primer paso. De lo contrario, instala la única dependencia que necesitamos:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` es un parser probado en batalla que hace que “load html from url” sea pan comido.

## Paso 1: Cargar HTML desde una URL con Python  

Lo primero que debes hacer al aprender **how to get favicon** es obtener el código fuente de la página. Esta es la parte de “load html from url” del proceso.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

¿Por qué usar `requests`? Maneja redirecciones, verificación HTTPS y tiempos de espera automáticamente, lo que significa menos sorpresas cuando más adelante intentes **get website icons**.

## Paso 2: Analizar el documento y encontrar enlaces de íconos  

Ahora que tenemos el HTML, necesitamos localizar todos los elementos `<link>` cuyo atributo `rel` indique un ícono. Este es el corazón de **how to get favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Observa que verificamos tanto `icon` como `shortcut icon` porque los sitios más antiguos aún usan este último. Este pequeño matiz suele confundir a la gente cuando buscan “how to extract favicons”.

## Paso 3: Extraer href de los elementos link  

Con las etiquetas relevantes en mano, el siguiente paso lógico—**extract href from link**—es directo.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Usar `urljoin` garantiza que, incluso si un sitio proporciona una ruta relativa como `/favicon.ico`, terminarás con una URL absoluta correcta—crucial para un script fiable de **how to get favicon**.

## Paso 4: Opcional – Validar y filtrar URLs de íconos  

A veces una página lista muchos íconos (Apple touch icons, PNGs de varios tamaños, etc.). Si solo te interesa el clásico archivo `.ico`, filtra en consecuencia. Este paso muestra **how to extract favicons** de un tipo específico.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Siéntete libre de ajustar el filtro: reemplaza `".ico"` por `".png"` o verifica `rel="apple-touch-icon"` si necesitas íconos de alta resolución.

## Paso 5: Descargar los archivos de ícono (si deseas la imagen real)  

Extraer las URLs es solo la mitad de la batalla; descargar te brinda un archivo que puedes mostrar o almacenar. Aquí tienes un ayudante rápido:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Ejecutar esto después de los pasos anteriores te dará una copia local de cada favicon descubierto, perfecta para caché o análisis offline.

## Paso 6: Juntándolo todo – Ejemplo completo y funcional  

A continuación tienes el script completo, listo para ejecutar, que demuestra **how to get favicon** de cualquier sitio. Copia‑pega, cambia `target_url` y observa la salida.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Expected output (truncated for brevity):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Si el sitio solo ofrece PNG o Apple touch icons, el script listará esas URLs en su lugar, mostrándote exactamente **how to get favicon** en cualquier escenario.

## Preguntas frecuentes y casos especiales  

### ¿Qué pasa si el sitio usa una etiqueta `<meta>` en lugar de `<link>`?  
Algunas páginas antiguas incrustan la URL del ícono en una `<meta name="msapplication‑TileImage">`. Puedes ampliar `find_icon_links` para buscar también esas meta etiquetas y tratarlas de la misma forma.

### ¿Cómo manejo URLs relativas que empiezan con `//`?  
`urljoin` resuelve automáticamente las URLs relativas al protocolo (`//example.com/favicon.ico`) basándose en el esquema de la URL base, por lo que no necesitas lógica adicional.

### ¿Puedo obtener múltiples tamaños (p. ej., 32×32, 180×180) automáticamente?  
Sí—simplemente omite el paso `filter_ico_urls`. El script devolverá cada URL de ícono que descubra, incluidos PNGs de diversas dimensiones. Luego puedes ordenar o seleccionar según el patrón del nombre de archivo.

### ¿Funciona en sitios que bloquean bots?  
Si un sitio devuelve 403 o requiere un User‑Agent personalizado, ajusta la llamada `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Ese pequeño cambio suele resolver “how to get favicon” en dominios más restrictivos.

## Visión general visual  

![Diagrama que muestra el flujo de cómo obtener el favicon de un sitio web – cargar HTML, analizar etiquetas link, extraer href, descarga opcional](how-to-get-favicon-diagram.png "diagrama del flujo de cómo obtener el favicon")

*El texto alternativo de la imagen contiene la palabra clave principal, cumpliendo con el SEO para imágenes.*

## Conclusión  

Hemos recorrido **how to get favicon** paso a paso: cargar HTML desde una URL,

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}