---
category: general
date: 2026-07-02
description: Impara come caricare HTML in Python, ottenere un elemento per ID ed estrarre
  il testo da un file. Questo tutorial pratico mostra come leggere file HTML con BeautifulSoup.
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: it
og_description: Come caricare HTML in Python ed estrarre testo usando BeautifulSoup.
  Segui la guida per leggere un file HTML, ottenere l'elemento per ID e stampare il
  suo contenuto.
og_title: Come caricare HTML in Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: Come caricare HTML in Python – Guida passo‑a‑passo
url: /it/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come caricare HTML in Python – Tutorial completo

Ti sei mai chiesto **come caricare HTML** in uno script Python senza impazzire? Non sei l'unico. Che tu stia facendo scraping di un sito di notizie, elaborando un report locale, o semplicemente abbia bisogno di estrarre un titolo da un modello di email, padroneggiare l'arte di caricare HTML è una competenza indispensabile per qualsiasi sviluppatore.

In questa guida vedremo **come ottenere un elemento** per ID, **come estrarre testo**, e infine stampare il risultato—tutto mantenendo il codice pulito e Pythonic. Tratteremo anche le sfumature di **leggere un file HTML in Python**, così potrai copiare‑incollare una soluzione funzionante subito.

> **Consiglio:** L'esempio utilizza la popolare libreria *BeautifulSoup* perché è leggera, ben documentata e funziona sia con strutture HTML semplici che complesse.

## Cosa ti serve

- Python 3.9 o più recente (il codice funziona anche su 3.10+)
- `beautifulsoup4` e `lxml` installati (`pip install beautifulsoup4 lxml`)
- Un file HTML di esempio – lo chiameremo `sample.html` e lo posizioneremo in una cartella chiamata `YOUR_DIRECTORY`

Tutto qui. Nessun browser pesante, nessun Selenium, solo puro Python.

## Passo 1: Come caricare HTML – Leggere il file in memoria

La prima cosa da fare è **leggere il file HTML** dal disco. Questa è la base di tutti i passaggi successivi, quindi facciamolo correttamente.

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*Perché è importante:* L'uso di `Path.read_text` astrae le terminazioni di riga specifiche del sistema operativo e gestisce automaticamente UTF‑8, che è la codifica de‑facto per le pagine web moderne. Se il file manca, `Path.read_text` solleverà un chiaro `FileNotFoundError`, rendendo il debug indolore.

## Passo 2: Analizzare il documento HTML

Ora che abbiamo una stringa grezza, dobbiamo **caricare HTML** in un oggetto parser. BeautifulSoup ci fornisce un'API comoda per navigare il DOM.

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*Perché lxml?* Il parser `lxml` è significativamente più veloce del parser integrato di Python e gestisce markup malformato in modo più elegante—perfetto per HTML del mondo reale che potresti fare scraping.

## Passo 3: Ottenere l'elemento per ID – Individuare l'intestazione

Con il documento analizzato, rispondiamo alla domanda **come ottenere un elemento** con un ID specifico. Nel nostro esempio cerchiamo un tag `<h1>` il cui attributo `id` è uguale a "main-header".

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

Se l'elemento non viene trovato, `header` sarà `None`. È buona pratica proteggersi da questo caso:

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## Passo 4: Come estrarre testo – Ottenere il contenuto interno

Ora che abbiamo l'elemento, estrarre il suo contenuto testuale è un gioco da ragazzi. Questo risponde a **come estrarre testo** da un tag.

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` concatena automaticamente tutti i nodi di testo annidati, quindi non è necessario iterare manualmente sui figli. Il flag `strip=True` rimuove i caratteri di nuova riga e gli spazi, fornendoti una stringa pulita.

## Passo 5: Stampare il risultato – Verificare che tutto funzioni

Infine, stampiamo il valore sulla console. Questo rispecchia la riga `print(header.text_content)` nello snippet originale.

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

Se esegui lo script e vedi il titolo previsto, congratulazioni—hai **letto con successo un file HTML in Python**, individuato un elemento per ID e estratto il suo testo.

## Esempio completo funzionante

Di seguito trovi lo script completo, pronto per l'esecuzione. Copialo in un file chiamato `extract_header.py` ed esegui `python extract_header.py`.

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**Output previsto** (supponendo che `sample.html` contenga `<h1 id="main-header">Welcome to My Site</h1>`):

```
Welcome to My Site
```

Questo è tutto—uno script, nessuna dipendenza extra oltre a BeautifulSoup e lxml.

## Domande comuni e casi particolari

### E se l'HTML è malformato?

Il parser `lxml` di BeautifulSoup è indulgente, ma per markup gravemente rotto potresti voler ricorrere al `html.parser` integrato. Sostituisci "lxml" con "html.parser" nel costruttore di `BeautifulSoup`.

### Come gestire più elementi con lo stesso ID?

La specifica HTML prevede che gli ID siano unici, ma la realtà a volte è diversa. Usa `soup.find_all(id="duplicate-id")` per ottenere una lista, poi itera su di essa.

### È necessario leggere da un URL invece che da un file?

Sostituisci la logica di lettura del file con `requests.get(url).text`. Ricorda di installare il pacchetto `requests` (`pip install requests`) e gestire gli errori di rete in modo appropriato.

### Vuoi estrarre altri attributi (ad es., `class` o `href`)?

Accedili semplicemente come a un dizionario: `header['class']` o `header['href']`. Se l'attributo potrebbe mancare, usa `.get('class')` per evitare `KeyError`.

## Riepilogo visivo

![esempio di come caricare html](https://example.com/placeholder-image.png "esempio di come caricare html")

*Testo alternativo:* esempio di come caricare html – un diagramma che mostra il flusso dalla lettura del file all'estrazione del testo.

## Riepilogo

Abbiamo coperto **come caricare HTML** in Python, dimostrato **come ottenere un elemento** per ID, e mostrato **come estrarre testo** da quell'elemento. Seguendo i passaggi sopra puoi affidabilmente **leggere un file HTML in Python**, manipolare il DOM e ottenere esattamente ciò di cui hai bisogno.

## Cosa c'è dopo?

- **Esplora i selettori CSS:** Usa `soup.select_one('.my-class')` per query più flessibili.
- **Esegui scraping di più pagine:** Combina questo pattern con `requests` e un ciclo per elaborare più siti in batch.
- **Scrivi nuovamente su HTML:** BeautifulSoup ti permette anche di modificare l'albero e salvare le modifiche—utile per attività di templating.
- **Ottimizzazione delle prestazioni:** Per file di grandi dimensioni, considera parser in streaming come `lxml.etree.iterparse`.

Sentiti libero di sperimentare—cambia l'ID, prova tag diversi, o anche passa a `xml.etree.ElementTree` se lavori con XHTML. I concetti rimangono gli stessi, e ora hai una solida base per qualsiasi avventura di parsing HTML.

Buon coding! Se incontri un problema o hai un caso d'uso interessante da condividere, lascia un commento qui sotto.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Caricare documenti HTML da file in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Come interrogare HTML in Java – Tutorial completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Come modificare HTML usando Aspose.HTML per Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}