---
category: general
date: 2026-08-06
description: Convertir HTML a PDF en Python con un ejemplo completo. Aprende a generar
  PDF a partir de HTML, guardar HTML como PDF y manejar casos límite comunes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: es
lastmod: 2026-08-06
og_description: Convierte HTML a PDF en Python y automatiza la creación de documentos.
  Sigue esta guía para generar PDF a partir de HTML, guardar HTML como PDF y personalizar
  la salida.
og_image_alt: Example of convert html to pdf script in Python
og_title: Convertir HTML a PDF en Python – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Convertir HTML a PDF en Python – guía paso a paso
url: /es/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML a PDF en Python – guía paso a paso

Si necesitas **convertir HTML a PDF** rápidamente, este tutorial muestra una solución completa en Python. Verás cómo generar PDF a partir de HTML, guardar HTML como PDF y controlar el proceso de conversión sin salir de tu código.

La guía te lleva a través de la instalación de una biblioteca confiable, la carga de un documento HTML, la realización de la conversión y la verificación del resultado. Al final podrás crear PDF a partir de un archivo HTML en cualquier proyecto Python, ya sea que la fuente sea una página estática o un marcado generado dinámicamente.

## Lo que aprenderás

* Instalar las dependencias `pdfkit` y `wkhtmltopdf` requeridas para la conversión de HTML a PDF.  
* Cargar un documento HTML desde disco o desde una cadena.  
* Generar PDF a partir de HTML con opciones personalizadas de tamaño de página, márgenes y codificación.  
* Guardar HTML como PDF usando una única llamada a función.  
* Manejar casos típicos como recursos faltantes, caracteres Unicode y archivos grandes.  

**Prerequisitos** – Python 3.8+ y familiaridad básica con I/O de archivos. No se requieren servicios externos.

## Convertir HTML a PDF – flujo de trabajo general

El proceso de conversión consta de tres fases lógicas:

1. **Preparación** – instalar el conversor y asegurarse de que el binario `wkhtmltopdf` sea accesible.  
2. **Manejo de la entrada** – leer el archivo HTML o construir el marcado programáticamente.  
3. **Generación de la salida** – invocar el conversor, escribir el archivo PDF y confirmar el resultado.

Cada fase se cubre en un paso dedicado a continuación.

## Paso 1: Instalar las bibliotecas requeridas

`pdfkit` proporciona un contenedor ligero de Python alrededor del motor ampliamente usado `wkhtmltopdf`. Instala ambos con `pip` y verifica la ruta del binario.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Si prefieres un binario portátil, descarga la versión adecuada desde la [página de GitHub de wkhtmltopdf](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) y colócala en un directorio que esté añadido a tu `PATH`. El script comprobará la ruta automáticamente más adelante.

## Paso 2: Cargar el documento HTML

Puedes leer un archivo estático, obtener contenido remoto o construir HTML sobre la marcha. El ejemplo a continuación carga un archivo local llamado `sample.html` ubicado en el directorio que definas.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Leer el archivo como una cadena Unicode garantiza que caracteres como “é”, “ß” o glifos asiáticos se conserven durante la conversión. Este paso es esencial cuando **generas PDF a partir de HTML** que contiene texto internacional.

## Paso 3: Generar PDF a partir de HTML

`pdfkit.from_string` convierte una cadena que contiene marcado HTML en un archivo PDF. Puedes pasar un diccionario de opciones para controlar el tamaño de página, los márgenes y el comportamiento de encabezados/pies de página.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

La llamada anterior **crea PDF a partir del archivo HTML** almacenado en `sample.pdf`. Si el HTML de origen hace referencia a CSS o imágenes locales, la bandera `enable‑local‑file‑access` permite que `wkhtmltopdf` resuelva esos recursos.

### Por qué funciona este enfoque

* `pdfkit` delega el trabajo pesado a `wkhtmltopdf`, que renderiza HTML con el motor WebKit, garantizando alta fidelidad al diseño original.  
* Proveer un diccionario de opciones te permite afinar la salida sin modificar el HTML mismo.  
* Usar `from_string` mantiene el flujo en memoria, lo cual es útil cuando el HTML se genera sobre la marcha.

## Paso 4: Guardar HTML como PDF y verificar la salida

Después de la conversión, puede que quieras confirmar que el PDF existe y es legible. El fragmento a continuación verifica el tamaño del archivo y abre el PDF con el visor predeterminado del sistema (dependiendo de la plataforma).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Ejecutar el script muestra un mensaje de éxito y lanza el visor de PDF para que puedas confirmar instantáneamente que el diseño coincide con el HTML original. Este paso completa el ciclo de **guardar html como pdf**.

## Paso 5: Opciones avanzadas – crear PDF a partir de archivo HTML con configuraciones personalizadas

A veces tienes un archivo HTML físico en disco y prefieres `pdfkit.from_file` en lugar de cargar el contenido tú mismo. Este método es práctico cuando el HTML ya incluye rutas relativas complejas.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

También puedes incrustar una página de portada, tabla de contenidos o banderas de ejecución de JavaScript ampliando el diccionario `options`. Por ejemplo, para añadir una portada:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Estos ajustes demuestran **cómo convertir HTML a PDF** para pipelines de publicación más sofisticados.

## Problemas comunes y cómo evitarlos

| Problema | Causa | Solución |
|----------|-------|----------|
| Las imágenes o CSS no aparecen | `wkhtmltopdf` bloquea el acceso a archivos locales por defecto | Añade `"enable-local-file-access": None` al diccionario de opciones |
| Los caracteres Unicode aparecen corruptos | Falta la opción `encoding` o se lee el archivo con la codificación incorrecta | Siempre establece `"encoding": "UTF-8"` y lee el archivo HTML con UTF‑8 |
| El PDF está en blanco | Ruta incorrecta al binario `wkhtmltopdf` | Proporciona la ruta explícitamente: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Archivos HTML grandes provocan timeout | El timeout predeterminado es demasiado corto | Establece `"javascript-delay": "2000"` o incrementa el timeout con `"timeout": "60"` |

Abordar estos problemas asegura un proceso fiable de **generar pdf from html** en diferentes entornos.

## Script completo – ejemplo de extremo a extremo

Guarda lo siguiente como `html_to_pdf.py` y ejecútalo con `python html_to_pdf.py`. Ajusta `YOUR_DIRECTORY` para que apunte a la carpeta de tu proyecto.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}