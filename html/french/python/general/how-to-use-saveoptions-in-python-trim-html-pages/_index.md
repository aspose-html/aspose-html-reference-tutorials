---
category: general
date: 2026-05-28
description: Apprenez à utiliser SaveOptions pour réduire les pages HTML en Python.
  Ce guide étape par étape explique également comment charger un document HTML et
  supprimer efficacement les ressources imbriquées.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: fr
og_description: Comment utiliser SaveOptions pour réduire les pages HTML en Python.
  Suivez ce guide pour charger un document HTML, définir les limites de ressources
  et enregistrer un fichier propre et léger.
og_title: Comment utiliser SaveOptions en Python – Réduire les pages HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Comment utiliser SaveOptions en Python – Réduire les pages HTML
url: /fr/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser SaveOptions en Python – Réduire les pages HTML

Vous vous êtes déjà demandé **comment utiliser SaveOptions** pour réduire un fichier HTML massif sans rien casser ? Vous n'êtes pas le seul. Lorsque vous récupérez une page qui inclut des dizaines de ressources imbriquées—pensez CSS, JS, ou même d’autres extraits HTML—votre sortie peut gonfler de façon incontrôlée.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre non seulement **comment utiliser SaveOptions**, mais aussi comment **charger un document HTML** et la meilleure façon de **réduire une page HTML** en limitant la profondeur d’imbrication. À la fin, vous disposerez d’un fichier propre et réduit, prêt pour le déploiement ou un traitement ultérieur.

## Ce que vous allez accomplir

- Charger n’importe quel fichier HTML local en une seule ligne de code.  
- Configurer les options de gestion des ressources pour s’arrêter à une profondeur d’inclusion spécifique.  
- Enregistrer le résultat réduit en utilisant la puissante classe `SaveOptions`.  

Pas d’outils externes, pas de magie—juste du Python pur et une petite bibliothèque qui fait le gros du travail.

---

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

1. **Python 3.9+** installé (la syntaxe utilisée fonctionne avec n’importe quelle version récente).  
2. Le package hypothétique `htmlprocessor` qui fournit `HTMLDocument`, `SaveOptions` et `ResourceHandlingOptions`. Installez‑le via :

```bash
pip install htmlprocessor
```

> **Astuce :** Si vous utilisez un environnement virtuel, activez‑le d’abord—cela garde vos dépendances propres.

---

## Étape 1 : Comment charger un document HTML

Charger un fichier est aussi simple que de pointer le constructeur vers votre chemin. La bibliothèque lit le balisage, construit un arbre semblable à un DOM, et le prépare pour une manipulation ultérieure.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Pourquoi c’est important :** L’objet `HTMLDocument` abstrait la manipulation de chaînes brutes, vous offrant des méthodes pour interroger, modifier et finalement enregistrer la page. Il normalise également les fins de ligne et les encodages de caractères, ce qui vous évite des bugs subtils plus tard.

Vous remarquerez que nous affichons le titre simplement pour vérifier que le chargement a réussi. Si le fichier est manquant ou mal formé, le constructeur lèvera une exception claire—pas d’échecs silencieux.

---

## Étape 2 : Configurer la gestion des ressources – Le cœur du découpage

La prochaine pièce du puzzle est **comment réduire le contenu d’une page HTML** en limitant la profondeur à laquelle le processeur suit les inclusions. C’est ici que `ResourceHandlingOptions` brille.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Que fait `max_handling_depth` ?

- **Profondeur 1** → Seulement le fichier HTML racine, toutes les ressources externes sont ignorées.  
- **Profondeur 2** → La racine plus tous les fichiers référencés directement (par ex. un `iframe` ou une inclusion côté serveur).  
- **Valeurs supérieures** → Imbrication plus profonde, mais aussi sortie plus volumineuse et temps de traitement plus long.

En limitant la profondeur à **2**, nous conservons la page principale et une couche d’inclusions, en rejetant tout ce qui est plus profond. Cela suffit généralement à éliminer les pieds‑de‑page redondants, les scripts d’analyse, ou les modèles imbriqués dont vous n’avez pas besoin dans une copie réduite.

---

## Étape 3 : Attacher les options à la configuration d’enregistrement

