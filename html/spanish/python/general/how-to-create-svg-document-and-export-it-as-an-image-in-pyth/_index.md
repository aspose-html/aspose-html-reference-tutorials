---
category: general
date: 2026-10-02
description: Aprende a crear documentos SVG en Python, guardar SVG en un archivo y
  exportar la imagen SVG con un script corto y completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: es
lastmod: 2026-10-02
og_description: Crea un documento SVG en Python y exporta la imagen SVG con este tutorial
  práctico. Sigue el script, guarda el SVG en un archivo y reutiliza el gráfico vectorial
  al instante.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Crear documento SVG en Python – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Cómo crear un documento SVG y exportarlo como imagen en Python
url: /es/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un documento SVG y exportarlo como una imagen en Python

Si necesitas **crear un documento SVG** programáticamente, este tutorial te muestra exactamente cómo hacerlo con Python. Verás un script completo que construye un círculo simple, guarda el SVG en un archivo y produce una imagen SVG exportable que puedes incrustar donde quieras.

Generar gráficos vectoriales escalables desde código elimina el esfuerzo manual de dibujar formas en un editor GUI. Al final de esta guía podrás integrar la creación de SVG en pipelines de visualización de datos, generadores de informes automatizados o cualquier proyecto que requiera gráficos nítidos e independientes de la resolución.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- Python 3.8 o superior instalado
- La biblioteca `svgwrite` (instálala con `pip install svgwrite`)
- Permiso de escritura en el directorio donde se guardará el SVG

Estos requisitos mantienen el ejemplo liviano y compatible con la mayoría de entornos.

## Paso 1: Instalar e importar la biblioteca SVG

El primer paso es añadir la biblioteca de terceros que proporciona una API conveniente para la creación de SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstrae la estructura XML de un archivo SVG, permitiéndote centrarte en la geometría en lugar de en el marcado bruto.

## Paso 2: Crear un objeto de documento SVG

Ahora puedes **crear un documento SVG** instanciando `svgwrite.Drawing`. Este objeto representa el elemento raíz `<svg>` y contiene todas las formas posteriores.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

El argumento `size` define las dimensiones en píxeles renderizadas, mientras que `viewBox` establece un sistema de coordenadas que coincide con la geometría que definirás más adelante.

## Paso 3: Añadir un elemento círculo

Un círculo se define por su centro (`cx`, `cy`) y radio (`r`). Usa el ayudante `circle` para asignar estos atributos.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

El círculo se sitúa en el centro del lienzo de 100 × 100, dejando un margen de 10 píxeles en cada lado. Ajusta `fill` y `stroke` para que coincidan con el lenguaje de diseño.

## Paso 4: Guardar el SVG en un archivo

Con el gráfico ensamblado, puedes **guardar el SVG en un archivo** usando el método `save`. Esto escribe XML bien formado que los navegadores y editores vectoriales entienden.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

El archivo `circle.svg` ahora se encuentra en el directorio de trabajo actual. Puedes abrirlo en un navegador web, Inkscape o cualquier herramienta que soporte el formato SVG.

## Paso 5: Verificar la imagen SVG exportada

Abre el archivo guardado en un navegador para confirmar el resultado. Deberías ver un círculo centrado con los colores especificados. El XML bruto se ve así:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Como SVG es vectorial, puedes escalar la imagen sin pérdida de calidad, lo que la hace ideal para diseños web responsivos o impresión de alta resolución.

## Consejo profesional: Exportar SVG como PNG o JPEG

Si necesitas una versión raster, combina el archivo SVG con una herramienta de conversión como **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Este paso demuestra **exportar la imagen SVG** a un formato bitmap, útil cuando los sistemas posteriores no pueden renderizar SVG directamente.

## Variaciones comunes y casos límite

| Variación | Cómo manejarlo |
|-----------|----------------|
| Múltiples formas | Llama a `dwg.add()` para cada nuevo elemento (rect, line, path). |
| Dimensiones dinámicas | Calcula `size` y `viewBox` a partir de los datos antes de crear `Drawing`. |
| Etiquetas de texto | Usa `dwg.text("Label", insert=("10", "20"))` y aplica estilo con `font_size` y `fill`. |
| Reutilizar el documento | Mantén el objeto `Drawing` en memoria y llama a `save()` cada vez que necesites un archivo actualizado. |
| Archivos grandes | Transmite la salida usando `dwg.tostring()` y escribe a un objeto de archivo manualmente para evitar picos de memoria. |

Abordar estos escenarios asegura que tu script **cómo generar SVG** escale desde íconos simples hasta diagramas complejos.

## Recapitulación del script completo

A continuación se muestra el ejemplo completo y ejecutable que incorpora todos los pasos y la conversión opcional:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Ejecutar este script produce `circle.svg` y, si `cairosvg` está instalado, `circle.png`. Ambos archivos están listos para incluirse en páginas web, informes o procesamiento adicional.

## Conclusión

Ahora sabes cómo **crear un documento SVG** en Python, **guardar SVG en un archivo** y **exportar la imagen SVG** para un uso más amplio. El ejemplo cubre las llamadas API esenciales, explica por qué cada paso es importante y ofrece extensiones para gráficos más complejos.

A continuación, explora temas adicionales del **tutorial de SVG Python** como dibujar rutas, aplicar degradados y animar elementos. Integrar estas técnicas te permitirá generar gráficos vectoriales dinámicos y basados en datos directamente desde tus aplicaciones Python. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear y gestionar documentos SVG en Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Guardar documento SVG en Aspose.HTML para Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg a png java – Convertir SVG a imagen con Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}