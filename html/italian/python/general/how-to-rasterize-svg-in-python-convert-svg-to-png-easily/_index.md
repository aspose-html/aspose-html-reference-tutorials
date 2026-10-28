---
category: general
date: 2026-10-28
description: Scopri come rasterizzare SVG in Python e convertire SVG in PNG con uno
  script semplice usando CairoSVG. Salva SVG come PNG in pochi secondi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: it
lastmod: 2026-10-28
og_description: 'Come rasterizzare SVG in Python: questa guida ti mostra come convertire
  SVG in PNG usando CairoSVG, coprendo installazione, codice e risoluzione dei problemi.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Come rasterizzare SVG in Python – guida rapida da SVG a PNG
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: Come rasterizzare SVG in Python – converti SVG in PNG facilmente
url: /it/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rasterizzare SVG in Python – convertire SVG in PNG facilmente

Se hai bisogno di **how to rasterize svg** per una web‑app, un report o una build automatizzata, questa guida ti offre una soluzione pronta all'uso. Vedrai come **convert svg to png** con poche righe di Python, e il risultato è un PNG nitido che puoi memorizzare o servire immediatamente.

Il tutorial copre tutto, dall'installazione della libreria necessaria alla gestione dei casi limite come file di grandi dimensioni o impostazioni DPI personalizzate. Alla fine, sarai in grado di **save svg as png**, **export svg as png**, e integrare il processo in qualsiasi workflow Python.

## Cosa ti servirà

- Python 3.8+ (il codice funziona su 3.9, 3.10 e versioni successive)
- `pip` per installare i pacchetti
- Un file SVG locale (ad es., `logo.svg`) che desideri rasterizzare
- Opzionale: ambiente virtuale per una gestione pulita delle dipendenze

> **Pro tip:** Usare un ambiente virtuale (`python -m venv .venv`) isola la dipendenza CairoSVG dai tuoi pacchetti Python globali.

## Come rasterizzare SVG in Python

Il modo più semplice per **how to rasterize svg** è con la libreria **CairoSVG**. CairoSVG legge l'XML SVG, lo renderizza con il motore grafico Cairo e scrive l'immagine raster in PNG, PDF o altri formati bitmap.

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### Perché CairoSVG?

- **Pure Python**: Nessun bisogno di strumenti da riga di comando esterni una volta installato il pacchetto.
- **SVG‑compliant**: Supporta la maggior parte delle funzionalità SVG 1.1, inclusi gradienti, maschere e testo.
- **Flexible output**: Oltre a PNG, puoi esportare in PDF, PS o anche byte grezzi.

### Analisi passo‑passo

1. **Install the library** – `pip install cairosvg` scarica le binding compilate di Cairo.  
2. **Import the module** – `import cairosvg` ti dà accesso all'helper `svg2png`.  
3. **Call `svg2png`** – Passa il percorso del file SVG (o un URL) e il percorso di destinazione PNG. Gli opzionali `output_width`, `output_height` e `dpi` ti permettono di controllare dimensione e risoluzione.  
4. **Handle errors** – Il blocco `try/except` stampa un messaggio chiaro se l'SVG è malformato o la directory di output non è scrivibile.

## Convertire SVG in PNG con CairoSVG

Se ti serve solo una singola riga per una conversione rapida, il frammento seguente fa il lavoro senza la funzione wrapper:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Questa è l'illustrazione più concisa di **convert svg to png**. Legge `logo.svg` dalla directory corrente e scrive `logo.png` accanto.

## Salvare SVG come PNG – verifica il risultato

Dopo aver eseguito lo script, dovresti vedere un file PNG nel percorso di destinazione. Aprilo con qualsiasi visualizzatore di immagini per confermare:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Se il PNG appare sfocato, aumenta l'argomento `dpi` (ad es., `dpi=300`) per generare un raster ad alta risoluzione.

## Esportare SVG come PNG in diversi formati

CairoSVG può anche produrre **PDF**, **PostScript** o byte **PNG** grezzi. Di seguito un esempio di esportazione in un oggetto `BytesIO` quando hai bisogno dell'immagine in memoria (ad es., per una risposta Flask):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Casi limite che potresti incontrare

| Situation                               | Recommended handling |
|----------------------------------------|----------------------|
| **Large SVG (dimensioni megapixel)**   | Aumenta `dpi` o imposta esplicitamente `output_width`/`output_height` per evitare picchi di memoria. |
| **Font mancanti**                      | Installa i font richiesti sul sistema o incorporali nell'SVG usando i tag `<style>`. |
| **Problemi di trasparenza**            | PNG preserva l'alpha di default; se ti serve uno sfondo solido, passa `background_color="#FFFFFF"` a `svg2png`. |
| **Elaborazione batch**                 | Itera su una directory di SVG e chiama `rasterize_svg` per ogni file. |

## Esempio completo funzionante

Di seguito uno script minimale e autonomo che puoi copiare‑incollare in un file chiamato `svg_to_png.py` ed eseguire immediatamente.

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Eseguendo `python svg_to_png

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come rasterizzare SVG in Python – Guida completa](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convertire SVG in PNG in Python – Guida all'esportazione ad alta risoluzione](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Creare documento SVG in Python – Guida alla conversione SVG in PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}