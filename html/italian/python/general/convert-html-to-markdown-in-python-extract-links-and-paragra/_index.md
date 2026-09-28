---
category: general
date: 2026-09-26
description: Converti HTML in Markdown con Python, estraendo i link dall'HTML e salvando
  l'HTML come Markdown. Scopri come convertire l'HTML passo passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: it
lastmod: 2026-09-26
og_description: Converti HTML in Markdown con Python, estraendo i link dall'HTML e
  salvando l'HTML come Markdown. Segui questa guida completa.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Converti HTML in Markdown con Python – estrai link e paragrafi
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Converti HTML in Markdown con Python – estrai facilmente link e paragrafi
url: /it/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti HTML in Markdown con Python – estrai link e paragrafi facilmente

Se hai bisogno di **convertire HTML in Markdown** mantenendo solo le parti utili, questa guida ti mostra come farlo con poche righe di Python. Che tu stia estraendo post di blog, archiviando documentazione o pulendo il corpo delle email, imparerai un metodo affidabile per estrarre link da HTML e salvare HTML come Markdown.

Il tutorial copre tutto, dall'installazione del pacchetto necessario alla gestione di casi particolari come tag `<a>` vuoti o paragrafi annidati. Alla fine avrai uno script pronto all'uso che **converte HTML in Markdown**, estrae link da HTML e persino estrae paragrafi da HTML quando ti servono.

---

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.8 o versioni successive installate  
* Accesso al pacchetto Python `groupdocs-conversion` (la libreria che fornisce `HTMLDocument`, `MarkdownSaveOptions` e `Converter`)  
* Un file HTML locale da elaborare (ad esempio `article.html`)

Puoi installare la libreria con pip:

```bash
pip install groupdocs-conversion
```

> **Suggerimento professionale:** Usa un ambiente virtuale (`python -m venv venv`) per mantenere le dipendenze isolate.

---

## Passo 1: Carica il documento HTML sorgente

La prima operazione è creare un oggetto `HTMLDocument` che punti al tuo file sorgente. Questo oggetto astrae l'HTML grezzo e fornisce al convertitore un punto di ingresso pulito.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Perché è importante:* Caricare il documento in questo modo consente alla libreria di analizzare il DOM una sola volta, così le operazioni successive (come l'estrazione di link o paragrafi) sono veloci ed efficienti in termini di memoria.

---

## Passo 2: Crea le opzioni di salvataggio Markdown e seleziona le funzionalità di cui hai bisogno

`MarkdownSaveOptions` ti permette di decidere quali elementi HTML sopravvivono alla conversione. Il flag `features` utilizza un OR bitwise per combinare le opzioni.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Perché è importante:* Specificando `LINKS` e `PARAGRAPHS` **estrai link da HTML** e **estrai paragrafi da HTML** scartando tutto il resto (stili, script, immagini). Se in seguito ti servono solo i link, sostituisci `MarkdownFeatures.PARAGRAPHS` con `0` (o omettilo).

---

## Passo 3: Converti l'HTML in Markdown usando le opzioni configurate

Ora chiama il metodo statico `convert_html`, passando il documento sorgente, il percorso di destinazione e le opzioni appena create.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Perché è importante:* La conversione avviene in un unico passaggio, applicando il filtro di funzionalità che hai definito. Il file risultante (`article_links.md`) contiene solo link e paragrafi formattati in Markdown, esattamente ciò di cui hai bisogno quando vuoi **salvare HTML come Markdown** per ulteriori elaborazioni.

---

## Script completo – tutto insieme

Di seguito trovi uno script completo, eseguibile, che puoi copiare‑incollare in un file chiamato `html_to_md.py`. Regola i percorsi in base al tuo ambiente.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Output previsto

Eseguendo lo script si genera un file simile al seguente (il contenuto esatto dipende dall'HTML sorgente):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Appaiono solo il testo del link e il testo del paragrafo; tutti gli altri elementi HTML vengono rimossi.

---

## Estrarre solo link o solo paragrafi (varianti avanzate)

A volte hai bisogno di **come convertire HTML** in un file Markdown che contenga solo un tipo di elemento.

### 1. Estrarre solo i link

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Estrarre solo i paragrafi

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Entrambe le varianti riutilizzano la stessa chiamata `convert_html`, così non devi scrivere logiche di conversione separate.

---

## Gestione dei casi particolari

| Situazione                               | Correzione consigliata |
|------------------------------------------|------------------------|
| Il file HTML contiene tag `<a>` vuoti    | Il convertitore salta automaticamente i link vuoti. Se vedi voci `[]()` residue, imposta `md_options.removeEmptyLinks = True`. |
| Paragrafi annidati (`<p>` dentro `<div>`) | La libreria appiattisce i paragrafi annidati, preservando l'ordine del testo. Nessun codice aggiuntivo necessario. |
| Caratteri non ASCII nei titoli dei link | Assicurati che il tuo file Python sia salvato con codifica UTF‑8 e apri il file di output con `encoding="utf-8"` se lo leggi in seguito. |
| File HTML molto grandi (≥ 50 MB)         | Processa il file a blocchi usando `HTMLDocument(stream=io.BytesIO(...))` per evitare di caricare l'intero file in memoria. |

---

## Domande frequenti

**D: Funziona con frammenti HTML (senza tag `<html>` radice)?**  
R: Sì. `HTMLDocument` accetta qualsiasi frammento ben formato; il convertitore tratta il frammento come corpo del documento.

**D: Posso mantenere le immagini con la sintassi Markdown per le immagini?**  
R: Aggiungi `MarkdownFeatures.IMAGES` al flag `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**D: Come converto molti file in una directory?**  
R: Avvolgi `convert_html_to_markdown` in un ciclo che attraversa la directory con `os.listdir` o `pathlib.Path.rglob("*.html")`.

---

## Conclusione

Ora sai come **convertire HTML in Markdown** con Python, estraendo selettivamente **link da HTML** e **paragrafi da HTML**. Lo script dimostra l'approccio standard—caricare il documento, configurare `MarkdownSaveOptions` e eseguire `Converter.convert_html`. Con qualche piccola modifica puoi anche **salvare HTML come Markdown** contenente solo link, solo paragrafi o una rappresentazione completa e fedele.

Prossimi passi consigliati:

* Aggiungere `MarkdownFeatures.HEADINGS` per preservare i titoli di sezione.  
* Usare il Markdown risultante come input per generatori di siti statici come MkDocs o Hugo.  
* Automatizzare conversioni di massa per un intero repository di documentazione.

Buona conversione!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}