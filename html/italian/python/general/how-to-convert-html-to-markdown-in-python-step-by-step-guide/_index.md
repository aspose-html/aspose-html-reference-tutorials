---
category: general
date: 2026-10-02
description: converti HTML in Markdown in Python con un esempio completo. Scopri come
  salvare HTML come Markdown, scegliere i formattatori e abilitare funzionalità specifiche.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: it
lastmod: 2026-10-02
og_description: converti HTML in Markdown in Python con codice pratico, opzioni di
  formattazione e flag di funzionalità. Segui questa guida per salvare rapidamente
  l'HTML come Markdown.
og_image_alt: Screenshot of Python code converting HTML to Markdown
og_title: Converti HTML in Markdown con Python – tutorial completo
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: Enabling only the needed features
    text: You can fine‑tune the output by turning on specific feature flags. In this
      example we keep **links** and **paragraphs** while disabling images, tables,
      and other constructs.
  - name: Expected output (`output.md`)
    text: '```markdown # Project Overview'
  - name: Missing or malformed `href` attributes
    text: 'If an `<a>` tag lacks a valid `href`, the converter inserts the link text
      without a URL. To preserve readability, you may want to post‑process the Markdown:'
  - name: Converting large HTML files
    text: 'For multi‑megabyte HTML files, stream the input to avoid loading the entire
      markup into memory:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: Come convertire HTML in Markdown con Python – guida passo passo
url: /it/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire HTML in Markdown in Python – guida passo‑passo

Se hai bisogno di **convertire HTML in Markdown**, questa guida ti mostra una soluzione completa e eseguibile in Python. Vedrai come **salvare HTML come Markdown**, scegliere il formatter corretto e abilitare solo le funzionalità di cui hai bisogno.

Convertire HTML in Markdown è un'operazione comune quando desideri documentazione leggera, contenuti per siti statici o file di testo sotto controllo di versione. Questo tutorial copre tutto, dall'installazione della libreria alla gestione dei casi limite, così potrai applicare la tecnica a qualsiasi sorgente HTML.

## Prerequisiti

* Python 3.8 o versioni successive installato.
* Accesso a `pip` per installare pacchetti di terze parti.
* Familiarità di base con i tag HTML e la sintassi Markdown.

Non sono richieste dipendenze di sistema aggiuntive perché la libreria di conversione è puramente Python.

## Installa la libreria GroupDocs Conversion

Il campione di codice utilizza il pacchetto Python **GroupDocs.Conversion**, che fornisce `HTMLDocument`, `MarkdownSaveOptions` e `Converter`. Installalo con:

```bash
pip install groupdocs-conversion
```

> **Suggerimento:** Usa un ambiente virtuale (`python -m venv venv`) per mantenere il pacchetto isolato dagli altri progetti.

## Passo 1: Crea un `HTMLDocument` da una stringa

Il primo passo è avvolgere il tuo HTML grezzo in un'istanza di `HTMLDocument`. Questo oggetto astrae la sorgente, sia che provenga da una stringa, un file o un URL remoto.

```python
from groupdocs.conversion import HTMLDocument

# Example HTML – you can replace this with any valid markup
html_content = "<h1>Title</h1><p>Hello <a href='https://example.com'>world</a></p>"
html_doc = HTMLDocument(html_content)
```

*Perché è importante:* `HTMLDocument` analizza il markup una sola volta, consentendo al convertitore di lavorare con una rappresentazione normalizzata invece del testo grezzo.

## Passo 2: Configura `MarkdownSaveOptions`

`MarkdownSaveOptions` ti permette di controllare il formato di output e quali funzionalità Markdown vengono generate. La libreria supporta due formatter:

* **DEFAULT** – Markdown standard compatibile con CommonMark.
* **GIT** – Markdown in stile Git (aggiunge tabelle, barrato, ecc.).

Per la maggior parte degli scenari di controllo di versione, è preferito il formatter **GIT**.

```python
from groupdocs.conversion import MarkdownSaveOptions

md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT
```

### Abilitare solo le funzionalità necessarie

Puoi perfezionare l'output attivando flag di funzionalità specifici. In questo esempio manteniamo **links** e **paragraphs** disabilitando immagini, tabelle e altre costruzioni.

