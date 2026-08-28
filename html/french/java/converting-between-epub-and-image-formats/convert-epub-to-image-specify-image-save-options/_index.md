---
date: 2026-03-13
description: Apprenez à convertir des fichiers EPUB en images avec Aspose.HTML pour
  Java, à définir une taille de page personnalisée et à changer la couleur de fond
  de l'image pour des résultats optimaux.
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Convertir EPUB en image avec Aspose.HTML pour Java – Définir une taille de
  page personnalisée
url: /fr/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

 "Questions fréquentes". Keep Q/A.

Make sure to keep code placeholders unchanged.

Now produce final content with same structure.

Let's craft translation.

Be careful with apostrophes and French punctuation (space before colon, etc). But not required.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir EPUB en image avec Aspose.HTML for Java – définir une taille de page personnalisée

Dans le monde en constante évolution du développement web, Aspose.HTML for Java se présente comme un outil puissant, et aujourd'hui nous nous concentrerons sur **la façon de définir une taille de page personnalisée** lors de la conversion d'un EPUB en image. Que vous construisiez une bibliothèque numérique, génériez des miniatures ou créiez des captures d'écran haute résolution, maîtriser ce paramètre vous permet de **convertir EPUB en image** avec des fichiers qui correspondent exactement à vos exigences de mise en page.

## Réponses rapides
- **Que signifie « définir une taille de page personnalisée » ?** Cela vous permet de spécifier la largeur et la hauteur de chaque page image générée.  
- **Puis‑je changer la couleur de fond de l'image ?** Oui, vous pouvez spécifier n'importe quelle couleur à l'aide de `ImageSaveOptions`.  
- **Quels formats sont pris en charge ?** JPEG, PNG, GIF, et plus via `ImageFormat`.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour les tests ; une licence commerciale est requise pour la production.  
- **Quelle version de Java est requise ?** Java 1.7 ou supérieure est entièrement prise en charge.

## Qu’est‑ce que « définir une taille de page personnalisée » dans la conversion EPUB → image ?
Définir une taille de page personnalisée signifie que vous contrôlez les dimensions de l'image rendue (par ex. 3000 × 1000 pixels). Cela est utile lorsque vous avez besoin de captures d'écran haute résolution de livres électroniques ou que vous souhaitez que la sortie corresponde à une mise en page précise.

## Pourquoi définir une taille de page personnalisée et changer la couleur de fond de l'image ?
Les tailles de page personnalisées offrent une flexibilité pour différentes cibles d’affichage : écrans mobiles, PDF prêts à imprimer ou miniatures web. Modifier la couleur de fond vous aide à respecter votre identité visuelle ou à améliorer la lisibilité des images contenant des éléments transparents.

## Prérequis

Avant de nous lancer dans la **conversion d’epub en image**, assurez‑vous d’avoir les éléments suivants :

