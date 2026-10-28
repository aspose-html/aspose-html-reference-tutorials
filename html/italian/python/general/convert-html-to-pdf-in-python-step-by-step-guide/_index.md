---
category: general
date: 2026-08-06
description: Converti HTML in PDF con Python con un esempio completo. Impara a generare
  PDF da HTML, salvare HTML come PDF e gestire i casi limite più comuni.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: it
lastmod: 2026-08-06
og_description: Converti HTML in PDF con Python e automatizza la creazione di documenti.
  Segui questa guida per generare PDF da HTML, salvare HTML come PDF e personalizzare
  l'output.
og_image_alt: Example of convert html to pdf script in Python
og_title: Converti HTML in PDF con Python – tutorial completo
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
title: Converti HTML in PDF con Python – guida passo passo
url: /it/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti HTML in PDF con Python – guida passo‑passo

Se hai bisogno di **convertire HTML in PDF** rapidamente, questo tutorial mostra una soluzione completa in Python. Vedrai come generare PDF da HTML, salvare HTML come PDF e controllare il processo di conversione senza uscire dal tuo codice.

La guida ti accompagna nell'installazione di una libreria affidabile, nel caricamento di un documento HTML, nell'esecuzione della conversione e nella verifica del risultato. Alla fine potrai creare PDF da file HTML in qualsiasi progetto Python, sia che la sorgente sia una pagina statica sia che il markup sia generato dinamicamente.

## Cosa imparerai

* Installare le dipendenze `pdfkit` e `wkhtmltopdf` necessarie per la conversione da HTML a PDF.  
* Caricare un documento HTML da disco o da una stringa.  
* Generare PDF da HTML con opzioni personalizzate di dimensione pagina, margini e codifica.  
* Salvare HTML come PDF usando una singola chiamata di funzione.  
* Gestire casi tipici come risorse mancanti, caratteri Unicode e file di grandi dimensioni.  

**Prerequisiti** – Python 3.8+ e familiarità di base con I/O di file. Non sono richiesti servizi esterni.

## Converti HTML in PDF – flusso di lavoro generale

Il processo di conversione è composto da tre fasi logiche:

1. **Preparazione** – installare il convertitore e assicurarsi che il binario `wkhtmltopdf` sia raggiungibile.  
2. **Gestione dell'input** – leggere il file HTML o costruire il markup programmaticamente.  
3. **Generazione dell'output** – invocare il convertitore, scrivere il file PDF e confermare il risultato.

Ogni fase è trattata in un passaggio dedicato di seguito.

## Passo 1: Installa le librerie richieste

`pdfkit` fornisce un leggero wrapper Python attorno al motore ampiamente usato `wkhtmltopdf`. Installa entrambi con `pip` e verifica il percorso del binario.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Se preferisci un binario portatile, scarica la release appropriata dalla [pagina GitHub di wkhtmltopdf](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) e posizionala in una directory aggiunta al tuo `PATH`. Lo script controllerà il percorso automaticamente in seguito.

## Passo 2: Carica il documento HTML

Puoi leggere un file statico, recuperare contenuti remoti o costruire HTML al volo. L'esempio qui sotto carica un file locale chiamato `sample.html` situato in una directory da te definita.

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

Leggere il file come stringa Unicode garantisce che caratteri come “é”, “ß” o glifi asiatici siano preservati durante la conversione. Questo passaggio è essenziale quando **generi PDF da HTML** contenente testo internazionale.

## Passo 3: Genera PDF da HTML

`pdfkit.from_string` converte una stringa contenente markup HTML in un file PDF. Puoi passare un dizionario di opzioni per controllare dimensione pagina, margini e comportamento di header/footer.

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

La chiamata sopra **crea PDF da file HTML** salvato in `sample.pdf`. Se l'HTML di origine fa riferimento a CSS o immagini locali, il flag `enable‑local‑file‑access` permette a `wkhtmltopdf` di risolvere quelle risorse.

### Perché questo approccio funziona

* `pdfkit` delega il lavoro pesante a `wkhtmltopdf`, che rende l'HTML con il motore WebKit, garantendo alta fedeltà al layout originale.  
* Fornire un dizionario di opzioni ti consente di perfezionare l'output senza modificare l'HTML stesso.  
* Usare `from_string` mantiene il flusso in memoria, utile quando l'HTML è generato al volo.

## Passo 4: Salva HTML come PDF e verifica l'output

Dopo la conversione, potresti voler confermare che il PDF esista e sia leggibile. Lo snippet qui sotto controlla la dimensione del file e apre il PDF con il visualizzatore di sistema predefinito (specifico per piattaforma).

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

L'esecuzione dello script stampa un messaggio di successo e avvia il visualizzatore PDF così da poter confermare immediatamente che il layout corrisponda all'HTML originale. Questo passaggio completa il ciclo **save html as pdf**.

## Passo 5: Opzioni avanzate – crea PDF da file HTML con impostazioni personalizzate

A volte hai un file HTML fisico su disco e preferisci `pdfkit.from_file` invece di caricare il contenuto manualmente. Questo metodo è comodo quando l'HTML include già percorsi relativi complessi.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Puoi anche incorporare una pagina di copertina, un indice o flag di esecuzione JavaScript estendendo il dizionario `options`. Per esempio, per aggiungere una copertina:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Queste modifiche dimostrano **come convertire HTML in PDF** per pipeline di pubblicazione più sofisticate.

## Problemi comuni e come evitarli

| Problema | Causa | Rimedio |
|----------|-------|---------|
| Immagini o CSS non compaiono | `wkhtmltopdf` blocca l'accesso a file locali per impostazione predefinita | Aggiungi `"enable-local-file-access": None` al dizionario delle opzioni |
| Caratteri Unicode diventano illeggibili | Opzione `encoding` mancante o lettura del file con charset errato | Imposta sempre `"encoding": "UTF-8"` e leggi il file HTML con UTF‑8 |
| Il PDF è vuoto | Percorso errato al binario `wkhtmltopdf` | Fornisci il percorso esplicitamente: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| File HTML di grandi dimensioni causano timeout | Timeout predefinito troppo breve | Imposta `"javascript-delay": "2000"` o aumenta il timeout con `"timeout": "60"` |

Affrontare questi problemi garantisce un processo **generate pdf from html** affidabile in diversi ambienti.

## Script completo – esempio end‑to‑end

Salva quanto segue come `html_to_pdf.py` ed eseguilo con `python html_to_pdf.py`. Modifica `YOUR_DIRECTORY` per puntare alla cartella del tuo progetto.

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


## Cosa dovresti imparare dopo?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}