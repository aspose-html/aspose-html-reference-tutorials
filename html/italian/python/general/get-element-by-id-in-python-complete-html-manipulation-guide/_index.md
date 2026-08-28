---
category: general
date: 2026-05-31
description: Impara come ottenere un elemento per ID, cambiare il colore di sfondo
  in HTML, leggere il testo HTML e impostare un attributo HTML usando Python. Tutorial
  passo‑passo.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: it
og_description: Ottieni l'elemento per ID, leggi il testo HTML, imposta un attributo
  HTML e cambia il colore di sfondo usando Python in una guida unica e facile da seguire.
og_title: Ottieni l'elemento per ID in Python – Tutorial completo di manipolazione
  HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Recupera l'elemento per ID in Python – Guida completa alla manipolazione HTML
url: /it/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get element by id in Python – Guida completa alla manipolazione HTML

Ti è mai capitato di **get element by id** da una pagina HTML mentre scrivi uno script Python veloce? Non sei solo—la maggior parte degli sviluppatori incontra lo stesso ostacolo quando inizia a fare crawling di siti o a modificare report locali. La buona notizia? Con poche righe di codice puoi leggere il testo dell'elemento, cambiare il suo colore di sfondo e persino impostare nuovi attributi, il tutto senza uscire dal tuo editor.

In questo tutorial percorreremo un esempio reale: caricare un file locale `sample.html`, estrarre l'elemento il cui ID è `main‑content`, stampare il suo testo interno e infine cambiare il colore di sfondo in un grigio chiaro. Alla fine saprai anche **how to read HTML text**, **how to set HTML attribute**, e perché **manipulate HTML with Python** è una competenza utile in qualsiasi toolbox di automazione.

## Cosa ti servirà

- **Python 3.9+** (qualsiasi versione recente funziona)
- La libreria **`lxml`** (o **BeautifulSoup** se preferisci) – useremo `lxml.html` perché fornisce un'API pulita in stile `get_element_by_id`.
- Un piccolo file HTML chiamato `sample.html` situato in una cartella chiamata `YOUR_DIRECTORY`. Sentiti libero di copiare lo snippet qui sotto in quel file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

È tutto—nessun framework sofisticato, solo puro Python e un file HTML statico.

## Passo 1: Installa la libreria necessaria

Se non hai ancora installato `lxml`, apri un terminale ed esegui:

```bash
pip install lxml
```

*Consiglio professionale:* Usare un ambiente virtuale mantiene pulito il tuo Python globale, specialmente quando inizi a gestire più progetti.

## Passo 2: Carica il documento HTML

Ora leggeremo il file in un oggetto documento `lxml.html`. Pensalo come trasformare il testo grezzo in un albero navigabile.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Eseguendo questo stampa “Document loaded successfully.” Se il file non viene trovato, Python solleverà un `FileNotFoundError`—è bene catturarlo subito prima di inseguire un elemento fantasma.

## Passo 3: Get element by id

Ecco il nocciolo della questione. `lxml` ci fornisce un comodo metodo `get_element_by_id` che rispecchia l'API DOM che useresti in JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Quando l'elemento esiste, vedrai stampato “Element found!” nella console. Questo è il passo **get element by id** che alimenta la maggior parte delle nostre manipolazioni successive.

## Passo 4: How to read HTML text

Una volta ottenuto l'elemento, estrarre il suo testo visibile è un gioco da ragazzi. Il metodo `text_content()` restituisce tutto ciò che è dentro, senza i tag.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Output previsto:

```
Inner text: Hello, world! This is the original text.
```

Potresti chiederti, *e se l'elemento contiene tag annidati?* `text_content()` funziona comunque—concatena tutti i nodi di testo discendenti, fornendoti una stringa pulita che puoi registrare, memorizzare o passare a un altro algoritmo.

## Passo 5: How to set HTML attribute

Cambiare o aggiungere attributi è altrettanto semplice. Il metodo `set` ti permette di assegnare qualsiasi nome di attributo tu voglia.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

Quella riga dimostra **how to set HTML attribute** al volo. Puoi sostituire `"data-modified"` con `"class"`, `"title"` o qualsiasi altro attributo supportato dall'elemento.

## Passo 6: Change background colour HTML

Ora la modifica visiva. Per cambiare il colore di sfondo, iniettiamo un attributo `style` che sovrascrive quello predefinito.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Dopo aver eseguito lo script, il `div` in `sample.html` avrà questo aspetto quando lo apri in un browser:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Questa è la tecnica **change background colour html** che puoi riutilizzare per qualsiasi elemento—basta sostituire il codice colore.

## Passo 7: Manipulate HTML with Python – Mettere tutto insieme

Di seguito lo script completo, eseguibile, che combina tutti i passaggi. Salvalo come `modify_html.py` ed eseguilo dalla stessa directory della tua cartella `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Cosa fa lo script, riga per riga

1. **Imports** `lxml.html` per il parsing e `pathlib` per percorsi indipendenti dal sistema operativo.  
2. **Loads** `sample.html` e abortisce con un errore chiaro se il file manca.  
3. **Retrieves** l'elemento usando **get element by id**.  
4. **Prints** il testo dell'elemento—mostrando **how to read HTML text**.  
5. **Adds** un attributo personalizzato, illustrando **how to set HTML attribute**.  
6. **Changes** il colore di sfondo, soddisfacendo il requisito **change background colour html**.  
7. **Writes** il markup aggiornato in `sample_modified.html`, così potrai aprirlo in un browser e vedere le modifiche.

Eseguendo lo script otterrai un output console simile a:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Apri `sample_modified.html` e noterai lo sfondo grigio dietro il testo—la prova che **manipulate HTML with python** funziona davvero.

## Problemi comuni e come evitarli

- **Missing ID** – Se l'elemento target non esiste, `get_element_by_id` restituisce `None`. Controlla sempre `None` prima di accedere alle proprietà; altrimenti otterrai un `AttributeError`.  
- **Encoding issues** – Quando leggi pagine non‑ASCII, passa `encoding='utf-8'` a `html.parse` o assicurati che il file sia salvato in UTF‑8.  
- **Overwriting existing styles** – Impostare l'attributo `style` sostituisce eventuali stili inline precedenti. Se devi preservare le regole esistenti, leggi prima il valore corrente di `style`, aggiungi la tua nuova regola, poi riscrivilo.  
- **File permissions** – Scrivere nella stessa cartella può fallire su sistemi di sola lettura. Scegli un percorso di output scrivibile, come abbiamo fatto con `sample_modified.html`.

## Estendere l'esempio

Ora che hai padroneggiato le basi, considera i prossimi passi:

- **Loop over multiple IDs** – Usa una lista di ID e itera con un `for` loop per elaborare in batch sezioni di una pagina.  
- **Replace text content** – Chiama `elem.text = "New text"` per modificare la stringa visibile.  
- **Add child elements** – Use `

## Cosa dovresti imparare dopo?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}