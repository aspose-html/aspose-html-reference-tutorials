---
category: general
date: 2026-10-21
description: Scopri come convertire rapidamente HTML in PNG. Questo tutorial copre
  anche l'esportazione di pagine web in PNG e la conversione di file HTML in PNG con
  Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: it
lastmod: 2026-10-21
og_description: Converti HTML in PNG con Python. Segui questa guida chiara per esportare
  la pagina web in PNG, gestire i casi particolari e automatizzare la generazione
  di immagini.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Converti HTML in PNG con Python – guida completa di programmazione
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
title: Come convertire HTML in PNG in Python – guida passo passo
url: /it/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertire HTML in PNG con Python – guida completa di programmazione

Se hai bisogno di **convertire HTML in PNG**, questa guida ti mostra un modo affidabile per farlo con Python puro. Che tu stia esportando un report statico, generando miniature per una galleria o automatizzando screenshot per i test, otterrai una soluzione completa e eseguibile in pochi minuti.

Vedrai anche come **esportare una pagina web in PNG**, comprenderai la differenza tra convertire un file HTML e un URL live, e imparerai le migliori pratiche per gestire pagine grandi o contenuti dinamici. Non sono necessari servizi esterni—solo pochi pacchetti Python e uno script breve.

## Prerequisiti

- Python 3.9+ installato (il codice funziona su Windows, macOS e Linux)
- Accesso a un terminale o prompt dei comandi
- Familiarità di base con il gestore di pacchetti di Python (`pip`)

Avrai bisogno del pacchetto `imgkit` (un leggero wrapper attorno a `wkhtmltoimage`) e del binario `wkhtmltoimage` stesso. Entrambi sono gratuiti e open‑source.

## Passo 1: Installa gli strumenti necessari

Il primo passo è installare `wkhtmltoimage` e il wrapper Python che comunica con esso.

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

> **Perché questo passo è importante** – `wkhtmltoimage` rende l'HTML usando il motore WebKit, producendo PNG pixel‑perfect. `imgkit` semplicemente inoltra le tue opzioni al binario, così ottieni la stessa qualità che avresti da un browser.

## Passo 2: Verifica l'installazione

Esegui un rapido controllo per confermare che il binario sia raggiungibile da Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Se lo script stampa il percorso di `wkhtmltoimage`, sei pronto a convertire HTML in PNG. Se ricevi un `OSError`, verifica che il binario sia presente nel `PATH` del tuo sistema.

## Passo 3: Scrivi una funzione di conversione riutilizzabile

Incapsulare la logica in una funzione rende più semplice **convertire un file HTML in PNG** o **esportare una pagina web in PNG** da qualsiasi punto del tuo progetto.

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

> **Perché avvolgiamo sia `from_file` che `from_url`** – La stessa funzione ora supporta **come convertire HTML in immagine** per file locali e pagine web live, mantenendo il tuo codice DRY (Don’t Repeat Yourself).

## Passo 4: Converti un file HTML locale in PNG

Posiziona un file HTML chiamato `sample.html` in una cartella denominata `assets`. Poi chiama l'helper che abbiamo appena definito:

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

### Output previsto

Eseguendo lo script stampa:

```
✅ Successfully saved PNG to: output/sample.png
```

Un nuovo file `output/sample.png` ora contiene un'istantanea pixel‑perfect di `sample.html`. Aprendolo in qualsiasi visualizzatore di immagini mostra la pagina renderizzata esattamente come apparirebbe in un browser.

## Passo 5: Esporta una pagina web live in PNG

Se hai bisogno di **esportare una pagina web in PNG** per un URL che cambia frequentemente (ad esempio, una dashboard), passa semplicemente la stringa URL invece del percorso del file.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Perché regolare la dimensione del viewport?

Le pagine web progettate per schermi desktop spesso appaiono ristrette se renderizzate con una larghezza piccola. Aumentando le opzioni `width` e `height`, catturi l'intero layout, il che è particolarmente utile per le attività di **esportare una pagina web in PNG**.

## Passo 6: Gestisci casi limite comuni

### 6.1 Pagine grandi o scroll infinito

Per pagine che caricano contenuti in modo pigro (ad esempio, scroll infinito), aumenta il ritardo JavaScript e opzionalmente imposta un viewport più grande:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Pagine protette da autenticazione

Se una pagina richiede un cookie di sessione, puoi incorporare l'intestazione del cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Immagini o font mancanti

`wkhtmltoimage` rispetta il flag `--disable-local-file-access` per motivi di sicurezza. Se il tuo HTML fa riferimento a risorse locali, abilitalo esplicitamente:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Passo 7: Verifica il risultato programmaticamente (opzionale)

A volte è necessario confermare che il PNG sia stato generato correttamente (ad esempio, nelle pipeline CI). Il frammento seguente controlla la dimensione del file e le dimensioni:

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

Se il PNG supera questi controlli, puoi usarlo in modo sicuro nei processi a valle come la generazione di PDF, allegati email o pipeline di machine‑learning.

## Conclusione

Ora disponi di un metodo completo e pronto per la produzione per **convertire HTML in PNG** usando Python. La guida ha coperto:

- Installazione di `wkhtmltoimage` e `imgkit`
- Verifica dell'ambiente
- Una funzione riutilizzabile `convert_html_to_png` che gestisce sia file locali sia URL
- Esempi reali per **esportare una pagina web in PNG**, **come convertire HTML in immagine**, e **convertire un file HTML in PNG**
- Gestione dei casi limite per pagine grandi, autenticazione e risorse locali
- Passaggi di verifica opzionali per pipeline CI/CD

Sentiti libero di sperimentare con opzioni aggiuntive di `imgkit`—come `zoom`, `crop-h` o `crop-w`—per perfezionare l'output per il tuo caso d'uso specifico. Per i prossimi passi, potresti esplorare:

- Convertire i PNG in un report PDF (`img2pdf` library)
- Automatizzare la conversione batch di un'intera cartella di file HTML
- Usare Selenium per pagine che richiedono il rendering completo del browser (ad esempio, framework JavaScript pesanti)

Buon coding e goditi gli screenshot pixel‑perfect!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convertire HTML in PNG – Guida Python Completa](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convertire HTML in PNG con Python – Guida Completa al Salvataggio in Streaming](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convertire SVG in PNG con Python usando Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}