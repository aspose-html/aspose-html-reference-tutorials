---
category: general
date: 2026-11-17
description: converti svg in png usando Python in poche righe. impara a salvare SVG
  come PNG con impostazioni di conversione opzionali.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: it
lastmod: 2026-11-17
og_description: converti svg in png in Python con un esempio conciso. segui i passaggi
  per esportare SVG come PNG in modo efficiente.
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: Converti SVG in PNG con Python – guida rapida
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: Come convertire SVG in PNG con Python – guida passo passo
url: /it/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire SVG in PNG in Python – guida passo‑passo

Se hai bisogno di **convertire svg in png**, questa guida mostra una soluzione completa che puoi eseguire subito. Vedrai anche come **salvare svg come png** con impostazioni opzionali per dimensione e colore di sfondo.

Generare immagini raster da file SVG vettoriali è comune quando fornisci grafiche ai browser, crei miniature o inserisci immagini nei PDF. Il tutorial copre tutto, dall'installazione della libreria necessaria alla gestione di casi particolari come file mancanti o SVG molto grandi.

## Prerequisiti

* Python 3.8 o versioni successive installate.
* Accesso a un terminale o prompt dei comandi.
* Il pacchetto `cairosvg`, che esegue il lavoro pesante per la conversione **svg in immagine raster**.

Puoi installare il pacchetto con un unico comando pip:

```bash
pip install cairosvg
```

> **Consiglio professionale:** Usa un ambiente virtuale per mantenere le dipendenze isolate da altri progetti.

## Come convertire SVG in PNG in Python

Il nucleo del processo consiste in tre azioni: caricare l'SVG, opzionalmente regolare i parametri di conversione e scrivere il file PNG. Il codice qui sotto implementa tutti e tre i passaggi in una funzione riutilizzabile.

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Perché funziona

* `cairosvg.svg2png` legge il file SVG (`url=svg_path`) e scrive un file PNG (`write_to=png_path`).  
* La funzione solleva un errore chiaro se l'SVG di origine non può essere trovato, il che ti aiuta a debugare i problemi di percorso del file fin da subito.  
* Tenere la logica di conversione all'interno di una funzione la rende facile da riutilizzare in più script o da integrare in applicazioni più grandi.

## Opzionale: perfeziona la conversione

Se hai bisogno di una dimensione di output specifica o di uno sfondo diverso, `cairosvg.svg2png` accetta argomenti aggiuntivi. Di seguito è una variante che imposta una larghezza di 300 px e uno sfondo bianco.

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

Puoi chiamare questa funzione nello stesso modo della versione base, passando qualsiasi larghezza o colore preferisci.

## Domande comuni e casi particolari

**Cosa succede se l'SVG contiene font esterni?**  
`cairosvg` incorpora automaticamente i font referenziati, ma i file dei font devono essere raggiungibili dalla posizione dell'SVG. Posiziona i file dei font accanto all'SVG o usa URL assoluti.

**Come gestire SVG molto grandi?**  
I file di grandi dimensioni possono consumare molta memoria. Puoi trasmettere (stream) il contenuto SVG invece di caricarlo dal disco:

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Posso convertire più file in batch?**  
Avvolgi la chiamata di conversione in un ciclo e usa `Path.glob("*.svg")` per scoprire tutti gli SVG in una directory.

## Output previsto

Eseguire lo script di esempio stampa una singola riga che conferma la conversione:

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

Il file risultante `image.png` si trova nella stessa directory e può essere aperto con qualsiasi visualizzatore di immagini.

## Conclusione

Ora sai come **convertire svg in png** in Python, come **salvare svg come png**, e come **esportare svg come png** con dimensioni personalizzate. Lo stesso approccio funziona per qualsiasi file SVG, trasformando le grafiche vettoriali in un formato **svg in immagine raster** adatto per pagine web, report o miniature.

I prossimi passi potrebbero includere:

* Esplorare i parametri `export svg as png` per il controllo DPI.
* Integrare la funzione di conversione in un endpoint Flask o Django per fornire la generazione di immagini on‑the‑fly.
* Usare la keyword secondaria **how to convert svg to png** per cercare casi d'uso più avanzati come l'elaborazione batch o pipeline CI/CD.

Sentiti libero di sperimentare con impostazioni diverse e condividere i tuoi risultati con la community!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}