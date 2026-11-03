---
category: general
date: 2026-06-04
description: Ottieni rapidamente il testo da EPUB e impara come leggere i file EPUB,
  convertire gli EPUB in testo ed estrarre i capitoli usando Python.
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: it
og_description: Ottieni il testo da EPUB con Python in pochi minuti. Questo tutorial
  mostra come leggere i file EPUB, convertire EPUB in testo e gestire i casi limite
  più comuni.
og_title: Ottieni il testo da EPUB in Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: Estrai il testo da EPUB in Python – Guida completa
url: /it/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni testo da EPUB in Python – Guida completa

Ti sei mai chiesto **come leggere i file EPUB** senza aprire un ingombrante lettore? Forse devi estrarre il primo capitolo per un'analisi, o vuoi semplicemente **convertire EPUB in testo** per una ricerca rapida. Qualunque sia il caso, sei nel posto giusto. In questo tutorial ti mostreremo come **ottenere testo da EPUB** usando poche righe di Python, e spiegheremo anche il perché di ogni passaggio così potrai adattare la soluzione a qualsiasi libro.

Passeremo in rassegna l'installazione della libreria giusta, il caricamento dell'EPUB, l'estrazione del primo elemento `<section>` e la stampa del suo contenuto in testo semplice. Alla fine avrai uno script riutilizzabile che funziona su qualsiasi EPUB che inserisci in una cartella.

## Prerequisiti

- Python 3.8+ (il codice usa f‑strings e pathlib)
- Un IDE moderno o semplicemente un terminale
- I pacchetti `ebooklib` e `beautifulsoup4` (installali con `pip install ebooklib beautifulsoup4`)

Non sono necessari altri strumenti esterni, e lo script funziona su Windows, macOS e Linux.

---

## Ottieni testo da EPUB – Passo‑per‑passo

Di seguito trovi la logica centrale che fa esattamente quello che promette il titolo: **ottiene testo da EPUB** e stampa il primo capitolo. Lo scomporremo così da capire ogni riga.

### Passo 1: Importare le librerie e caricare l'EPUB

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*Perché questo passo?*  
`ebooklib` conosce la struttura basata su ZIP dei file EPUB, mentre `BeautifulSoup` rende indolore l'analisi dell'HTML incorporato. Usare `Path` mantiene il codice indipendente dal sistema operativo.

### Passo 2: Recuperare il primo capitolo (primo elemento `<section>`)

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*Perché questo passo?*  
Gli EPUB memorizzano ogni capitolo come file HTML. Il ciclo si ferma al primo documento, che è spesso la copertina o l'introduzione. Puntando al primo `<section>` miriamo direttamente al primo vero capitolo, ma forniamo anche un fallback all'elemento `<body>` per i libri che non usano le sezioni.

### Passo 3: Rimuovere i tag e stampare il testo semplice

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*Perché questo passo?*  
`get_text()` è il modo più semplice per **convertire EPUB in testo**. L'argomento `separator` garantisce che ogni elemento a blocco inizi su una nuova riga, rendendo l'output leggibile.

### Script completo – Pronto da eseguire

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

Salva questo file come `extract_epub.py` ed esegui `python extract_epub.py`. Se tutto è configurato correttamente, vedrai il testo del primo capitolo stampato sulla console.

![Screenshot dell'output del terminale che mostra il testo estratto dall'EPUB](get-text-from-epub.png "Esempio di output di Get text from EPUB")

---

## Converti EPUB in testo – Scalare il processo

Il frammento sopra gestisce un singolo capitolo, ma la maggior parte dei progetti richiede l'intero libro come una grande stringa. Ecco una rapida estensione che itera su **tutti** gli elementi documento, concatena il loro testo pulito e lo scrive in un file `.txt`.

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**Consiglio professionale:** Alcuni EPUB includono script o tag di stile che possono confondere `BeautifulSoup`. Se noti caratteri strani, aggiungi `soup = BeautifulSoup(item.get_content(), "lxml")` e installa `lxml` per un parser più rigoroso.

---

## Come leggere i file EPUB in modo efficiente – Problemi comuni

1. **Sorprese di codifica** – Gli EPUB sono file ZIP contenenti HTML UTF‑8. Se ottieni `UnicodeDecodeError`, forza UTF‑8 durante la lettura: `item.get_content().decode("utf-8", errors="ignore")`.
2. **Lingue multiple** – I libri con lingue miste possono includere tag `<section>` separati per lingua. Usa `soup.find_all("section")` e filtra per l'attributo `lang` se necessario.
3. **Immagini e note a piè di pagina** – Lo script rimuove i tag, quindi il testo alternativo delle immagini scompare. Se ti servono, estrai gli attributi `alt` di `<img>` o i link delle note a piè di pagina `<a>` prima della pulizia.
4. **Libri voluminosi** – Scrivere ogni capitolo in memoria può esaurire la RAM. Scrivi ogni capitolo pulito direttamente su file in modalità append per mantenere basso l'uso di memoria.

---

## FAQ – Risposte rapide alle domande tipiche

**D: Posso usarlo con un file .mobi?**  
R: Non direttamente. `.mobi` usa un formato di contenitore diverso. Converti prima in EPUB (Calibre fa un ottimo lavoro), poi applica lo stesso script.

**D: E se l'EPUB non contiene tag `<section>`?**  
R: Il fallback a `<body>` (mostrato nel codice) copre questo caso. Puoi anche cercare `<div class="chapter">` se l'editore usa markup personalizzato.

**D: `ebooklib` è l'unica libreria disponibile?**  
R: No. Alternative includono `zipfile` + parsing HTML manuale, o `pypub` per un'API di livello più alto. `ebooklib` è popolare perché astrae la gestione ZIP e fornisce i tipi di elemento subito pronti.

---

## Conclusione

Ora sai come **ottenere testo da EPUB** usando Python, sia che ti serva solo il primo capitolo sia l'intero libro. Il tutorial ha coperto i passaggi essenziali per **convertire EPUB in testo**, spiegato il ragionamento dietro ogni riga e evidenziato i casi limite che potresti incontrare.  

Successivamente, prova a estendere lo script per estrarre i metadati (titolo, autore) con `book.get_metadata('DC', 'title')`, o sperimenta formati di output come Markdown o JSON. Gli stessi principi si applicano, così sarai pronto ad affrontare qualsiasi sfida di parsing di file simili.

Buon coding, e sentiti libero di lasciare un commento se incontri difficoltà!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire EPUB in PDF con Java – Usando Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Converti EPUB in immagini usando Aspose HTML per Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Converti EPUB in PDF e immagini con Aspose.HTML per Java](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}