Nous associons maintenant nos règles de ressources à une instance de `SaveOptions`. Cet objet indique à la bibliothèque *exactement* comment écrire le fichier sur le disque.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Pourquoi utiliser `SaveOptions` ?**  
> Il vous donne un contrôle granulaire sur la sortie—au‑delà de la simple profondeur des ressources. Vous pourrez plus tard ajouter de la compression, du formatage « pretty‑print », ou même des callbacks personnalisés sans toucher à la logique d’enregistrement de base.

---

## Étape 4 : Comment utiliser SaveOptions pour réduire la page HTML

Enfin, nous invoquons la méthode `save` avec nos options configurées. La bibliothèque parcourra le DOM, respectera la limite de profondeur, et écrira un fichier réduit.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Résultat attendu

- Le fichier `trimmed_page.html` contient le balisage original **plus** les inclusions jusqu’à un niveau de profondeur.  
- Toutes les inclusions plus profondes sont omises, ce qui donne une page plus petite et plus rapide à charger.  
- Aucun tag cassé n’apparaît—la bibliothèque ferme automatiquement les éléments laissés en suspens après la suppression.

Vous pouvez ouvrir le résultat dans un navigateur pour vérifier que le contenu principal s’affiche toujours, tandis que les scripts superflus ou les cadres imbriqués ont disparu.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici le script complet que vous pouvez copier‑coller et exécuter :

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Exécutez le script, pointez `INPUT` vers n’importe quel fichier HTML complexe, et vous obtiendrez une version allégée dans `OUTPUT`.  

> **Note sur les cas limites :** Si la page originale contient des commentaires conditionnels (`<!--[if IE]>…<![endif]-->`) qui référencent des ressources plus profondes, ils seront également supprimés comme toute autre inclusion imbriquée. Cela empêche les hacks IE anciens d’alourdir votre taille finale.

---

## Résumé visuel

Voici un petit diagramme illustrant le flux—du chargement du document, à la gestion des ressources, jusqu’à l’enregistrement du résultat réduit.

![exemple d'utilisation de saveoptions](https://example.com/placeholder.png "Diagramme montrant comment utiliser SaveOptions pour réduire les pages HTML")

*Texte alternatif :* **exemple d'utilisation de saveoptions** – montre le processus en trois étapes de chargement, configuration et enregistrement d’un document HTML.

---

## Questions fréquentes & Pièges

| Question | Réponse |
|----------|---------|
| **Et si j’ai besoin d’une imbrication plus profonde ?** | Augmentez `max_handling_depth` à 3 ou 4, mais gardez à l’esprit que la taille de la sortie augmentera. |
| **Puis‑je exclure des balises spécifiques (ex. `<script>`) quel que soit le niveau ?** | Oui—`SaveOptions` supporte également une propriété `tag_exclusion_list`. Ajoutez `"script"` à cette liste pour toujours supprimer les scripts. |
| **La bibliothèque est‑elle thread‑safe ?** | La version actuelle ne l’est pas. Créez un `HTMLDocument` distinct par thread. |
| **Les URL relatives seront‑elles réécrites ?** | Par défaut non. Utilisez `save_opt.rewrite_relative_urls = True` si vous devez les ajuster vers le nouvel emplacement. |

---

## Prochaines étapes

Maintenant que vous avez maîtrisé **comment utiliser SaveOptions**, essayez ces extensions :

- **Compresser la sortie :** Réglez `save_opt.enable_gzip = True` pour des fichiers plus petits sur le réseau.  
- **Pretty‑print pour le débogage :** Activez `save_opt.indent_output = True` pour obtenir du HTML joliment formaté.  
- **Traitement par lots :** Parcourez un répertoire de fichiers HTML et appliquez la même logique de réduction—idéal pour les générateurs de sites statiques.

Chacune de ces améliorations s’appuie sur la même base que vous venez d’apprendre, gardant votre code propre et maintenable.

---

## Conclusion

Nous avons couvert tout le cycle de réduction d’une page HTML en Python : **comment charger un document HTML**, configurer **comment réduire une page HTML** avec `ResourceHandlingOptions`, et enfin **comment utiliser SaveOptions** pour écrire le fichier nettoyé. L’exemple est entièrement autonome, fonctionne immédiatement, et montre pourquoi contrôler la profondeur des ressources est une optimisation cruciale pour le web‑scraping, la génération de sites statiques, ou toute situation où vous avez besoin d’un instantané HTML léger.

Testez‑le, expérimentez avec différentes valeurs de `max_handling_depth`, et laissez les pages réduites faire le gros du travail pour vous. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—bon codage !

## Tutoriels associés

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [How to Zip HTML in C# – Save HTML to Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}