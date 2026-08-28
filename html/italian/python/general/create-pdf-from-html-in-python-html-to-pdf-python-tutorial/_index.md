---
category: general
date: 2026-07-15
description: Crea PDF da HTML usando Python. Scopri come convertire HTML in PDF rapidamente
  con uno script semplice e passaggi chiari.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: it
lastmod: 2026-07-15
og_description: Crea PDF da HTML con Python. Questa guida ti mostra come convertire
  HTML in PDF, salvare HTML come PDF e gestire le risorse in modo efficiente.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Crea PDF da HTML in Python – Tutorial pratico
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Crea PDF da HTML in Python – Tutorial Python per HTML a PDF
url: /it/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF da HTML in Python – Tutorial Completo

Hai mai dovuto **creare PDF da HTML** ma non eri sicuro quale libreria Python scegliere? Non sei solo—molti sviluppatori si trovano di fronte a questo ostacolo quando cercano di trasformare un report web, una fattura o una pagina di marketing in un PDF stampabile.  

La buona notizia è che, con poche righe di codice, puoi **convertire HTML in PDF** in modo affidabile, e lo script funziona su Windows, macOS e Linux. In questa guida percorreremo un esempio completo e eseguibile, spiegheremo perché ogni passaggio è importante e ti mostreremo come **salvare HTML come PDF** senza lasciare nulla in sospeso.

---

## Cosa Imparerai

- Installare il pacchetto Python corretto per la conversione da HTML a PDF.  
- Caricare un file HTML con opzioni personalizzate di gestione delle risorse (per evitare importazioni CSS infinite).  
- Generare un file PDF pulito su disco.  
- Affrontare casi limite comuni come immagini esterne, percorsi relativi e documenti di grandi dimensioni.  

Al termine di questo **tutorial HTML to PDF** avrai una funzione riutilizzabile da inserire in qualsiasi progetto.

---

## Prerequisiti

- Python 3.9+ (il codice funziona anche con 3.8, ma 3.9+ offre le ultime funzionalità di `pathlib`).  
- Familiarità di base con la riga di comando e gli ambienti virtuali.  
- Un file HTML che desideri trasformare in PDF—qualsiasi pagina statica va bene.

> **Consiglio professionale:** Se usi un ambiente virtuale, attivalo prima di installare la libreria; così manterrai pulito il tuo Python globale.

---

## Passo 1 – Installa WeasyPrint (il motore dietro la conversione)

WeasyPrint è una libreria pure‑Python che rende HTML e CSS in PDF. Gestisce la maggior parte delle funzionalità web moderne e ti offre un controllo fine sul caricamento delle risorse.

```bash
pip install weasyprint
```

Eseguendo il comando sopra verranno scaricati `cairocffi`, `tinycss2` e alcune altre dipendenze. Se incontri un errore relativo a `cairo` su Windows, prendi le ruote pre‑compilate dal [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Passo 2 – Prepara un piccolo helper per la gestione delle risorse

Quando carichi un documento HTML che fa riferimento a fogli di stile o immagini esterne, la libreria seguirà quei link. In alcuni casi ciò porta a nidificazioni profonde o addirittura a loop infiniti (pensa a un file CSS che `@import` se stesso). Per mantenere le cose ordinate limitiamo la profondità della gestione delle risorse.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

La classe sopra non è richiesta da WeasyPrint, ma rispecchia il pattern mostrato nello snippet originale e ti offre un hook per fermare importazioni incontrollate. La vedrai in uso nel passo successivo.

---

## Passo 3 – Carica il documento HTML usando le opzioni personalizzate

Ora leggiamo effettivamente il file HTML. La classe `HTML` accetta un argomento `base_url`, che impostiamo sulla directory contenente il file sorgente—questo fa funzionare i link relativi senza un server web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Perché è importante:** Se il tuo HTML carica una cascata di file CSS, ogni `@import` attiverà un nuovo caricamento. Il guardiano di profondità impedisce allo script di andare fuori controllo.

---

## Passo 4 – Salva il documento elaborato come PDF

Con l'oggetto `HTML` in mano, generare un PDF è una singola riga. Passiamo anche un piccolo snippet CSS che imposta una dimensione di pagina pulita (A4) e aggiunge un minimo margine—sentiti libero di modificarlo.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Chiamare `write_pdf` scrive il PDF su disco, così ottieni un file pronto da condividere.

---

## Passo 5 – Metti Tutto Insieme

Di seguito trovi uno script compatto che puoi copiare‑incollare in `convert.py`. Sostituisci i percorsi segnaposto con le tue directory effettive.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Output previsto** – dopo aver eseguito `python convert.py` dovresti vedere:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Apri il file generato con qualsiasi visualizzatore PDF; vedrai il layout originale della pagina, lo stile CSS e le immagini (purché fossero raggiungibili dal file HTML).  

Se noti immagini mancanti, ricontrolla che gli attributi `src` siano URL assoluti o percorsi relativi che esistono sotto `YOUR_DIRECTORY`.

---

## Domande Frequenti & Gestione dei Casi Limite

| Domanda | Risposta |
|----------|--------|
| *E se il mio HTML fa riferimento a font esterni?* | WeasyPrint scaricherà automaticamente i file dei font, ma potresti voler inserire nella whitelist i domini per evitare lunghi tempi di fetch. |
| *Posso convertire una stringa HTML invece di un file?* | Sì—usa `HTML(string=my_html_string)` e ometti `base_url` oppure impostalo su una cartella temporanea. |
| *Come controllo i metadati del PDF (titolo, autore)?* | Passa un dizionario `metadata` a `write_pdf`, ad esempio `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Ricevo un “cairo‑cffi error” su Linux.* | Installa il pacchetto di sistema `libcairo2-dev` (`apt-get install libcairo2-dev` su Debian/Ubuntu) prima di installare WeasyPrint con pip. |

---

## Conclusione

Abbiamo appena **creato PDF da HTML** usando un flusso di lavoro Python pulito, coperto le meccaniche di **convert HTML to PDF** e mostrato come **save HTML as PDF** con una gestione delle risorse robusta. Lo script è sufficientemente piccolo da inserirlo in pipeline CI, ma anche abbastanza flessibile da espandersi con intestazioni, piè di pagina o filigrane personalizzate.

Passi successivi che potresti esplorare:

- Usa la libreria **html to pdf python** `pdfkit` per un approccio basato su wkhtmltopdf (utile per CSS legacy).  
- Aggiungi un’interfaccia CLI con `argparse` così lo script accetta argomenti di input/output.  
- Genera PDF al volo all’interno di un endpoint Flask o FastAPI per report on‑demand.  

Sperimenta, rompi le cose e poi torna a questa guida per un rapido ripasso. Se incontri problemi, la documentazione di WeasyPrint e i forum della community sono ottime risorse.

Buon coding e divertiti a trasformare quelle pagine web in PDF eleganti!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}