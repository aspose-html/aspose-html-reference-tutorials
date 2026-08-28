---
category: general
date: 2026-05-31
description: Apprenez comment obtenir un élément par son ID, changer la couleur de
  fond HTML, lire le texte HTML et définir un attribut HTML à l'aide de Python. Tutoriel
  étape par étape.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: fr
og_description: Obtenez un élément par son ID, lisez le texte HTML, définissez un
  attribut HTML et changez la couleur de fond HTML en utilisant Python dans un guide
  simple et facile à suivre.
og_title: Récupérer un élément par ID en Python – Tutoriel complet de manipulation
  HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Récupérer un élément par ID en Python – Guide complet de manipulation HTML
url: /fr/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir un élément par id en Python – Guide complet de manipulation HTML

Vous avez déjà eu besoin de **get element by id** depuis une page HTML en écrivant un script Python rapide ? Vous n'êtes pas seul—la plupart des développeurs rencontrent ce même obstacle lorsqu'ils commencent à explorer des sites ou à ajuster des rapports locaux. La bonne nouvelle ? En quelques lignes de code, vous pouvez lire le texte de l'élément, changer sa couleur de fond, et même définir de nouveaux attributs, le tout sans quitter votre éditeur.

Dans ce tutoriel, nous allons parcourir un exemple réel : charger un fichier `sample.html` local, récupérer l'élément dont l'ID est `main‑content`, afficher son texte interne, et enfin remplacer la couleur de fond par un gris clair. À la fin, vous saurez également **how to read HTML text**, **how to set HTML attribute**, et pourquoi **manipulate HTML with Python** est une compétence pratique dans toute boîte à outils d'automatisation.

## Ce dont vous avez besoin

- **Python 3.9+** (toute version récente fonctionne)
- La bibliothèque **`lxml`** (ou **BeautifulSoup** si vous préférez) – nous utiliserons `lxml.html` car elle fournit une API propre de type `get_element_by_id`.
- Un petit fichier HTML nommé `sample.html` placé dans un dossier appelé `YOUR_DIRECTORY`. N'hésitez pas à copier l'extrait ci‑dessous dans ce fichier :

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

C’est tout—pas de frameworks sophistiqués, juste du Python pur et un fichier HTML statique.

## Étape 1 : Installer la bibliothèque requise

Si vous n'avez pas encore installé `lxml`, ouvrez un terminal et exécutez :

```bash
pip install lxml
```

*Astuce :* Utiliser un environnement virtuel garde votre Python global propre, surtout lorsque vous commencez à jongler avec plusieurs projets.

## Étape 2 : Charger le document HTML

Nous allons maintenant lire le fichier dans un objet document `lxml.html`. Considérez cela comme la transformation du texte brut en un arbre navigable.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

L'exécution affiche « Document loaded successfully ». Si le fichier est introuvable, Python lèvera une `FileNotFoundError`—il est bon de la capturer tôt avant de courir après un élément fantôme.

## Étape 3 : Get element by id

Voici le cœur du sujet. `lxml` nous fournit une méthode pratique `get_element_by_id` qui reflète l'API DOM que vous utiliseriez en JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Lorsque l'élément existe, vous verrez « Element found! » affiché dans la console. C’est l’étape **get element by id** qui alimente la plupart de nos manipulations ultérieures.

## Étape 4 : How to read HTML text

Une fois que vous avez l'élément, extraire son texte visible est un jeu d'enfant. La méthode `text_content()` renvoie tout le contenu intérieur, dépouillé des balises.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Sortie attendue :

```
Inner text: Hello, world! This is the original text.
```

Vous pourriez vous demander, *et si l'élément contient des balises imbriquées ?* `text_content()` fonctionne toujours—il concatène tous les nœuds texte descendants, vous fournissant une chaîne propre que vous pouvez journaliser, stocker ou transmettre à un autre algorithme.

## Étape 5 : How to set HTML attribute

Modifier ou ajouter des attributs est tout aussi simple. La méthode `set` vous permet d'assigner n'importe quel nom d'attribut.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Sortie :

```
New attribute value: true
```

Cette ligne montre **how to set HTML attribute** à la volée. Vous pouvez remplacer `"data-modified"` par `"class"`, `"title"` ou tout autre attribut supporté par l'élément.

## Étape 6 : Change background colour HTML

Passons maintenant à l'ajustement visuel. Pour changer la couleur de fond, nous injectons un attribut `style` qui surcharge la valeur par défaut.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Après avoir exécuté le script, le `div` dans `sample.html` apparaîtra ainsi lorsque vous l'ouvrirez dans un navigateur :

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

C’est la technique **change background colour html** que vous pouvez réutiliser pour n'importe quel élément—il suffit de remplacer le code couleur.

## Étape 7 : Manipulate HTML with Python – Mettre tout ensemble

Voici le script complet et exécutable qui combine chaque étape. Enregistrez-le sous le nom `modify_html.py` et exécutez-le depuis le même répertoire que votre dossier `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Ce que fait le script, ligne par ligne

1. **Imports** `lxml.html` pour l'analyse et `pathlib` pour des chemins indépendants du système d'exploitation.  
2. **Loads** `sample.html` et interrompt avec une erreur claire si le fichier est absent.  
3. **Retrieves** l'élément en utilisant **get element by id**.  
4. **Prints** le texte de l'élément—illustrant **how to read HTML text**.  
5. **Adds** un attribut personnalisé, illustrant **how to set HTML attribute**.  
6. **Changes** la couleur de fond, remplissant le besoin **change background colour html**.  
7. **Writes** le balisage mis à jour dans `sample_modified.html`, afin que vous puissiez l'ouvrir dans un navigateur et voir les modifications.

L'exécution du script produit une sortie console similaire à :

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Ouvrez `sample_modified.html` et vous remarquerez le fond gris derrière le texte—la preuve que **manipulate HTML with python** fonctionne réellement.

## Pièges courants & comment les éviter

- **Missing ID** – Si l'élément cible n'existe pas, `get_element_by_id` renvoie `None`. Vérifiez toujours `None` avant d'accéder aux propriétés ; sinon vous obtiendrez une `AttributeError`.
- **Encoding issues** – Lors de la lecture de pages non‑ASCII, passez `encoding='utf-8'` à `html.parse` ou assurez‑vous que votre fichier est enregistré en UTF‑8.
- **Overwriting existing styles** – Définir l'attribut `style` remplace les styles en ligne précédents. Si vous devez conserver les règles existantes, lisez d'abord la valeur actuelle de `style`, ajoutez votre nouvelle règle, puis réécrivez‑la.
- **File permissions** – Écrire dans le même dossier peut échouer sur des systèmes en lecture‑seule. Choisissez un chemin de sortie inscriptible, comme nous l'avons fait avec `sample_modified.html`.

## Étendre l'exemple

Maintenant que vous avez maîtrisé les bases, envisagez les étapes suivantes :

- **Loop over multiple IDs** – Utilisez une liste d'IDs et itérez avec une boucle `for` pour traiter par lot des sections d'une page.  
- **Replace text content** – Appelez `elem.text = "New text"` pour modifier la chaîne visible.  
- **Add child elements** – Utilisez `

## Que devriez‑vous apprendre ensuite ?

- [Comment modifier du HTML avec Aspose.HTML pour Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Comment interroger du HTML en Java – Tutoriel complet](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Comment convertir du HTML en PDF Java – En utilisant Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}