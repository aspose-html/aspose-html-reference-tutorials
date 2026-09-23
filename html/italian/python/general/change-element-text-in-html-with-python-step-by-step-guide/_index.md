---
category: general
date: 2026-09-23
description: Cambia il testo di un elemento in un file HTML usando Python. Scopri
  come caricare un file HTML, modificare il tag title e aggiornare il titolo HTML
  in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: it
lastmod: 2026-09-23
og_description: Modifica il testo di un elemento in un documento HTML usando Python.
  Questo tutorial mostra come caricare un file HTML, modificare il tag <title> e aggiornare
  il titolo HTML in poche righe di codice.
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: Modifica il testo di un elemento in HTML con Python – guida rapida
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: Modifica il testo di un elemento HTML con Python – guida passo passo
url: /it/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifica il testo di un elemento in HTML con Python – guida passo‑paso

Se hai bisogno di **modificare il testo di un elemento** in un documento HTML, questa guida ti mostra esattamente come farlo con Python. Che tu stia correggendo un tag `<title>` obsoleto o aggiornando qualsiasi altro elemento, imparerai a **caricare il file HTML**, modificare il testo e **aggiornare il titolo HTML** (o qualsiasi elemento) in modo sicuro.

Cambiare il titolo di una pagina web è un'operazione comune quando si puliscono dati estratti, si generano pagine statiche o si automatizzano aggiornamenti SEO. In questo tutorial tu:

* Caricherai un file HTML dal disco.
* Individuerai l'elemento `<title>` e **modificherai il tag title**.
* Salverai il documento modificato, effettuando effettivamente **l'aggiornamento del titolo HTML**.

Tutto il codice necessario è incluso, e ogni passaggio spiega **perché** l'operazione è importante, non solo **cosa** digitare.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.9 o versioni successive installate.
* La libreria `lxml` (`pip install lxml`).  
  `lxml` fornisce un parsing HTML veloce e conforme agli standard e una manipolazione affidabile.
* Una directory contenente il file HTML che vuoi modificare (sostituisci `YOUR_DIRECTORY` con il percorso reale).

## Passo 1: Carica il file HTML

Il primo passo è **caricare il file HTML** in un albero DOM (Document Object Model) che Python può gestire. Usare `lxml.html` ti dà il supporto XPath e una gestione affidabile degli elementi.

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**Perché è importante:**  
Il parsing crea una rappresentazione strutturata della pagina, permettendoti di interrogare gli elementi direttamente. Senza caricare il file, non puoi **modificare il testo di un elemento** in modo sicuro perché lavoreresti con stringhe grezze, il che è soggetto a errori.

## Passo 2: Individua l'elemento `<title>` e **modifica il testo dell'elemento**

Ora che il documento è caricato, puoi **modificare il tag title**. L'espressione XPath `".//title"` trova il primo elemento `<title>` nella gerarchia del documento.

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**Perché è importante:**  
Assegnando direttamente a `title_elem.text` **modifichi il testo dell'elemento** senza alterare il markup circostante. Questo approccio preserva spazi bianchi, commenti e altri tag, garantendo che l'output rimanga HTML valido.

### Caso limite: più tag `<title>`

Gli standard HTML consentono solo un elemento `<title>`, ma file malformati a volte ne contengono più di uno. Se devi gestire questa situazione, itera su tutte le corrispondenze:

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## Passo 3: Salva il documento modificato – **aggiorna il titolo HTML**

Dopo la modifica, scrivi l'albero nuovamente su disco. Usare `pretty_print=True` mantiene il file leggibile.

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**Perché è importante:**  
Il salvataggio crea un nuovo file che riflette l'operazione di **modifica del testo dell'elemento**. Se devi sovrascrivere il file originale, usa semplicemente lo stesso percorso per `output_path`.

## Script completo in un unico blocco

Mettendo tutto insieme, ecco uno script autonomo che **carica il file HTML**, **modifica il testo dell'elemento** e **aggiorna il titolo HTML**:

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

Eseguendo questo script otterrai un file `updated.html` il cui `<title>` ora contiene **New Title**.

## Varianti comuni della tecnica

### Modifica di altri elementi (es. `<h1>`)

Se devi **modificare il testo di un elemento** per un'intestazione invece del titolo, adatta l'XPath:

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### Conservare gli spazi bianchi esistenti

Quando l'HTML originale utilizza indentazione all'interno dei tag, `pretty_print` potrebbe riformattarla. Per mantenere la formattazione originale, ometti `pretty_print`:

```python
doc.write(destination, encoding="utf-8")
```

### Lavorare con caratteri Unicode

`lxml` gestisce automaticamente Unicode. Assicurati che il file sorgente sia salvato con codifica UTF‑8; altrimenti, specifica la codifica corretta quando apri il file.

## Pro tip e insidie

* **Pro tip:** Usa `doc.xpath("//title/text()")` se ti serve solo il contenuto testuale senza modificare l'elemento.
* **Attenzione a:** file HTML che contengono un `<title>` dentro un `<svg>` o altro namespace non‑HTML. In questi casi, affina l'XPath per puntare alla sezione `<head>`: `doc.find(".//head/title")`.
* **Suggerimento di performance:** per l'elaborazione batch di migliaia di file, riutilizza la stessa istanza del parser per ridurre l'overhead.

## Conclusione

Ora sai come **modificare il testo di un elemento** in un documento HTML usando Python, in particolare come **caricare il file HTML**, **modificare il tag title** e **aggiornare il titolo HTML**. L'esempio completo dimostra un approccio affidabile basato su librerie, valido sia per HTML ben formato sia per HTML leggermente malformato.

Da qui puoi:

* Applicare lo stesso schema ad altri tag (`<h2>`, `<meta>`, ecc.).
* Combinare questo script con una pipeline di web‑scraping per pulire grandi collezioni di pagine.
* Esplorare l'API più ricca di `lxml` per la manipolazione di attributi, selettori CSS e serializzazione HTML.

Buon coding, e sentiti libero di sperimentare con diversi elementi per padroneggiare la manipolazione HTML in Python!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑paso per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci alternativi nei tuoi progetti.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}