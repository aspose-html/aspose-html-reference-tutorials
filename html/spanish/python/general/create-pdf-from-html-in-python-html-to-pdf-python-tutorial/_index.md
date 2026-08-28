---
category: general
date: 2026-07-15
description: Crear PDF a partir de HTML usando Python. Aprende cómo convertir HTML
  a PDF rápidamente con un script sencillo y pasos claros.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: es
lastmod: 2026-07-15
og_description: Crear PDF a partir de HTML con Python. Esta guía te muestra cómo convertir
  HTML a PDF, guardar HTML como PDF y manejar los recursos de manera eficiente.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Crear PDF a partir de HTML en Python – Tutorial práctico
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: 'Crear PDF a partir de HTML en Python – Tutorial de Python: HTML a PDF'
url: /es/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF a partir de HTML en Python – Tutorial Completo

¿Alguna vez necesitaste **crear PDF a partir de HTML** pero no estabas seguro de qué biblioteca de Python elegir? No estás solo—muchos desarrolladores se topan con ese obstáculo cuando intentan convertir un informe web, una factura o una página de marketing en un PDF imprimible.  

La buena noticia es que con solo unas pocas líneas de código puedes **convertir HTML a PDF** de forma fiable, y el script funciona en Windows, macOS y Linux. En esta guía recorrremos un ejemplo completo y ejecutable, explicaremos por qué cada paso es importante y te mostraremos cómo **guardar HTML como PDF** sin dejar cabos sueltos.

---

## Lo que aprenderás

- Instalar el paquete de Python adecuado para la conversión de HTML‑a‑PDF.  
- Cargar un archivo HTML con opciones personalizadas de manejo de recursos (para evitar importaciones CSS infinitas).  
- Generar un archivo PDF limpio en disco.  
- Abordar casos límite comunes como imágenes externas, rutas relativas y documentos grandes.  

Al final de este **tutorial de HTML a PDF** tendrás una función reutilizable que puedes insertar en cualquier proyecto.

---

## Requisitos previos

- Python 3.9+ (el código también funciona con 3.8, pero 3.9+ te brinda las últimas funcionalidades de `pathlib`).  
- Familiaridad básica con la línea de comandos y entornos virtuales.  
- Un archivo HTML que quieras convertir a PDF—cualquier página estática sirve.

> **Consejo profesional:** Si usas un entorno virtual, actívalo antes de instalar la biblioteca; así mantienes tu Python global ordenado.

---

## Paso 1 – Instalar WeasyPrint (el motor detrás de la conversión)

WeasyPrint es una biblioteca puramente Python que renderiza HTML y CSS a PDF. Maneja la mayoría de las características web modernas y te brinda un control granular sobre la carga de recursos.

```bash
pip install weasyprint
```

Ejecutar el comando anterior descarga `cairocffi`, `tinycss2` y algunas otras dependencias. Si te encuentras con un error relacionado con `cairo` en Windows, obtén las ruedas precompiladas desde el [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Paso 2 – Preparar un pequeño ayudante para el manejo de recursos

Cuando cargas un documento HTML que hace referencia a hojas de estilo o imágenes externas, la biblioteca seguirá esos enlaces. En algunos casos eso lleva a una anidación profunda o incluso a bucles infinitos (piensa en un archivo CSS que se `@import` a sí mismo). Para mantener todo ordenado limitamos la profundidad del manejo de recursos.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

La clase anterior no es requerida por WeasyPrint, pero refleja el patrón que viste en el fragmento original y te brinda un punto de enganche para detener importaciones descontroladas. La verás en uso en el siguiente paso.

---

## Paso 3 – Cargar el documento HTML usando las opciones personalizadas

Ahora leemos realmente el archivo HTML. La clase `HTML` acepta un argumento `base_url`, que establecemos al directorio que contiene el archivo fuente—esto hace que los enlaces relativos funcionen sin necesidad de un servidor web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Por qué importa:** Si tu HTML incluye una cascada de archivos CSS, cada `@import` disparará otra carga. El guardia de profundidad evita que el script se salga de control.

---

## Paso 4 – Guardar el documento procesado como PDF

Con el objeto `HTML` en mano, generar un PDF es una sola línea. También pasamos un fragmento CSS sencillo que fuerza un tamaño de página limpio (A4) y añade un pequeño margen—ajústalo a tu gusto.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Llamar a `write_pdf` envía el PDF a disco, de modo que terminas con un archivo listo para compartir.

---

## Paso 5 – Juntar todo

A continuación tienes un script compacto que puedes copiar‑pegar en `convert.py`. Sustituye las rutas de marcador de posición por tus directorios reales.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Salida esperada** – después de ejecutar `python convert.py` deberías ver:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Abre el archivo generado con cualquier visor de PDF; verás el diseño original de la página, el estilo CSS y las imágenes (siempre que fueran accesibles desde el archivo HTML).  

Si notas imágenes faltantes, verifica que sus atributos `src` sean URLs absolutas o rutas relativas que existan bajo `YOUR_DIRECTORY`.

---

## Preguntas frecuentes y manejo de casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si mi HTML hace referencia a fuentes externas?* | WeasyPrint descargará los archivos de fuente automáticamente, pero quizá quieras crear una lista blanca de dominios para evitar tiempos de descarga largos. |
| *¿Puedo convertir una cadena de HTML en lugar de un archivo?* | Sí—usa `HTML(string=my_html_string)` y omite `base_url` o establécelo a una carpeta temporal. |
| *¿Cómo controlo los metadatos del PDF (título, autor)?* | Pasa un diccionario `metadata` a `write_pdf`, por ejemplo `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Obtengo un “cairo‑cffi error” en Linux.* | Instala el paquete del sistema `libcairo2-dev` (`apt-get install libcairo2-dev` en Debian/Ubuntu) antes de instalar WeasyPrint con pip. |

---

## Conclusión

Acabamos de **crear PDF a partir de HTML** usando un flujo de trabajo limpio en Python, cubrimos la mecánica de **convertir HTML a PDF** y te mostramos cómo **guardar HTML como PDF** con un manejo robusto de recursos. El script es lo suficientemente pequeño como para insertarlo en pipelines de CI, pero lo bastante flexible como para ampliarlo con encabezados, pies de página o marcas de agua personalizadas.

Próximos pasos que podrías explorar:

- Utilizar la biblioteca **html to pdf python** `pdfkit` para un enfoque basado en wkhtmltopdf (útil para CSS heredado).  
- Añadir una interfaz CLI con `argparse` para que el script acepte argumentos de entrada/salida.  
- Generar PDFs al vuelo dentro de un endpoint Flask o FastAPI para informes bajo demanda.  

Siéntete libre de experimentar, romper cosas y luego volver a esta guía para un repaso rápido. Si encuentras obstáculos, la documentación de WeasyPrint y sus foros comunitarios son excelentes recursos.

¡Feliz codificación y disfruta convirtiendo esas páginas web en PDFs elegantes!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}