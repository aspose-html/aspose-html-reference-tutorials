---
category: general
date: 2026-10-21
description: Impara a analizzare l'HTML in Python, caricare un documento HTML, utilizzare
  i selettori CSS ed estrarre rapidamente i collegamenti ipertestuali dall'HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: it
lastmod: 2026-10-21
og_description: Come analizzare l'HTML in Python usando i selettori CSS. Carica un
  documento HTML, seleziona i link ed estrai gli hyperlink dall'HTML con codice pulito.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Come analizzare l'HTML in Python – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Come analizzare l'HTML in Python usando i selettori CSS
url: /it/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come analizzare HTML in Python usando i selettori CSS

Se hai bisogno di **come analizzare html** in uno script Python, questa guida ti mostra esattamente come fare. Imparerai a caricare un documento HTML, a usare la sintassi dei selettori per trovare gli elementi e a estrarre i collegamenti ipertestuali da html senza scrivere un parser personalizzato.

L'analisi di HTML è un compito comune per scraper web, pipeline di data‑analysis o test automatizzati. Alla fine di questo tutorial avrai una funzione riutilizzabile che carica un documento HTML, seleziona tutti i tag `<a>` con un selettore CSS e restituisce un elenco pulito di URL.

## Cosa ti servirà

- Python 3.8+ (il codice funziona su qualsiasi versione recente)  
- La libreria **lxml** (`pip install lxml`) – fornisce parsing HTML veloce e supporto ai selettori CSS  
- Un file HTML che vuoi analizzare (ad es., `sample.html`)  

Non sono necessari strumenti aggiuntivi; tutto funziona con la libreria standard e un unico pacchetto di terze parti.

## Passo 1: Come analizzare HTML – caricare il documento

Il primo passo in qualsiasi workflow HTML è leggere il file in memoria. Usare **lxml.html** ti fornisce un oggetto albero che supporta i selettori CSS.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Perché è importante:**  
`load_html` astrae il boilerplate di lettura del file e garantisce che il documento sia analizzato con un parser HTML tollerante. Questo è il modo più sicuro per **load html document python** senza preoccuparsi di markup malformato.

## Passo 2: Come usare il selettore – trovare tutti gli elementi link

Una volta caricato il documento, puoi usare un selettore CSS per individuare ogni tag `<a>`. Il selettore `"a"` corrisponde a tutti gli elementi anchor, ma puoi affinarlo (ad es., `"a.external"` o `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Perché è importante:**  
L'approccio **how to use selector** ti permette di esprimere query complesse in una singola stringa leggibile, evitando la traversata manuale dell'albero. Funziona per qualsiasi pattern CSS supportato da `lxml.cssselect`.

## Passo 3: Estrarre i collegamenti ipertestuali da HTML e elaborarli

Ora che hai un elenco di elementi `<a>`, puoi estrarre l'attributo `href` da ciascuno. L'helper qui sotto normalizza anche gli URL relativi rispetto a un URL di base (se ne fornisci uno).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Output previsto** (supponendo che `sample.html` contenga tre link):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Perché è importante:**  
`extract_hyperlinks` è il cuore di **extract hyperlinks from html**. Gestisce elegantemente gli attributi `href` mancanti, risolve i link relativi e restituisce una semplice lista Python che puoi passare a ulteriori elaborazioni (ad es., requests, pandas o un database).

## Esempio completo end‑to‑end

Unendo le tre funzioni ottieni uno script unico che carica un file, seleziona tutti gli anchor e stampa ogni collegamento ipertestuale.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Eseguendo `python parse_links.py` stampa ogni collegamento ipertestuale, completamente risolto, sulla console. Questo script dimostra **how to parse html**, **how to use selector** e **extract hyperlinks from html** in un unico flusso riutilizzabile.

## Varianti comuni e gestione dei casi limite

| Situazione | Cosa cambiare | Motivo |
|------------|---------------|--------|
| **Sono necessari solo URL assoluti** | Omettere l'argomento `base_url` in `extract_hyperlinks` | Mantiene intatti gli URL relativi |
| **Hai bisogno anche del testo del link** | Restituire una tupla `(href, link.text_content())` da `extract_hyperlinks` | Ti consente di salvare sia l'URL sia il testo dell'anchor |
| **File HTML di grandi dimensioni** | Usare `lxml.etree.iterparse` con un filtro di selettore CSS | Riduce l'uso di memoria tramite streaming |
| **Selettore diverso** | Sostituire `"a"` con `"nav a[href]"` o `"div.content a.external"` | Mira a un sottoinsieme di link, utile per **how to use selector** in pagine complesse |

**Consiglio professionale:** Valida sempre gli URL estratti prima di effettuare richieste di rete. Un rapido controllo con `urlparse` può filtrare stringhe malformate e proteggere il tuo scraper da crash.

## Conclusione

Ora sai **how to parse html** in Python, come **load html document python**, come **how to use selector** per mirare gli elementi e come **extract hyperlinks from html** in modo efficiente. L'esempio completo sopra è pronto per essere copiato‑incollato nel tuo progetto, e puoi adattare ogni funzione per casi d'uso più avanzati come paginazione, contenuti generati da JavaScript o crawling multi‑pagina.

Passi successivi che potresti esplorare includono:

- Usare **requests‑html** o **Playwright** per recuperare pagine che richiedono l'esecuzione di JavaScript.  
- Salvare gli URL estratti in un CSV o in un database SQLite per analisi successive.  
- Aggiungere gestione degli errori per timeout di rete e codici di stato HTTP.

Buona analisi e sentiti libero di sperimentare con diversi selettori per sbloccare tutta la potenza delle query HTML basate su CSS in Python!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}