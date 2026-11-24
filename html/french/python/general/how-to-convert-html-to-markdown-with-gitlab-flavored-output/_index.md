---
category: general
date: 2026-11-24
description: Convertir le HTML en Markdown avec Python en utilisant les options de
  type GitLab et extraire facilement les liens.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: fr
lastmod: 2026-11-24
og_description: Convertir le HTML en Markdown en Python en utilisant les options de
  style GitLab, enregistrer le HTML en tant que Markdown et extraire les liens vers
  le Markdown avec un exemple complet.
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: Convertir le HTML en Markdown avec une sortie au format GitLab – Guide Python
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: Comment convertir du HTML en Markdown avec une sortie au format GitLab en Python
url: /fr/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir du HTML en Markdown avec une sortie au format GitLab en Python

Si vous devez **convertir du HTML en Markdown**, ce guide présente une solution complète, prête à l’emploi. Vous verrez comment enregistrer du HTML en markdown en utilisant le formatage au style GitLab et comment extraire les liens vers le markdown sans quitter le code.

L’approche fonctionne avec la bibliothèque Aspose.HTML for Python, qui fournit une API de conversion en une seule ligne et un contrôle granulaire sur le type de Markdown. À la fin du tutoriel, vous disposerez d’un script qui génère des fichiers markdown au format GitLab propres et une liste de liens extraits.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

* Python 3.8 ou une version ultérieure installé.
* Un accès à `pip` pour l’installation des paquets.
* Un fichier HTML local (par ex., `article.html`) que vous souhaitez convertir.
* Une connaissance de base de l’exécution de scripts Python depuis la ligne de commande.

Aucun outil supplémentaire n’est requis ; la bibliothèque gère le parsing, la conversion et l’extraction des liens en interne.

## Installer la bibliothèque Aspose.HTML for Python

L’API de conversion se trouve dans le paquet `aspose.html`. Installez‑le avec `pip` :

```bash
pip install aspose-html
```

Le paquet regroupe les classes `HTMLDocument`, `MarkdownSaveOptions` et `Converter` utilisées plus tard dans le script. L’installation se termine en quelques secondes et ne nécessite aucun runtime supplémentaire.

## Charger le document HTML

Créer un objet `HTMLDocument` charge le fichier source en mémoire. Le constructeur accepte un chemin de fichier ou une URL.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

L’instance `doc` représente maintenant l’arbre DOM complet, permettant au convertisseur de lire chaque élément, y compris les liens et les balises de paragraphe.

## Configurer les options Markdown au format GitLab

Le markdown au format GitLab diffère du CommonMark standard dans la façon dont il traite les liens et les paragraphes. La classe `MarkdownSaveOptions` vous permet de spécifier le formateur et le jeu de fonctionnalités dont vous avez besoin.

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

Définir `features` à `["Link", "Paragraph"]` garantit que la conversion se concentre sur l’extraction des liens tout en préservant la structure des paragraphes, ce qui est idéal pour la documentation ou la génération de changelogs.

## Exécuter la conversion et enregistrer en Markdown

Avec le document chargé et les options configurées, invoquez la méthode statique `Converter.convert`. Elle écrit le résultat directement dans le fichier cible.

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

Après l’exécution, `article.md` contient du markdown au format GitLab qui reflète les liens et les paragraphes du HTML d’origine.

## Vérifier la sortie et extraire les liens vers le markdown

Ouvrez le fichier généré pour confirmer la conversion. Vous devriez voir la syntaxe des liens (`[text](url)`) et les sauts de paragraphe qui correspondent à la source.

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

Si vous avez besoin de la liste brute d’URL pour un traitement ultérieur, vous pouvez les extraire du `HTMLDocument` avant la conversion :

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

Cette étape montre **comment extraire les liens vers le markdown** en utilisant le même DOM déjà chargé, évitant ainsi une seconde analyse.

## Script complet

Assembler le tout donne un script autonome que vous pouvez intégrer à n’importe quel projet :

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

Exécution du script :

```bash
python convert_html_to_gitlab_md.py
```

produit `article.md` avec du markdown au format GitLab et affiche la liste des URL extraites.

## Variations courantes et cas limites

| Scénario                              | Ajustement                                                                    |
|--------------------------------------|-------------------------------------------------------------------------------|
| **HTML complet (images, tableaux, etc.)** | Ajoutez `"Image"` ou `"Table"` à `features` pour conserver ces éléments.      |
| **Autre saveur de Markdown**        | Changez `formatter="GIT"` en `"COMMONMARK"` ou `"GFM"` pour d’autres plateformes. |
| **Fichiers volumineux (> 50 MB)**    | Utilisez les API de streaming (`HTMLDocument.open`) pour éviter de charger le fichier entier. |
| **Caractères Unicode**               | Assurez‑vous que le fichier source est encodé en UTF‑8 ; la bibliothèque préserve l’encodage. |

Ces variations vous permettent de réutiliser le même modèle pour **enregistrer du HTML en markdown** dans de nombreux contextes.

## Astuces professionnelles

* **Réutiliser les options :** Créez une seule instance de `MarkdownSaveOptions` et réutilisez‑la si vous convertissez plusieurs fichiers dans un job batch.
* **Valider les liens :** Après extraction, lancez un simple `requests.head(url)` pour détecter les URL cassées.
* **Verrouiller la version :** Fixez la version d’Aspose.HTML (`aspose-html==23.10`) afin d’éviter les changements inattendus de l’API.

## Conclusion

Vous savez maintenant comment **convertir du HTML en markdown** en utilisant un formateur au format GitLab, **enregistrer du HTML en markdown**, et **extraire les liens vers le markdown** avec un script Python concis. La solution fonctionne immédiatement, gère les cas limites typiques et peut être étendue à d’autres saveurs de Markdown ou à des fonctionnalités HTML supplémentaires.

### Prochaines étapes

* Explorez la liste `features` pour inclure des images, des tableaux ou des blocs de code.
* Intégrez ce script dans une pipeline CI afin de générer automatiquement de la documentation à partir de sources HTML.
* Combinez les liens extraits avec un service de vérification de liens pour maintenir des références saines.

N’hésitez pas à adapter le script à vos propres flux de travail et à partager vos résultats avec la communauté !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [How to convert HTML to Markdown with GitLab‑flavored markdown in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [convert html to markdown python – save markdown file with python](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}