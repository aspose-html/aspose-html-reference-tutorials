---
category: general
date: 2026-06-16
description: Comment redimensionner rapidement un SVG en Python – charger un fichier
  SVG avec Python, éditer un fichier SVG avec Python, et même redimensionner en lot
  des fichiers SVG grâce à un petit script.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: fr
og_description: Comment redimensionner un SVG en Python ? Apprenez à charger un fichier
  SVG avec Python, à le modifier et à redimensionner en lot des fichiers SVG grâce
  à un exemple clair et exécutable.
og_title: Comment redimensionner un SVG en Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Comment redimensionner un SVG en Python – Guide étape par étape
url: /fr/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redimensionner un SVG en Python – Tutoriel complet

Vous vous êtes déjà demandé **comment redimensionner un SVG** sans ouvrir d'éditeur graphique ? Peut‑être avez‑vous un logo qui doit faire 200 px de large pour une bannière web, ou vous préparez des dizaines d'icônes pour une application mobile. Bonne nouvelle ? Vous pouvez tout faire en Python—pas de Photoshop, pas d'interface Inkscape, juste quelques lignes de code.

Dans ce guide, nous allons parcourir le chargement d’un fichier SVG en Python, la modification de ses dimensions, et même le redimensionnement d’un dossier complet de SVG d’un seul coup. À la fin, vous serez capable de **load SVG file Python**, **edit SVG file Python**, et **batch resize SVG files** en toute confiance.

## Prérequis

- Python 3.8+ installé (la commande standard `python` fonctionne)
- La bibliothèque `svgwrite` ou `lxml` – nous utiliserons `lxml` car elle offre un accès direct au DOM.
- Un dossier de SVG que vous souhaitez redimensionner (par ex. `assets/icons/`)

Vous n’avez besoin d’aucun outil GUI ; tout s’exécute depuis le terminal.

---

## Étape 1 : Installer la bibliothèque requise

Tout d’abord, récupérez `lxml` depuis PyPI. Elle est petite, rapide, et nous permet de manipuler directement les attributs XML.

```bash
pip install lxml
```

> **Astuce :** Si vous travaillez dans un environnement virtuel, activez‑le avant d’exécuter la commande. Cela garde les dépendances de votre projet propres.

## Étape 2 : Charger un fichier SVG en Python

Nous allons maintenant **load SVG file Python** à la façon—lire le XML, obtenir l’élément racine `<svg>`, et afficher sa taille actuelle.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Pourquoi c’est important :** `lxml` nous fournit un vrai DOM, nous permettant d’interroger ou de modifier n’importe quel attribut—parfait pour les tâches **edit SVG file Python**.

## Étape 3 : Modifier la largeur (et la hauteur) – Comment redimensionner un SVG

Les SVG sont vectoriels, vous pouvez donc définir la largeur, la hauteur, ou les deux. Si vous ne changez que la largeur, le viewBox conservera le ratio d’aspect, mais de nombreux outils respectent également un attribut de hauteur correspondant. Voici une fonction d’aide qui redimensionne tout en préservant le ratio d’aspect original :

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

La fonction ci‑dessus est le cœur de **how to resize SVG**. Elle lit la taille actuelle, calcule une hauteur proportionnelle, et écrit les nouveaux attributs dans le fichier.

## Étape 4 : Enregistrer le SVG modifié

Après modification, vous devez écrire les changements sur le disque. Cela complète le cycle **edit SVG file Python**.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

Exécutez le script complet et vous verrez un nouveau `logo_resized.svg` qui fait exactement 200 px de large.

## Étape 5 : Redimensionner plusieurs fichiers SVG – Redimensionner un dossier complet

Maintenant que nous pouvons **load SVG file Python**, **edit SVG file Python**, et les enregistrer, parcourons un répertoire et appliquons la même transformation à chaque fichier. C’est la réponse à **batch resize SVG files**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### Ce que cela fait :

1. **Collecte** chaque fichier `.svg` dans le dossier source.
2. **Charge** chaque fichier en utilisant la même routine que pour un SVG unique.
3. **Redimensionne** à la largeur souhaitée tout en conservant le ratio d’aspect.
4. **Écrit** le résultat dans un nouveau dossier, en laissant les originaux intacts.

Vous avez maintenant un pipeline prêt à l’emploi pour **batch resize SVG files**.

## Étape 6 : Cas limites et pièges courants

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Attributs `width`/`height` manquants | Certains SVG ne dépendent que du `viewBox`. | Si les attributs sont absents, revenir aux dimensions du viewBox (`viewBox="0 0 w h"`). |
| Unités autres que `px` (ex. `pt`, `%`) | Le script ne supprime que les `px`. | Étendre l’appel `replace` ou utiliser une expression régulière pour capturer toute unité. |
| Éléments `<symbol>` ou `<use>` complexes | Redimensionner la racine peut ne pas affecter les symboles imbriqués. | Appliquer les mêmes changements d’attributs à chaque balise `<symbol>`, ou utiliser CSS `transform: scale()`. |
| Caractères Unicode ou spéciaux dans les noms de fichiers | `pathlib` gère la plupart des cas, mais Windows peut rencontrer des problèmes avec certains caractères. | S’assurer que les noms de fichiers sont en UTF‑8, ou les renommer avant le traitement. |

Traiter ces points à l’avance vous évite d’avoir des icônes cassées plus tard.

## Étape 7 : Vérifier le résultat

Une vérification rapide peut être effectuée avec un petit extrait HTML :

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

Ouvrez le fichier dans un navigateur—les deux images devraient être identiques, mais la version redimensionnée affichera une largeur de **200 px** dans les outils de développement.

---

## Conclusion

Vous savez maintenant **how to resize SVG** en utilisant du pur Python, d’un fichier unique à un répertoire complet. Le flux de travail couvre **load SVG file Python**, **edit SVG file Python**, et **batch resize SVG files**—tout cela avec seulement quelques fonctions.

Testez‑le : essayez différentes largeurs, expérimentez le redimensionnement uniquement en hauteur, ou ajoutez une interface en ligne de commande avec `argparse`. Les possibilités sont infinies, et le script est suffisamment léger pour être intégré dans des pipelines de build, des jobs CI, ou des utilitaires de bureau.

Des questions sur la gestion des dégradés, des polices intégrées, ou l’intégration dans une application Flask ? Laissez un commentaire, et nous explorerons ces aspects ensemble. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Aspose.HTML के साथ .NET में SVG को इमेज में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}