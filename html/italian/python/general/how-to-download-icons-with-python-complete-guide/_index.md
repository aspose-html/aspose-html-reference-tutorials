---
category: general
date: 2026-05-31
description: Impara come scaricare icone usando Python. Tratteremo anche come estrarre
  il favicon, leggere un documento HTML con Python e scrivere un file binario in Python,
  tutto in un unico tutorial.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: it
og_description: Come scaricare icone usando Python spiegato passo passo. Impara a
  estrarre il favicon, leggere un documento HTML con Python e scrivere un file binario
  in Python.
og_title: Come scaricare icone con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Come scaricare icone con Python – Guida completa
url: /it/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come scaricare icone con Python – Guida completa

Ti sei mai chiesto **come scaricare icone** da un sito web senza dover fare clic destro manualmente su ciascuna? Non sei l'unico. Che tu stia costruendo uno strumento di audit del brand o voglia semplicemente una copia locale di ogni favicon che incontri, padroneggiare questo compito ti fa risparmiare tempo e battute di tasto.

In questo tutorial vedremo **come scaricare icone** da un file HTML usando Python puro. Ti mostreremo anche **come estrarre favicon**, dimostreremo **read html document python**, e spiegheremo **write binary file python** così otterrai una cartella ordinata di file .ico pronta per qualsiasi progetto.

---

## Cosa ti servirà

- Python 3.8+ (la libreria standard è sufficiente)
- Una copia locale della pagina HTML che vuoi analizzare (o un URL che puoi recuperare)
- Familiarità di base con I/O di file in Python  
- Nessun pacchetto esterno richiesto, ma `beautifulsoup4` può semplificare le cose se lo preferisci (opzionale)

Li hai? Ottimo—tuffiamoci.

![Esempio di come scaricare icone](https://example.com/placeholder.png "esempio di come scaricare icone")

---

## Passo 1: Carica il documento HTML in Python  

Prima di tutto, dobbiamo **load html python** style—leggere il file in memoria così possiamo ispezionare i suoi tag `<link>`. Il modo più semplice è aprire il file con la funzione integrata `open` e leggerlo come testo.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Perché questo passo?*  
Leggere l'HTML ci fornisce una stringa grezza che possiamo analizzare. Se salti questo passaggio e provi a lavorare direttamente con un percorso, il parser non avrà nulla da esaminare.

---

## Passo 2: Analizza il documento e trova i collegamenti alle icone  

Ora dobbiamo **read html document python** style. Sebbene potresti usare le regex, un piccolo parser HTML mantiene le cose affidabili. Python include `html.parser` che possiamo estendere per il nostro scopo.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Spiegazione**  

- `handle_starttag` viene attivato per ogni tag di apertura.  
- Filtriamo gli elementi `<link>` il cui attributo `rel` contiene la parola *icon*. Questo copre sia `rel="icon"` sia il più vecchio `rel="shortcut icon"`.  
- I valori `href` vengono memorizzati in `icon_hrefs`, pronti per il passo successivo.

---

## Passo 3: Risolvi i percorsi relativi (Opzionale ma utile)

Se l'HTML utilizza URL relativi, dobbiamo trasformarli in percorsi assoluti del file system. È qui che la conoscenza di **load html python** incontra `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Perché preoccuparsi?*  
Quando più tardi **write binary file python**, ti serve un percorso file reale. URL relativi come `images/favicon.ico` altrimenti causerebbero un `FileNotFoundError`.

---

## Passo 4: Scrivi ogni icona in un file binario locale  

Ecco il cuore di **how to download icons**. Itereremo sui percorsi risolti, leggeremo ogni icona come dati binari e la scriveremo in un nuovo file in una cartella dedicata `icons/`.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**Cosa sta succedendo?**  

- `os.makedirs(..., exist_ok=True)` garantisce che la cartella di output esista.  
- `shutil.copyfileobj` trasmette i byte dalla sorgente alla destinazione, che è il modo più efficiente in termini di memoria per **write binary file python**.  
- Nominiamo ogni file `icon_<index>.ico` per evitare collisioni.

**Output previsto**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

Dopo che lo script termina, avrai una raccolta pulita di file icona pronta per qualsiasi operazione a valle.

---

## Passo 5: Bonus – Scarica le icone direttamente da un URL remoto  

Se il tuo HTML è sul web invece che sul disco locale, sostituisci la parte di lettura del file con una piccola chiamata `requests`. Questo dimostra **how to extract favicon** da qualsiasi pagina live.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**Perché aggiungerlo?**  
Molti progetti reali hanno bisogno di estrarre favicons da siti live. Questo snippet mostra che puoi estendere la stessa logica di **how to download icons** a Internet con solo un paio di righe aggiuntive.

---

## Problemi comuni & consigli professionali

- **Mancante `rel="icon"`** – Alcuni siti incorporano icone tramite tag `<meta>` o CSS. Se ti servono, espandi il parser per cercare `<meta name="msapplication‑TileImage">` o URL di `background-image` CSS.  
- **Formati non‑ICO** – Le favicon moderne spesso usano `.png` o `.svg`. Il codice sopra funziona per qualsiasi immagine binaria; basta regolare l'estensione del file in `dest_path` se vuoi preservare il formato originale.  
- **Errori di permesso** – Quando scrivi file, assicurati che lo script abbia i permessi di scrittura sulla cartella di destinazione. Usare `os.makedirs(..., exist_ok=True)` evita crash per “directory non trovata”.  
- **File HTML di grandi dimensioni** – Per pagine massive, considera lo streaming del file riga per riga invece di caricare l'intera stringa in memoria. L'`HTMLParser` integrato può gestire feed incrementali.  

---

## Conclusione

Hai appena imparato **how to download icons** da un documento HTML usando Python puro. Attraverso **reading html document python**, analizzando i tag `<link rel="icon">`, risolvendo eventuali percorsi relativi e infine **write binary file python** per salvare ogni icona localmente, ora disponi di uno script riutilizzabile che funziona sia per pagine locali che remote.  

Prossimi passi? Prova a estendere il parser per catturare le Apple touch icons (`rel="apple-touch-icon"`), o integra lo script in una pipeline di web‑crawling più ampia che raccoglie favicons per centinaia di domini. I fondamenti trattati qui—analisi HTML, risoluzione dei percorsi e gestione di file binari—sono mattoni fondamentali per molte attività di automazione web.

Hai domande o vuoi condividere un caso d'uso interessante? Lascia un commento qui sotto, e buona caccia alle icone!

## Cosa dovresti imparare dopo?

- [Come modificare l'albero del documento HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Come convertire HTML in PDF Java – Usando Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Come convertire HTML in JPEG usando Aspose.HTML per Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}