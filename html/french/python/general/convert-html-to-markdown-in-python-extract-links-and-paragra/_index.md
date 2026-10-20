---
category: general
date: 2026-09-26
description: Convertir le HTML en Markdown avec Python, extraire les liens du HTML
  et enregistrer le HTML en Markdown. Apprenez à convertir le HTML étape par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: fr
lastmod: 2026-09-26
og_description: Convertissez le HTML en Markdown avec Python, extrayez les liens du
  HTML et enregistrez le HTML au format Markdown. Suivez ce guide complet.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Convertir le HTML en Markdown avec Python – extraire les liens et les paragraphes
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Convertir le HTML en Markdown avec Python – extraire facilement les liens et
  les paragraphes
url: /fr/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir du HTML en Markdown en Python – extraire facilement les liens et les paragraphes

Si vous devez **convertir du HTML en Markdown** tout en ne conservant que les parties utiles, ce guide vous montre comment le faire avec seulement quelques lignes de Python. Que vous extrayiez des articles de blog, archiviez de la documentation ou nettoyiez le corps d’e‑mails, vous apprendrez une méthode fiable pour extraire des liens du HTML et enregistrer du HTML en Markdown.

Le tutoriel couvre tout, de l'installation du paquet requis à la gestion des cas limites tels que les balises `<a>` vides ou les paragraphes imbriqués. À la fin, vous disposerez d'un script prêt à l'emploi qui **convertit du HTML en Markdown**, extrait les liens du HTML, et même extrait les paragraphes du HTML lorsque vous en avez besoin.

---

## Prérequis

* Python 3.8 ou version plus récente installé  
* Accès au paquet Python `groupdocs-conversion` (la bibliothèque qui fournit `HTMLDocument`, `MarkdownSaveOptions` et `Converter`)  
* Un fichier HTML local que vous souhaitez traiter (par ex., `article.html`)

Vous pouvez installer la bibliothèque avec pip :

```bash
pip install groupdocs-conversion
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv venv`) pour isoler les dépendances.

---

## Étape 1 : Charger le document HTML source

La première opération consiste à créer un objet `HTMLDocument` qui pointe vers votre fichier source. Cet objet abstrait le HTML brut et fournit au convertisseur un point d'entrée propre.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Pourquoi c’est important :* Charger le document de cette façon permet à la bibliothèque d’analyser le DOM une seule fois, de sorte que les opérations suivantes (comme l'extraction de liens ou de paragraphes) soient rapides et économes en mémoire.

---

## Étape 2 : Créer les options d’enregistrement Markdown et sélectionner les fonctionnalités dont vous avez besoin

`MarkdownSaveOptions` vous permet de choisir quels éléments HTML survivent à la conversion. Le drapeau `features` utilise un OU bit à bit pour combiner les options.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Pourquoi c’est important :* En spécifiant `LINKS` et `PARAGRAPHS`, vous **extrayez les liens du HTML** et **extrayez les paragraphes du HTML** tout en rejetant tout le reste (styles, scripts, images). Si vous avez ensuite besoin uniquement des liens, remplacez `MarkdownFeatures.PARAGRAPHS` par `0` (ou omettez‑le).

---

## Étape 3 : Convertir le HTML en Markdown en utilisant les options configurées

Appelez maintenant la méthode statique `convert_html`, en passant le document source, le chemin de destination et les options que vous venez de créer.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Pourquoi c’est important :* La conversion s’effectue en un seul passage, en appliquant le filtre de fonctionnalités que vous avez défini. Le fichier résultant (`article_links.md`) ne contient que des liens et des paragraphes formatés en Markdown, ce qui correspond exactement à ce dont vous avez besoin lorsque vous souhaitez **enregistrer du HTML en Markdown** pour un traitement en aval.

---

## Script complet – tout ensemble

Voici un script complet et exécutable que vous pouvez copier‑coller dans un fichier nommé `html_to_md.py`. Ajustez les chemins pour qu’ils correspondent à votre environnement.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Résultat attendu

L’exécution du script génère un fichier similaire à celui-ci (le contenu exact dépend du HTML source) :

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Seuls le texte du lien et le texte du paragraphe apparaissent ; tous les autres éléments HTML sont supprimés.

---

## Extraire uniquement les liens ou uniquement les paragraphes (variantes avancées)

Parfois, vous avez besoin **de convertir du HTML** en un fichier Markdown qui ne contient qu’un seul type d’élément.

### 1. Extraire uniquement les liens

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extraire uniquement les paragraphes

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Les deux variantes réutilisent le même appel `convert_html`, vous n’avez donc pas besoin d’écrire une logique de conversion séparée.

---

## Gestion des cas limites

| Situation                               | Solution recommandée |
|----------------------------------------|----------------------|
| Le fichier HTML contient des balises `<a>` vides | Le convertisseur ignore automatiquement les liens vides. Si vous voyez des entrées `[]()` errantes, définissez `md_options.removeEmptyLinks = True`. |
| Paragraphes imbriqués (`<p>` à l'intérieur d'un `<div>`) | La bibliothèque aplatit les paragraphes imbriqués, en préservant l'ordre du texte. Aucun code supplémentaire n’est nécessaire. |
| Caractères non ASCII dans les titres de liens | Assurez‑vous que votre fichier Python est enregistré avec l’encodage UTF‑8 et ouvrez le fichier de sortie avec `encoding="utf-8"` si vous le lisez plus tard. |
| Fichiers HTML très volumineux (≥ 50 Mo) | Traitez le fichier par morceaux en utilisant `HTMLDocument(stream=io.BytesIO(...))` pour éviter de charger le fichier entier en mémoire. |

---

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec des fragments HTML (sans balise racine `<html>`) ?**  
R : Oui. `HTMLDocument` accepte tout fragment bien formé ; le convertisseur traite le fragment comme le corps du document.

**Q : Puis‑je conserver les images avec la syntaxe d’image Markdown ?**  
R : Ajoutez `MarkdownFeatures.IMAGES` au drapeau `features` :  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q : Comment convertir de nombreux fichiers dans un répertoire ?**  
R : Enveloppez `convert_html_to_markdown` dans une boucle qui parcourt le répertoire avec `os.listdir` ou `pathlib.Path.rglob("*.html")`.

---

## Conclusion

Vous savez maintenant comment **convertir du HTML en Markdown** en Python tout en extrayant sélectivement **les liens du HTML** et **les paragraphes du HTML**. Le script illustre l’approche standard — charger le document, configurer `MarkdownSaveOptions`, et exécuter `Converter.convert_html`. Avec quelques ajustements, vous pouvez également **enregistrer du HTML en Markdown** contenant uniquement des liens, uniquement des paragraphes, ou une représentation fidèle complète.

Ensuite, vous pourriez explorer :

* Ajouter `MarkdownFeatures.HEADINGS` pour conserver les titres de sections.  
* Utiliser le Markdown résultant comme entrée pour des générateurs de sites statiques comme MkDocs ou Hugo.  
* Automatiser les conversions en masse pour l’ensemble d’un dépôt de documentation.

Bonne conversion !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convertir du HTML en Markdown en .NET avec Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convertir du HTML en Markdown avec Aspose.HTML pour Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Comment définir le décalage lors de la conversion du HTML en Markdown en Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}