1. **Environnement Java** – Un kit de développement Java installé sur votre machine. Si vous n’avez pas encore Java, vous pouvez le télécharger [ici](https://www.java.com).

2. **Aspose.HTML for Java** – La bibliothèque Aspose.HTML for Java. Téléchargez la dernière version depuis la [page Aspose.HTML for Java](https://releases.aspose.com/html/java/).

## Importer les packages

Pour travailler avec Aspose.HTML for Java, importez les espaces de noms requis :

```java
// Import the required Aspose.HTML for Java packages
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import java.io.FileInputStream;
```

## Guide étape par étape

### Étape 1 : Ouvrir un fichier EPUB existant en lecture

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

Ici nous ouvrons le fichier EPUB source. Remplacez `"input.epub"` par le chemin vers votre fichier e‑book.

### Étape 2 : Initialiser ImageSaveOptions avec des paramètres personnalisés (définir une taille de page personnalisée & changer la couleur de fond)

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(
    Length.fromPixels(3000),
    Length.fromPixels(1000)
);
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

Dans ce bloc nous **définissons une taille de page personnalisée** à 3000 × 1000 pixels et changeons le fond en AliceBlue. N’hésitez pas à ajuster le `size` ou le `Color` selon votre projet (par ex. `Color.getWhite()` pour un fond blanc pur).

### Étape 3 : Convertir EPUB en image

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

Cette ligne effectue la conversion proprement dite. Le fichier de sortie (`"output.jpg"`) contiendra l'image rendue avec les dimensions et le fond que vous avez spécifiés. Vous pouvez également changer l’extension du fichier en `.png` si vous préférez **java convert epub png**. La bibliothèque prend en charge à la fois le **format d’image JPEG** et le **format d’image PNG**, vous offrant ainsi de la flexibilité pour le traitement en aval.

### Étape 4 : Fermer les ressources (géré automatiquement)

L’instruction `try‑with‑resources` ferme automatiquement le `FileInputStream`, garantissant qu’aucune poignée de fichier ne reste ouverte.

## Cas d’utilisation courants

- **Génération de miniatures** pour les bibliothèques d’e‑books.  
- **Création de captures d'écran haute résolution** pour la documentation ou le marketing.  
- **Traitement par lots** de grandes collections d’EPUB en actifs PNG/JPEG pour des galeries web.  
- **Automatisation de l’extraction d’images** pour les outils d’accessibilité qui nécessitent des aperçus visuels des e‑books.

## Conseils et meilleures pratiques

- **Astuce pro :** Utilisez `Length.fromInches()` ou `Length.fromCentimeters()` si vous préférez les unités physiques aux pixels.  
- **Astuce performance :** Pour les gros EPUB, envisagez d’augmenter la taille du tas JVM (`-Xmx2g`) afin d’éviter les problèmes de mémoire.  
- **Gestion des erreurs :** Enveloppez l’appel de conversion dans un bloc `try‑catch` pour capturer `IOException` ou `AsposeException`.  
- **Contrôle de la qualité :** Ajustez `options.setQuality(90)` pour affiner la compression JPEG sans perte perceptible.

## Problèmes courants et solutions

- **Erreurs de mémoire insuffisante :** Augmentez la taille du tas ou traitez l’EPUB par petits morceaux en rendant les pages individuellement.  
- **Fond blanc apparaissant noir :** Assurez‑vous d’avoir défini une couleur de fond ; les fonds transparents peuvent apparaître noirs dans certains visionneurs.  
- **Dimensions d’image inattendues :** Vérifiez que l’objet `Size` reflète exactement les valeurs en pixels souhaitées ; rappelez‑vous que les réglages DPI n’affectent pas la taille en pixels.  
- **Fonctionnalités EPUB non prises en charge :** Aspose.HTML gère pleinement EPUB3, mais les polices personnalisées peuvent devoir être intégrées ou référencées correctement.

## Questions fréquentes

**Q : Puis‑je convertir des fichiers EPUB vers d’autres formats d’image ?**  
R : Oui, vous pouvez spécifier des formats tels que PNG ou GIF en changeant `ImageFormat.Jpeg` en `ImageFormat.Png` ou `ImageFormat.Gif`.

**Q : Aspose.HTML for Java prend‑il en charge EPUB3 ?**  
R : Absolument. La bibliothèque supporte entièrement EPUB3, vous permettant de travailler avec les dernières normes d’e‑books.

**Q : Comment gérer les erreurs pendant le processus de conversion ?**  
R : Implémentez des blocs `try‑catch` autour du code de conversion pour capturer et consigner les exceptions, assurant ainsi la robustesse de votre application.

**Q : Puis‑je personnaliser la taille et la qualité de l’image ?**  
R : Oui, modifiez l’objet `Size` pour les dimensions et utilisez `options.setQuality(int)` pour contrôler la qualité de compression JPEG.

**Q : Aspose.HTML for Java est‑il compatible avec toutes les versions de Java ?**  
R : La bibliothèque fonctionne avec Java 1.7 et supérieures, couvrant un large éventail d’environnements de développement.

## Conclusion

En suivant ce guide, vous savez maintenant comment **convertir EPUB en image** tout en **définissant une taille de page personnalisée** et **en changeant la couleur de fond de l’image** avec Aspose.HTML for Java. Ces capacités vous permettent de produire des images parfaitement dimensionnées et brandées pour n’importe quel flux de travail en aval — qu’il s’agisse d’une galerie de miniatures, d’une brochure marketing ou d’un service automatisé d’aperçu d’e‑books. N’hésitez pas à expérimenter avec différentes dimensions, couleurs et formats de sortie pour répondre à vos besoins spécifiques.

---

**Dernière mise à jour** : 2026-03-13  
**Testé avec** : Aspose.HTML for Java 24.10  
**Auteur** : Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}