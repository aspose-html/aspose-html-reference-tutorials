---
category: general
date: 2026-06-07
description: Cómo agregar un prefijo a los encabezados HTML usando Python. Aprende
  a seleccionar varios encabezados, cambiar los títulos HTML y guardar el HTML modificado
  de manera eficiente.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: es
og_description: Cómo agregar un prefijo a los encabezados HTML usando Python. Este
  tutorial muestra cómo seleccionar varios encabezados, cambiar los títulos HTML y
  guardar el HTML modificado en solo unas pocas líneas.
og_title: Cómo agregar un prefijo a los encabezados HTML con Python – Guía rápida
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: Cómo agregar un prefijo a los encabezados HTML con Python – Guía paso a paso
url: /es/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar un prefijo a los encabezados HTML con Python – Tutorial completo

Agregar un prefijo a los encabezados HTML usando Python es una necesidad común cuando mantienes un sitio que recibe actualizaciones frecuentes. En esta guía recorreremos la selección de múltiples encabezados, la modificación de los títulos HTML y el guardado del HTML modificado, todo sin salir de tu editor.  

Si alguna vez te has preguntado si puedes automatizar la insignia “marcar como actualizado” en docenas de páginas, estás en el lugar correcto. También abordaremos cómo **modify html with python** de forma escalable, para que no tengas que abrir cada archivo manualmente.

## Lo que lograrás

Al final de este tutorial podrás:

* **Seleccionar múltiples encabezados** (`h1`, `h2`, `h3`) en una sola pasada.  
* **Agregar un prefijo personalizado** (p.ej., `[Updated]`) al texto de cada encabezado.  
* **Guardar html modificado** en disco, preservando la estructura original de archivos.  
* Entender las compensaciones entre diferentes analizadores HTML de Python y elegir el que mejor se adapte a tu proyecto.

Sin servicios externos, sin frameworks pesados—solo Python puro y un par de bibliotecas bien mantenidas.

---

## Cómo agregar un prefijo al texto de los encabezados en Python

A continuación se muestra un ejemplo mínimo y ejecutable que demuestra la idea principal. Utiliza la biblioteca **`lxml`** junto con **`cssselect`** para soporte de selectores, lo que replica el método `query_selector_all` que viste en el fragmento original.

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**Salida esperada** (extracto de `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Observa cómo cada encabezado ahora comienza con la etiqueta `[Updated]`, exactamente lo que queríamos cuando preguntamos **how to add prefix** a nuestros títulos.

### Por qué funciona este enfoque

* **`lxml` + `cssselect`** te brinda todo el poder de los selectores CSS, haciendo que el paso de “seleccionar múltiples encabezados” sea una sola línea.  
* El método `text_content()` extrae de forma segura el texto interno, evitando entidades HTML o etiquetas hijas.  
* Escribir de nuevo con `pretty_print=True` mantiene el archivo legible para humanos, lo cual es útil para diffs en control de versiones.

---

## Seleccionando múltiples encabezados con selectores CSS

Si vienes de un entorno JavaScript, la sintaxis de `cssselect` te resultará familiar. El selector `"h1, h2, h3"` es una **lista separada por comas**, lo que significa “capturar cualquier elemento que coincida *con cualquiera* de estos tres”.  

También podrías ampliar el alcance:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

O reducirlo a una sección específica:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Estos pequeños ajustes te permiten **seleccionar múltiples encabezados** con precisión láser, lo cual es especialmente útil cuando tienes un sitio de documentación masivo y solo deseas actualizar una subsección.

---

## Guardando archivos HTML modificados de forma segura

Cuando **save modified html**, deseas evitar corromper el archivo original. El patrón mostrado arriba escribe en un nuevo archivo (`article_updated.html`). De esa forma puedes:

1. Verificar los cambios en una herramienta de diff.  
2. Revertir instantáneamente si algo parece incorrecto.  
3. Mantener el original intacto para fines de auditoría.

Si prefieres una edición in‑place, simplemente intercambia las rutas:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Pero recuerda: **siempre haz una copia de seguridad** antes de sobrescribir, especialmente en servidores de producción.

---

## Cambiar títulos HTML vs. encabezados

Podrías preguntarte si “cambiar títulos HTML” es lo mismo que prefijar encabezados. En la terminología HTML, la etiqueta `<title>` vive dentro de `<head>` y controla el título de la pestaña del navegador, mientras que los encabezados (`<h1>…<h3>`) aparecen en el cuerpo de la página.

Si necesitas **change html titles** también, el mismo flujo de trabajo con `lxml` se aplica:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Ahora tanto el título de la página como los encabezados visibles llevan la misma bandera `[Updated]`, perfecto para auditorías SEO donde deseas consistencia entre los metadatos y el contenido de la página.

---

## Bibliotecas alternativas para modify html with python

Aunque `lxml` es rápido y rico en funciones, quizás ya estés usando **BeautifulSoup** (bs4) en tu proyecto. Aquí tienes la misma lógica en un estilo más “pythonic”:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Ambas bibliotecas te permiten **modify html with python**, así que elige la que coincida con tu stack actual. `BeautifulSoup` destaca cuando necesitas un análisis indulgente de marcado malformado, mientras que `lxml` ofrece velocidad superior para lotes grandes.

---

## Consejos profesionales y errores comunes

* **La codificación importa** – siempre abre los archivos con `encoding="utf-8"` para evitar errores Unicode en caracteres no ASCII.  
* **Evita el doble prefijo** – si ejecutas el script dos veces, obtendrás `[Updated] [Updated] …`. Prevén esto verificando `heading.text.startswith(prefix)`.  
* **Preserva los espacios en blanco** – la llamada `strip()` elimina espacios sueltos, manteniendo la salida ordenada.  
* **Procesamiento por lotes** – envuelve todo el flujo en un bucle `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` para actualizar una carpeta completa con un solo comando.  

---

## Ejemplo completo y funcional: actualización por lotes de un directorio

A continuación hay un script compacto que itera sobre cada archivo `.html` en un directorio, agrega prefijos a los encabezados, actualiza el `<title>` y escribe un nuevo archivo con `_updated` añadido.

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

Ejecuta una vez, y cada archivo HTML en `YOUR_DIRECTORY` recibirá una nueva insignia `[Updated]`, sin necesidad de edición manual.

---

## Conclusión

Hemos cubierto **how to add prefix** a los encabezados HTML usando Python, demostrado cómo **select multiple headings**, mostrado cómo **save modified html** de forma segura, y también tocado **change html titles** para una renovación completa. Al aprovechar `lxml` o `BeautifulSoup`, ahora dispones de una caja de herramientas sólida para **modify html with python** en proyectos del mundo real.

¿Próximos pasos? Prueba agregar marcas de tiempo en lugar de una etiqueta estática, o genera un archivo de registro de cambios que liste cada archivo que modificaste. También podrías conectar este script a una canalización CI para que cada despliegue lo haga automáticamente

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cómo agregar CSS – CSS en línea a documentos HTML en Aspose.HTML para Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Cómo consultar HTML en Java – Tutorial completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}