---
category: general
date: 2026-05-31
description: Impara a estrarre SVG da HTML usando Python. Questo tutorial passo‑passo
  mostra come leggere un documento HTML, salvare i file SVG e salvare gli SVG inline
  in modo efficiente.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: it
og_description: Come estrarre SVG da HTML usando Python. Segui questo tutorial per
  leggere il documento HTML, salvare i file SVG e gestire gli SVG inline senza sforzo.
og_title: Come estrarre SVG da HTML con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Come estrarre SVG da HTML con Python – Guida completa
url: /it/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre SVG da HTML con Python – Guida completa

Ti sei mai chiesto **come estrarre SVG** da una pagina HTML caotica senza impazzire? Non sei l'unico. Che tu stia costruendo un web‑scraper, una pipeline di design, o abbia semplicemente bisogno di esportare icone in batch, sapere **come estrarre SVG** è un trucco utile che fa risparmiare tempo e mal di testa.

In questo tutorial ti mostreremo esattamente **come estrarre SVG** usando la libreria Aspose.HTML per Python. Leggeremo il documento HTML, estrarremo sia il markup `<svg>` inline **e** i riferimenti SVG esterni, quindi **salveremo i file SVG** su disco—tutto in uno script ordinato e riutilizzabile. Alla fine avrai una soluzione pronta all'uso che potrai adattare ai tuoi progetti.

> **Consiglio professionale:** Se ti serve solo un rapido sguardo alla pagina, `BeautifulSoup` funziona altrettanto, ma Aspose.HTML ti fornisce un DOM completo, rendendo l'estrazione sia degli SVG inline che di quelli collegati un gioco da ragazzi.

## Cosa ti servirà

* Python 3.8+ (il codice utilizza le f‑string, quindi 3.6+ è il minimo assoluto)
* `pip install aspose-html` – la libreria commerciale che alimenta il nostro parsing HTML
* Una cartella con un file `input.html` che contiene gli SVG che desideri estrarre
* Permessi di scrittura sulla directory di output (la chiameremo `YOUR_DIRECTORY`)

Tutto qui—nessun binario aggiuntivo, nessun browser headless. Semplice, vero?

## Passo 1: Leggere il documento HTML con Aspose.HTML

La prima cosa da fare è **leggere il documento HTML** così da poter attraversare il suo albero DOM. Aspose.HTML ti fornisce un oggetto `HTMLDocument` che si comporta come il `document` di un browser.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Perché è importante:* Caricando l'HTML in un DOM appropriato, eviti le insidie del parsing basato su regex e ottieni gratuitamente metodi come `get_elements_by_tag_name` e `query_selector_all`.

## Passo 2: Raccogliere tutti gli elementi <svg> inline

Gli SVG inline sono quei blocchi `<svg>…</svg>` che si trovano direttamente all'interno dell'HTML. Per **salvare SVG inline** abbiamo solo bisogno del loro HTML esterno.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Nota che stiamo aggiungendo il markup grezzo direttamente in `svg_contents`. Successivamente decideremo se ogni voce è un markup o un percorso file.

## Passo 3: Trovare riferimenti SVG esterni (tag img e object)

Molte pagine collegano file SVG esterni tramite `<img src="icon.svg">` o `<object data="logo.svg">`. Per **estrarre SVG da HTML** dobbiamo catturare anche quegli URL.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Attenzione ai casi limite:* Se l'URL SVG è relativo, dovrai unirlo al percorso base del file HTML. Per brevità assumiamo che l'HTML sia nella stessa cartella dei file SVG.

## Passo 4: Scrivere ogni SVG in un file separato

Ora che abbiamo una lista mista di stringhe di markup e percorsi file, itereremo e **salveremo i file SVG**. Lo script distingue automaticamente tra markup inline e un riferimento a un file esistente.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Ciò che vedrai:** Dopo che lo script termina, `YOUR_DIRECTORY` conterrà file chiamati `svg_0.svg`, `svg_1.svg`, … ognuno contenente o il markup inline originale o una copia dell'SVG esterno.

### Output previsto

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Se un file di riferimento è mancante, lo script stampa un avviso ma continua—quindi un link rotto non interromperà l'intera estrazione.

## Gestire le difficoltà comuni

| Problema | Perché succede | Soluzione rapida |
|----------|----------------|------------------|
| **Gli URL relativi si rompono** | L'attributo `src` può essere `"../assets/icon.svg"` | Usa `os.path.join(os.path.dirname(html_path), src)` per risolvere. |
| **Nomi file duplicati** | Due SVG con lo stesso nome vengono sovrascritti | Includi un hash del contenuto nel nome file (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **SVG inline di grandi dimensioni causano picchi di memoria** | Memorizzare tutto il markup in una lista prima di scrivere | Trasmetti ogni elemento direttamente a un file invece di bufferizzare. |
| **Immagini non‑SVG passano inosservate** | Alcuni tag `<img>` terminano con `.svg?version=1` | Rimuovi le query string prima del controllo dell'estensione (`src.split('?')[0]`). |

## Script completo da copiare‑incollare

Di seguito trovi il programma completo, pronto all'esecuzione. Salvalo come `extract_svg.py`, modifica `YOUR_DIRECTORY` e avvia `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Riepilogo – Come estrarre SVG in poche parole

* **Leggi il documento HTML** con `HTMLDocument`.
* **Raccogli gli `<svg>` inline** tramite `get_elements_by_tag_name`.
* **Individua gli SVG esterni** usando un selettore CSS che termina con `.svg`.
* **Salva ogni elemento**—scrivi il markup direttamente su un file o copia il file di riferimento.
* **Gestisci i casi limite** come percorsi relativi, duplicati e file mancanti.

Questa è l'intera risposta a **come estrarre SVG** da una pagina HTML, racchiusa in un unico script facile da modificare.

## Cosa fare dopo?

Ora che puoi **estrarre SVG** in modo affidabile, considera queste idee successive:

* **Elaborazione batch:** Scorri una directory di file HTML per creare una libreria di icone.
* **Ottimizzazione:** Esegui ogni SVG salvato attraverso SVGO (un ottimizzatore Node.js) per ridurre le dimensioni del file.
* **Conversione:** Usa `cairosvg` o `svglib` per trasformare gli SVG in PNG per browser legacy.
* **Estrazione metadati:** Analizza i tag `<title>` o `<desc>` all'interno di ogni SVG per etichette ricercabili.

Ognuno di questi argomenti tocca le nostre parole chiave secondarie—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—quindi troverai molto materiale da esplorare.

---

*Buon hacking! Se incontri problemi, lascia un commento qui sotto o contattami su GitHub. Il mondo degli SVG è vasto, ma con gli strumenti giusti, estrarli è un gioco da ragazzi.*

## Cosa dovresti imparare dopo?

- [Salva documento SVG in Aspose.HTML per Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Come convertire SVG in XPS con Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Renderizzare un documento SVG in formato PNG in .NET con Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}