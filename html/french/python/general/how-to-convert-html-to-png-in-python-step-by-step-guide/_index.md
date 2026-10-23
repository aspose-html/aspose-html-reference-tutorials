---
category: general
date: 2026-10-21
description: Apprenez à convertir rapidement du HTML en PNG. Ce tutoriel couvre également
  l'exportation d'une page Web en PNG et la conversion d'un fichier HTML en PNG avec
  Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: fr
lastmod: 2026-10-21
og_description: Convertir le HTML en PNG avec Python. Suivez ce guide clair pour exporter
  une page web en PNG, gérer les cas limites et automatiser la génération d'images.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Convertir HTML en PNG avec Python – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Comment convertir du HTML en PNG avec Python – guide étape par étape
url: /fr/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir du HTML en PNG avec Python – guide complet de programmation

Si vous devez **convertir du HTML en PNG**, ce guide vous montre une méthode fiable pour le faire avec du Python pur. Que vous exportiez un rapport statique, génériez des miniatures pour une galerie, ou automatisiez des captures d’écran pour des tests, vous obtiendrez une solution complète et exécutable en quelques minutes.

Vous verrez également comment **exporter une page web en PNG**, comprendrez la différence entre la conversion d’un fichier HTML et d’une URL en direct, et apprendrez les meilleures pratiques pour gérer les pages volumineuses ou le contenu dynamique. Aucun service externe n’est requis — juste quelques packages Python et un court script.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Python 3.9+ installé (le code fonctionne sous Windows, macOS et Linux)
- Un accès à un terminal ou à l’invite de commandes
- Une connaissance de base du gestionnaire de paquets Python (`pip`)

Vous aurez besoin du package `imgkit` (un léger wrapper autour de `wkhtmltoimage`) et du binaire `wkhtmltoimage` lui‑même. Les deux sont gratuits et open‑source.

## Étape 1 : Installer les outils requis

La première étape consiste à installer `wkhtmltoimage` et le wrapper Python qui communique avec lui.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Pourquoi cette étape est importante** – `wkhtmltoimage` rend le HTML en utilisant le moteur WebKit, produisant des PNG pixel‑perfect. `imgkit` se contente de transmettre vos options au binaire, vous obtenez donc la même qualité qu’un navigateur.

## Étape 2 : Vérifier l’installation

Exécutez un rapide contrôle pour confirmer que le binaire est accessible depuis Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Si le script affiche le chemin vers `wkhtmltoimage`, vous êtes prêt à convertir du HTML en PNG. Si vous obtenez une `OSError`, vérifiez que le binaire se trouve bien dans le `PATH` de votre système.

## Étape 3 : Écrire une fonction de conversion réutilisable

Encapsuler la logique dans une fonction facilite **la conversion d’un fichier HTML en PNG** ou **l’exportation d’une page web en PNG** depuis n’importe où dans votre projet.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Pourquoi nous enveloppons à la fois `from_file` et `from_url`** – La même fonction prend désormais en charge **comment convertir du HTML en image** pour les fichiers locaux et les pages web en direct, gardant votre code DRY (Don’t Repeat Yourself).

## Étape 4 : Convertir un fichier HTML local en PNG

Placez un fichier HTML nommé `sample.html` dans un dossier appelé `assets`. Puis appelez l’assistant que nous venons de définir :

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Résultat attendu

L’exécution du script affiche :

```
✅ Successfully saved PNG to: output/sample.png
```

Un nouveau fichier `output/sample.png` contient maintenant une capture pixel‑perfect de `sample.html`. L’ouvrir avec n’importe quel visualiseur d’images montre la page rendue exactement comme elle apparaîtrait dans un navigateur.

## Étape 5 : Exporter une page web en direct en PNG

Si vous devez **exporter une page web en PNG** pour une URL qui change fréquemment (par ex., un tableau de bord), passez simplement la chaîne d’URL au lieu d’un chemin de fichier.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Pourquoi ajuster la taille du viewport ?

Les pages conçues pour les écrans de bureau ont souvent l’air à l’étroit si elles sont rendues avec une petite largeur. En augmentant les options `width` et `height`, vous capturez la mise en page complète, ce qui est particulièrement utile pour les tâches **exporter une page web en PNG**.

## Étape 6 : Gérer les cas limites courants

### 6.1 Pages volumineuses ou défilement infini

Pour les pages qui chargent le contenu de façon paresseuse (par ex., défilement infini), augmentez le délai JavaScript et, éventuellement, définissez un viewport plus grand :

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Pages protégées par authentification

Si une page nécessite un cookie de session, vous pouvez intégrer l’en‑tête du cookie :

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Images ou polices manquantes

`wkhtmltoimage` respecte le drapeau `--disable-local-file-access` pour des raisons de sécurité. Si votre HTML référence des ressources locales, activez‑les explicitement :

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Étape 7 : Vérifier le résultat par programme (optionnel)

Parfois, il faut confirmer que le PNG a été généré correctement (par ex., dans des pipelines CI). Le fragment suivant vérifie la taille du fichier et ses dimensions :

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Si le PNG passe ces contrôles, vous pouvez l’utiliser en toute sécurité dans les processus en aval tels que la génération de PDF, les pièces jointes d’e‑mail, ou les pipelines d’apprentissage automatique.

## Conclusion

Vous disposez maintenant d’une méthode complète et prête pour la production afin de **convertir du HTML en PNG** avec Python. Le guide a couvert :

- L’installation de `wkhtmltoimage` et `imgkit`
- La vérification de l’environnement
- Une fonction réutilisable `convert_html_to_png` qui gère à la fois les fichiers locaux et les URL
- Des exemples concrets pour **exporter une page web en PNG**, **comment convertir du HTML en image**, et **convertir un fichier HTML en PNG**
- La prise en charge des cas limites pour les pages volumineuses, l’authentification et les ressources locales
- Des étapes de vérification optionnelles pour les pipelines CI/CD

N’hésitez pas à expérimenter avec d’autres options `imgkit` — telles que `zoom`, `crop-h` ou `crop-w` — pour affiner la sortie selon votre cas d’usage. Pour les prochaines étapes, vous pourriez explorer :

- Convertir les PNG en un rapport PDF (bibliothèque `img2pdf`)
- Automatiser la conversion par lot d’un dossier complet de fichiers HTML
- Utiliser Selenium pour les pages nécessitant un rendu complet du navigateur (par ex., frameworks JavaScript lourds)

Bon codage, et profitez de captures d’écran pixel‑perfect !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convertir du HTML en PNG – Guide complet Python](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convertir du HTML en PNG avec Python – Guide complet d’enregistrement en streaming](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convertir du SVG en PNG avec Python en utilisant Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}