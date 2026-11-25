---
category: general
date: 2026-08-25
description: Impara a creare un documento HTML, selezionare gli elementi CSS, modificare
  il testo HTML e salvare il file HTML usando un semplice script Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: it
lastmod: 2026-08-25
og_description: Crea un documento HTML, seleziona l'elemento CSS, modifica il testo
  HTML e salva il file HTML in poche righe di Python. Segui questo tutorial completo.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Crea un documento HTML e modifica il suo contenuto con Python – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Come creare un documento HTML e modificarne il contenuto in Python
url: /it/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un documento html e modificarne il contenuto in Python

Se hai bisogno di **create html document** da zero e modificare i suoi elementi programmaticamente, questa guida ti mostra esattamente come. Vedrai uno script breve e eseguibile che crea un file, seleziona un paragrafo con un selettore CSS, aggiorna il testo e scrive il risultato su disco.

Lavorare con HTML in Python è comune quando si generano report, template email o contenuti per siti statici. Alla fine di questo tutorial sarai in grado di **select element css**, **modify html text** e **save html file** senza lasciare il comfort del tuo IDE.

## Prerequisiti

* Python 3.9 o versioni successive installato.
* I pacchetti `beautifulsoup4` e `lxml` (installali con `pip install beautifulsoup4 lxml`).
* Permessi di scrittura nella directory in cui prevedi di salvare il file di output.

Non sono necessari strumenti aggiuntivi; la libreria standard gestisce le operazioni di I/O sui file.

## Passo 1: Installa le librerie richieste

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` fornisce un'API comoda per l'analisi e la manipolazione di HTML, mentre `lxml` offre un parser veloce che comprende i selettori CSS.

## Passo 2: Crea il documento HTML iniziale

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Il costruttore `BeautifulSoup` crea un oggetto **create html document** in memoria. L'uso del parser `"lxml"` garantisce il pieno supporto ai selettori CSS.

## Passo 3: Seleziona l'elemento paragrafo usando un selettore CSS

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

Il metodo `select_one` implementa la logica **select element css**, restituendo il primo tag corrispondente. Se il selettore non corrisponde a nulla, `para` sarà `None`, quindi è consigliabile un controllo difensivo nel codice di produzione.

## Passo 4: Modifica il contenuto testuale del paragrafo

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Assegnare a `para.string` esegue un'operazione **modify html text**. BeautifulSoup aggiorna l'albero DOM sottostante, quindi la modifica è riflessa quando il documento viene serializzato.

## Passo 5: Salva l'HTML aggiornato in un file

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

La chiamata `open` insieme a `write` implementa la funzionalità **save html file**. L'uso di `prettify()` produce un output correttamente indentato, utile durante il debugging.

### Script completo per copia‑incolla veloce

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Eseguendo `python edit_html.py` si crea `updated.html` contenente:

```html
<p>
 New
</p>
```

## Varianti comuni e casi limite

### Selezionare più elementi

Se hai bisogno di selettori **select element css** che corrispondono a più tag (ad esempio, `"div.note"`), usa `doc.select("div.note")` che restituisce una lista. Itera sulla lista per applicare le modifiche a ciascun elemento.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Conservare gli attributi esistenti

Quando sostituisci il testo, BeautifulSoup mantiene tutti gli attributi sul tag. Per esempio:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Gestire gli elementi mancanti in modo elegante

Nei script di produzione, spesso si incontrano HTML malformati. Avvolgi la selezione in una condizione o in un blocco try‑except, come mostrato al Passo 4, per evitare crash.

### Scrivere in una directory specifica

Sostituisci `output_path` con un percorso assoluto o relativo:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Assicurati che la directory esista; altrimenti, Python solleverà `FileNotFoundError`.

## Consigli professionali

* **Performance** – Per file HTML di grandi dimensioni, preferisci `lxml.etree` direttamente; BeautifulSoup aggiunge un sottile livello di astrazione che è comodo ma leggermente più lento.
* **Encoding** – Apri sempre i file con `encoding="utf-8"` per preservare i caratteri non ASCII.
* **Testing** – Dopo la modifica, puoi verificare l'output con `assert "New" in open(output_path).read()` in un test unitario.

## Conclusione

Ora sai come **create html document**, utilizzare una query **select element css** per individuare un nodo, **modify html text**, e infine **save html file** con Python. Questo schema si scala a trasformazioni più complesse come aggiornamenti massivi, modifiche di attributi o generazione di template.

Successivamente, esplora argomenti correlati come **how to edit html** usando espressioni XPath, generare pagine HTML complete con Jinja2, o automatizzare l'elaborazione batch di più file. Ognuno di questi si basa sui passaggi fondamentali mostrati qui e amplia il tuo set di strumenti per la manipolazione programmatica di HTML.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}