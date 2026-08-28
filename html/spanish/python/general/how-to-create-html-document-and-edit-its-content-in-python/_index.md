---
category: general
date: 2026-08-25
description: Aprende cómo crear un documento HTML, seleccionar elementos CSS, modificar
  texto HTML y guardar el archivo HTML usando un script simple de Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: es
lastmod: 2026-08-25
og_description: Crea un documento HTML, selecciona el elemento CSS, modifica el texto
  HTML y guarda el archivo HTML en unas pocas líneas de Python. Sigue este tutorial
  completo.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Crear documento HTML y editar su contenido con Python – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Cómo crear un documento HTML y editar su contenido en Python
url: /es/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un documento html y editar su contenido en Python

Si necesitas **create html document** desde cero y cambiar sus elementos programáticamente, esta guía te muestra exactamente cómo. Verás un script corto y ejecutable que crea un archivo, selecciona un párrafo con un selector CSS, actualiza el texto y escribe el resultado de nuevo en el disco.

Trabajar con HTML en Python es común al generar informes, plantillas de correo electrónico o contenido de sitios estáticos. Al final de este tutorial podrás **select element css**, **modify html text** y **save html file** sin salir de la comodidad de tu IDE.

## Requisitos previos

* Python 3.9 o superior instalado.
* Los paquetes `beautifulsoup4` y `lxml` (instala con `pip install beautifulsoup4 lxml`).
* Permiso de escritura en el directorio donde planeas almacenar el archivo de salida.

No se requieren herramientas adicionales; la biblioteca estándar maneja la E/S de archivos.

## Paso 1: Instalar las bibliotecas requeridas

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` proporciona una API conveniente para analizar y manipular HTML, mientras que `lxml` ofrece un analizador rápido que entiende los selectores CSS.

## Paso 2: Crear el documento HTML inicial

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

El constructor `BeautifulSoup` crea un objeto **create html document** en memoria. Usar el analizador `"lxml"` garantiza soporte completo de selectores CSS.

## Paso 3: Seleccionar el elemento párrafo usando un selector CSS

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

El método `select_one` implementa la lógica de **select element css**, devolviendo la primera etiqueta coincidente. Si el selector no coincide con nada, `para` será `None`, por lo que es aconsejable realizar una verificación defensiva en código de producción.

## Paso 4: Modificar el contenido de texto del párrafo

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Asignar a `para.string` realiza una operación de **modify html text**. BeautifulSoup actualiza el árbol DOM subyacente, por lo que el cambio se refleja al serializar el documento.

## Paso 5: Guardar el HTML actualizado en un archivo

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

La llamada `open` junto con `write` implementa la funcionalidad de **save html file**. Usar `prettify()` produce una salida bien indentada, lo cual es útil durante la depuración.

### Script completo para copiar y pegar rápidamente

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Ejecutar `python edit_html.py` crea `updated.html` que contiene:

```html
<p>
 New
</p>
```

## Variaciones comunes y casos límite

### Seleccionar múltiples elementos

Si necesitas selectores **select element css** que coincidan con varias etiquetas (p. ej., `"div.note"`), usa `doc.select("div.note")` que devuelve una lista. Itera sobre la lista para aplicar cambios a cada elemento.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Preservar atributos existentes

Cuando reemplazas el texto, BeautifulSoup conserva cualquier atributo en la etiqueta. Por ejemplo:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Manejar elementos faltantes de forma elegante

En scripts de producción, a menudo encuentras HTML malformado. Envuelve la selección en una condición o bloque try‑except, como se muestra en el Paso 4, para evitar fallos.

### Escribir en un directorio específico

Reemplaza `output_path` con una ruta absoluta o relativa:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Asegúrate de que el directorio exista; de lo contrario, Python lanzará `FileNotFoundError`.

## Consejos profesionales

* **Performance** – Para archivos HTML grandes, prefiere usar `lxml.etree` directamente; BeautifulSoup añade una capa de abstracción ligera que es conveniente pero ligeramente más lenta.
* **Encoding** – Siempre abre los archivos con `encoding="utf-8"` para preservar caracteres no ASCII.
* **Testing** – Después de la modificación, puedes verificar la salida con `assert "New" in open(output_path).read()` en una prueba unitaria.

## Conclusión

Ahora sabes cómo **create html document**, usar una consulta **select element css** para localizar un nodo, **modify html text**, y finalmente **save html file** con Python. Este patrón se escala a transformaciones más complejas como actualizaciones masivas, cambios de atributos o generación de plantillas.

A continuación, explora temas relacionados como **how to edit html** usando expresiones XPath, generar páginas HTML completas con Jinja2, o automatizar el procesamiento por lotes de múltiples archivos. Cada uno de ellos se basa en los pasos principales demostrados aquí y amplía tu conjunto de herramientas para la manipulación programática de HTML.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear documento HTML con Aspose.HTML – Guía paso a paso](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [Cómo editar el árbol de documentos HTML en Aspose.HTML para Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Guardar documento HTML en Aspose.HTML para Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}