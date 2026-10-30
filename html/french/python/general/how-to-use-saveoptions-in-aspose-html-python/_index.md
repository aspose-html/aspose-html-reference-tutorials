---
category: general
date: 2026-07-27
description: Comment utiliser SaveOptions dans Aspose.HTML (Python) pour convertir
  une grande page HTML et gérer les ressources efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: fr
lastmod: 2026-07-27
og_description: Comment utiliser SaveOptions dans Aspose.HTML (Python) vous permet
  de convertir une grande page HTML tout en appliquant la gestion des ressources pour
  des résultats propres et rapides.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Comment utiliser SaveOptions dans Aspose.HTML – Guide Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Comment utiliser SaveOptions dans Aspose.HTML (Python)
url: /fr/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser SaveOptions dans Aspose.HTML (Python)

Comment utiliser SaveOptions dans Aspose.HTML pour Python est une question que de nombreux développeurs se posent lorsqu’ils manipulent des fichiers HTML massifs. Si vous devez **convertir une grande page HTML** tout en gardant un contrôle strict sur **l'application de la gestion des ressources**, vous êtes au bon endroit.  

Dans ce tutoriel, nous parcourrons un scénario réel : prendre une page HTML volumineuse, limiter la profondeur à laquelle les ressources imbriquées sont récupérées, puis enregistrer (ou convertir) le résultat avec un contrôle cristallin. Pas de références vagues, seulement un exemple complet et exécutable que vous pouvez copier‑coller dans votre projet dès aujourd’hui.

> **Astuce :** `SaveOptions` d’Aspose.HTML ne sert pas seulement à enregistrer en HTML mais aussi à convertir en PDF, PNG ou même DOCX. Le même modèle que nous présentons ci‑dessous s’applique à tous ces formats.

---

## Ce dont vous avez besoin

- **Python 3.8+** (le code utilise des annotations de type mais fonctionne sur toute version récente)  
- **Aspose.HTML for Python via .NET** – installez avec `pip install aspose-html`  
- Un **fichier HTML volumineux** que vous souhaitez réduire ou transformer (l’exemple utilise `big_page.html`)  
- Une quantité modeste d’espace disque pour le fichier de sortie  

C’est tout — aucune bibliothèque supplémentaire, aucun outil de construction lourd.

---

## Comment utiliser SaveOptions avec les options de gestion des ressources

C’est le cœur du sujet. Nous créerons une instance de `SaveOptions`, y attacherons un objet `ResourceHandlingOptions` qui indique à Aspose.HTML jusqu’à quelle profondeur il doit suivre les ressources liées, puis transmettrons le tout à la méthode `save` du document.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Pourquoi cela fonctionne :**  
- `HTMLDocument` charge le fichier original, en analysant chaque `<img>`, `<link>`, `<script>`, etc.  
- `ResourceHandlingOptions.max_handling_depth` indique au moteur d’arrêter de suivre les ressources après trois niveaux d’imbrication — idéal pour éviter les boucles infinies sur les pages qui intègrent d’autres pages.  
- `SaveOptions` est le conteneur qui transporte à la fois le format de sortie (HTML par défaut) et les règles de gestion des ressources.  
- Enfin, `doc.save` écrit le nouveau fichier, en appliquant les règles que nous venons de définir.

Lorsque vous exécutez le script, vous verrez un nouveau fichier à `big_page_processed.html`. Ouvrez-le dans un navigateur ; vous remarquerez que toutes les images, styles et scripts jusqu’à trois niveaux de profondeur sont toujours présents, tandis que les références plus profondes ont été supprimées. Cela réduit considérablement la taille du fichier sans casser la mise en page principale de la page—exactement ce dont vous avez besoin lorsque vous **convertissez une grande page HTML** pour une utilisation hors ligne ou pour l’envoi par e‑mail.

---

## Convertir efficacement une grande page HTML

Si votre objectif est de *convertir une grande page HTML* en une version plus légère, l’extrait ci‑dessus effectue déjà la majeure partie du travail. Cependant, vous pourriez vouloir changer complètement le format de sortie. Aspose.HTML rend cela possible en une seule ligne :

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Il suffit de remplacer la propriété `format` par `"PNG"`, `"JPEG"` ou `"DOCX"` et vous obtenez une chaîne de conversion complète. Les mêmes règles d’**application de la gestion des ressources** restent intactes, de sorte que le PDF résultant n’incorporera pas chaque fichier CSS externe du site original—seulement ceux qui se trouvent dans la profondeur de trois niveaux que vous avez définie.

---

## Appliquer la gestion des ressources aux ressources imbriquées

Approfondissons un peu l’**application de la gestion des ressources** de manière efficace. Supposons que votre HTML contienne une feuille de style qui importe elle‑même d’autres feuilles de style, chacune récupérant des images. Sans limite de profondeur, Aspose.HTML pourrait suivre la chaîne indéfiniment, gonflant la mémoire et l’utilisation du CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Profondeur 0** – Aucun ressource externe n’est récupérée ; vous obtenez un squelette HTML minimal.  
- **Profondeur 1** – Seules les ressources de premier ordre (balises `<img>` directes, fichiers CSS immédiats) sont incluses.  
- **Profondeur 2+** – Les imbrications plus profondes sont respectées, utile pour les sites complexes où les styles dépendent d’autres styles.

Choisissez la profondeur qui correspond à votre scénario de **conversion d’une grande page HTML**. Pour les newsletters par e‑mail, la profondeur 1 suffit souvent. Pour une archive locale, la profondeur 3 (comme dans l’exemple principal) offre un bon équilibre.

---

## Exemple complet fonctionnel – Du début à la fin

Ci‑dessous se trouve un script autonome que vous pouvez placer dans un fichier nommé `process_html.py`. Il comprend la gestion des erreurs, la journalisation et un petit utilitaire qui affiche la réduction de taille que vous avez obtenue.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Sortie attendue (console) :**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Ouvrez le fichier traité ; vous verrez une page plus légère qui ressemble toujours à l’originale. Si vous avez changé `fmt` en `"PDF"`, la console afficherait la taille du fichier PDF et vous pourriez l’ouvrir avec n’importe quel lecteur PDF.

---

## Questions fréquentes et cas particuliers

- **Et si la page référence des ressources via HTTPS qui nécessitent une authentification ?**  
  Aspose.HTML suit les redirections mais n’envoie pas les informations d’identification automatiquement. Vous pouvez pré‑télécharger ces actifs ou utiliser un gestionnaire `WebRequest` personnalisé (hors du cadre de ce guide).

- **Puis‑je conserver le CSS en ligne tout en supprimant les fichiers externes ?**  
  Oui—définissez `resource_options.max_handling_depth = 0`. Cela ignore les fichiers externes mais laisse intacts les blocs `<style>`.

- **Qu’en est‑il des images très volumineuses qui alourdissent toujours la sortie ?**  
  Après l’enregistrement, vous pouvez exécuter une passe secondaire avec Pillow pour réduire la taille des images, ou laisser les options de compression d’image intégrées d’Aspose.HTML s’en charger (utilisez `save_options.image_quality`).

- **La limite de profondeur s’applique-t-elle par type de ressource ?**  
  La limite est globale pour tous les types de ressources (images, scripts, styles). Si vous avez besoin d’un contrôle granulaire, vous devrez filtrer les ressources manuellement après le chargement du document.

---

## Conclusion

Vous avez maintenant une bonne compréhension de **comment utiliser SaveOptions** dans Aspose.HTML

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir HTML en PDF en Java – Utilisation d’Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Comment convertir HTML en MHTML avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Comment utiliser Aspose pour rendre HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}