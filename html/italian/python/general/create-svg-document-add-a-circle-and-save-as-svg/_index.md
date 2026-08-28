---
category: general
date: 2026-07-31
description: Impara a creare un documento SVG, aggiungere un cerchio e salvare rapidamente
  il file SVG. Esporta il grafico come SVG con poche righe di codice Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: it
lastmod: 2026-07-31
og_description: Crea un documento SVG, aggiungi un cerchio e salva il file SVG in
  pochi secondi. Questa guida ti mostra come esportare il grafico come SVG con codice
  chiaro e funzionante.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Crea documento SVG – Aggiungi un cerchio e salva come SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Crea documento SVG – Aggiungi un cerchio e salva come SVG
url: /it/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea documento SVG – Aggiungi un cerchio e salva come SVG

Hai mai avuto bisogno di **create SVG document** dal codice ma non sapevi da dove cominciare? Non sei solo; molti sviluppatori incontrano questo ostacolo quando si avvicinano per la prima volta alla grafica vettoriale. In questo tutorial passeremo in rassegna un piccolo esempio autonomo che ti mostra come **add circle to SVG**, poi **save SVG file** così potrai **export graphic as SVG** per l'uso sul web o negli strumenti di design.

Terremo le cose leggere: solo poche righe di Python, una popolare libreria di supporto SVG e una breve spiegazione. Alla fine avrai un `circle.svg` pronto all'uso nella tua cartella, e comprenderai perché ogni passaggio è importante—senza vaghi scorciatoie “vedi la documentazione”.

## Cosa ti servirà

- Python 3.8+ (qualsiasi versione recente va bene)
- Il pacchetto `svgwrite` – installalo con `pip install svgwrite`
- Un editor di testo o IDE (VS Code, PyCharm, o anche Notepad va bene)
- Permessi di scrittura nella directory in cui vuoi salvare il file

Tutto qui. Nessuna dipendenza pesante, nessun servizio esterno.

## Passo 1: Configura il documento SVG

Creare un documento SVG è semplice come istanziare un oggetto `Drawing` da `svgwrite`. Pensa a questo oggetto come alla tela vuota dove vive ogni forma.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Perché è importante:** La classe `Drawing` gestisce tutto il boilerplate XML per te—namespace, intestazioni e l'elemento radice `<svg>`. Specificando un nome file in anticipo sappiamo già dove finirà il file, il che rende il passaggio successivo **save svg file** banale.

### Consiglio professionale
Se prevedi di generare molti file in un ciclo, assegna a ogni `Drawing` un nome unico o usa `io.BytesIO` per tenere tutto in memoria finché non sei pronto a scrivere.

## Passo 2: Aggiungi un cerchio al SVG

Ora che il documento esiste, aggiungiamo **add circle to SVG**. Il metodo `add()` accetta qualsiasi oggetto forma; un `Circle` è perfetto per un semplice punto rosso al centro.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Perché usiamo le variabili `center` e `radius`:** Inserire numeri direttamente rende il codice più difficile da leggere e mantenere. Dando un nome ai valori chiariamo l'intento—questo cerchio è esattamente al centro di una tela 200 × 200 e abbastanza grande da essere evidente.

### Caso limite – Sfondo trasparente
Se ti serve uno sfondo trasparente (il valore predefinito per SVG), puoi omettere l'impostazione di `fill` sulla radice. Per uno sfondo bianco, aggiungi:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Posiziona questo prima di aggiungere il cerchio così il rettangolo rimane sotto.

## Passo 3: Salva il file SVG

Con la forma al suo posto, l'ultimo passo è **save SVG file**. Il metodo `save()` scrive l'XML su disco, e poiché abbiamo già dato al `Drawing` un nome file, una singola chiamata fa il lavoro.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Cosa succede dietro le quinte?** `svgwrite` serializza l'albero degli elementi in una stringa, aggiunge la dichiarazione XML e lo scrive usando la codifica UTF‑8. Se la directory di destinazione non esiste, Python solleverà un `FileNotFoundError`; assicurati che il percorso sia valido o crealo con `os.makedirs()`.

### Bonus: Esporta la grafica come SVG programmaticamente
Se ti serve il contenuto SVG come stringa—ad esempio, per incorporarlo in un'email HTML—puoi chiamare `dwg.tostring()` invece di `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script completo, pronto da eseguire:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Output previsto:** Dopo aver eseguito lo script, vedrai un file `circle.svg` nella stessa cartella. Aprirlo in un browser o in qualsiasi editor vettoriale mostra un cerchio rosso centrato su un quadrato bianco—esattamente ciò che abbiamo programmato.

## Domande comuni e insidie

- **E se volessi una forma diversa?** Sostituisci `dwg.circle` con `dwg.rect`, `dwg.ellipse` o anche una stringa `<path>` personalizzata. L'API è coerente tra le forme.
- **Posso incorporare l'SVG direttamente in HTML?** Assolutamente. Il file che hai appena creato può essere referenziato con `<img src="circle.svg" alt="Red circle">` o inserito inline con i tag `<svg>`.
- **Perché non scrivere XML grezzo?** Potresti, ma librerie come `svgwrite` gestiscono le particolarità dei namespace e rendono il codice molto più manutenibile—soprattutto quando inizi ad aggiungere gradienti o animazioni.

## Conclusione

Ora sai come **create SVG document**, **add circle to SVG**, e **save SVG file** così da poter **export graphic as SVG** con poche righe di Python. Il modello è scalabile: sostituisci il cerchio con qualsiasi forma vettoriale, itera sui dati per generare grafici, o elabora in batch gli asset per un design system.

Prossimi passi? Prova ad aggiungere etichette di testo, sperimentare con i gradienti, o generare un'intera galleria di icone in un unico script. Se sei curioso di funzionalità più avanzate, consulta la documentazione di `svgwrite` sui gruppi (`<g>`), le trasformazioni e il supporto alle animazioni.

Buon coding, e che i tuoi vettori rimangano sempre nitidi!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Salva documento SVG in Aspose.HTML per Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Crea e gestisci documenti SVG in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Converti SVG in immagine con Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}