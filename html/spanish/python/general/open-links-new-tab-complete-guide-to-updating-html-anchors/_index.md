---
category: general
date: 2026-07-05
description: Abrir enlaces en una nueva pestaña usando Python – aprende cómo agregar
  target="_blank", cambiar el objetivo del enlace, usar el selector de atributo contiene
  y guardar el HTML modificado sin esfuerzo.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: es
og_description: Abre enlaces en una nueva pestaña rápidamente. Este tutorial muestra
  cómo agregar target="_blank", cambiar el objetivo del enlace y guardar el HTML modificado
  con Python.
og_title: Abrir enlaces en una nueva pestaña – Guía paso a paso para actualizar HTML
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Abrir enlaces en una nueva pestaña – Guía completa para actualizar anclas HTML
url: /es/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abrir enlaces en una nueva pestaña – Guía completa para actualizar anclas HTML

¿Alguna vez necesitaste **abrir enlaces en una nueva pestaña** en una página HTML estática pero no sabías por dónde empezar? No estás solo. Muchos desarrolladores se topan con este problema al limpiar sitios heredados o al agregar ajustes de accesibilidad. En este tutorial recorreremos una solución práctica que **añade target blank**, **cambia el objetivo del enlace**, y guarda de forma segura el **html modificado**—todo con unas pocas líneas de Python.

También cubriremos cómo usar un **attribute contains selector** para que solo toques los anclajes que realmente te importan (por ejemplo, cada enlace que apunta a *example.com*). Al final, tendrás un script reutilizable que puedes incorporar a cualquier proyecto, sin importar su tamaño.

## Lo que aprenderás

- Cargar un archivo HTML en un objeto de documento manipulable.  
- Seleccionar elementos `<a>` cuyo atributo `href` contenga una subcadena específica.  
- **Add target blank** y establecer el atributo `rel="noopener"` para mejorar la seguridad.  
- **Save modified html** de nuevo en disco sin perder el formato.  

No hay dependencias externas más allá de la biblioteca estándar y **beautifulsoup4** (una instalación mínima). Si ya usas otro parser, los conceptos se traducen directamente.

---

## Requisitos previos

- Python 3.8+ instalado en tu máquina.  
- Familiaridad básica con HTML y Python.  
- Paquete `beautifulsoup4` (`pip install beautifulsoup4`).  

Eso es todo—no se requieren frameworks pesados.

---

## Paso 1: Cargar el documento HTML

Primero lo primero: necesitamos leer el archivo fuente y pasarlo a BeautifulSoup. Piensa en esto como abrir un lienzo en blanco donde puedes dibujar nuevos atributos.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** Usar `Path` mantiene el código independiente del SO, y `html.parser` está integrado, por lo que no necesitas parsers adicionales para tareas simples.

---

## Paso 2: Usar un Attribute Contains Selector para encontrar los enlaces correctos

Solo queremos tocar los anclajes que apuntan a *example.com*. El selector CSS `a[href*='example.com']` hace exactamente eso—`*=` significa “contiene”. El método `select` de BeautifulSoup entiende esta sintaxis.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** Si necesitas una coincidencia sin distinción de mayúsculas/minúsculas, cambia a un pequeño bucle que verifique `if 'example.com' in a.get('href', '').lower()`.

Ahora `anchor_elements` contiene cada enlace que nos importa, listo para la siguiente transformación.

---

## Paso 3: Cambiar el objetivo del enlace – Añadir target blank y asegurar el enlace

Abrir un enlace en una nueva pestaña es tan simple como establecer `target="_blank"`. Sin embargo, los navegadores modernos recomiendan también añadir `rel="noopener"` (o `noreferrer`) para evitar que la página recién abierta acceda a la ventana original mediante `window.opener`. Este pequeño ajuste de seguridad puede detener ataques de phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** Crea automáticamente el atributo si falta, y lo sobrescribe si ya existe—perfecto para una operación de **change link target**.

---

## Paso 4: Guardar el HTML modificado en disco

El paso final es escribir el marcado actualizado en un nuevo archivo. Mantener el original intacto te permite revertir los cambios si algo sale mal.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** Formatea el HTML con una buena indentación, haciendo que el archivo guardado sea más fácil de leer y comparar después. Si prefieres el espacio en blanco original, reemplaza `prettify()` por `str(soup)`.

---

## Script completo – Solución de un clic

A continuación tienes el script completo, listo para ejecutar. Guárdalo como `update_links.py` y ejecuta `python update_links.py` desde tu terminal.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Resultado esperado

Supongamos que `links.html` originalmente contenía:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Después de ejecutar el script, `links-updated.html` se verá así:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Solo el enlace a *example.com* recibió los atributos de **add target blank**, demostrando que nuestro **attribute contains selector** funcionó exactamente como se esperaba.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si un enlace ya tiene un atributo `rel`?

Nuestro bucle lo sobrescribe con `"noopener"`. Si necesitas conservar valores existentes (p. ej., `"nofollow"`), concatena en su lugar:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### ¿Cómo manejar múltiples dominios?

Simplemente amplía la lista de selectores:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### ¿`prettify()` cambia la estructura original del HTML?

Re‑indenta pero no altera el orden de las etiquetas ni los valores de los atributos. Si debes mantener el espacio en blanco exacto original, reemplaza `prettify()` por `str(soup)` como se mencionó antes.

---

## Consejos profesionales para scripts listos para producción

- **Backup before overwriting:** Añade un paso de copia (`shutil.copy`) para mantener el archivo original seguro.  
- **Logging instead of print:** Usa el módulo `logging` para proyectos escalables.  
- **Batch processing:** Recorre un directorio con `Path.rglob("*.html")` para actualizar muchos archivos en una sola ejecución.  

Estos ajustes convierten un simple script de **open links new tab** en una utilidad robusta para cualquier flujo de trabajo de mantenimiento web.

---

## Conclusión

Ahora dispones de un método sólido y reutilizable para **open links new tab** en cualquier colección de HTML estático. Aprovechando un **attribute contains selector**, puedes **change link target** precisamente donde lo necesitas, **add target blank**, y **save modified html** sin perder el formato.

Pruébalo en una página de prueba y luego escálalo a todo tu sitio. ¿Necesitas ajustar el selector para PDFs, imágenes u otros dominios? Simplemente modifica la cadena CSS—todo lo demás permanece igual.

No dudes en dejar un comentario si encuentras alguna anomalía, o compartir cómo extendiste el script para tus propios proyectos. ¡Feliz codificación, y que todos tus anclajes se abran exactamente donde deseas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cómo agregar CSS – CSS en línea a documentos HTML en Aspose.HTML para Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}