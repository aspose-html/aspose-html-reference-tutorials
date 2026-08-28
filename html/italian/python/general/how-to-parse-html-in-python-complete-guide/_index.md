---
category: general
date: 2026-05-28
description: Come analizzare rapidamente HTML in Python — caricare il file HTML, utilizzare
  un selettore CSS ed estrarre gli attributi href con un esempio di XPath contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: it
og_description: 'Come analizzare l''HTML in Python: impara a caricare un file HTML,
  utilizzare i selettori CSS e ottenere gli attributi href con un esempio di XPath
  contains.'
og_title: Come analizzare l'HTML in Python – Passo dopo passo
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Come analizzare HTML in Python – Guida completa
url: /it/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come analizzare HTML in Python – Guida completa

Ti sei mai chiesto **come analizzare HTML** in uno script Python senza dover ricorrere a un browser ingombrante? Non sei l'unico. La maggior parte di noi ha solo bisogno di **caricare un file HTML**, estrarre qualche titolo e magari recuperare uno o due link per il download. In questo tutorial ti mostrerò esattamente questo—usando una piccola libreria, un selettore CSS e un esempio di XPath contains per **ottenere i valori dell'attributo href**.

Percorreremo l'intero processo, dalla lettura di un documento HTML locale alla stampa dei dati che ti interessano. Nessuna perdita di tempo, solo un esempio pratico e funzionante che puoi inserire nel tuo progetto già da oggi.

## Cosa imparerai

- Come **caricare un file HTML** con un parser leggero.
- Come **usare la sintassi dei selettori CSS** per recuperare elementi come i titoli degli articoli.
- Come creare un **esempio di XPath contains** che filtra i link.
- Come ottenere in modo sicuro i valori dell'**attributo href** dai nodi corrispondenti.
- Suggerimenti per gestire markup malformato ed estendere lo script.

Ti basta Python 3.8+ e i pacchetti `lxml` e `cssselect`—entrambi installabili con un unico comando `pip`.

---

## Passo 1: Carica il file HTML

Prima di tutto, devi avere il contenuto HTML in memoria. Il modulo `lxml.html` fornisce un comodo helper `fromstring`, ma quando hai un file su disco la funzione `parse` è ancora più pulita.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Perché è importante:** Caricare il file una sola volta mantiene basso l'uso di memoria e ti fornisce un unico oggetto `root` che supporta sia i selettori CSS sia le query XPath. Se il file manca o non è leggibile, `html.parse` solleverà un chiaro `OSError`, che potrai gestire in seguito.

### Pro tip
Se lavori con una stringa anziché con un file, sostituisci `html.parse` con `html.fromstring(your_html_string)`.

---

## Passo 2: Usa il selettore CSS per ottenere i titoli

I selettori CSS sono concisi e familiari a chiunque abbia scritto un foglio di stile. Prendiamo tutti i `<h2>` all'interno di un `<article>`—perfetti per i titoli delle notizie.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Output previsto** (supponendo che l'HTML di esempio contenga due articoli):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Perché CSS?** È leggibile, veloce e funziona subito con `lxml`. Il metodo `cssselect` traduce il selettore in un'espressione XPath dietro le quinte, offrendoti il meglio di entrambi i mondi.

---

## Passo 3: Esempio di XPath contains – Trova i link “download”

A volte serve un controllo più granulare di quello offerto da CSS. La funzione `contains()` di XPath brilla quando vuoi corrispondere una sottostringa all'interno di un attributo, come tutti i link che puntano a un download.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Output di esempio**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Perché XPath contains?** Ti consente di filtrare direttamente sui valori degli attributi senza loop Python aggiuntivi. Questo è il classico **xpath contains example** che vedi spesso nei tutorial, ma qui è accoppiato a un caso d'uso reale.

---

## Passo 4: Raggruppa tutto in una funzione riutilizzabile

Hard‑coding di percorsi e stampe va bene per un test veloce, ma il codice di produzione preferisce le funzioni. Di seguito trovi un compatto helper che restituisce sia i titoli che i link per il download.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Ora puoi chiamare la funzione e stampare i risultati in modo leggibile:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Eseguire lo script produce lo stesso output di prima, ma ora è confezionato ordinatamente per il riutilizzo.

---

## Passo 5: Gestione dei casi limite e delle insidie comuni

1. **Attributo `href` mancante** – XPath restituirà comunque il nodo `<a>` anche se `href` è assente. Proteggi il tuo codice da `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **URL relativi vs. assoluti** – Se i tuoi link sono relativi, potresti volerli risolvere rispetto all'URL di base:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **HTML malformato** – `lxml` è indulgente, ma un markup estremamente rotto può causare un `XMLSyntaxError` in `html.parse`. Avvolgi la chiamata di parsing in un blocco `try/except` per registrare e saltare i file problematici.

4. **Prestazioni con file di grandi dimensioni** – Per pagine multi‑megabyte, considera lo streaming con `iterparse` invece di caricare l'intero DOM in memoria.

---

## Panoramica visiva (opzionale)

![Come analizzare HTML diagramma di flusso che mostra carica file → selettore CSS → XPath contains → ottieni attributo href](how-to-parse-html-flow.png "Come analizzare HTML diagramma di flusso")

*Il testo alternativo include la parola chiave principale per soddisfare la SEO.*

---

## Conclusione

Abbiamo coperto **come analizzare HTML** in Python dall'inizio alla fine: caricamento di un file HTML, utilizzo di un selettore CSS per estrarre i titoli degli articoli, creazione di un esempio di XPath contains per individuare i link di download e, infine, **ottenere in modo sicuro i valori dell'attributo href**. La funzione riutilizzabile `parse_news_html` dimostra un approccio pulito e manutenibile che puoi adattare a qualsiasi compito di scraping.

Pronto per la prossima sfida? Prova ad estendere lo script per:

- Analizzare tabelle con query XPath `//table//tr`.
- Estrarre gli attributi `src` delle immagini usando un altro **xpath contains example**.
- Passare al fetching asincrono con `aiohttp` per pagine web live.

Buona analisi, e ricorda—una volta che avrai padroneggiato queste basi, il resto dello scraping HTML diventerà un gioco da ragazzi. Se incontri problemi, lascia un commento qui sotto—risolviamo insieme!

## Tutorial correlati

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}