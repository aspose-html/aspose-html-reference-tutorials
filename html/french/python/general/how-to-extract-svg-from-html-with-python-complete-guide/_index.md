---
category: general
date: 2026-05-31
description: Apprenez à extraire le SVG du HTML avec Python. Ce tutoriel pas à pas
  montre comment lire un document HTML, enregistrer des fichiers SVG et sauvegarder
  le SVG intégré efficacement.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: fr
og_description: Comment extraire du SVG à partir d’un HTML avec Python. Suivez ce
  tutoriel pour lire un document HTML, enregistrer les fichiers SVG et gérer le SVG
  intégré sans effort.
og_title: Comment extraire du SVG à partir de HTML avec Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Comment extraire le SVG d'HTML avec Python – Guide complet
url: /fr/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du SVG depuis du HTML avec Python – Guide complet

Vous vous êtes déjà demandé **comment extraire du SVG** d’une page HTML désordonnée sans perdre patience ? Vous n'êtes pas seul. Que vous construisiez un web‑scraper, un pipeline de conception, ou que vous ayez simplement besoin d’exporter en lot des icônes, savoir **comment extraire du SVG** est une astuce pratique qui fait gagner du temps et évite les maux de tête.

Dans ce tutoriel, nous vous montrerons exactement **comment extraire du SVG** en utilisant la bibliothèque Aspose.HTML pour Python. Nous lirons le document HTML, extraire à la fois le balisage `<svg>` en ligne **et** les références SVG externes, puis **enregistrer les fichiers SVG** sur le disque — le tout dans un script propre et réutilisable. À la fin, vous disposerez d’une solution prête à l’emploi que vous pourrez adapter à vos propres projets.

> **Astuce :** Si vous ne cherchez qu’un aperçu rapide de la page, `BeautifulSoup` fonctionne aussi, mais Aspose.HTML vous fournit un DOM complet, rendant l’extraction à la fois des SVG en ligne et liés un jeu d’enfant.

## Ce dont vous avez besoin

* Python 3.8+ (le code utilise des f‑strings, donc 3.6+ est le strict minimum)
* `pip install aspose-html` – la bibliothèque commerciale qui alimente notre analyse HTML
* Un dossier contenant un fichier `input.html` qui renferme les SVG que vous souhaitez extraire
* Permission d’écriture sur le répertoire de sortie (nous l’appellerons `YOUR_DIRECTORY`)

C’est tout — pas de binaires supplémentaires, pas de navigateurs sans tête. Simple, non ?

## Étape 1 : Lire le document HTML avec Aspose.HTML

La première chose à faire est de **lire le document HTML** afin de pouvoir parcourir son arbre DOM. Aspose.HTML vous fournit un objet `HTMLDocument` qui se comporte comme le `document` d’un navigateur.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Pourquoi c’est important :* En chargeant le HTML dans un DOM approprié, vous évitez les écueils du parsing basé sur les expressions régulières, et vous obtenez gratuitement des méthodes comme `get_elements_by_tag_name` et `query_selector_all`.

## Étape 2 : Rassembler tous les éléments <svg> en ligne

Les SVG en ligne sont ces blocs `<svg>…</svg>` qui se trouvent directement dans le HTML. Pour **enregistrer le SVG en ligne** nous n’avons besoin que de leur HTML externe.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Notez que nous ajoutons le balisage brut directement dans `svg_contents`. Plus tard, nous déciderons si chaque entrée est du markup ou un chemin de fichier.

## Étape 3 : Trouver les références SVG externes (balises img et object)

De nombreuses pages lient des fichiers SVG externes via `<img src="icon.svg">` ou `<object data="logo.svg">`. Pour **extraire du SVG depuis le HTML** nous devons également capturer ces URL.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Avertissement de cas particulier :* Si l’URL du SVG est relative, vous devrez la joindre au chemin de base du fichier HTML. Par souci de concision, nous supposons que le HTML se trouve à côté des fichiers SVG.

## Étape 4 : Écrire chaque SVG dans un fichier séparé

Maintenant que nous disposons d’une liste mixte de chaînes de markup et de chemins de fichiers, nous allons itérer et **enregistrer les fichiers SVG**. Le script distingue automatiquement le markup en ligne d’une référence à un fichier existant.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Ce que vous verrez :** Après l’exécution du script, `YOUR_DIRECTORY` contiendra des fichiers nommés `svg_0.svg`, `svg_1.svg`, … chacun contenant soit le markup en ligne original, soit une copie du SVG externe.

### Résultat attendu

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Si un fichier référencé est manquant, le script affiche un avertissement mais continue — ainsi, un lien cassé n’arrêtera pas l’ensemble de l’extraction.

## Gestion des problèmes courants

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Les URL relatives se cassent** | L’attribut `src` peut être `"../assets/icon.svg"` | Utilisez `os.path.join(os.path.dirname(html_path), src)` pour résoudre. |
| **Noms de fichiers en double** | Deux SVG avec le même nom sont écrasés | Incluez un hachage du contenu dans le nom de fichier (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Les SVG en ligne volumineux provoquent des pics de mémoire** | Stocker tout le markup dans une liste avant l’écriture | Diffusez chaque élément directement dans un fichier au lieu de le mettre en mémoire tampon. |
| **Des images non‑SVG passent à travers** | Certains tags `<img>` se terminent par `.svg?version=1` | Supprimez les chaînes de requête avant la vérification de l’extension (`src.split('?')[0]`). |

## Script complet à copier‑coller

Ci-dessous se trouve le programme complet, prêt à être exécuté. Enregistrez-le sous `extract_svg.py`, ajustez `YOUR_DIRECTORY`, puis lancez `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Récapitulatif – Comment extraire du SVG en bref

- **Lire le document HTML** avec `HTMLDocument`.
- **Rassembler les `<svg>` en ligne** via `get_elements_by_tag_name`.
- **Localiser les SVG externes** en utilisant un sélecteur CSS qui se termine par `.svg`.
- **Enregistrer chaque élément** — écrire le markup directement dans un fichier ou copier le fichier référencé.
- **Gérer les cas particuliers** comme les chemins relatifs, les doublons et les fichiers manquants.

C’est la réponse complète à **comment extraire du SVG** d’une page HTML, encapsulée dans un script unique et facile à modifier.

## Et après ?

Maintenant que vous pouvez **extraire du SVG** de manière fiable, envisagez ces idées complémentaires :

- **Traitement par lots :** Parcourez un répertoire de fichiers HTML pour constituer une bibliothèque d’icônes.
- **Optimisation :** Passez chaque SVG enregistré dans SVGO (un optimiseur Node.js) pour réduire la taille du fichier.
- **Conversion :** Utilisez `cairosvg` ou `svglib` pour transformer les SVG en PNG pour les navigateurs anciens.
- **Extraction de métadonnées :** Analysez les balises `<title>` ou `<desc>` à l’intérieur de chaque SVG pour obtenir des libellés recherchables.

Chacun de ces sujets touche nos mots‑clés secondaires — **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** — vous trouverez donc de nombreuses ressources à explorer.

---

*Bon hacking ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou contactez‑moi sur GitHub. Le monde du SVG est vaste, mais avec les bons outils, l’extraire devient un jeu d'enfant.*

## Que devriez‑vous apprendre ensuite ?

- [Enregistrer un document SVG avec Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Comment convertir un SVG en XPS avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}