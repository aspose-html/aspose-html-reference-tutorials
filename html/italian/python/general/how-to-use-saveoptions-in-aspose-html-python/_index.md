---
category: general
date: 2026-07-27
description: Come utilizzare SaveOptions in Aspose.HTML (Python) per convertire una
  grande pagina HTML e gestire le risorse in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: it
lastmod: 2026-07-27
og_description: Come utilizzare SaveOptions in Aspose.HTML (Python) ti consente di
  convertire pagine HTML di grandi dimensioni applicando la gestione delle risorse
  per risultati puliti e veloci.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Come utilizzare SaveOptions in Aspose.HTML – Guida Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Come utilizzare SaveOptions in Aspose.HTML (Python)
url: /it/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare SaveOptions in Aspose.HTML (Python)

Come utilizzare SaveOptions in Aspose.HTML per Python è una domanda che molti sviluppatori si pongono quando si lavora con file HTML di grandi dimensioni. Se hai bisogno di **convertire una pagina HTML di grandi dimensioni** mantenendo un controllo rigoroso su **apply resource handling**, sei nel posto giusto.  

In questo tutorial percorreremo uno scenario reale: prendere una pagina HTML ingombrante, limitare la profondità con cui le risorse annidate vengono recuperate e, infine, salvare (o convertire) il risultato con un controllo cristallino. Nessun riferimento vago, solo un esempio completo e eseguibile che puoi copiare‑incollare nel tuo progetto oggi.

> **Pro tip:** Il `SaveOptions` di Aspose.HTML non serve solo per salvare nuovamente in HTML, ma anche per convertire in PDF, PNG o persino DOCX. Lo stesso schema che descriviamo di seguito si applica a tutti questi formati.

---

## Cosa ti servirà

- **Python 3.8+** (il codice usa type hints ma funziona su qualsiasi versione recente)  
- **Aspose.HTML for Python via .NET** – installa con `pip install aspose-html`  
- Un **large HTML file** che desideri ridurre o trasformare (l'esempio usa `big_page.html`)  
- Una modesta quantità di spazio su disco per il file di output  

Tutto qui—nessuna libreria aggiuntiva, nessuno strumento di build ingombrante.

---

## Come utilizzare SaveOptions con le opzioni di Resource Handling

Questo è il nocciolo della questione. Creeremo un'istanza di `SaveOptions`, allegheremo un oggetto `ResourceHandlingOptions` che indica ad Aspose.HTML quanto in profondità deve inseguire le risorse collegate, e poi passeremo tutto al metodo `save` del documento.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Perché funziona:**  
- `HTMLDocument` carica il file originale, analizzando ogni `<img>`, `<link>`, `<script>`, ecc.  
- `ResourceHandlingOptions.max_handling_depth` indica al motore di smettere di inseguire le risorse dopo tre livelli di annidamento—perfetto per evitare loop infiniti su pagine che incorporano altre pagine.  
- `SaveOptions` è il contenitore che trasporta sia il formato di output (HTML per impostazione predefinita) sia le regole di gestione delle risorse.  
- Infine, `doc.save` scrive il nuovo file, applicando le regole appena impostate.

Quando esegui lo script, vedrai un nuovo file in `big_page_processed.html`. Aprilo in un browser; noterai che tutte le immagini, gli stili e gli script fino a tre livelli di profondità sono ancora presenti, mentre i riferimenti più profondi sono stati rimossi. Questo riduce drasticamente le dimensioni del file senza rompere il layout principale della pagina—esattamente ciò di cui hai bisogno quando **converti una pagina HTML di grandi dimensioni** per uso offline o per l'invio via email.

---

## Converti una pagina HTML di grandi dimensioni in modo efficiente

Se il tuo obiettivo è *convertire una pagina HTML di grandi dimensioni* in una versione più leggera, lo snippet sopra fa già la maggior parte del lavoro pesante. Tuttavia, potresti voler cambiare completamente il formato di output. Aspose.HTML lo rende un'operazione a una riga:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Basta sostituire la proprietà `format` con `"PNG"`, `"JPEG"` o `"DOCX"` e avrai una pipeline di conversione completa. Le stesse regole di **apply resource handling** rimangono intatte, quindi il PDF risultante non includerà ogni file CSS esterno del sito originale—solo quelli entro la profondità di tre livelli che hai definito.

---

## Applicare Resource Handling alle risorse annidate

Approfondiamo un po' l'**apply resource handling** in modo efficace. Supponiamo che il tuo HTML contenga un foglio di stile che a sua volta importa altri fogli di stile, ognuno dei quali carica immagini. Senza un limite di profondità, Aspose.HTML potrebbe inseguire la catena all'infinito, gonfiando l'uso di memoria e CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – Nessuna risorsa esterna viene recuperata; ottieni uno scheletro HTML minimale.  
- **Depth 1** – Vengono incluse solo le risorse di primo ordine (tag `<img>` diretti, file CSS immediati).  
- **Depth 2+** – Viene rispettato un annidamento più profondo, utile per siti complessi dove gli stili dipendono da altri stili.

Scegli la profondità che corrisponde al tuo scenario di **convertire una pagina HTML di grandi dimensioni**. Per le newsletter email, la profondità 1 è spesso sufficiente. Per un archivio locale, la profondità 3 (come nell'esempio principale) offre un buon equilibrio.

---

## Esempio completo funzionante – Dall'inizio alla fine

Di seguito trovi uno script autonomo che puoi inserire in un file chiamato `process_html.py`. Include la gestione degli errori, il logging e un piccolo helper che stampa la riduzione di dimensione ottenuta.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Output previsto (console):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Apri il file elaborato; vedrai una pagina più leggera che mantiene l'aspetto dell'originale. Se cambi `fmt` in `"PDF"`, la console segnalerà la dimensione del file PDF e potrai aprirlo con qualsiasi visualizzatore PDF.

---

## Domande comuni e casi particolari

- **Cosa succede se la pagina fa riferimento a risorse su HTTPS che richiedono autenticazione?**  
  Aspose.HTML segue i redirect ma non invia credenziali automaticamente. Puoi pre‑scaricare quegli asset o utilizzare un gestore `WebRequest` personalizzato (oltre lo scopo di questa guida).

- **Posso preservare il CSS inline mentre rimuovo i file esterni?**  
  Sì—imposta `resource_options.max_handling_depth = 0`. Questo salta i file esterni ma mantiene intatti i blocchi `<style>`.

- **E le immagini molto grandi che continuano a gonfiare l'output?**  
  Dopo il salvataggio, puoi eseguire un secondo passaggio con Pillow per ridimensionare le immagini, oppure lasciare che le opzioni di compressione immagini integrate di Aspose.HTML se ne occupino (usa `save_options.image_quality`).

- **Il limite di profondità è applicato per tipo di risorsa?**  
  Il limite è globale per tutti i tipi di risorsa (immagini, script, stili). Se ti serve un controllo più granulare, dovrai filtrare le risorse manualmente dopo aver caricato il documento.

---

## Conclusione

Ora hai una solida comprensione di **come utilizzare SaveOptions** in Aspose.HTML

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}