```python
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Perché è importante:* Limitare le funzionalità riduce la dimensione del file generato e previene elementi Markdown inattesi che gli strumenti a valle potrebbero non supportare.

## Passo 3: Converti il documento

Con l'`HTMLDocument` di origine e le `MarkdownSaveOptions` configurate, la conversione è una singola chiamata a `Converter.convert`. Fornisci un percorso assoluto o relativo per il file di output.

```python
from groupdocs.conversion import Converter

output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)
```

Al termine della chiamata, `output.md` contiene la rappresentazione Markdown dell'HTML originale.

## Script completo che puoi eseguire oggi

Di seguito trovi lo script completo e autonomo che incorpora tutti i passaggi precedenti. Salvalo come `html_to_md.py` ed esegui `python html_to_md.py`.

```python
# html_to_md.py
# Complete example that converts HTML to Markdown using GroupDocs.Conversion

from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# 1️⃣  Create the HTMLDocument – replace the string with your own HTML source
html_content = """
<h1>Project Overview</h1>
<p>Welcome to the <a href="https://github.com/example">example repo</a>.</p>
<ul>
  <li>Feature A</li>
  <li>Feature B</li>
</ul>
"""
html_doc = HTMLDocument(html_content)

# 2️⃣  Prepare Markdown save options
md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT  # Git‑flavored Markdown
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH |
    MarkdownSaveOptions.Features.LIST      # include lists for this example
)

# 3️⃣  Perform the conversion
output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)

print(f"Conversion complete – Markdown saved to {output_path}")
```

### Output previsto (`output.md`)

```markdown
# Project Overview

Welcome to the [example repo](https://github.com/example).

- Feature A
- Feature B
```

L'output corrisponde alla struttura HTML originale mostrando solo le funzionalità che abbiamo abilitato (links, paragraphs e lists).

## Gestione dei casi limite comuni

### Attributi `href` mancanti o malformati

Se un tag `<a>` manca di un `href` valido, il convertitore inserisce il testo del link senza URL. Per preservare la leggibilità, potresti voler post‑processare il Markdown:

```python
import re

def fix_broken_links(md_text):
    # Replace stray brackets like [text]() with just the text
    return re.sub(r'\[([^\]]+)\]\(\)', r'\1', md_text)

with open(output_path, "r+", encoding="utf-8") as f:
    content = f.read()
    f.seek(0)
    f.write(fix_broken_links(content))
    f.truncate()
```

### Conversione di file HTML di grandi dimensioni

Per file HTML di più megabyte, trasmetti lo stream di input per evitare di caricare l'intero markup in memoria:

```python
with open("large_input.html", "r", encoding="utf-8") as src:
    html_doc = HTMLDocument(src.read())
```

Il processo di conversione rimane invariato perché `HTMLDocument` astrae la dimensione della sorgente.

## Formatter alternativi

Se preferisci CommonMark puro invece dell'output in stile Git, cambia il formatter:

```python
md_opts.formatter = MarkdownSaveOptions.Formatter.DEFAULT
```

Questo produce un file Markdown più minimale, utile quando si puntano piattaforme che non supportano le estensioni Git.

## Attività correlate che potresti esplorare dopo

* **Convert Markdown back to HTML** – utile per l'anteprima della documentazione.
* **Export HTML to PDF** – un altro flusso di lavoro comune correlato alla **html to markdown conversion**.
* **Batch process a folder of HTML files** – itera sui file e riutilizza la stessa istanza di `MarkdownSaveOptions`.

Tutte queste seguono lo stesso schema: crea un documento sorgente, configura le opzioni di salvataggio e chiama `Converter.convert`.

## Conclusione

Ora sai come **convertire HTML in Markdown** in Python, come **salvare HTML come Markdown** con un controllo preciso delle funzionalità, e perché la scelta del formatter giusto è importante per gli strumenti a valle. L'esempio dimostra un approccio pulito e riutilizzabile che funziona per stringhe singole, file o URL, e include suggerimenti per gestire link mancanti e input di grandi dimensioni.

Sentiti libero di sperimentare con ulteriori `MarkdownSaveOptions.Features` (ad es., `IMAGE`, `TABLE`) per adattare l'output alle esigenze del tuo progetto. Se hai trovato utile questa guida, condividila con i colleghi o collegala dalla documentazione del tuo progetto. Buona conversione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}