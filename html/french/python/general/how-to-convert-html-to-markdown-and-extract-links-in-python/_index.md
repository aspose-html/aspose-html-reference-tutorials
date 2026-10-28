---
category: general
date: 2026-10-28
description: 'convertir le HTML en Markdown avec Python : apprenez à extraire les
  liens du HTML et à les enregistrer au format Markdown de type GitLab en seulement
  trois étapes.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- how to convert html document
language: fr
lastmod: 2026-10-28
og_description: convertissez le HTML en Markdown rapidement avec Python. Ce guide
  montre comment extraire les liens du HTML et produire du Markdown au format GitLab
  en trois étapes simples.
og_image_alt: Screenshot of Python script converting HTML to GitLab‑flavored Markdown
  with extracted links
og_title: Convertir le HTML en Markdown et extraire les liens avec Python
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  headline: How to convert HTML to Markdown and extract links in Python
  type: TechArticle
- description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  name: How to convert HTML to Markdown and extract links in Python
  steps:
  - name: Multiple input sources
    text: 'If you need to batch‑process a folder of HTML files, wrap the conversion
      in a loop:'
  - name: Missing links
    text: When an HTML document contains no `<a>` elements, the converter still creates
      a valid Markdown file containing only the permitted paragraphs. No additional
      error handling is required, but you can check `save_options.features` if you
      need to enforce the presence of links.
  - name: Custom output encoding
    text: 'If your target system expects UTF‑8 with a BOM, set the encoding on the
      `MarkdownSaveOptions`:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: Comment convertir le HTML en Markdown et extraire les liens en Python
url: /fr/python/general/how-to-convert-html-to-markdown-and-extract-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir du HTML en Markdown et extraire les liens en Python

Si vous avez besoin de **convertir du HTML en Markdown**, ce tutoriel vous fournit une solution complète, prête à l’emploi. Vous verrez comment extraire les liens du HTML, choisir le formatteur Markdown de type GitLab, et enregistrer le résultat en quelques lignes de code.

Le guide couvre tout ce dont vous avez besoin : les packages requis, le chargement du HTML depuis différentes sources, la configuration de `MarkdownSaveOptions`, et la gestion des cas particuliers tels que les liens manquants ou les répertoires de sortie personnalisés. À la fin, vous pourrez répondre à la question *comment convertir un document HTML* en Markdown propre et riche en liens pour n’importe quel flux de travail en aval.

## Prérequis

- Python 3.8 ou supérieur
- package `aspose-html` (la bibliothèque officielle Aspose.HTML pour Python)
- Familiarité de base avec les scripts Python et les entrées/sorties de fichiers

You can install the library with:

```bash
pip install aspose-html
```

> **Astuce :** Utilisez un environnement virtuel pour isoler les dépendances.

## Étape 1 : Charger le contenu HTML

La première étape consiste à créer un objet `HTMLDocument`. Aspose.HTML accepte une chaîne, un chemin de fichier ou une URL, vous pouvez donc choisir la source qui correspond à votre projet.

```python
from aspose.html import HTMLDocument

# Example 1: Load from a raw HTML string
html_string = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
html_doc = HTMLDocument(html_string)

# Example 2: Load from a local file
# html_doc = HTMLDocument("input.html")

# Example 3: Load from a remote URL
# html_doc = HTMLDocument("https://www.example.com")
```

> **Pourquoi c’est important :** Charger le document une fois vous fournit un objet de type DOM que le convertisseur peut parcourir, garantissant que tous les nœuds de liens et de paragraphes sont disponibles pour l’extraction.

## Étape 2 : Configurer les options d’enregistrement Markdown

`MarkdownSaveOptions` vous permet de contrôler le format de sortie et les fonctionnalités HTML qui sont traduites. Pour **extraire les liens du HTML** tout en conservant les paragraphes, activez les fonctionnalités `LINK` et `PARAGRAPH` et choisissez le formatteur GitLab.

```python
from aspose.html import MarkdownSaveOptions

save_options = MarkdownSaveOptions()
# Use GitLab‑flavored Markdown (supports task lists, tables, etc.)
save_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only links and paragraphs – other tags (e.g., images) are ignored
save_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

> **Pourquoi c’est important :** Limiter les fonctionnalités réduit le bruit dans la sortie et garantit que le Markdown résultant ne contient que les éléments qui vous intéressent — idéal pour les pipelines de documentation ou les générateurs de sites statiques.

## Étape 3 : Convertir le document HTML et écrire le fichier

Appelez maintenant `Converter.convert_html`, en passant le document, les options et le chemin de destination.

```python
from aspose.html import Converter

