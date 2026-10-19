---
category: general
date: 2026-06-10
description: Carga HTML desde una URL para obtener rápidamente los íconos del sitio
  web. Aprende cómo extraer favicons, obtener las URLs de los favicons del sitio y
  manejar casos especiales en Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: es
og_description: Cargar HTML desde una URL para extraer favicons y obtener las URLs
  de los favicons del sitio web. Un tutorial paso a paso de Python para desarrolladores.
og_title: Cargar HTML desde URL y obtener íconos del sitio web – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Cargar HTML desde una URL y obtener los íconos del sitio web – Guía completa
url: /es/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cargar HTML desde URL y Obtener Iconos de Sitios Web – Guía Completa

¿Alguna vez necesitaste **cargar HTML desde URL** solo para obtener el pequeño logo de un sitio? No estás solo. Ya sea que estés construyendo un gestor de marcadores, un panel de SEO, o simplemente un proyecto personal, obtener los iconos de los sitios web es una pieza pequeña pero esencial del rompecabezas.

En este tutorial te mostraremos **cómo extraer favicons** usando Python puro—sin Selenium pesado, sin trucos de navegador. Al final podrás **obtener URLs de favicons de sitios web**, manejar rutas relativas e incluso capturar múltiples iconos si un sitio los proporciona. ¿Listo? Vamos a sumergirnos.

## ¿Por qué cargar HTML desde URL en primer lugar?

Cargar el HTML sin procesar de una página te da acceso directo a las etiquetas `<link>` que los navegadores usan para localizar favicons. Esas etiquetas suelen verse así:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Si puedes obtener ese marcado, puedes leer programáticamente el atributo `href` y descargar la imagen tú mismo. Es más rápido que raspar capturas de pantalla, y funciona para cualquier sitio que siga las convenciones estándar.

## Paso 1 – Cargar el documento HTML desde una URL

Lo primero que necesitamos es una forma de obtener el código fuente de la página. La opción más popular en Python es la biblioteca **requests** porque es simple, fiable y maneja redirecciones de forma automática.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Consejo profesional:** Si trabajas detrás de un proxy corporativo, pasa `proxies=` a `requests.get`. Además, establecer un tiempo de espera corto evita que tu script se quede colgado en sitios muertos.

Ahora podemos llamar a `fetch_html("https://example.com")` y obtener una cadena que contiene el marcado de la página. Esto es el núcleo de **cargar HTML desde URL**—el resto del flujo de trabajo trabaja con esa cadena.

## Paso 2 – Obtener iconos del sitio web

Una vez que tenemos el HTML, el siguiente paso es localizar cada elemento `<link>` cuyo atributo `rel` mencione “icon”. El módulo incorporado `html.parser` puede hacer el trabajo, pero **BeautifulSoup** hace que el código sea mucho más legible.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Observa cómo usamos `urljoin` para convertir `"/favicon.ico"` en `"https://example.com/favicon.ico"`—ese es un caso límite común al **obtener iconos del sitio web**. Algunos sitios incluso sirven diferentes iconos para distintos dispositivos, por lo que podrías terminar con un puñado de URLs. No hay problema; simplemente los recopilamos todos.

## Paso 3 – Extraer URLs de favicons y mostrarlos

Unir las piezas es sencillo. Obtendremos el HTML, ejecutaremos el extractor y imprimiremos la lista resultante. El script final se ve así:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Salida esperada

Ejecutar el script contra un sitio que proporciona un favicon estándar podría darte:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Si el sitio suministra múltiples iconos (Apple touch icon, shortcut icon, etc.), verás una lista más larga:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Ese es todo el flujo de trabajo de **extraer URLs de favicons**—compacto, con pocas dependencias y listo para integrarse en cualquier proyecto.

## Manejo de problemas comunes

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **href` relativo sin una etiqueta `<base>`** | `urljoin` asume la URL de la página como base, lo que funciona en la mayoría de los casos. | Si existe una etiqueta `<base href="...">`, léela primero y pásala como `base_url`. |
| **Falta `rel="icon"`** | Algunos sitios usan `rel="shortcut icon"` o valores personalizados. | Extiende la lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirecciones a un dominio diferente** | El favicon puede estar alojado en un CDN. | `urljoin` resolverá correctamente el nuevo dominio porque usa la URL final de la solicitud (`response.url`). |
| **Enlaces rotos (404)** | El HTML apunta a un archivo que ya no existe. | Después de extraer las URLs, puedes verificar cada una con una solicitud HEAD antes de usarlas. |
| **Múltiples etiquetas `<link>` con el mismo icono** | Entradas duplicadas inflan la lista. | Usa `set(icon_urls)` para eliminar duplicados antes de devolverlas. |

## Avanzando – Obtener URLs de favicons de sitios web en lote

Si necesitas **obtener URLs de favicons de sitios web** para una lista de dominios, envuelve la lógica `main` en un bucle:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Este patrón escala bien, y puedes añadir caché (p. ej., con `functools.lru_cache`) para evitar golpear repetidamente el mismo sitio.

## Visión general visual

![Load HTML from URL diagram](load-html-url.png)

*Texto alternativo: Diagrama de cargar HTML desde URL que muestra los pasos obtener → analizar → extraer.*

## Conclusión

Hemos recorrido una solución completa y lista para producción sobre cómo **cargar HTML desde URL** y **obtener iconos de sitios web** usando solo las bibliotecas requests y BeautifulSoup de Python. Al extraer los atributos `href` de las etiquetas `<link rel="icon">`, puedes **extraer URLs de favicons**, manejar rutas relativas e incluso recuperar múltiples formatos de iconos—todo en unas pocas docenas de líneas de código.

¿Qué sigue? Intenta descargar los iconos a una carpeta local, generar un CSV de mapeos dominio‑a‑favicon, o integrar esta lógica en una API Flask que sirva favicons bajo demanda. Las posibilidades para **obtener URLs de favicons de sitios web** son infinitas, y la técnica central sigue siendo la misma.

¿Tienes preguntas sobre casos límite, o quieres compartir un ajuste ingenioso? Deja un comentario abajo—¡feliz caza de iconos!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}