---
category: general
date: 2026-06-10
description: Chargez le HTML en Python pour extraire les images SVG de vos pages —
  code pas à pas, conseils et gestion des cas limites.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: fr
og_description: Charger du HTML en Python et extraire des images SVG avec un exemple
  clair et exécutable. Apprenez à rechercher les éléments SVG dans le HTML et à gérer
  les cas limites.
og_title: Charger du HTML en Python – Extraire efficacement les images SVG
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
title: Charger du HTML en Python – Guide complet pour extraire les images SVG
url: /fr/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Charger du HTML en Python – Guide complet pour extraire les images SVG

Vous avez déjà eu besoin de **load HTML in Python** juste pour extraire chaque graphique SVG d’une page ? Vous n’êtes pas le seul. Que vous construisiez un web‑scraper, génériez un rapport d’actifs, ou soyez simplement curieux des icônes utilisées par un site, savoir comment **extract SVG images** vous évite beaucoup de recherche manuelle.

Dans ce tutoriel, nous parcourrons une solution pratique, de bout en bout, qui **loads HTML in Python**, puis **searches HTML SVG** les éléments, **finds inline SVG**, et récupère même les fichiers SVG externes référencés par les balises `<img>`. À la fin, vous disposerez d’un script réutilisable, de quelques astuces pour les cas difficiles, et d’une vision claire du rendu.

## Ce que vous en retirerez

* Un script Python entièrement exécutable qui analyse un fichier HTML local (ou une page récupérée) et répertorie chaque SVG qu’il trouve.  
* Compréhension de la différence entre **inline SVG** (`<svg>…</svg>`) et **external SVG** (`<img src="… .svg">`).  
* Stratégies pour gérer le balisage malformé, les fichiers manquants et les particularités de l’espace de noms.  
* Idées pour étendre le code — sauvegarder les SVG, les convertir en PNG, ou les injecter dans une base de données.

### Prérequis

* Python 3.8+ installé.  
* Familiarité de base avec les bibliothèques `requests` et `BeautifulSoup` de Python (nous les importerons, pas besoin d’approfondir).  
* Un fichier HTML local ou une URL que vous souhaitez analyser.  

Maintenant, plongeons‑y.

## Charger du HTML en Python – Configurer le parseur

La toute première étape consiste à **load HTML in Python**. Vous pouvez soit lire un fichier depuis le disque, soit récupérer une page distante. Ci‑dessus se trouve un helper minimal mais robuste qui fait les deux :

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

> **Pourquoi c’est important :** L’utilisation de `BeautifulSoup` masque les particularités du parsing de chaînes brutes, et la fonction gère élégamment les fichiers locaux ainsi que les URL distantes. Elle lève également une exception si une requête réseau échoue—vous saurez immédiatement quand quelque chose ne va pas.

## Extraire les images SVG – Trouver les éléments SVG en ligne

Une fois le document chargé, l’étape logique suivante est de **find inline SVG** les balises. Le SVG en ligne est intégré directement dans le balisage HTML, ce qui signifie que vous pouvez le récupérer directement depuis le DOM.

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

*Astuce :* Si la page utilise des espaces de noms SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` trouve toujours la balise car il ignore les espaces de noms par défaut. C’est une commodité appréciable lorsque vous **searches HTML SVG**.

## Rechercher HTML SVG – Gérer les références externes `<img>`

De nombreux sites n’intègrent pas le SVG directement ; ils référencent des fichiers externes via `<img src="icon.svg">`. Pour les capturer, nous devons parcourir chaque balise `<img>`, vérifier son `src`, et voir s’il se termine par `.svg`.

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

> **Alerte cas limite :** Certaines pages utilisent des chaînes de requête (`icon.svg?v=2`) ou des fragments (`icon.svg#layer`). La vérification `endswith(".svg")` fonctionne toujours car nous ne regardons que la fin de la chaîne en minuscules. Si vous avez besoin d’une validation plus stricte, envisagez d’utiliser `urllib.parse` pour supprimer les paramètres d’abord.

## Trouver SVG en ligne – Rapporter les résultats

Maintenant que nous disposons de deux listes—une pour le balisage SVG en ligne et une autre pour les références de fichiers externes—nous pouvons les combiner et rapporter le nombre total. Cela reflète le fragment original que vous avez posté, mais ajoute un peu plus de contexte.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Assembler le tout – Script complet

Ci‑dessous se trouve le programme complet, prêt à être exécuté. Enregistrez‑le sous le nom `extract_svg.py` et pointez‑le vers un fichier HTML local ou une URL.

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

### Sortie attendue

Exécuter le script sur un exemple `sample.html` pourrait produire :

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Si vous décommentez le bloc de téléchargement, le SVG externe

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}