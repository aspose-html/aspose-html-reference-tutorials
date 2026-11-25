---
category: general
date: 2026-07-31
description: Aprende a crear un documento SVG, añadir un círculo y guardar el archivo
  SVG rápidamente. Exporta el gráfico como SVG con unas pocas líneas de código Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: es
lastmod: 2026-07-31
og_description: Crea un documento SVG, añade un círculo y guarda el archivo SVG en
  segundos. Esta guía te muestra cómo exportar el gráfico como SVG con código claro
  y ejecutable.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Crear documento SVG – Añadir un círculo y guardar como SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Crear documento SVG – Añadir un círculo y guardar como SVG
url: /es/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento SVG – Añadir un círculo y guardar como SVG

¿Alguna vez necesitaste **crear un documento SVG** desde código pero no sabías por dónde empezar? No estás solo; muchos desarrolladores se topan con esa barrera cuando se inician en los gráficos vectoriales. En este tutorial recorreremos un pequeño ejemplo autocontenido que muestra cómo **añadir un círculo a SVG**, luego **guardar el archivo SVG** para que puedas **exportar el gráfico como SVG** y usarlo en la web o en herramientas de diseño.

Mantendremos las cosas ligeras: solo unas pocas líneas de Python, una popular biblioteca auxiliar de SVG y una breve explicación. Al final tendrás un `circle.svg` listo para usar en tu carpeta, y comprenderás por qué cada paso es importante—sin atajos vagos de “ver la documentación”.

## Lo que necesitarás

- Python 3.8+ (cualquier versión reciente sirve)
- El paquete `svgwrite` – instálalo con `pip install svgwrite`
- Un editor de texto o IDE (VS Code, PyCharm, o incluso Notepad sirve)
- Permiso de escritura en el directorio donde deseas guardar el archivo

Eso es todo. Sin dependencias pesadas, sin servicios externos.

## Paso 1: Configurar el documento SVG

Crear un documento SVG es tan simple como instanciar un objeto `Drawing` de `svgwrite`. Piensa en este objeto como el lienzo en blanco donde vivirán todas las formas.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Por qué importa:** La clase `Drawing` se encarga de todo el boilerplate XML por ti—espacios de nombres, encabezados y el elemento raíz `<svg>`. Al especificar un nombre de archivo desde el principio ya sabemos dónde terminará, lo que hace que el paso posterior de **guardar archivo SVG** sea trivial.

### Consejo profesional
Si planeas generar muchos archivos en un bucle, asigna a cada `Drawing` un nombre único o usa `io.BytesIO` para mantener todo en memoria hasta que estés listo para escribir.

## Paso 2: Añadir un círculo al SVG

Ahora que el documento existe, vamos a **añadir un círculo a SVG**. El método `add()` acepta cualquier objeto de forma; un `Circle` es perfecto para un simple punto rojo en el centro.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Por qué usamos variables `center` y `radius`:** Codificar números directamente hace que el código sea más difícil de leer y mantener. Al nombrar los valores aclaramos la intención—este círculo está justo en el medio de un lienzo de 200 × 200 y es lo suficientemente grande como para ser visible.

### Caso límite – Fondo transparente
Si necesitas un fondo transparente (el valor predeterminado para SVG), puedes omitir establecer un `fill` en la raíz. Para un fondo blanco, añade:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Colócalo antes de añadir el círculo para que el rectángulo quede debajo.

## Paso 3: Guardar el archivo SVG

Con la forma en su lugar, el acto final es **guardar el archivo SVG**. El método `save()` escribe el XML en disco, y como ya le dimos a `Drawing` un nombre de archivo, una sola llamada hace el trabajo.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **¿Qué ocurre tras bambalinas?** `svgwrite` serializa el árbol de elementos a una cadena, añade la declaración XML y lo escribe usando codificación UTF‑8. Si el directorio de destino no existe, Python lanzará un `FileNotFoundError`; asegúrate de que la ruta sea válida o créala con `os.makedirs()`.

### Bonus: Exportar el gráfico como SVG programáticamente

Si necesitas el contenido SVG como cadena—por ejemplo, para incrustarlo en un correo HTML—puedes llamar a `dwg.tostring()` en lugar de `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Ejemplo completo y funcional

Juntándolo todo, aquí tienes un script completo y listo para ejecutar:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Salida esperada:** Después de ejecutar el script, verás un archivo `circle.svg` en la misma carpeta. Al abrirlo en un navegador o cualquier editor vectorial verás un círculo rojo centrado en un cuadrado blanco—exactamente lo que programamos.

## Preguntas frecuentes y trampas comunes

- **¿Qué pasa si quiero una forma diferente?** Cambia `dwg.circle` por `dwg.rect`, `dwg.ellipse` o incluso una cadena `<path>` personalizada. La API es consistente entre formas.
- **¿Puedo incrustar el SVG directamente en HTML?** Por supuesto. El archivo que acabas de crear puede referenciarse con `<img src="circle.svg" alt="Red circle">` o incrustarse con etiquetas `<svg>`.
- **¿Por qué no escribir XML puro?** Podrías, pero bibliotecas como `svgwrite` manejan peculiaridades de los espacios de nombres y hacen que el código sea mucho más mantenible—especialmente cuando empiezas a añadir degradados o animaciones.

## Conclusión

Ahora sabes cómo **crear un documento SVG**, **añadir un círculo a SVG** y **guardar el archivo SVG** para que puedas **exportar el gráfico como SVG** con solo unas cuantas líneas de Python. El patrón escala: reemplaza el círculo por cualquier forma vectorial, itera sobre datos para generar gráficos, o procesa en lote activos para un sistema de diseño.

¿Próximos pasos? Prueba añadiendo etiquetas de texto, experimenta con degradados o genera una galería completa de íconos en un solo script. Si te interesa profundizar, revisa la documentación de `svgwrite` sobre grupos (`<g>`), transformaciones y soporte de animación.

¡Feliz codificación, y que tus vectores siempre se mantengan nítidos!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}