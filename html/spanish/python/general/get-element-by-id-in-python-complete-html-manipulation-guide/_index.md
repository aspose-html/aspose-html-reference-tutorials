---
category: general
date: 2026-05-31
description: Aprende cómo obtener un elemento por id, cambiar el color de fondo en
  HTML, leer el texto HTML y establecer un atributo HTML usando Python. Tutorial paso
  a paso.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: es
og_description: Obtén un elemento por id, lee el texto HTML, establece un atributo
  HTML y cambia el color de fondo del HTML usando Python en una guía única y fácil
  de seguir.
og_title: Obtener elemento por id en Python – Tutorial completo de manipulación de
  HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Obtener elemento por id en Python – Guía completa de manipulación de HTML
url: /es/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtener elemento por id en Python – Guía completa de manipulación HTML

¿Alguna vez necesitaste **obtener elemento por id** de una página HTML mientras escribías un script rápido en Python? No estás solo: la mayoría de los desarrolladores se topan con ese mismo obstáculo al comenzar a rastrear sitios o a modificar informes locales. ¿La buena noticia? Con unas pocas líneas de código puedes leer el texto del elemento, cambiar su color de fondo y hasta establecer nuevos atributos, todo sin salir de tu editor.

En este tutorial recorreremos un ejemplo del mundo real: cargar un `sample.html` local, extraer el elemento cuyo ID es `main‑content`, imprimir su texto interno y, finalmente, cambiar el color de fondo a un gris claro. Al final también sabrás **cómo leer texto HTML**, **cómo establecer un atributo HTML**, y por qué **manipular HTML con Python** es una habilidad útil en cualquier caja de herramientas de automatización.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener:

- **Python 3.9+** (cualquier versión reciente sirve)
- La biblioteca **`lxml`** (o **BeautifulSoup** si lo prefieres) – usaremos `lxml.html` porque ofrece una API estilo `get_element_by_id` muy limpia.
- Un pequeño archivo HTML llamado `sample.html` ubicado en una carpeta llamada `YOUR_DIRECTORY`. Puedes copiar el fragmento a continuación en ese archivo:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

Eso es todo—sin frameworks elegantes, solo Python puro y un archivo HTML estático.

## Paso 1: Instalar la biblioteca requerida

Si aún no has instalado `lxml`, abre una terminal y ejecuta:

```bash
pip install lxml
```

*Consejo profesional:* usar un entorno virtual mantiene tu Python global ordenado, especialmente cuando empiezas a manejar varios proyectos.

## Paso 2: Cargar el documento HTML

Ahora leeremos el archivo en un objeto documento `lxml.html`. Piensa en esto como convertir el texto bruto en un árbol navegable.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Al ejecutar esto se imprimirá “Document loaded successfully.” Si el archivo no se encuentra, Python lanzará un `FileNotFoundError`—es bueno capturarlo temprano antes de perseguir un elemento fantasma.

## Paso 3: Obtener elemento por id

Aquí está el núcleo del asunto. `lxml` nos brinda el práctico método `get_element_by_id` que refleja la API DOM que usarías en JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Cuando el elemento exista, verás “Element found!” impreso en la consola. Este es el paso **get element by id** que impulsa la mayoría de nuestras manipulaciones posteriores.

## Paso 4: Cómo leer texto HTML

Una vez que tienes el elemento, extraer su texto visible es pan comido. El método `text_content()` devuelve todo lo que está dentro, sin etiquetas.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Salida esperada:

```
Inner text: Hello, world! This is the original text.
```

Podrías preguntarte, *¿qué pasa si el elemento contiene etiquetas anidadas?* `text_content()` sigue funcionando—concatena todos los nodos de texto descendientes, dándote una cadena limpia que puedes registrar, almacenar o pasar a otro algoritmo.

## Paso 5: Cómo establecer un atributo HTML

Cambiar o añadir atributos es igual de sencillo. El método `set` te permite asignar cualquier nombre de atributo que desees.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Salida:

```
New attribute value: true
```

Esa línea muestra **how to set HTML attribute** sobre la marcha. Puedes reemplazar `"data-modified"` por `"class"`, `"title"` o cualquier otro atributo que el elemento acepte.

## Paso 6: Cambiar color de fondo HTML

Ahora el ajuste visual. Para cambiar el color de fondo, inyectamos un atributo `style` que sobrescribe el valor predeterminado.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Después de ejecutar el script, el `div` en `sample.html` se verá así al abrirlo en un navegador:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Esta es la técnica **change background colour html** que puedes reutilizar en cualquier elemento—solo cambia el código de color.

## Paso 7: Manipular HTML con Python – Uniendo todo

A continuación tienes el script completo y ejecutable que combina cada paso. Guárdalo como `modify_html.py` y ejecútalo desde el mismo directorio que tu carpeta `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Qué hace el script, línea por línea

1. **Imports** `lxml.html` para el análisis y `pathlib` para rutas independientes del SO.  
2. **Loads** `sample.html` y aborta con un error claro si el archivo falta.  
3. **Retrieves** el elemento usando **get element by id**.  
4. **Prints** el texto del elemento—mostrando **how to read HTML text**.  
5. **Adds** un atributo personalizado, ilustrando **how to set HTML attribute**.  
6. **Changes** el color de fondo, cumpliendo con el requisito **change background colour html**.  
7. **Writes** el marcado actualizado a `sample_modified.html`, para que puedas abrirlo en un navegador y ver los cambios.

Ejecutar el script produce una salida en consola similar a:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Abre `sample_modified.html` y notarás el fondo gris detrás del texto—prueba de que **manipulate HTML with python** realmente funciona.

## Errores comunes y cómo evitarlos

- **ID faltante** – Si el elemento objetivo no existe, `get_element_by_id` devuelve `None`. Siempre verifica `None` antes de acceder a propiedades; de lo contrario obtendrás un `AttributeError`.  
- **Problemas de codificación** – Al leer páginas no ASCII, pasa `encoding='utf-8'` a `html.parse` o asegura que tu archivo esté guardado en UTF‑8.  
- **Sobrescribir estilos existentes** – Establecer el atributo `style` reemplaza cualquier estilo en línea previo. Si necesitas preservar reglas existentes, lee primero el valor actual de `style`, agrega tu nueva regla y vuelve a escribirlo.  
- **Permisos de archivo** – Escribir de nuevo en la misma carpeta puede fallar en sistemas de solo lectura. Elige una ruta de salida escribible, como hicimos con `sample_modified.html`.

## Extender el ejemplo

Ahora que dominas lo básico, considera los siguientes pasos:

- **Recorrer varios IDs** – Usa una lista de IDs e itera con un `for` para procesar en lote secciones de una página.  
- **Reemplazar contenido de texto** – Llama a `elem.text = "New text"` para alterar la cadena visible.  
- **Añadir elementos hijos** – Usa `

## ¿Qué deberías aprender después?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}