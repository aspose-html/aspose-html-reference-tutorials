---
category: general
date: 2026-10-21
description: Aprende a convertir HTML a PNG rápidamente. Este tutorial también cubre
  cómo exportar una página web a PNG y convertir un archivo HTML a PNG con Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: es
lastmod: 2026-10-21
og_description: Convierte HTML a PNG con Python. Sigue esta guía clara para exportar
  una página web a PNG, manejar casos límite y automatizar la generación de imágenes.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Convertir HTML a PNG en Python – guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Cómo convertir HTML a PNG en Python – guía paso a paso
url: /es/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML a PNG en Python – guía completa de programación

Si necesitas **convertir HTML a PNG**, esta guía te muestra una forma fiable de hacerlo con Python puro. Ya sea que estés exportando un informe estático, generando miniaturas para una galería, o automatizando capturas de pantalla para pruebas, obtendrás una solución completa y ejecutable en minutos.

También verás cómo **exportar una página web a PNG**, comprenderás la diferencia entre convertir un archivo HTML y una URL en vivo, y aprenderás las mejores prácticas para manejar páginas grandes o contenido dinámico. No se requieren servicios externos, solo unos pocos paquetes de Python y un script breve.

## Requisitos previos

- Python 3.9+ instalado (el código funciona en Windows, macOS y Linux)
- Acceso a una terminal o símbolo del sistema
- Familiaridad básica con el gestor de paquetes de Python (`pip`)

Necesitarás el paquete `imgkit` (un contenedor ligero alrededor de `wkhtmltoimage`) y el binario `wkhtmltoimage` en sí. Ambos son gratuitos y de código abierto.

## Paso 1: Instalar las herramientas necesarias

El primer paso es instalar `wkhtmltoimage` y el contenedor de Python que se comunica con él.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Por qué este paso es importante** – `wkhtmltoimage` renderiza HTML usando el motor WebKit, produciendo PNGs píxel‑perfectos. `imgkit` simplemente reenvía tus opciones al binario, por lo que obtienes la misma calidad que tendrías en un navegador.

## Paso 2: Verificar la instalación

Ejecuta una verificación rápida para confirmar que el binario es accesible desde Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Si el script muestra la ruta a `wkhtmltoimage`, estás listo para convertir HTML a PNG. Si obtienes un `OSError`, verifica que el binario esté en el `PATH` de tu sistema.

## Paso 3: Escribir una función de conversión reutilizable

Encapsular la lógica en una función facilita **convertir un archivo HTML a PNG** o **exportar una página web a PNG** desde cualquier parte de tu proyecto.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Por qué envolvemos tanto `from_file` como `from_url`** – La misma función ahora soporta **cómo convertir HTML a imagen** para archivos locales y páginas web en vivo, manteniendo tu código DRY (Don’t Repeat Yourself).

## Paso 4: Convertir un archivo HTML local a PNG

Coloca un archivo HTML llamado `sample.html` en una carpeta llamada `assets`. Luego llama al ayudante que acabamos de definir:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Salida esperada

Ejecutar el script muestra:

```
✅ Successfully saved PNG to: output/sample.png
```

Un nuevo archivo `output/sample.png` ahora contiene una captura píxel‑perfecta de `sample.html`. Abrirlo en cualquier visor de imágenes muestra la página renderizada exactamente como aparecería en un navegador.

## Paso 5: Exportar una página web en vivo a PNG

Si necesitas **exportar una página web a PNG** para una URL que cambia frecuentemente (p. ej., un panel), simplemente pasa la cadena URL en lugar de una ruta de archivo.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### ¿Por qué ajustar el tamaño del viewport?

Las páginas web diseñadas para pantallas de escritorio a menudo se ven apretadas si se renderizan con un ancho pequeño. Al aumentar las opciones `width` y `height`, capturas el diseño completo, lo cual es especialmente útil para tareas de **exportar página web a PNG**.

## Paso 6: Manejar casos límite comunes

### 6.1 Páginas grandes o desplazamiento infinito

Para páginas que cargan contenido de forma perezosa (p. ej., desplazamiento infinito), aumenta el retraso de JavaScript y, opcionalmente, establece un viewport más grande:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Páginas protegidas por autenticación

Si una página requiere una cookie de sesión, puedes incrustar el encabezado de cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Imágenes o fuentes faltantes

`wkhtmltoimage` respeta la bandera `--disable-local-file-access` por seguridad. Si tu HTML hace referencia a recursos locales, habilítalos explícitamente:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Paso 7: Verificar el resultado programáticamente (opcional)

A veces necesitas confirmar que el PNG se generó correctamente (p. ej., en pipelines de CI). El siguiente fragmento verifica el tamaño del archivo y sus dimensiones:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Si el PNG pasa estas verificaciones, puedes usarlo con seguridad en procesos posteriores como generación de PDF, adjuntos de correo electrónico o pipelines de aprendizaje automático.

## Conclusión

Ahora tienes un método completo y listo para producción para **convertir HTML a PNG** usando Python. La guía cubrió:

- Instalación de `wkhtmltoimage` y `imgkit`
- Verificación del entorno
- Una función reutilizable `convert_html_to_png` que maneja tanto archivos locales como URLs
- Ejemplos del mundo real para **exportar página web a PNG**, **cómo convertir HTML a imagen**, y **convertir archivo HTML a PNG**
- Manejo de casos límite para páginas grandes, autenticación y recursos locales
- Pasos de verificación opcionales para pipelines CI/CD

Siéntete libre de experimentar con opciones adicionales de `imgkit` —como `zoom`, `crop-h` o `crop-w`— para afinar la salida según tu caso de uso específico. Como próximos pasos, podrías explorar:

- Convertir los PNGs en un informe PDF (biblioteca `img2pdf`)
- Automatizar la conversión por lotes de una carpeta completa de archivos HTML
- Usar Selenium para páginas que requieren renderizado completo del navegador (p. ej., frameworks JavaScript pesados)

¡Feliz codificación y disfruta de las capturas de pantalla píxel‑perfectas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convertir HTML a PNG – Guía completa de Python](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convertir HTML a PNG en Python – Guía completa de guardado en streaming](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convertir SVG a PNG en Python usando Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}