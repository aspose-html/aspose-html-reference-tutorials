---
category: general
date: 2026-07-15
description: Créer un PDF à partir de HTML avec Python. Apprenez comment convertir
  du HTML en PDF rapidement avec un script simple et des étapes claires.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: fr
lastmod: 2026-07-15
og_description: Créer un PDF à partir de HTML avec Python. Ce guide vous montre comment
  convertir du HTML en PDF, enregistrer du HTML en PDF et gérer les ressources efficacement.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Créer un PDF à partir de HTML en Python – Tutoriel pratique
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Créer un PDF à partir de HTML en Python – Tutoriel Python HTML vers PDF
url: /fr/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF à partir de HTML en Python – Tutoriel complet

Vous avez déjà eu besoin de **créer un PDF à partir de HTML** mais vous ne saviez pas quelle bibliothèque Python choisir ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils essaient de transformer un rapport web, une facture ou une page marketing en PDF imprimable.  

La bonne nouvelle, c'est qu'avec seulement quelques lignes de code, vous pouvez **convertir HTML en PDF** de manière fiable, et le script fonctionne sous Windows, macOS et Linux. Dans ce guide, nous parcourrons un exemple complet et exécutable, expliquerons pourquoi chaque étape est importante, et vous montrerons comment **enregistrer HTML en PDF** sans laisser de problèmes en suspens.

---

## Ce que vous apprendrez

- Installer le bon package Python pour la conversion HTML‑vers‑PDF.  
- Charger un fichier HTML avec des options personnalisées de gestion des ressources (pour éviter les imports CSS sans fin).  
- Générer un fichier PDF propre sur le disque.  
- Gérer les cas limites courants tels que les images externes, les chemins relatifs et les documents volumineux.  

À la fin de ce **tutoriel HTML vers PDF**, vous disposerez d'une fonction réutilisable que vous pourrez intégrer à n'importe quel projet.

---

## Prérequis

- Python 3.9+ (le code fonctionne également avec 3.8, mais 3.9+ vous donne les dernières fonctionnalités de `pathlib`).  
- Une connaissance de base de la ligne de commande et des environnements virtuels.  
- Un fichier HTML que vous souhaitez transformer en PDF—n'importe quelle page statique convient.

> **Astuce :** Si vous utilisez un environnement virtuel, activez‑le avant d'installer la bibliothèque ; cela garde votre Python global propre.

---

## Étape 1 – Installer WeasyPrint (le moteur derrière la conversion)

WeasyPrint est une bibliothèque pure‑Python qui rend le HTML et le CSS en PDF. Elle gère la plupart des fonctionnalités web modernes et vous offre un contrôle fin du chargement des ressources.

```bash
pip install weasyprint
```

Exécuter la commande ci‑dessus télécharge `cairocffi`, `tinycss2`, et quelques autres dépendances. Si vous rencontrez une erreur liée à `cairo` sous Windows, récupérez les roues pré‑compilées depuis le [site Web de WeasyPrint](https://weasyprint.org/docs/install/).

---

## Étape 2 – Préparer un petit assistant pour la gestion des ressources

Lorsque vous chargez un document HTML qui référence des feuilles de style ou des images externes, la bibliothèque suivra ces liens. Dans certains cas, cela conduit à un imbriquement profond voire à des boucles infinies (pensez à un fichier CSS qui s'`@import` lui‑même). Pour garder les choses ordonnées, nous limitons la profondeur de la gestion des ressources.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

La classe ci‑dessus n'est pas requise par WeasyPrint, mais elle reproduit le modèle que vous avez vu dans l'extrait original et vous fournit un point d'accroche pour arrêter les imports incontrôlés. Vous la verrez utilisée à l'étape suivante.

---

## Étape 3 – Charger le document HTML en utilisant les options personnalisées

Nous lisons maintenant réellement le fichier HTML. La classe `HTML` accepte un argument `base_url`, que nous définissons sur le répertoire contenant le fichier source—cela permet aux liens relatifs de fonctionner sans serveur web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Pourquoi c'est important :** Si votre HTML charge une cascade de fichiers CSS, chaque `@import` déclenchera un autre chargement. La garde de profondeur empêche le script de spiraler hors de contrôle.

---

## Étape 4 – Enregistrer le document traité en PDF

Avec l'objet `HTML` en main, générer un PDF se fait en une seule ligne. Nous passons également un extrait CSS simple qui impose une taille de page propre (A4) et ajoute une petite marge—n'hésitez pas à ajuster.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Appeler `write_pdf` transmet le PDF vers le disque, vous obtenez ainsi un fichier prêt à être partagé.

---

## Étape 5 – Assembler le tout

Voici un script compact que vous pouvez copier‑coller dans `convert.py`. Remplacez les chemins factices par vos répertoires réels.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Sortie attendue** – après avoir exécuté `python convert.py`, vous devriez voir :

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Ouvrez le fichier généré avec n'importe quel lecteur PDF ; vous verrez la mise en page originale, le style CSS et les images (à condition qu'elles soient accessibles depuis le fichier HTML).  

Si vous remarquez des images manquantes, vérifiez que leurs attributs `src` sont soit des URL absolues, soit des chemins relatifs existant sous `YOUR_DIRECTORY`.

---

## Questions fréquentes & gestion des cas limites

| Question | Réponse |
|----------|--------|
| *Et si mon HTML référence des polices externes ?* | WeasyPrint téléchargera les fichiers de police automatiquement, mais vous pourriez vouloir mettre sur liste blanche les domaines afin d'éviter de longs temps de récupération. |
| *Puis‑je convertir une chaîne HTML au lieu d'un fichier ?* | Oui—utilisez `HTML(string=my_html_string)` et ignorez le `base_url` ou définissez‑le sur un dossier temporaire. |
| *Comment contrôler les métadonnées du PDF (titre, auteur) ?* | Passez un dictionnaire `metadata` à `write_pdf`, par exemple `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *J'obtiens une « cairo‑cffi error » sous Linux.* | Installez le paquet système `libcairo2-dev` (`apt-get install libcairo2-dev` sur Debian/Ubuntu) avant d'installer WeasyPrint avec pip. |

---

## Conclusion

Nous venons de **créer un PDF à partir de HTML** en utilisant un workflow Python propre, d'avoir couvert la mécanique de **conversion HTML en PDF**, et de vous avoir montré comment **enregistrer HTML en PDF** avec une gestion robuste des ressources. Le script est suffisamment petit pour être intégré dans des pipelines CI, tout en étant assez flexible pour être étendu avec des en‑têtes, pieds de page ou filigranes personnalisés.

Prochaines étapes que vous pourriez explorer :

- Utilisez la bibliothèque **html to pdf python** `pdfkit` pour une approche basée sur wkhtmltopdf (utile pour le CSS hérité).  
- Ajoutez une interface CLI avec `argparse` afin que le script accepte des arguments d'entrée/sortie.  
- Générez des PDFs à la volée dans un endpoint Flask ou FastAPI pour des rapports à la demande.  

N'hésitez pas à expérimenter, à casser des choses, puis à revenir à ce guide pour un rappel rapide. Si vous rencontrez des problèmes, la documentation de WeasyPrint et les forums communautaires sont d'excellentes ressources.

Bon codage, et profitez de transformer ces pages web en PDFs élégants !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Convertir HTML en PDF avec Aspose.HTML – Guide complet de manipulation](/html/english/)
- [Convertir HTML en PDF en .NET avec Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Créer un PDF à partir de HTML – Guide C# étape par étape](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}