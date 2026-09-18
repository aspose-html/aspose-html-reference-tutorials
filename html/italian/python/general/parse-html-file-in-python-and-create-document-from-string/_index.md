---
category: general
date: 2026-09-16
description: Analizza un file HTML in Python, carica il documento HTML da un file
  e crea un documento HTML da una stringa con codice semplice e pronto all'uso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: it
lastmod: 2026-09-16
og_description: Analizza file HTML in Python per leggere file HTML locali e creare
  documenti HTML da stringhe in modo rapido e affidabile.
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: Analizza file HTML in Python – crea documento da stringa
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: Analizza un file HTML in Python e crea un documento da una stringa
url: /it/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizza file HTML in Python e crea documento da stringa

Se hai bisogno di **parse HTML file in Python**, questa guida ti mostra esattamente come leggere un file HTML locale, caricare un documento HTML da file e anche **create HTML document from string**. Che tu stia facendo scraping di dati, testando template o generando contenuti dinamici, i passaggi seguenti ti offrono una soluzione completa e eseguibile.

In questo tutorial imparerai a:

* Leggere un file HTML locale usando le librerie standard di Python.
* Caricare un documento HTML da un percorso file.
* Creare un documento HTML direttamente da una stringa HTML.
* Gestire casi limite comuni come file mancanti e problemi di codifica.

I soli prerequisiti sono Python 3.8+ e la libreria `beautifulsoup4`, che installeremo nel primo passo.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8 o più recente | Garantisce compatibilità con type hints e sintassi moderna. |
| `beautifulsoup4` e `lxml` packages | Forniscono un parser robusto che può gestire HTML malformato e ti offrono un comodo oggetto simile a `HTMLDocument`. |
| Un file HTML di esempio (`index.html`) nella cartella del tuo progetto | Funziona come input per l'esempio **load html document from file**. |

Installa le dipendenze con pip:

```bash
pip install beautifulsoup4 lxml
```

## Analizza file HTML in Python

Il nucleo del tutorial è l'operazione **parse html file in python**. Avvolgeremo BeautifulSoup in una piccola classe helper chiamata `HTMLDocument` così l'API corrisponde all'esempio visto in precedenza.

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### Come funziona

1. **Detect source type** – Il costruttore verifica se il `source` fornito esiste su disco. Se esiste, **load html document from file**; altrimenti lo tratta come una stringa grezza, soddisfacendo il requisito **create html document from string**.
2. **Read the file** – Usiamo `Path.read_text(encoding="utf-8")`, che è il modo consigliato per **read local html file python** in modo sicuro.
3. **Parse with BeautifulSoup** – Il parser `lxml` è veloce e tollerante verso markup malformato.

## Carica documento HTML da file

Ora che abbiamo la classe `HTMLDocument`, caricare un file è semplice:

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**Output previsto** (supponendo che `index.html` contenga `<title>My Page</title>`):

```
Document title: My Page
```

Se il file non esiste, la classe solleva un chiaro `FileNotFoundError`, che puoi gestire nel codice di produzione.

## Crea documento HTML da stringa

Creare un documento direttamente da una stringa è utile per testare o generare HTML al volo:

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**Output previsto**:

```
String-based title: Hello
```

Poiché la stessa classe `HTMLDocument` gestisce entrambi gli scenari, ottieni un'API coerente per **parse html file in python**, sia che la sorgente sia un file sia che sia una stringa.

## Leggi file HTML locale in Python – gestione dei casi limite

Quando si lavora con file del mondo reale si incontrano spesso:

* **Missing files** – già gestito dal `FileNotFoundError`.
* **Different encodings** – puoi lasciare che BeautifulSoup indovini la codifica, ma specificare esplicitamente UTF‑8 è la soluzione più sicura.
* **Large files** – leggere l'intero file in memoria può essere costoso; puoi fare streaming con `BeautifulSoup(open(...), "lxml")` se necessario.

Ecco un wrapper difensivo che aggiunge queste salvaguardie:

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

Ora puoi chiamare `safe_load_html("index.html")` e ottenere lo stesso oggetto `HTMLDocument` con la certezza che gli errori vengano segnalati chiaramente.

## Consigli professionali e errori comuni

* **Avoid “just” using `open(...).read()`** – `Path.read_text` gestisce l'espansione del percorso e la codifica in una sola riga.
* **Don’t forget to close file handles** – `Path.read_text` lo fa automaticamente; se usi `open()`, avvolgilo in un blocco `with`.
* **Prefer `lxml` over the default parser** – è più veloce e più tollerante verso markup rotto, il che è essenziale quando **parse html file in python** dal web.
* **When creating from a string, ensure it’s a complete HTML document** – tag `<html>` o `<body>` mancanti possono portare a risultati `None` inaspettati quando interroghi gli elementi.

## Script completo da copiare‑incollare

Di seguito trovi uno script autonomo che dimostra ogni passaggio discusso. Salvalo come `html_demo.py` ed esegui `python html_demo.py`.



## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Salva documento HTML su file in Aspose.HTML per Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Carica documenti HTML da file in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Crea documento HTML con Aspose.HTML – Guida passo‑passo](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}