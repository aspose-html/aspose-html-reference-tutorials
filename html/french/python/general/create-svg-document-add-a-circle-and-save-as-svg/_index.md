---
category: general
date: 2026-07-31
description: Apprenez à créer un document SVG, ajouter un cercle et enregistrer rapidement
  le fichier SVG. Exportez le graphique au format SVG en quelques lignes de code Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: fr
lastmod: 2026-07-31
og_description: Créez un document SVG, ajoutez un cercle et enregistrez le fichier
  SVG en quelques secondes. Ce guide vous montre comment exporter le graphique au
  format SVG avec un code clair et exécutable.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Créer un document SVG – Ajouter un cercle et enregistrer au format SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Créer un document SVG – Ajouter un cercle et enregistrer au format SVG
url: /fr/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document SVG – Ajouter un cercle et enregistrer en SVG

Vous avez déjà eu besoin de **create SVG document** à partir du code mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul ; de nombreux développeurs rencontrent ce mur lorsqu’ils s’initient aux graphiques vectoriels. Dans ce tutoriel, nous allons parcourir un petit exemple autonome qui vous montre comment **add circle to SVG**, puis **save SVG file** afin que vous puissiez **export graphic as SVG** pour une utilisation sur le web ou dans des outils de design.

Nous resterons légers : quelques lignes de Python, une bibliothèque d’aide SVG populaire, et une petite explication. À la fin, vous disposerez d’un `circle.svg` prêt à l’emploi dans votre dossier, et vous comprendrez pourquoi chaque étape est importante—sans raccourcis vagues du type « voir la documentation ».

## Ce dont vous avez besoin

- Python 3.8+ (toute version récente convient)
- Le package `svgwrite` – installez‑le avec `pip install svgwrite`
- Un éditeur de texte ou un IDE (VS Code, PyCharm, ou même Notepad suffisent)
- Permission d’écriture dans le répertoire où vous souhaitez enregistrer le fichier

C’est tout. Pas de dépendances lourdes, pas de services externes.

## Étape 1 : Configurer le document SVG

Créer un document SVG est aussi simple que d’instancier un objet `Drawing` depuis `svgwrite`. Pensez à cet objet comme la toile vierge où chaque forme vit.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Pourquoi c’est important :** La classe `Drawing` gère tout le boilerplate XML pour vous—espaces de noms, en‑têtes, et l’élément racine `<svg>`. En spécifiant un nom de fichier dès le départ, nous savons déjà où le fichier sera enregistré, ce qui rend l’étape **save svg file** ultérieure triviale.

### Astuce pro
Si vous prévoyez de générer de nombreux fichiers dans une boucle, donnez à chaque `Drawing` un nom unique ou utilisez `io.BytesIO` pour tout garder en mémoire jusqu’à ce que vous soyez prêt à écrire.

## Étape 2 : Ajouter un cercle au SVG

Maintenant que le document existe, ajoutons **add circle to SVG**. La méthode `add()` accepte n’importe quel objet forme ; un `Circle` est parfait pour un simple point rouge au centre.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Pourquoi nous utilisons les variables `center` et `radius` :** Coder en dur les nombres rend le code plus difficile à lire et à maintenir. En nommant les valeurs, nous clarifions l’intention—ce cercle se trouve exactement au centre d’une toile de 200 × 200 et est suffisamment grand pour être visible.

### Cas particulier – Fond transparent
Si vous avez besoin d’un fond transparent (le comportement par défaut du SVG), vous pouvez ignorer la définition d’un `fill` sur la racine. Pour un fond blanc, ajoutez :

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Placez cela avant d’ajouter le cercle afin que le rectangle se trouve en dessous.

## Étape 3 : Enregistrer le fichier SVG

Avec la forme en place, l’acte final est de **save SVG file**. La méthode `save()` écrit le XML sur le disque, et comme nous avons déjà donné un nom de fichier au `Drawing`, un seul appel suffit.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Que se passe‑t‑il en coulisses ?** `svgwrite` sérialise l’arbre d’éléments en une chaîne, ajoute la déclaration XML, et l’écrit en encodage UTF‑8. Si le répertoire cible n’existe pas, Python lèvera une `FileNotFoundError` ; assurez‑vous que le chemin est valide ou créez‑le avec `os.makedirs()`.

### Bonus : Exporter le graphique en SVG par programme

Si vous avez besoin du contenu SVG sous forme de chaîne—par exemple pour l’intégrer dans un e‑mail HTML—vous pouvez appeler `dwg.tostring()` à la place de `save()` :

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Exemple complet fonctionnel

En rassemblant le tout, voici un script complet, prêt à être exécuté :

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Sortie attendue :** Après l’exécution du script, vous verrez un fichier `circle.svg` dans le même dossier. L’ouvrir dans un navigateur ou tout éditeur vectoriel affichera un cercle rouge centré sur un carré blanc—exactement ce que nous avons programmé.

## Questions fréquentes et pièges

- **Et si je veux une forme différente ?** Remplacez `dwg.circle` par `dwg.rect`, `dwg.ellipse`, ou même une chaîne `<path>` personnalisée. L’API est cohérente entre les formes.
- **Puis‑je intégrer le SVG directement dans du HTML ?** Absolument. Le fichier que vous venez de créer peut être référencé avec `<img src="circle.svg" alt="Red circle">` ou intégré en ligne avec des balises `<svg>`.
- **Pourquoi ne pas écrire du XML brut ?** Vous pourriez, mais des bibliothèques comme `svgwrite` gèrent les subtilités des espaces de noms et rendent le code beaucoup plus maintenable—surtout lorsque vous commencez à ajouter des dégradés ou des animations.

## Conclusion

Vous savez maintenant comment **create SVG document**, **add circle to SVG**, et **save SVG file** afin de **export graphic as SVG** en quelques lignes de Python. Le modèle s’adapte : remplacez le cercle par n’importe quelle forme vectorielle, bouclez sur des données pour générer des graphiques, ou traitez en lot des actifs pour un système de design.

Prochaines étapes ? Essayez d’ajouter des libellés texte, expérimentez les dégradés, ou générez une galerie complète d’icônes dans un seul script. Si vous êtes curieux des fonctionnalités avancées, consultez la documentation de `svgwrite` sur les groupes (`<g>`), les transformations et le support d’animation.

Bon codage, et que vos vecteurs restent toujours nets !


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}