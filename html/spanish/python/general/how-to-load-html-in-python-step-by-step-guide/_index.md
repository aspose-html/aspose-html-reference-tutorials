---
category: general
date: 2026-07-02
description: Aprende a cargar HTML en Python, obtener un elemento por id y extraer
  texto de un archivo. Este tutorial práctico muestra cómo leer archivos HTML con
  BeautifulSoup.
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: es
og_description: Cómo cargar HTML en Python y extraer texto usando BeautifulSoup. Sigue
  la guía para leer un archivo HTML, obtener el elemento por id y imprimir su contenido.
og_title: Cómo cargar HTML en Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: Cómo cargar HTML en Python – Guía paso a paso
url: /es/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo cargar HTML en Python – Tutorial completo

¿Alguna vez te has preguntado **cómo cargar HTML** en un script de Python sin volverte loco? No eres el único. Ya sea que estés raspando un sitio de noticias, procesando un informe local, o simplemente necesites extraer un titular de una plantilla de correo electrónico, dominar el arte de cargar HTML es una habilidad imprescindible para cualquier desarrollador.

En esta guía recorreremos **cómo obtener un elemento** por su ID, **cómo extraer texto**, y finalmente imprimir el resultado, todo mientras mantenemos el código limpio y Pythonic. También cubriremos los matices de **leer un archivo HTML en Python**, para que puedas copiar‑pegar una solución funcional ahora mismo.

> **Consejo profesional:** El ejemplo usa la popular biblioteca *BeautifulSoup* porque es ligera, está bien documentada y funciona con estructuras HTML tanto simples como complejas.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener:

- Python 3.9 o superior (el código también funciona en 3.10+)
- `beautifulsoup4` y `lxml` instalados (`pip install beautifulsoup4 lxml`)
- Un archivo HTML de muestra – lo llamaremos `sample.html` y lo colocaremos en una carpeta llamada `YOUR_DIRECTORY`

Eso es todo. Sin navegadores pesados, sin Selenium, solo Python puro.

## Paso 1: Cómo cargar HTML – Leer el archivo en memoria

Lo primero que debes hacer es **leer el archivo HTML** del disco. Esta es la base de cada paso posterior, así que hagámoslo bien.

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*Por qué es importante:* Usar `Path.read_text` abstrae los finales de línea específicos del SO y maneja automáticamente UTF‑8, que es la codificación de facto para páginas web modernas. Si el archivo falta, `Path.read_text` lanzará un claro `FileNotFoundError`, facilitando la depuración.

## Paso 2: Analizar el documento HTML

Ahora que tenemos una cadena cruda, necesitamos **cargar HTML** en un objeto parser. BeautifulSoup nos brinda una API conveniente para navegar el DOM.

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*¿Por qué lxml?* El parser `lxml` es significativamente más rápido que el parser incorporado de Python y maneja marcas malformadas de forma más elegante, perfecto para HTML del mundo real que puedas raspar.

## Paso 3: Obtener elemento por ID – Localizar el encabezado

Con el documento analizado, respondamos la pregunta **cómo obtener un elemento** con un ID específico. En nuestro ejemplo buscamos una etiqueta `<h1>` cuyo atributo `id` sea igual a `"main-header"`.

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

Si el elemento no se encuentra, `header` será `None`. Es una buena práctica protegerse contra eso:

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## Paso 4: Cómo extraer texto – Obtener el contenido interno

Ahora que tenemos el elemento, extraer su contenido textual es muy fácil. Esto responde **cómo extraer texto** de una etiqueta.

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` concatena automáticamente cualquier nodo de texto anidado, por lo que no necesitas iterar manualmente sobre los hijos. La bandera `strip=True` elimina los caracteres de nueva línea y los espacios, dándote una cadena limpia.

## Paso 5: Imprimir el resultado – Verificar que todo funciona

Finalmente, imprimamos el valor en la consola. Esto refleja la línea `print(header.text_content)` del fragmento original.

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

Si ejecutas el script y ves el titular esperado, felicidades—has **leído un archivo HTML en Python**, localizado un elemento por ID y extraído su texto.

## Ejemplo completo y funcional

A continuación está el script completo, listo para ejecutar. Cópialo en un archivo llamado `extract_header.py` y ejecuta `python extract_header.py`.

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**Salida esperada** (suponiendo que `sample.html` contiene `<h1 id="main-header">Welcome to My Site</h1>`):

```
Welcome to My Site
```

Eso es todo—un script, sin dependencias extra más allá de BeautifulSoup y lxml.

## Preguntas frecuentes y casos límite

### ¿Qué pasa si el HTML está malformado?

El parser `lxml` de BeautifulSoup es indulgente, pero para marcas gravemente rotas podrías volver al `html.parser` incorporado. Cambia "lxml" por "html.parser" en el constructor de `BeautifulSoup`.

### ¿Cómo manejar múltiples elementos con el mismo ID?

La especificación HTML dice que los IDs deben ser únicos, pero la realidad a veces difiere. Usa `soup.find_all(id="duplicate-id")` para obtener una lista y luego itera sobre ella.

### ¿Necesitas leer desde una URL en lugar de un archivo?

Reemplaza la lógica de lectura de archivo con `requests.get(url).text`. Recuerda instalar el paquete `requests` (`pip install requests`) y manejar los errores de red de forma adecuada.

### ¿Quieres extraer otros atributos (p.ej., `class` o `href`)?

Simplemente accede a ellos como un diccionario: `header['class']` o `header['href']`. Si el atributo podría faltar, usa `.get('class')` para evitar `KeyError`.

## Resumen visual

![ejemplo de cómo cargar html](https://example.com/placeholder-image.png "ejemplo de cómo cargar html")

*Texto alternativo:* ejemplo de cómo cargar html – un diagrama que muestra el flujo desde la lectura del archivo hasta la extracción de texto.

## Recapitulación

Hemos cubierto **cómo cargar HTML** en Python, demostrado **cómo obtener un elemento** por su ID, y mostrado **cómo extraer texto** de ese elemento. Siguiendo los pasos anteriores puedes de forma fiable **leer un archivo HTML en Python**, manipular el DOM y extraer exactamente lo que necesitas.

## ¿Qué sigue?

- **Explorar selectores CSS:** Usa `soup.select_one('.my-class')` para consultas más flexibles.
- **Raspar múltiples páginas:** Combina este patrón con `requests` y un bucle para procesar sitios en lote.
- **Escribir de nuevo a HTML:** BeautifulSoup también permite modificar el árbol y guardar cambios, útil para tareas de plantillas.
- **Ajuste de rendimiento:** Para archivos masivos, considera parsers de streaming como `lxml.etree.iterparse`.

Siéntete libre de experimentar—cambia el ID, prueba diferentes etiquetas, o incluso cambia a `xml.etree.ElementTree` si trabajas con XHTML. Los conceptos siguen siendo los mismos, y ahora tienes una base sólida para cualquier aventura de análisis HTML.

¡Feliz codificación! Si encuentras algún problema o tienes un caso de uso interesante para compartir, deja un comentario abajo.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cargar documentos HTML desde archivo en Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Cómo consultar HTML en Java – Tutorial completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Cómo editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}