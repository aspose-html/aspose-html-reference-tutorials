---
category: general
date: 2026-09-23
description: Modifier le texte d’un élément dans un fichier HTML avec Python. Apprenez
  à charger le fichier HTML, à modifier la balise <title> et à mettre à jour le titre
  HTML efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: fr
lastmod: 2026-09-23
og_description: Modifier le texte d’un élément dans un document HTML avec Python.
  Ce tutoriel montre comment charger un fichier HTML, modifier la balise <title> et
  mettre à jour le titre HTML en quelques lignes de code.
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: Modifier le texte d’un élément HTML avec Python – guide rapide
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: Modifier le texte d’un élément HTML avec Python – guide étape par étape
url: /fr/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier le texte d’un élément HTML avec Python – guide étape par étape

Si vous devez **modifier le texte d’un élément** dans un document HTML, ce guide vous montre exactement comment le faire avec Python. Que vous répariez une balise `<title>` obsolète ou que vous mettiez à jour tout autre élément, vous apprendrez à **charger un fichier HTML**, à modifier le texte, et à **mettre à jour le titre HTML** (ou tout autre élément) en toute sécurité.

Modifier le titre d’une page web est une tâche courante lors du nettoyage de données extraites, de la génération de pages de site statiques ou de l’automatisation de mises à jour SEO. Dans ce tutoriel, vous allez :

* Charger un fichier HTML depuis le disque.
* Localiser l’élément `<title>` et **modifier la balise title**.
* Enregistrer le document modifié, ce qui **met à jour le titre HTML**.

Tout le code nécessaire est inclus, et chaque étape explique **pourquoi** l’opération est importante, pas seulement **quoi** taper.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Python 3.9 ou une version plus récente installé.
* La bibliothèque `lxml` (`pip install lxml`).  
  `lxml` fournit une analyse et une manipulation HTML rapides et conformes aux standards.
* Un répertoire contenant le fichier HTML que vous souhaitez modifier (remplacez `YOUR_DIRECTORY` par le chemin réel).

## Étape 1 : Charger le fichier HTML

La première étape consiste à **charger le fichier HTML** dans un arbre DOM (Document Object Model) que Python peut manipuler. L’utilisation de `lxml.html` vous offre le support XPath et une gestion fiable des éléments.

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**Pourquoi c’est important :**  
L’analyse crée une représentation structurée de la page, vous permettant d’interroger les éléments directement. Sans charger le fichier, vous ne pouvez pas **modifier le texte d’un élément** en toute sécurité, car vous travailleriez avec des chaînes brutes, ce qui est source d’erreurs.

## Étape 2 : Localiser l’élément `<title>` et **modifier le texte d’un élément**

Maintenant que le document est chargé, vous pouvez **modifier la balise title**. L’expression XPath `".//title"` trouve le premier élément `<title>` dans la hiérarchie du document.

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**Pourquoi c’est important :**  
Attribuer directement à `title_elem.text` **modifie le texte de l’élément** sans altérer le balisage environnant. Cette approche préserve les espaces, les commentaires et les autres balises, garantissant que le résultat reste un HTML valide.

### Cas particulier : plusieurs balises `<title>`

Les standards HTML n’autorisent qu’une seule balise `<title>`, mais des fichiers mal formés peuvent parfois en contenir plusieurs. Si vous devez gérer cette situation, parcourez toutes les correspondances :

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## Étape 3 : Enregistrer le document modifié – **mettre à jour le titre HTML**

Après la modification, écrivez l’arbre de nouveau sur le disque. L’utilisation de `pretty_print=True` garde le fichier lisible.

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**Pourquoi c’est important :**  
L’enregistrement crée un nouveau fichier qui reflète l’opération **modifier le texte d’un élément**. Si vous devez écraser le fichier original, utilisez simplement le même chemin pour `output_path`.

## Script complet en un seul bloc

En rassemblant tous les éléments, voici un script autonome qui **charge le fichier HTML**, **modifie le texte d’un élément**, et **met à jour le titre HTML** :

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

L’exécution de ce script produit un fichier `updated.html` dont le `<title>` affiche maintenant **New Title**.

## Variantes courantes de la technique

### Modifier d’autres éléments (p. ex., `<h1>`)

Si vous devez **modifier le texte d’un élément** pour un titre plutôt que pour le `<title>`, ajustez l’XPath :

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### Conserver les espaces existants

Lorsque le HTML original utilise une indentation à l’intérieur des balises, `pretty_print` peut le reformater. Pour conserver le formatage d’origine, omettez `pretty_print` :

```python
doc.write(destination, encoding="utf-8")
```

### Travailler avec des caractères Unicode

`lxml` gère Unicode automatiquement. Assurez‑vous que le fichier source est enregistré avec l’encodage UTF‑8 ; sinon, spécifiez l’encodage correct lors de l’ouverture du fichier.

## Astuces pro et pièges

* **Astuce pro :** Utilisez `doc.xpath("//title/text()")` si vous avez seulement besoin du contenu texte sans modifier l’élément.
* **Attention à :** les fichiers HTML qui contiennent un `<title>` à l’intérieur d’un `<svg>` ou d’un autre espace de noms non‑HTML. Dans ces cas, affinez l’XPath pour cibler la section `<head>` : `doc.find(".//head/title")`.
* **Astuce de performance :** pour le traitement par lots de milliers de fichiers, réutilisez la même instance de parseur afin de réduire la surcharge.

## Conclusion

Vous savez maintenant comment **modifier le texte d’un élément** dans un document HTML avec Python, en particulier comment **charger le fichier HTML**, **modifier la balise title**, et **mettre à jour le titre HTML**. L’exemple complet montre une approche fiable, basée sur une bibliothèque, qui fonctionne aussi bien avec du HTML bien formé que légèrement mal formé.

À partir d’ici, vous pouvez :

* Appliquer le même modèle à d’autres balises (`<h2>`, `<meta>`, etc.).
* Combiner ce script avec un pipeline de web‑scraping pour nettoyer de grandes collections de pages.
* Explorer l’API plus riche de `lxml` pour la manipulation d’attributs, les sélecteurs CSS et la sérialisation HTML.

Bon codage, et n’hésitez pas à expérimenter avec différents éléments pour maîtriser la manipulation HTML en Python !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}