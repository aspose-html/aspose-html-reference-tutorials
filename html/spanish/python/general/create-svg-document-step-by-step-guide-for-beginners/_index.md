---
category: general
date: 2026-07-02
description: Crea documentos SVG rápidamente con Python. Aprende a guardar archivos
  SVG, generar una imagen SVG básica y exportar SVG desde el código en solo unas pocas
  líneas.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: es
og_description: Crea documentos SVG fácilmente. Esta guía muestra cómo generar SVG,
  guardar archivos SVG y exportar SVG desde el código con un ejemplo limpio en Python.
og_title: Crear documento SVG – Tutorial rápido de Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Crear documento SVG – Guía paso a paso para principiantes
url: /es/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento SVG – Guía paso a paso para principiantes

¿Alguna vez te has preguntado cómo **create SVG document** sin abrir un editor gráfico? No eres el único. Ya sea que necesites un pequeño ícono para una página web o un gráfico dinámico generado al vuelo, poder **create SVG document** programáticamente ahorra tiempo y mantiene todo bajo control de versiones.

En este tutorial recorreremos un ejemplo completo y ejecutable que te muestra exactamente cómo **create SVG document**, **save SVG file**, y hasta responde la persistente pregunta “**how to generate SVG**” que surge cuando automatizas gráficos. Al final tendrás un cuadrado rojo en el disco y sabrás cómo **export SVG from code** para cualquier proyecto futuro.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener:

* Python 3.9 o superior (la biblioteca estándar hace todo el trabajo pesado)
* Un editor de texto o IDE que prefieras—VS Code, PyCharm, o incluso Notepad sirven
* Permiso de escritura en una carpeta donde **save SVG file** (usaremos un directorio `output/`)

No se requieren paquetes externos, así que la configuración lleva literalmente un par de minutos.

## Paso 1: Configurar las funciones auxiliares SVG (Crear el documento)

Primero lo primero: necesitamos un pequeño ayudante que construya la estructura XML detrás de un SVG. Piensa en esto como el lienzo sobre el que más tarde añadiremos elementos **create basic SVG image**.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Por qué este paso es importante:** La clase `SVGDocument` abstrae la manipulación de XML de bajo nivel. Al envolverla en una clase mantenemos el resto del código limpio, lo cual es una buena práctica cuando **export SVG from code** en aplicaciones más grandes.

## Paso 2: Añadir un rectángulo – El núcleo de un ejemplo **Create Basic SVG Image**

Ahora que tenemos un objeto documento, añadamos un cuadrado rojo. Este es el corazón de la parte **create basic SVG image** del tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Explicación:**  
* Las coordenadas `x` y `y` del rectángulo le dan un margen de 10 píxeles para que no quede pegado al borde.  
* Usar un diccionario para los atributos hace que el código sea legible y refleja cómo **save SVG file** atributos en cualquier formato basado en XML.  
* Si alguna vez necesitas **how to generate SVG** formas distintas a rectángulos, simplemente cambia la etiqueta a `"circle"` o `"path"` y ajusta el diccionario de atributos en consecuencia.

## Paso 3: Persistir el SVG – Finalmente **Save SVG File** en disco

Hemos construido el documento en memoria; ahora lo escribiremos. Este es el momento en que el abstracto **create SVG document** se convierte en un archivo tangible que puedes abrir en un navegador.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Lo que verás:** Abrir `output/square.svg` en Chrome, Firefox o cualquier visor compatible con SVG mostrará un simple cuadrado rojo con un delgado borde blanco (el fondo del lienzo SVG). Esa es la prueba de que hemos **exported SVG from code** con éxito.

## Script completo – Solución de un solo archivo

A continuación tienes el script completo, listo para copiar y pegar en `create_svg.py`. Ejecutar `python create_svg.py` generará el archivo descrito arriba.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Salida esperada

Ejecutar el script imprime:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

Y el `square.svg` generado se ve así (vista simplificada):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Abrir el archivo renderiza un cuadrado rojo nítido—exactamente lo que nos propusimos **create basic SVG image**.

## Extender el ejemplo – Preguntas comunes respondidas

### ¿Cómo puedo añadir texto u otras formas?

Simplemente llama a `svg.create_element("text", {...})` o `svg.create_element("circle", {...})` y añádelos igual que el rectángulo. La misma lógica de **how to generate SVG** se aplica.

### ¿Qué pasa si necesito **export SVG from code** con un fondo transparente?

Elimina cualquier atributo `fill` del elemento raíz `<svg>` o establece `fill="none"` en las formas que deban ser transparentes. El XML sigue siendo válido; los navegadores renderizarán la transparencia automáticamente.

### ¿Puedo **save SVG file** con formato pretty‑printed?

`ElementTree` escribe XML compacto por defecto. Para una versión legible por humanos, puedes usar `xml.dom.minidom` para reformatear:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Reemplaza `svg.save(output_path)` por `pretty_save(svg, output_path)`.

### ¿Qué hay de rendimiento para SVGs grandes?

Al generar miles de elementos, considera construir primero una lista de objetos `ET.Element` y luego extender la raíz de una sola vez. Esto reduce el número de mutaciones del árbol y acelera la operación **save SVG file**.

## Consejos profesionales y trampas

* **Consejo profesional:** Siempre usa rutas absolutas (o `pathlib.Path`) cuando **saving SVG file**; las rutas relativas pueden romperse cuando tu script se ejecuta desde un directorio de trabajo diferente.  
* **Cuidado con:** Olvidar registrar el espacio de nombres SVG. Sin `ET.register_namespace("", SVGDocument.SVG_NS)`, la salida contendrá un prefijo redundante `ns0` que algunos navegadores interpretan incorrectamente.  
* **Error típico:** Mezclar tipos entero y cadena en los valores de atributos. XML espera cadenas, así que convertimos todo con `str()`—la clase auxiliar lo hace por ti, pero si la evitas podrías obtener un `TypeError`.  

## Conclusión

Acabamos de recorrer un ejemplo completo, de extremo a extremo, que muestra cómo **create SVG document**, **save SVG file**, y responder

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}