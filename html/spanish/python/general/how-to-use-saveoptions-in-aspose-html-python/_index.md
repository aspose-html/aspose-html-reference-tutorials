---
category: general
date: 2026-07-27
description: Cómo usar SaveOptions en Aspose.HTML (Python) para convertir una página
  HTML grande y aplicar la gestión de recursos de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: es
lastmod: 2026-07-27
og_description: Cómo usar SaveOptions en Aspose.HTML (Python) le permite convertir
  una página HTML grande mientras aplica la gestión de recursos para obtener resultados
  limpios y rápidos.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Cómo usar SaveOptions en Aspose.HTML – Guía de Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Cómo usar SaveOptions en Aspose.HTML (Python)
url: /es/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar SaveOptions en Aspose.HTML (Python)

Cómo usar SaveOptions en Aspose.HTML para Python es una pregunta que muchos desarrolladores hacen al trabajar con archivos HTML masivos. Si necesitas **convertir una página HTML grande** mientras mantienes un control estricto sobre **apply resource handling**, estás en el lugar correcto.  

En este tutorial recorreremos un escenario del mundo real: tomar una página HTML voluminosa, limitar la profundidad a la que se extraen los recursos anidados y, finalmente, guardar (o convertir) el resultado con un control cristalino. Sin referencias vagas, solo un ejemplo completo y ejecutable que puedes copiar y pegar en tu proyecto hoy.

> **Consejo profesional:** `SaveOptions` de Aspose.HTML no solo funciona para guardar de nuevo en HTML, sino también para convertir a PDF, PNG o incluso DOCX. El mismo patrón que cubrimos a continuación se aplica a todos esos formatos.

---

## Lo que necesitarás

- **Python 3.8+** (el código usa anotaciones de tipo pero funciona en cualquier versión reciente)  
- **Aspose.HTML for Python via .NET** – instala con `pip install aspose-html`  
- Un **archivo HTML grande** que deseas reducir o transformar (el ejemplo usa `big_page.html`)  
- Una cantidad modesta de espacio en disco para el archivo de salida  

Eso es todo—sin bibliotecas adicionales, sin herramientas de compilación pesadas.

---

## Cómo usar SaveOptions con opciones de Resource Handling

Este es el núcleo del asunto. Crearemos una instancia de `SaveOptions`, adjuntaremos un objeto `ResourceHandlingOptions` que indica a Aspose.HTML qué tan profundo debe seguir los recursos enlazados, y luego pasaremos todo al método `save` del documento.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Por qué funciona esto:**  

- `HTMLDocument` carga el archivo original, analizando cada `<img>`, `<link>`, `<script>`, etc.  
- `ResourceHandlingOptions.max_handling_depth` indica al motor que deje de seguir los recursos después de tres niveles de anidación—perfecto para evitar bucles infinitos en páginas que incrustan otras páginas.  
- `SaveOptions` es el contenedor que lleva tanto el formato de salida (HTML por defecto) como las reglas de manejo de recursos.  
- Finalmente, `doc.save` escribe el nuevo archivo, aplicando las reglas que acabamos de establecer.

Cuando ejecutes el script, verás un nuevo archivo en `big_page_processed.html`. Ábrelo en un navegador; notarás que todas las imágenes, estilos y scripts hasta tres niveles de profundidad siguen presentes, mientras que las referencias más profundas se han eliminado. Esto reduce drásticamente el tamaño del archivo sin romper el diseño principal de la página—exactamente lo que necesitas cuando **convertir una página HTML grande** para uso offline o envío por correo electrónico.

---

## Convertir una página HTML grande de forma eficiente

Si tu objetivo es *convertir una página HTML grande* a una versión más ligera, el fragmento anterior ya realiza la mayor parte del trabajo. Sin embargo, podrías querer cambiar el formato de salida por completo. Aspose.HTML lo hace con una sola línea:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Simplemente reemplaza la propiedad `format` con `"PNG"`, `"JPEG"` o `"DOCX"` y tendrás una canalización de conversión completa. Las mismas reglas de **apply resource handling** permanecen intactas, por lo que el PDF resultante no incrustará cada archivo CSS externo del sitio original—solo aquellos dentro de la profundidad de tres niveles que definiste.

---

## Aplicar Resource Handling a recursos anidados

Profundicemos un poco más en **apply resource handling** de manera eficaz. Supongamos que tu HTML contiene una hoja de estilo que a su vez importa otras hojas de estilo, cada una cargando imágenes. Sin un límite de profundidad, Aspose.HTML podría seguir la cadena indefinidamente, inflando el uso de memoria y CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – No se obtienen recursos externos; obtienes un esqueleto HTML básico.  
- **Depth 1** – Solo se incluyen recursos de primer orden (etiquetas `<img>` directas, archivos CSS inmediatos).  
- **Depth 2+** – Se respeta la anidación más profunda, útil para sitios complejos donde los estilos dependen de otros estilos.

Elige la profundidad que coincida con tu escenario de **convertir una página HTML grande**. Para boletines de correo electrónico, la profundidad 1 suele ser suficiente. Para un archivo local, la profundidad 3 (como en el ejemplo principal) ofrece un buen equilibrio.

---

## Ejemplo completo y funcional – De principio a fin

A continuación tienes un script autónomo que puedes colocar en un archivo llamado `process_html.py`. Incluye manejo de errores, registro (logging) y un pequeño asistente que muestra la reducción de tamaño que lograste.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Salida esperada (consola):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Abre el archivo procesado; verás una página más ligera que aún se parece a la original. Si cambiaste `fmt` a `"PDF"`, la consola informará el tamaño del archivo PDF y podrás abrirlo en cualquier visor de PDF.

---

## Preguntas frecuentes y casos límite

- **¿Qué pasa si la página referencia recursos a través de HTTPS que requieren autenticación?**  
  Aspose.HTML sigue redirecciones pero no enviará credenciales automáticamente. Puedes pre‑descargar esos activos o usar un manejador `WebRequest` personalizado (más allá del alcance de esta guía).

- **¿Puedo preservar CSS inline mientras elimino archivos externos?**  
  Sí—establece `resource_options.max_handling_depth = 0`. Esto omite los archivos externos pero deja intactos los bloques `<style>`.

- **¿Qué pasa con imágenes muy grandes que siguen inflando la salida?**  
  Después de guardar, puedes ejecutar una pasada secundaria con Pillow para reducir el tamaño de las imágenes, o dejar que las opciones de compresión de imágenes incorporadas de Aspose.HTML lo manejen (usa `save_options.image_quality`).

- **¿Se aplica el límite de profundidad por tipo de recurso?**  
  El límite es global para todos los tipos de recursos (imágenes, scripts, estilos). Si necesitas un control granular, deberías filtrar los recursos manualmente después de cargar el documento.

---

## Conclusión

Ahora tienes una comprensión sólida de **cómo usar SaveOptions** en Aspose.HTML

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo convertir HTML a PDF en Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Cómo convertir HTML a MHTML con Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Cómo usar Aspose para renderizar HTML a PNG – Guía paso a paso](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}