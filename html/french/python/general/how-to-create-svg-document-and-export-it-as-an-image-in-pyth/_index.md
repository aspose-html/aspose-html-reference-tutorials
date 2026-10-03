---
category: general
date: 2026-10-02
description: Apprenez à créer un document SVG en Python, à enregistrer le SVG dans
  un fichier et à exporter l'image SVG avec un script court et complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: fr
lastmod: 2026-10-02
og_description: Créez un document SVG en Python et exportez l'image SVG avec ce tutoriel
  pratique. Suivez le script, enregistrez le SVG dans un fichier et réutilisez le
  graphique vectoriel instantanément.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Créer un document SVG en Python – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Comment créer un document SVG et l’exporter en tant qu’image en Python
url: /fr/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un document SVG et l'exporter en tant qu'image en Python

Si vous devez **créer un document SVG** de manière programmatique, ce tutoriel vous montre exactement comment le faire avec Python. Vous verrez un script complet qui crée un cercle simple, enregistre le SVG dans un fichier, et produit une image SVG exportable que vous pouvez intégrer n'importe où.

Générer des graphiques vectoriels évolutifs à partir du code élimine l'effort manuel de dessin des formes dans un éditeur GUI. À la fin de ce guide, vous pourrez intégrer la création de SVG dans des pipelines de visualisation de données, des générateurs de rapports automatisés, ou tout projet nécessitant des graphiques nets et indépendants de la résolution.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

- Python 3.8 ou version plus récente installé
- La bibliothèque `svgwrite` (installer avec `pip install svgwrite`)
- Permission d'écriture sur le répertoire où le SVG sera enregistré

Ces exigences maintiennent l'exemple léger et compatible avec la plupart des environnements.

## Étape 1 : Installer et importer la bibliothèque SVG

La première étape consiste à ajouter la bibliothèque tierce qui fournit une API pratique pour la création de SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstrait la structure XML d'un fichier SVG, vous permettant de vous concentrer sur la géométrie plutôt que sur le balisage brut.

## Étape 2 : Créer un objet document SVG

Vous pouvez maintenant **créer un document SVG** en instanciant `svgwrite.Drawing`. Cet objet représente l'élément racine `<svg>` et contient toutes les formes suivantes.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

L'argument `size` définit les dimensions en pixels rendues, tandis que `viewBox` établit un système de coordonnées qui correspond à la géométrie que vous définirez plus tard.

## Étape 3 : Ajouter un élément cercle

Un cercle est défini par son centre (`cx`, `cy`) et son rayon (`r`). Utilisez l'assistant `circle` pour ajouter ces attributs.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Le cercle se trouve au centre du canevas de 100 × 100, laissant une marge de 10 pixels de chaque côté. Ajustez `fill` et `stroke` pour correspondre à votre langage de conception.

## Étape 4 : Enregistrer le SVG dans un fichier

Une fois le graphique assemblé, vous pouvez **enregistrer le SVG dans un fichier** en utilisant la méthode `save`. Cela écrit un XML bien formé que les navigateurs et les éditeurs vectoriels comprennent.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Le fichier `circle.svg` se trouve maintenant dans le répertoire de travail actuel. Vous pouvez l'ouvrir dans un navigateur web, Inkscape, ou tout outil supportant le format SVG.

## Étape 5 : Vérifier l'image SVG exportée

Ouvrez le fichier enregistré dans un navigateur pour confirmer le résultat. Vous devriez voir un cercle centré avec les couleurs spécifiées. Le XML brut ressemble à ceci :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Comme le SVG est basé sur des vecteurs, vous pouvez mettre à l'échelle l'image sans perte de qualité, ce qui le rend idéal pour les conceptions web réactives ou les impressions haute résolution.

## Astuce : Exporter le SVG en PNG ou JPEG

Si vous avez besoin d'une version raster, combinez le fichier SVG avec un outil de conversion tel que **CairoSVG** :

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Cette étape montre comment **exporter l'image SVG** vers un format bitmap, utile lorsque les systèmes en aval ne peuvent pas rendre le SVG directement.

## Variations courantes et cas limites

| Variation | Comment gérer |
|-----------|---------------|
| Formes multiples | Appelez `dwg.add()` pour chaque nouvel élément (rect, line, path). |
| Dimensions dynamiques | Calculez `size` et `viewBox` à partir des données avant de créer le `Drawing`. |
| Étiquettes de texte | Utilisez `dwg.text("Label", insert=("10", "20"))` et stylisez avec `font_size` et `fill`. |
| Réutiliser le document | Conservez l'objet `Drawing` en mémoire et appelez `save()` chaque fois que vous avez besoin d'un fichier mis à jour. |
| Fichiers volumineux | Diffusez la sortie en utilisant `dwg.tostring()` et écrivez dans un objet fichier manuellement pour éviter les pics de mémoire. |

Gérer ces scénarios garantit que votre script **comment générer du SVG** s'adapte des icônes simples aux diagrammes complexes.

## Récapitulatif du script complet

Voici l'exemple complet et exécutable qui intègre toutes les étapes et la conversion optionnelle :

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

L'exécution de ce script produit `circle.svg` et, si `cairosvg` est installé, `circle.png`. Les deux fichiers sont prêts à être inclus dans des pages web, des rapports ou pour un traitement ultérieur.

## Conclusion

Vous savez maintenant comment **créer un document SVG** en Python, **enregistrer le SVG dans un fichier**, et **exporter l'image SVG** pour une utilisation plus large. L'exemple couvre les appels d'API essentiels, explique pourquoi chaque étape est importante, et propose des extensions pour des graphiques plus complexes.

Ensuite, explorez d'autres sujets du **tutoriel SVG Python** tels que le tracé de chemins, l'application de dégradés et l'animation d'éléments. Intégrer ces techniques vous permettra de générer des graphiques vectoriels dynamiques et basés sur les données directement depuis vos applications Python. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer et gérer des documents SVG dans Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Enregistrer un document SVG dans Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg en png java – Convertir SVG en image avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}