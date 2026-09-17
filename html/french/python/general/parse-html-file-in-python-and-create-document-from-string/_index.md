---
category: general
date: 2026-09-16
description: Analyser un fichier HTML en Python, charger un document HTML depuis un
  fichier et créer un document HTML à partir d’une chaîne avec un code simple, prêt
  à l’exécution.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: fr
lastmod: 2026-09-16
og_description: Analyser un fichier HTML en Python pour lire des fichiers HTML locaux
  et créer des documents HTML à partir de chaînes rapidement et de manière fiable.
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: Analyser un fichier HTML en Python – créer un document à partir d’une chaîne
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: Analyser un fichier HTML en Python et créer un document à partir d’une chaîne
url: /fr/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analyser un fichier HTML en Python et créer un document à partir d'une chaîne

Si vous devez **parse HTML file in Python**, ce guide vous montre exactement comment lire un fichier HTML local, charger un document HTML depuis un fichier, et également **create HTML document from string**. Que vous fassiez du scraping de données, testiez des modèles ou génériez du contenu dynamique, les étapes ci‑dessous vous offrent une solution complète et exécutable.

Dans ce tutoriel vous apprendrez à :

* Lire un fichier HTML local en utilisant les bibliothèques standard de Python.
* Charger un document HTML depuis un chemin de fichier.
* Créer un document HTML directement à partir d’une chaîne HTML.
* Gérer les cas limites courants tels que les fichiers manquants et les problèmes d’encodage.

Les seules prérequis sont Python 3.8+ et la bibliothèque `beautifulsoup4`, que nous installerons à la première étape.

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Python 3.8 or newer | Garantit la compatibilité avec les annotations de type et la syntaxe moderne. |
| `beautifulsoup4` and `lxml` packages | Fournissent un analyseur robuste capable de gérer le HTML malformé et vous offrent un objet pratique de type `HTMLDocument`‑like. |
| A sample HTML file (`index.html`) in your project folder | Servira d’entrée pour l’exemple **load html document from file**. |

Installez les dépendances avec pip :

```bash
pip install beautifulsoup4 lxml
```

## Analyser un fichier HTML en Python

Le cœur du tutoriel est l’opération **parse html file in python**. Nous allons encapsuler BeautifulSoup dans une petite classe d’aide appelée `HTMLDocument` afin que l’API corresponde à l’exemple que vous avez vu précédemment.

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### Comment ça fonctionne

1. **Detect source type** – Le constructeur vérifie si le `source` fourni existe sur le disque. S’il existe, nous **load html document from file** ; sinon nous le traitons comme une chaîne brute, satisfaisant ainsi le besoin **create html document from string**.
2. **Read the file** – Nous utilisons `Path.read_text(encoding="utf-8")`, qui est la méthode recommandée pour **read local html file python** en toute sécurité.
3. **Parse with BeautifulSoup** – L’analyseur `lxml` est rapide et tolérant aux balises malformées.

## Charger un document HTML depuis un fichier

Maintenant que nous disposons de la classe `HTMLDocument`, charger un fichier est simple :

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**Sortie attendue** (en supposant que `index.html` contienne `<title>My Page</title>`):

```
Document title: My Page
```

Si le fichier n’existe pas, la classe lève une `FileNotFoundError` claire, que vous pouvez intercepter dans le code de production.

## Créer un document HTML à partir d’une chaîne

Créer un document directement à partir d’une chaîne est utile pour les tests ou la génération d’HTML à la volée :

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**Sortie attendue** :

```
String-based title: Hello
```

Comme la même classe `HTMLDocument` gère les deux scénarios, vous obtenez une API cohérente pour **parse html file in python**, que la source soit un fichier ou une chaîne.

## Lire un fichier HTML local en Python – gestion des cas limites

Lorsque vous traitez des fichiers réels, vous rencontrez souvent :

* **Missing files** – déjà géré par la `FileNotFoundError`.
* **Different encodings** – vous pouvez laisser BeautifulSoup deviner l’encodage, mais spécifier explicitement UTF‑8 est le plus sûr.
* **Large files** – lire le fichier entier en mémoire peut être coûteux ; vous pouvez le diffuser avec `BeautifulSoup(open(...), "lxml")` si nécessaire.

Voici un wrapper de protection qui ajoute ces garde-fous :

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

Vous pouvez maintenant appeler `safe_load_html("index.html")` et obtenir le même objet `HTMLDocument` en étant sûr que les erreurs sont signalées clairement.

## Astuces professionnelles et pièges courants

* **Avoid “just” using `open(...).read()`** – `Path.read_text` gère l’expansion du chemin et l’encodage en une seule ligne.
* **Don’t forget to close file handles** – `Path.read_text` le fait automatiquement ; si vous utilisez `open()`, encapsulez-le dans un bloc `with`.
* **Prefer `lxml` over the default parser** – il est plus rapide et plus tolérant aux balises cassées, ce qui est essentiel lorsque vous **parse html file in python** depuis le web.
* **When creating from a string, ensure it’s a complete HTML document** – l’absence de balises `<html>` ou `<body>` peut entraîner des résultats `None` inattendus lors de l’interrogation d’éléments.

## Script complet à copier‑coller

Voici un script autonome qui illustre chaque étape abordée. Enregistrez‑le sous le nom `html_demo.py` et exécutez `python html_demo.py`.

```python
#!/usr/bin/env python3
"""
Complete example: parse html file in python, load html document from file,
and create html document from string.
"""

from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """Wraps BeautifulSoup to provide a simple document interface."""
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            self._load_from_file(Path(source))
        else:
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        return self.soup.title.string.strip() if self.soup.title else ""

    def pretty(self) -> str:
        return self.soup.prettify()


def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """Safely load a local HTML file, handling common errors."""
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; specify the correct encoding.")


def main():
    # Load from a real file (replace with your actual path)
    file_doc = safe_load_html("YOUR_DIRECTORY/index.html")
    print("File‑based title :", file_doc.title())
    print("\nPretty‑printed HTML from file:\n", file_doc.pretty()[:200], "...")

    # Create from a raw string
    html_str = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
    string_doc = HTMLDocument(html


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Enregistrer le document HTML dans un fichier avec Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Charger des documents HTML depuis un fichier avec Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Créer un document HTML avec Aspose.HTML – Guide étape par étape](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}