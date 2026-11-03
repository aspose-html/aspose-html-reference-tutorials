---
category: general
date: 2026-07-18
description: Convertir HTML en EPUB en Python rapidement. Apprenez comment charger
  un fichier HTML en Python et également convertir HTML en MHTML à l'aide de bibliothèques
  simples.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: fr
lastmod: 2026-07-18
og_description: Convertissez du HTML en EPUB avec Python grâce à un exemple clair
  et exécutable. Apprenez également à charger un fichier HTML en Python et à convertir
  du HTML en MHTML en quelques minutes.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Convertir le HTML en EPUB avec Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Convertir le HTML en EPUB avec Python – Guide complet étape par étape
url: /fr/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML en EPUB avec Python – Guide complet étape par étape

Vous êtes‑vous déjà demandé comment **convertir HTML en EPUB** sans vous arracher les cheveux ? Vous n'êtes pas le seul—les développeurs ont constamment besoin de transformer des pages web en livres électroniques pour la lecture hors ligne, et le faire en Python est étonnamment simple. Dans ce tutoriel, nous allons parcourir le chargement d'un fichier HTML en Python, la conversion de ce HTML en EPUB, et même transformer la même source en MHTML pour des archives compatibles avec les e‑mails.

À la fin du guide, vous disposerez d'un script prêt à l'exécution qui prend un seul fichier `sample.html` et génère à la fois `sample.epub` et `sample.mhtml`. Pas de mystère, juste du code clair et des explications.

---

![Diagramme du pipeline de conversion](https://example.com/images/convert-html-epub.png "Diagramme montrant le flux de conversion html en epub")

## Ce que vous allez construire

- **Charger un fichier HTML en Python** en utilisant les modules intégrés `pathlib` et `io`.  
- **Convertir HTML en EPUB** avec la bibliothèque `ebooklib`, qui gère le format conteneur EPUB pour vous.  
- **Convertir HTML en MHTML** (également appelé MHT) en utilisant le package `email`, créant une archive web à fichier unique que les navigateurs peuvent ouvrir directement.  

Nous couvrirons également :

- Les dépendances requises et comment les installer.  
- La gestion des erreurs afin que votre script échoue proprement.  
- Comment personnaliser les métadonnées comme le titre et l'auteur du fichier EPUB.  

Prêt ? Plongeons‑y.

---

## Prérequis

Avant de commencer à coder, assurez-vous d'avoir :

1. **Python 3.9+** – la syntaxe utilisée ici fonctionne avec n'importe quelle version récente.  
2. **pip** – pour installer les paquets tiers.  
3. Un fichier HTML simple, par ex., `sample.html`, placé dans un dossier que vous contrôlez.  

Si vous avez déjà tout cela, super—passez à la section suivante.  

> **Astuce :** Gardez votre HTML bien formé (sections `<head>` et `<body>` correctes). Bien que `ebooklib` tente de corriger les petits problèmes, une source propre vous évite des maux de tête plus tard.

---

## Étape 1 – Installer les bibliothèques requises

Nous avons besoin de deux packages externes :

- **ebooklib** – pour la génération d'EPUB.  
- **beautifulsoup4** – optionnel, mais pratique pour nettoyer le HTML avant la conversion.

Run this in your terminal:

```bash
pip install ebooklib beautifulsoup4
```

> **Pourquoi ces bibliothèques ?** `ebooklib` construit la structure EPUB basée sur ZIP pour vous, en gérant automatiquement le dossier `META‑INF`, `content.opf` et `toc.ncx`. `beautifulsoup4` nous permet de nettoyer le HTML, assurant que le livre électronique final s'affiche correctement sur tous les lecteurs.

---

## Étape 2 – Charger le fichier HTML en Python

Charger un fichier HTML est simple, mais nous l'envelopperons dans une petite fonction d'aide qui renvoie un objet **BeautifulSoup** pour un traitement ultérieur.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Explication :**  
- `Path` nous fournit une gestion de fichiers indépendante du système d'exploitation.  
- L'utilisation de `read_text` évite le code boilerplate `open`/`close`.  
- Retourner un objet `BeautifulSoup` signifie que nous pouvons ensuite supprimer les scripts, corriger les balises cassées ou injecter une feuille de style avant de **convertir HTML en EPUB**.

---

## Étape 3 – Convertir HTML en EPUB

Maintenant que nous pouvons **charger un fichier HTML en Python**, transformons-le en un EPUB propre. La fonction ci‑dessous accepte un objet `BeautifulSoup`, un chemin de destination et des métadonnées optionnelles.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Pourquoi cela fonctionne :**  
- `ebooklib.epub.EpubBook` abstrait le conteneur ZIP et les fichiers de manifeste requis.  
- Nous générons un UUID comme identifiant pour éviter les ID dupliqués si vous créez de nombreux livres.  
- Le `spine` indique aux lecteurs l'ordre des chapitres ; un livre à un seul chapitre suffit pour la plupart des sources HTML simples.  

**Exécution de la conversion :**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Lorsque vous exécutez le script, vous verrez une coche verte confirmant l'emplacement du fichier EPUB.

---

## Étape 4 – Convertir HTML en MHTML

MHTML (ou MHT) regroupe le HTML et toutes ses ressources (images, CSS) dans un seul fichier MIME. Le package `email` de Python peut créer ce format sans dépendances externes.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Points clés :**  

- Le type MIME `multipart/related` indique aux navigateurs que la partie HTML et ses ressources font partie du même ensemble.  
- Nous parcourons les balises `<img>` pour incorporer les images ; si vous n'avez pas besoin d'images, vous pouvez ignorer ce bloc.  
- `Content-Location` utilise une URI `file://` afin que les navigateurs puissent résoudre les ressources en interne.  

**Appel de la fonction :**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Vous avez maintenant à la fois `sample.epub` et `sample.mhtml` côte à côte.

---

## Script complet – Toutes les étapes dans un seul fichier

Voici le script complet, prêt à l'exécution, qui combine tout. Enregistrez-le sous le nom `convert_html.py` et remplacez `YOUR_DIRECTORY` par le chemin contenant votre `sample.html`.



## Ce que vous devriez apprendre ensuite

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment convertir HTML en MHTML avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Comment convertir EPUB en PDF avec Java – En utilisant Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Comment convertir EPUB en images avec Aspose.HTML pour Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}