---
category: general
date: 2026-11-27
description: Crea un documento SVG y guarda el archivo SVG usando Python. Aprende
  a exportar un vector como SVG y generar una imagen SVG rápidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: es
lastmod: 2026-11-27
og_description: Crea un documento SVG y guarda el archivo SVG con Python. Esta guía
  te muestra cómo exportar vectores como SVG y generar una imagen SVG en minutos.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Crear documento SVG y guardar archivo SVG usando Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Crear documento SVG y guardar archivo SVG con Python
url: /es/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento SVG y guardar archivo SVG con Python

Si necesitas **crear SVG document** desde cero, esta guía te acompañará paso a paso en todo el proceso. Verás cómo **save SVG file** en disco, exportar el vector como SVG y obtener una imagen SVG lista para usar en solo unas pocas líneas de código.

Generar gráficos escalables programáticamente es útil para informes, íconos de UI o cualquier situación en la que quieras imágenes independientes de la resolución. Al final de este tutorial podrás responder “**how to create SVG**?” para formas simples y ampliar el patrón a ilustraciones vectoriales complejas.

## What you’ll need

- Python 3.8 o superior  
- El paquete `svgwrite` (instalable vía `pip`)  
- Un directorio con permisos de escritura para el archivo de salida  

No se requieren editores gráficos externos; todo se ejecuta desde la línea de comandos.

## Step 1: Install the `svgwrite` library

`svgwrite` ofrece una API limpia y Pythonic para construir marcado SVG. Instálalo una vez con:

```bash
pip install svgwrite
```

> **Pro tip:** Usa un entorno virtual (`python -m venv .venv`) para mantener las dependencias aisladas.

## Step 2: Create SVG document

Ahora creamos realmente los objetos **create SVG document**. La clase `Drawing` representa el elemento raíz `<svg>` y maneja los espacios de nombres automáticamente.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

La instancia `Drawing` es el punto de entrada para todas las operaciones SVG posteriores. Al especificar `size` establecemos las dimensiones del lienzo, lo que influye en cómo los navegadores renderizan la imagen.

## Step 3: Add a red circle element

Agregar formas es sencillo. El método `circle` crea un elemento `<circle>`; luego lo adjuntamos a la raíz.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Por qué elegimos un círculo: los círculos son primitivas vectoriales que demuestran escalabilidad sin pérdida de calidad, lo que hace que la salida sea ideal para probar flujos de trabajo **export vector as SVG**.

## Step 4: Save SVG file

Finalmente, escribe el marcado en disco. Este paso cumple con el requisito de **save SVG file** y produce un archivo que puedes abrir en cualquier navegador o editor vectorial.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Al ejecutar el script, verás un mensaje en la consola confirmando la ubicación del archivo generado.

### Expected output

El `circle.svg` resultante contiene:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Abrir el archivo en un navegador muestra un círculo rojo nítido y, al ser basado en vectores, puedes hacer zoom indefinidamente sin pixelación.

## Step 5: Common variations and edge cases

### Exporting more complex vectors

Si necesitas **export vector as SVG** para ilustraciones con múltiples formas, simplemente repite el patrón `dwg.add()` con otras primitivas (`rect`, `line`, `path`, etc.). Por ejemplo:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Handling Unicode and text

SVG soporta elementos de texto con soporte completo de Unicode. Usa `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` para incrustar etiquetas multilingües.

### Saving to a different location

Cuando **save SVG image** a una carpeta especificada por el usuario, valida la ruta para evitar errores de permisos:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minifying the output

Para pipelines de producción, puede que quieras un archivo de menor tamaño. Pasa `pretty=False` a `dwg.tostring()` y escribe el resultado manualmente:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## How to create SVG with alternative libraries (optional)

Aunque `svgwrite` es liviano y puro‑Python, existen otros ecosistemas:

- **cairosvg** – convierte PNG, PDF o HTML a SVG.  
- **lxml** – te permite construir marcado SVG manualmente usando APIs XML.  

Elegir una biblioteca depende de la complejidad de tu proyecto y de las dependencias existentes.

## Conclusion

Ahora sabes cómo **create SVG document**, agregar formas vectoriales y **save SVG file** usando Python. La solución completa muestra los pasos para **export vector as SVG**, generar una **SVG image** y responder la consulta común **how to create SVG** programáticamente.

Desde aquí puedes:

- Extender el script con bucles para generar gráficos o íconos automáticamente.  
- Integrar la salida SVG en aplicaciones web o plantillas de correo electrónico.  
- Explorar animaciones añadiendo elementos `<animate>` con `svgwrite`.

¡Experimenta con diferentes formas, colores y degradados para aprovechar al máximo el poder de los gráficos vectoriales escalables en tus proyectos Python! ¡Feliz codificación!


## What Should You Learn Next?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}