---
category: general
date: 2026-08-25
description: Apprenez à créer un document HTML, sélectionner un élément CSS, modifier
  le texte HTML et enregistrer le fichier HTML à l'aide d'un script Python simple.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: fr
lastmod: 2026-08-25
og_description: Créez un document HTML, sélectionnez l'élément CSS, modifiez le texte
  HTML et enregistrez le fichier HTML en quelques lignes de Python. Suivez ce tutoriel
  complet.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Créer un document HTML et modifier son contenu avec Python – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Comment créer un document HTML et modifier son contenu en Python
url: /fr/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un document html et modifier son contenu en Python

Si vous avez besoin de **create html document** à partir de zéro et de modifier ses éléments de manière programmatique, ce guide vous montre exactement comment faire. Vous verrez un petit script exécutable qui crée un fichier, sélectionne un paragraphe avec un sélecteur CSS, met à jour le texte et écrit le résultat sur le disque.

Travailler avec du HTML en Python est courant lors de la génération de rapports, de modèles d'e‑mail ou de contenu de site statique. À la fin de ce tutoriel, vous serez capable de **select element css**, **modify html text**, et **save html file** sans quitter le confort de votre IDE.

## Prérequis

* Python 3.9 ou version plus récente installé.
* Les paquets `beautifulsoup4` et `lxml` (installez avec `pip install beautifulsoup4 lxml`).
* Permission d'écriture sur le répertoire où vous prévoyez de stocker le fichier de sortie.

Aucun outil supplémentaire n'est requis ; la bibliothèque standard gère les entrées/sorties de fichiers.

## Étape 1 : Installer les bibliothèques requises

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` fournit une API pratique pour analyser et manipuler le HTML, tandis que `lxml` offre un analyseur rapide qui comprend les sélecteurs CSS.

## Étape 2 : Créer le document HTML initial

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Le constructeur `BeautifulSoup` crée un objet **create html document** en mémoire. L'utilisation du parseur `"lxml"` garantit une prise en charge complète des sélecteurs CSS.

## Étape 3 : Sélectionner l'élément paragraphe à l'aide d'un sélecteur CSS

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

La méthode `select_one` implémente la logique **select element css**, renvoyant la première balise correspondante. Si le sélecteur ne correspond à rien, `para` sera `None`, il est donc conseillé d'effectuer une vérification défensive dans le code de production.

## Étape 4 : Modifier le contenu texte du paragraphe

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Attribuer une valeur à `para.string` effectue une opération **modify html text**. BeautifulSoup met à jour l'arbre DOM sous-jacent, de sorte que la modification soit reflétée lors de la sérialisation du document.

## Étape 5 : Enregistrer le HTML mis à jour dans un fichier

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

L'appel `open` combiné à `write` implémente la fonctionnalité **save html file**. L'utilisation de `prettify()` produit une sortie correctement indentée, ce qui est utile lors du débogage.

### Script complet pour copier‑coller rapidement

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

L'exécution de `python edit_html.py` crée `updated.html` contenant :

```html
<p>
 New
</p>
```

## Variations courantes et cas limites

### Sélectionner plusieurs éléments

Si vous avez besoin de sélecteurs **select element css** qui correspondent à plusieurs balises (par ex., `"div.note"`), utilisez `doc.select("div.note")` qui renvoie une liste. Parcourez la liste pour appliquer les modifications à chaque élément.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Conserver les attributs existants

Lorsque vous remplacez le texte, BeautifulSoup conserve tous les attributs de la balise. Par exemple :

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Gérer les éléments manquants gracieusement

Dans les scripts de production, vous rencontrez souvent du HTML malformé. Enveloppez la sélection dans une condition ou un bloc try‑except, comme illustré à l'étape 4, pour éviter les plantages.

### Écrire dans un répertoire spécifique

Remplacez `output_path` par un chemin absolu ou relatif :

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Assurez‑vous que le répertoire existe ; sinon, Python lèvera `FileNotFoundError`.

## Astuces professionnelles

* **Performance** – Pour de gros fichiers HTML, privilégiez `lxml.etree` directement ; BeautifulSoup ajoute une fine couche d'abstraction qui est pratique mais légèrement plus lente.
* **Encodage** – Ouvrez toujours les fichiers avec `encoding="utf-8"` pour conserver les caractères non‑ASCII.
* **Tests** – Après modification, vous pouvez vérifier la sortie avec `assert "New" in open(output_path).read()` dans un test unitaire.

## Conclusion

Vous savez maintenant comment **create html document**, utiliser une requête **select element css** pour localiser un nœud, **modify html text**, et enfin **save html file** avec Python. Ce modèle s'étend à des transformations plus complexes comme des mises à jour en masse, des modifications d'attributs ou la génération de modèles.

Ensuite, explorez des sujets connexes comme **how to edit html** avec des expressions XPath, la génération de pages HTML complètes avec Jinja2, ou l'automatisation du traitement par lots de plusieurs fichiers. Chacun de ces sujets s'appuie sur les étapes fondamentales présentées ici et élargit votre boîte à outils pour la manipulation programmatique du HTML.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un document HTML avec Aspose.HTML – Guide étape par étape](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [Comment modifier l'arbre du document HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Enregistrer le document HTML dans Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}