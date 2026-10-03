---
category: general
date: 2026-10-02
description: Impara a creare un documento SVG in Python, salvare l'SVG su file ed
  esportare l'immagine SVG con uno script breve e completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: it
lastmod: 2026-10-02
og_description: Crea un documento SVG in Python ed esporta l'immagine SVG con questo
  tutorial pratico. Segui lo script, salva l'SVG su file e riutilizza il grafico vettoriale
  immediatamente.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Crea un documento SVG in Python – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Come creare un documento SVG ed esportarlo come immagine in Python
url: /it/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un documento SVG ed esportarlo come immagine in Python

Se hai bisogno di **creare un documento SVG** programmaticamente, questo tutorial ti mostra esattamente come farlo con Python. Vedrai uno script completo che costruisce un semplice cerchio, salva l'SVG su file e produce un'immagine SVG esportabile che puoi incorporare ovunque.

Generare grafica vettoriale scalabile dal codice elimina lo sforzo manuale di disegnare forme in un editor GUI. Alla fine di questa guida potrai integrare la creazione di SVG nei pipeline di visualizzazione dati, nei generatori di report automatizzati o in qualsiasi progetto che richieda grafiche nitide e indipendenti dalla risoluzione.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Python 3.8 o versioni successive installato
- La libreria `svgwrite` (installala con `pip install svgwrite`)
- Permessi di scrittura nella directory in cui verrà salvato l'SVG

Questi requisiti mantengono l'esempio leggero e compatibile con la maggior parte degli ambienti.

## Passo 1: Installa e importa la libreria SVG

Il primo passo è aggiungere la libreria di terze parti che fornisce un'API comoda per la creazione di SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` astrae la struttura XML di un file SVG, permettendoti di concentrarti sulla geometria invece che sul markup grezzo.

## Passo 2: Crea un oggetto documento SVG

Ora puoi **creare un documento SVG** istanziando `svgwrite.Drawing`. Questo oggetto rappresenta l'elemento radice `<svg>` e contiene tutte le forme successive.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

L'argomento `size` definisce le dimensioni in pixel renderizzate, mentre `viewBox` stabilisce un sistema di coordinate che corrisponde alla geometria che definirai più avanti.

## Passo 3: Aggiungi un elemento cerchio

Un cerchio è definito dal suo centro (`cx`, `cy`) e dal raggio (`r`). Usa l'helper `circle` per impostare questi attributi.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Il cerchio si trova al centro della tela 100 × 100, lasciando un margine di 10 pixel su ogni lato. Regola `fill` e `stroke` per adattarli al tuo linguaggio di design.

## Passo 4: Salva l'SVG su file

Con la grafica assemblata, puoi **salvare l'SVG su file** usando il metodo `save`. Questo scrive XML ben formato che browser e editor vettoriali comprendono.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Il file `circle.svg` ora risiede nella directory di lavoro corrente. Puoi aprirlo in un browser web, Inkscape o qualsiasi strumento che supporti il formato SVG.

## Passo 5: Verifica l'immagine SVG esportata

Apri il file salvato in un browser per confermare l'output. Dovresti vedere un cerchio centrato con i colori specificati. L'XML grezzo appare così:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Poiché SVG è basato su vettori, puoi scalare l'immagine senza perdita di qualità, rendendola ideale per design web responsivi o stampa ad alta risoluzione.

## Consiglio professionale: Esporta SVG come PNG o JPEG

Se ti serve una versione raster, combina il file SVG con uno strumento di conversione come **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Questo passo dimostra **esportare l'immagine SVG** in un formato bitmap, utile quando i sistemi a valle non possono renderizzare SVG direttamente.

## Varianti comuni e casi limite

| Variante | Come gestirla |
|----------|---------------|
| Forme multiple | Chiama `dwg.add()` per ogni nuovo elemento (rect, line, path). |
| Dimensioni dinamiche | Calcola `size` e `viewBox` dai dati prima di creare `Drawing`. |
| Etichette di testo | Usa `dwg.text("Label", insert=("10", "20"))` e stilizza con `font_size` e `fill`. |
| Riutilizzare il documento | Mantieni l'oggetto `Drawing` in memoria e chiama `save()` ogni volta che ti serve un file aggiornato. |
| File di grandi dimensioni | Trasmetti l'output usando `dwg.tostring()` e scrivi su un oggetto file manualmente per evitare picchi di memoria. |

Affrontare questi scenari garantisce che il tuo script **come generare SVG** si adatti da icone semplici a diagrammi complessi.

## Riepilogo script completo

Di seguito trovi l'esempio completo, eseguibile, che incorpora tutti i passaggi e la conversione opzionale:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Eseguendo questo script otterrai `circle.svg` e, se `cairosvg` è installato, `circle.png`. Entrambi i file sono pronti per essere inseriti in pagine web, report o ulteriori elaborazioni.

## Conclusione

Ora sai come **creare un documento SVG** in Python, **salvare l'SVG su file** e **esportare l'immagine SVG** per un uso più ampio. L'esempio copre le chiamate API essenziali, spiega perché ogni passo è importante e offre estensioni per grafiche più complesse.

Successivamente, esplora altri argomenti del **tutorial SVG Python** come il disegno di percorsi, l'applicazione di gradienti e l'animazione di elementi. Integrare queste tecniche ti permetterà di generare grafica vettoriale dinamica e guidata dai dati direttamente dalle tue applicazioni Python. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea e gestisci documenti SVG in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Salva documento SVG in Aspose.HTML per Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Converti SVG in immagine con Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}