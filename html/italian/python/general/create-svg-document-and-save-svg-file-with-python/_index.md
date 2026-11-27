---
category: general
date: 2026-11-27
description: Crea un documento SVG e salva il file SVG usando Python. Impara a esportare
  il vettore come SVG e a generare rapidamente un’immagine SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: it
lastmod: 2026-11-27
og_description: Crea un documento SVG e salva il file SVG con Python. Questa guida
  ti mostra come esportare il vettore come SVG e produrre un'immagine SVG in pochi
  minuti.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Crea documento SVG e salva file SVG usando Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Crea documento SVG e salva file SVG con Python
url: /it/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea documento SVG e salva file SVG con Python

Se hai bisogno di **create SVG document** da zero, questa guida ti accompagna passo passo attraverso l'intero processo. Vedrai come **save SVG file** su disco, esportare il vettore come SVG, e ottenere un'immagine SVG pronta all'uso in poche righe di codice.

Generare grafiche scalabili programmaticamente è utile per report, icone UI, o qualsiasi situazione in cui desideri immagini indipendenti dalla risoluzione. Alla fine di questo tutorial sarai in grado di rispondere a “**how to create SVG**?” per forme semplici e di estendere il modello a opere vettoriali complesse.

## Di cosa avrai bisogno

- Python 3.8 o versioni successive  
- Il pacchetto `svgwrite` (installabile via `pip`)  
- Una directory scrivibile per il file di output  

Non sono richiesti editor grafici esterni; tutto funziona dalla riga di comando.

## Passo 1: Installa la libreria `svgwrite`

`svgwrite` fornisce un'API pulita e Pythonic per costruire markup SVG. Installala una volta con:

```bash
pip install svgwrite
```

> **Consiglio:** Usa un ambiente virtuale (`python -m venv .venv`) per mantenere le dipendenze isolate.

## Passo 2: Crea documento SVG

Ora creiamo effettivamente oggetti **create SVG document**. La classe `Drawing` rappresenta l'elemento radice `<svg>` e gestisce automaticamente i namespace.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

L'istanza `Drawing` è il punto di ingresso per tutte le operazioni SVG successive. Specificando `size` impostiamo le dimensioni della tela, che influenzano il modo in cui i browser renderizzano l'immagine.

## Passo 3: Aggiungi un elemento cerchio rosso

Aggiungere forme è semplice. Il metodo `circle` crea un elemento `<circle>`; lo colleghiamo quindi alla radice.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Perché scegliamo un cerchio: i cerchi sono primitive vettoriali che dimostrano scalabilità senza perdita di qualità, rendendo l'output ideale per testare i flussi di lavoro **export vector as SVG**.

## Passo 4: Salva file SVG

Infine, scrivi il markup su disco. Questo passo soddisfa il requisito **save SVG file** e produce un file che puoi aprire in qualsiasi browser o editor vettoriale.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Quando esegui lo script, vedrai un messaggio nella console che conferma la posizione del file generato.

### Output previsto

Il file `circle.svg` risultante contiene:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Aprendo il file in un browser si visualizza un cerchio rosso nitido, e poiché è basato su vettori puoi ingrandire indefinitamente senza pixelatura.

## Passo 5: Variazioni comuni e casi limite

### Esportare vettori più complessi

Se hai bisogno di **export vector as SVG** per illustrazioni con più forme, ripeti semplicemente il pattern `dwg.add()` con altre primitive (`rect`, `line`, `path`, ecc.). Per esempio:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Gestire Unicode e testo

SVG supporta elementi di testo con pieno supporto Unicode. Usa `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` per incorporare etichette multilingue.

### Salvare in una posizione diversa

Quando **save SVG image** in una cartella specificata dall'utente, valida il percorso per evitare errori di permessi:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minificare l'output

Per pipeline di produzione, potresti voler un file di dimensioni minori. Passa `pretty=False` a `dwg.tostring()` e scrivi il risultato manualmente:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Come creare SVG con librerie alternative (opzionale)

Mentre `svgwrite` è leggera e pure‑Python, esistono altri ecosistemi:

- **cairosvg** – converte PNG, PDF o HTML in SVG.  
- **lxml** – ti permette di costruire markup SVG manualmente usando le API XML.  

La scelta della libreria dipende dalla complessità del tuo progetto e dalle dipendenze esistenti.

## Conclusione

Ora sai come **create SVG document**, aggiungere forme vettoriali e **save SVG file** usando Python. La soluzione completa dimostra i passaggi per **export vector as SVG**, generare un **SVG image**, e rispondere alla comune domanda **how to create SVG** programmaticamente.

Da qui puoi:

- Estendere lo script con cicli per generare grafici o icone automaticamente.  
- Integrare l'output SVG in applicazioni web o template email.  
- Esplorare animazioni aggiungendo elementi `<animate>` con `svgwrite`.  

Sperimenta con forme, colori e gradienti diversi per sfruttare appieno la potenza della grafica vettoriale scalabile nei tuoi progetti Python. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea documento SVG – Aggiungi un cerchio e salva come SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Crea documento SVG in Python – Guida alla conversione SVG in PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Carica file SVG Python – Guida completa a esportazione, incorporamento e conversione](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}