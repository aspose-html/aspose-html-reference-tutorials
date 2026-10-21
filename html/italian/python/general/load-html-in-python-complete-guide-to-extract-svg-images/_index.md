---
category: general
date: 2026-06-10
description: Carica HTML in Python per estrarre le immagini SVG dalle tue pagine—codice
  passo‑passo, consigli e gestione dei casi limite.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: it
og_description: Carica HTML in Python ed estrai immagini SVG con un esempio chiaro
  e eseguibile. Scopri come cercare gli elementi SVG nell'HTML e gestire i casi limite.
og_title: Carica HTML in Python – Estrai immagini SVG in modo efficiente
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Caricare HTML in Python – Guida completa per estrarre immagini SVG
url: /it/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Caricare HTML in Python – Guida Completa per Estrarre Immagini SVG

Hai mai dovuto **caricare HTML in Python** solo per estrarre tutte le grafiche SVG da una pagina? Non sei l’unico. Che tu stia costruendo uno scraper web, generando un report di asset, o semplicemente sia curioso di sapere quali icone usa un sito, sapere come **estrarre immagini SVG** ti fa risparmiare molto tempo di ricerca manuale.

In questo tutorial percorreremo una soluzione pratica, end‑to‑end, che **carica HTML in Python**, poi **cerca elementi HTML SVG**, **trova SVG inline** e persino recupera i file SVG esterni referenziati da tag `<img>`. Alla fine avrai uno script riutilizzabile, una serie di consigli per le parti più complesse e un quadro chiaro di come appare l’output.

## Cosa Imparerai

* Uno script Python completamente eseguibile che analizza un file HTML locale (o una pagina recuperata) e elenca tutti gli SVG che riesce a trovare.  
* La differenza tra **SVG inline** (`<svg>…</svg>`) e **SVG esterno** (`<img src="… .svg">`).  
* Strategie per gestire markup malformato, file mancanti e particolarità dei namespace.  
* Idee per estendere il codice—salvare gli SVG, convertirli in PNG, o inserirli in un database.

### Prerequisiti

* Python 3.8+ installato.  
* Familiarità di base con le librerie Python `requests` e `BeautifulSoup` (le importeremo, non serve un approfondimento).  
* Un file HTML locale o un URL che vuoi analizzare.  

Ora, immergiamoci.

## Caricare HTML in Python – Configurare il Parser

Il primo passo è **caricare HTML in Python**. Puoi leggere un file dal disco o recuperare una pagina remota. Di seguito trovi un helper minimale ma robusto che fa entrambe le cose:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Perché è importante:** L’uso di `BeautifulSoup` astrae le stranezze del parsing di stringhe grezze, e la funzione gestisce elegantemente sia file locali sia URL remoti. Inoltre solleva un’eccezione se una richiesta di rete fallisce—così saprai subito quando qualcosa è andato storto.

## Estrarre Immagini SVG – Trovare Elementi SVG Inline

Una volta caricato il documento, il passo successivo è **trovare i tag SVG inline**. L'SVG inline è incorporato direttamente nel markup HTML, il che significa che puoi prelevarlo direttamente dal DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Consiglio professionale:* Se la pagina utilizza namespace SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` trova comunque il tag perché ignora i namespace per impostazione predefinita. È una comoda scorciatoia quando vuoi semplicemente **cercare HTML SVG**.

## Cercare HTML SVG – Gestire Riferimenti `<img>` Esterni

Molti siti non incorporano SVG direttamente; li referenziano tramite file esterni con `<img src="icon.svg">`. Per catturarli, dobbiamo iterare su tutti i tag `<img>`, controllare il loro `src` e verificare se termina con `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Attenzione ai casi limite:** Alcune pagine usano query string (`icon.svg?v=2`) o frammenti (`icon.svg#layer`). Il controllo `endswith(".svg")` funziona comunque perché consideriamo solo la parte finale della stringa in minuscolo. Se ti serve una validazione più rigorosa, valuta l’uso di `urllib.parse` per rimuovere i parametri prima.

## Trovare SVG Inline – Segnalare i Risultati

Ora che abbiamo due liste—una per il markup SVG inline e un’altra per i riferimenti a file esterni—possiamo combinarle e segnalare il conteggio totale. Questo rispecchia lo snippet originale che hai pubblicato, ma aggiunge un po’ più di contesto.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Mettere Tutto Insieme – Script Completo

Di seguito trovi il programma completo, pronto per l’esecuzione. Salvalo come `extract_svg.py` e puntalo a un file HTML locale o a un URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Output Atteso

Eseguendo lo script su un esempio `sample.html` potresti ottenere:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Se decommenti il blocco di download, gli SVG esterni


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}