output_path = "output.md"  # Change to your desired directory/file name
Converter.convert_html(html_doc, save_options, output_path)
print(f"Markdown file saved to {output_path}")
```

L’exécution du script produit un fichier `output.md` avec le contenu suivant :

```markdown
# Title

Sample [link](https://example.com)
```

Remarquez que seul le titre, le paragraphe et le lien apparaissent — exactement ce que nous avions demandé en configurant `save_options`.

## Gestion des variations courantes et des cas particuliers

### Plusieurs sources d’entrée

Si vous devez traiter en lot un dossier de fichiers HTML, encapsulez la conversion dans une boucle :

```python
import pathlib
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

input_folder = pathlib.Path("html_inputs")
output_folder = pathlib.Path("markdown_outputs")
output_folder.mkdir(exist_ok=True)

options = MarkdownSaveOptions()
options.formatter = MarkdownSaveOptions.Formatter.GIT
options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)

for html_path in input_folder.glob("*.html"):
    doc = HTMLDocument(str(html_path))
    md_path = output_folder / (html_path.stem + ".md")
    Converter.convert_html(doc, options, str(md_path))
    print(f"Converted {html_path.name} → {md_path.name}")
```

### Liens manquants

Lorsqu’un document HTML ne contient aucun élément `<a>`, le convertisseur crée tout de même un fichier Markdown valide contenant uniquement les paragraphes autorisés. Aucun traitement d’erreur supplémentaire n’est nécessaire, mais vous pouvez vérifier `save_options.features` si vous devez imposer la présence de liens.

### Encodage de sortie personnalisé

Si votre système cible attend du UTF‑8 avec un BOM, définissez l’encodage sur le `MarkdownSaveOptions` :

```python
save_options.encoding = "utf-8-sig"
```

## Exemple complet et exécutable

En rassemblant tous les éléments, voici un script autonome que vous pouvez copier‑coller et exécuter immédiatement :

```python
# convert_html_to_markdown.py
# -------------------------------------------------
# Demonstrates how to convert HTML to Markdown while
# extracting only links and paragraphs using Aspose.HTML.
# -------------------------------------------------

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def main():
    # 1️⃣ Load HTML – replace this with your own source if needed
    html = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
    document = HTMLDocument(html)

    # 2️⃣ Configure Markdown options (GitLab flavor, links + paragraphs only)
    options = MarkdownSaveOptions()
    options.formatter = MarkdownSaveOptions.Formatter.GIT
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # 3️⃣ Convert and save
    output_file = "output.md"
    Converter.convert_html(document, options, output_file)
    print(f"✅ Markdown saved to {output_file}")

if __name__ == "__main__":
    main()
```

Exécutez avec :

```bash
python convert_html_to_markdown.py
```

Vous verrez `output.md` contenant la représentation Markdown attendue.

## Conclusion

Vous savez maintenant comment **convertir du HTML en Markdown** en Python, extraire les liens du HTML, et contrôler le format de sortie avec `MarkdownSaveOptions`. Cette approche fonctionne pour des fichiers uniques, des lots, ou même des URL distantes, vous offrant une base flexible pour les générateurs de documentation, les pipelines de sites statiques, ou les scripts d’extraction de données.

**Prochaines étapes**

- Expérimentez d’autres `MarkdownSaveOptions.Features` comme `TABLE` ou `IMAGE` pour inclure davantage d’éléments HTML.
- Changez le formatteur en `MarkdownSaveOptions.Formatter.CommonMark` si vous avez besoin d’une conformité stricte à CommonMark.
- Combinez cette conversion avec un générateur de site statique (par ex., MkDocs) pour automatiser la publication de contenu.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convertir du HTML en Markdown Python – extraire les liens & paragraphes](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [Convertir du HTML en Markdown en Python – Guide GitLab Flavored](/html/english/python/general/convert-html-to-markdown-in-python-gitlab-flavored-guide/)
- [Convertir du HTML en Markdown avec Python – Guide complet](/html/english/python/general/convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}