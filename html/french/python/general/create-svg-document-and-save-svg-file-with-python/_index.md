---
category: general
date: 2026-11-27
description: Créer un document SVG et enregistrer le fichier SVG à l'aide de Python.
  Apprenez à exporter un vecteur au format SVG et à générer rapidement une image SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: fr
lastmod: 2026-11-27
og_description: Créer un document SVG et enregistrer le fichier SVG avec Python. Ce
  guide vous montre comment exporter un vecteur au format SVG et produire une image
  SVG en quelques minutes.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Créer un document SVG et enregistrer le fichier SVG avec Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Créer un document SVG et enregistrer le fichier SVG avec Python
url: /fr/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document SVG et enregistrer un fichier SVG avec Python

Si vous devez **créer un document SVG** à partir de zéro, ce guide vous accompagne tout au long du processus. Vous verrez comment **enregistrer le fichier SVG** sur le disque, exporter le vecteur au format SVG, et obtenir une image SVG prête à l'emploi en quelques lignes de code seulement.

Générer des graphiques évolutifs de manière programmatique est utile pour les rapports, les icônes d'interface utilisateur, ou toute situation où vous souhaitez des images indépendantes de la résolution. À la fin de ce tutoriel, vous serez capable de répondre à « **how to create SVG** ? » pour des formes simples et d'étendre le modèle à des illustrations vectorielles complexes.

## Ce dont vous avez besoin

- Python 3.8 ou plus récent  
- Le package `svgwrite` (installable via `pip`)  
- Un répertoire accessible en écriture pour le fichier de sortie  

Aucun éditeur graphique externe n'est requis ; tout s'exécute depuis la ligne de commande.

## Étape 1 : Installer la bibliothèque `svgwrite`

`svgwrite` fournit une API propre et Pythonique pour créer du balisage SVG. Installez‑la une fois avec :

```bash
pip install svgwrite
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv .venv`) pour garder les dépendances isolées.

## Étape 2 : Créer un document SVG

Nous créons maintenant réellement des objets **créer un document SVG**. La classe `Drawing` représente l'élément racine `<svg>` et gère automatiquement les espaces de noms.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

L'instance `Drawing` est le point d'entrée pour toutes les opérations SVG suivantes. En spécifiant `size`, nous définissons les dimensions du canevas, ce qui influence la façon dont les navigateurs affichent l'image.

## Étape 3 : Ajouter un élément cercle rouge

Ajouter des formes est simple. La méthode `circle` crée un élément `<circle>` ; nous l'attachons ensuite à la racine.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Pourquoi choisir un cercle : les cercles sont des primitives vectorielles qui démontrent l'évolutivité sans aucune perte de qualité, rendant la sortie idéale pour tester les flux de travail **export vector as SVG**.

## Étape 4 : Enregistrer le fichier SVG

Enfin, écrivez le balisage sur le disque. Cette étape satisfait l'exigence **save SVG file** et produit un fichier que vous pouvez ouvrir dans n'importe quel navigateur ou éditeur vectoriel.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Lorsque vous exécutez le script, vous verrez un message console confirmant l'emplacement du fichier généré.

### Sortie attendue

Le `circle.svg` résultant contient :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Ouvrir le fichier dans un navigateur affiche un cercle rouge net, et comme il est basé sur le vecteur, vous pouvez zoomer indéfiniment sans pixellisation.

## Étape 5 : Variations courantes et cas limites

### Exporter des vecteurs plus complexes

Si vous devez **export vector as SVG** pour des illustrations multi‑formes, répétez simplement le modèle `dwg.add()` avec d'autres primitives (`rect`, `line`, `path`, etc.). Par exemple :

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Gestion de l'Unicode et du texte

SVG prend en charge les éléments texte avec un support complet de l'Unicode. Utilisez `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` pour intégrer des libellés multilingues.

### Enregistrement à un autre emplacement

Lors de **save SVG image** vers un dossier spécifié par l'utilisateur, validez le chemin pour éviter les erreurs de permission :

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minifier la sortie

Pour les pipelines de production, vous pourriez vouloir une taille de fichier plus petite. Passez `pretty=False` à `dwg.tostring()` et écrivez le résultat manuellement :

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Comment créer un SVG avec des bibliothèques alternatives (optionnel)

Bien que `svgwrite` soit léger et pure‑Python, d'autres écosystèmes existent :

- **cairosvg** – convertit PNG, PDF ou HTML en SVG.  
- **lxml** – vous permet de créer manuellement du balisage SVG en utilisant les API XML.  

Le choix d'une bibliothèque dépend de la complexité de votre projet et des dépendances existantes.

## Conclusion

Vous savez maintenant comment **create SVG document**, ajouter des formes vectorielles, et **save SVG file** avec Python. La solution complète montre les étapes pour **export vector as SVG**, générer une **SVG image**, et répondre à la question courante **how to create SVG** de manière programmatique.

À partir d'ici, vous pouvez :

- Étendre le script avec des boucles pour générer automatiquement des graphiques ou des icônes.  
- Intégrer la sortie SVG dans des applications web ou des modèles d'e‑mail.  
- Explorer l'animation en ajoutant des éléments `<animate>` avec `svgwrite`.  

Expérimentez avec différentes formes, couleurs et dégradés pour exploiter pleinement la puissance des graphiques vectoriels évolutifs dans vos projets Python. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un document SVG – Ajouter un cercle et enregistrer en SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Créer un document SVG en Python – Guide de conversion SVG en PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Charger un fichier SVG Python – Guide complet pour exporter, intégrer et convertir](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}