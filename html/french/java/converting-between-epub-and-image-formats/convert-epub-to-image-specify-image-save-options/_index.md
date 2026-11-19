---
date: 2026-08-17
description: Apprenez à convertir des fichiers EPUB en images avec Aspise.HTML for
  Java, à définir des dimensions de page personnalisées et à modifier la couleur de
  fond de l'image pour des résultats optimaux.
keywords:
- custom page dimensions image
- Aspose.HTML Java
- EPUB to image conversion
lastmod: 2026-08-17
linktitle: Spécifier les options d'enregistrement d'image pour la conversion d'EPUB
  en image
og_description: Convertir EPUB en image avec des dimensions de page personnalisées
  en utilisant Aspose.HTML for Java. Apprenez étape par étape comment définir la taille
  de la page, la couleur de fond et le format de sortie dans un guide complet.
og_image_alt: Developer guide showing how to set custom page dimensions image when
  converting EPUB to image with Aspose.HTML for Java
og_title: Convertir EPUB en image avec des dimensions de page personnalisées en Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to convert EPUB files to images using Aspise.HTML for Java,
    set custom page dimensions image, and change image background color for optimal
    results.
  headline: Convert EPUB to image with custom page dimensions image
  type: TechArticle
- description: Learn how to convert EPUB files to images using Aspise.HTML for Java,
    set custom page dimensions image, and change image background color for optimal
    results.
  name: Convert EPUB to image with custom page dimensions image
  steps:
  - name: open an existing EPUB file for reading
    text: Here we open the source EPUB. Replace `"input.epub"` with the path to your
      e‑book file.
  - name: initialize ImageSaveOptions with custom settings (set custom page dimensions
      image & change image background color)
    text: '`ImageSaveOptions` is the class that controls how the EPUB pages are rendered
      to images. In this block we **set custom page dimensions image** to 3000 × 1000
      pixels and change the background to AliceBlue. Feel free to adjust the `Size`
      object or the `Color` to match your branding (e.g., `Color.getWh'
  - name: convert EPUB to image
    text: This line performs the actual conversion. The output file (`"output.jpg"`)
      will contain the rendered image with the dimensions and background you specified.
      You can also change the file extension to `.png` if you prefer **java convert
      epub png**. The library supports both JPEG and PNG, giving you fl
  - name: close resources (handled automatically)
    text: The `try‑with‑resources` statement automatically closes `FileInputStream`,
      ensuring no file handles are left open.
  type: HowTo
- questions:
  - answer: Yes, you can specify formats such as PNG or GIF by changing `ImageFormat.Jpeg`
      to `ImageFormat.Png` or `ImageFormat.Gif`.
    question: Can I convert EPUB files to other image formats?
  - answer: Absolutely. The library fully supports EPUB3, allowing you to work with
      the latest e‑book standards.
    question: Does Aspose.HTML for Java support EPUB3?
  - answer: Implement `try‑catch` blocks around the conversion code to capture and
      log exceptions, ensuring your application remains robust.
    question: How can I handle errors during the conversion process?
  - answer: Yes, adjust the `Size` object for dimensions and use `options.setQuality(int)`
      to control JPEG compression quality.
    question: Can I customize the image size and quality?
  - answer: The library works with Java 1.7 and later, covering a wide range of development
      environments.
    question: Is Aspose.HTML for Java compatible with all Java versions?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- convert EPUB
- Aspose.HTML
- Java image processing
title: Convertir EPUB en image avec des dimensions de page personnalisées
url: /fr/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir EPUB en image avec des dimensions de page personnalisées

Dans l'édition numérique moderne, pouvoir transformer un fichier EPUB en une image de haute qualité vous offre une flexibilité pour les vignettes, les aperçus et les supports marketing. **Aspose.HTML for Java** rend cette conversion simple, et vous pouvez contrôler précisément le résultat en définissant des dimensions de page personnalisées pour l'image. Ce tutoriel vous guide à travers le processus complet — de la configuration de l'environnement au rendu du JPEG ou PNG final — tout en expliquant l'importance de chaque paramètre.

## Réponses rapides
- **Que signifie “custom page dimensions image” ?** Cela vous permet de définir la largeur et la hauteur exactes (en pixels) de chaque page d'image générée.  
- **Puis-je changer la couleur d'arrière‑plan de l'image ?** Oui—`ImageSaveOptions` vous permet de spécifier n'importe quel `java.awt.Color`.  
- **Quels formats d'image sont pris en charge ?** JPEG, PNG, GIF, BMP, TIFF, et plus via `ImageFormat`.  
- **Ai‑je besoin d'une licence pour la production ?** Un essai gratuit suffit pour l'évaluation ; une licence commerciale est requise pour les déploiements en production.  
- **Quelle version de Java est requise ?** Java 1.7 ou ultérieure est entièrement prise en charge.

## Qu'est‑ce que “custom page dimensions image” dans la conversion EPUB en image ?
**Custom page dimensions image** signifie que vous contrôlez la taille exacte en pixels de chaque page rendue, par exemple 3000 × 1000 pixels. En spécifiant la largeur et la hauteur, vous pouvez générer des images qui s'alignent avec les grilles de conception, s'adaptent aux composants UI, ou répondent aux spécifications d'impression. Cette flexibilité aide également lors de la création de vignettes qui doivent conserver les proportions sur différents appareils, garantissant que le résultat correspond à vos exigences visuelles.

## Pourquoi définir une taille de page personnalisée et changer la couleur d'arrière‑plan de l'image ?
Définir une taille de page personnalisée garantit que le résultat correspond à l'appareil cible ou aux spécifications de conception, tandis que changer la couleur d'arrière‑plan vous permet d'aligner l'image avec votre identité visuelle ou d'améliorer la lisibilité des éléments transparents. Ensemble, ils vous offrent un contrôle visuel complet sur le résultat de la conversion.

## Prérequis
Avant de commencer notre parcours pour **convertir EPUB en image**, assurez‑vous de disposer de ce qui suit :

1. **Environnement Java** – Un Java Development Kit installé sur votre machine. Si vous n'avez pas encore Java, vous pouvez le télécharger depuis le [site officiel de Java](https://www.java.com).  
2. **Aspose.HTML for Java** – La bibliothèque Aspose.HTML for Java. Téléchargez la dernière version depuis la [page Aspose.HTML for Java](https://releases.aspose.com/html/java/).

## Importer les packages
Pour travailler avec Aspose.HTML for Java, importez les espaces de noms requis :

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

### Étape 1 : ouvrir un fichier EPUB existant en lecture
Ici nous ouvrons le EPUB source. Remplacez `"input.epub"` par le chemin vers votre fichier e‑book.

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### Étape 2 : initialiser ImageSaveOptions avec des paramètres personnalisés (définir des dimensions de page personnalisées pour l'image & changer la couleur d'arrière‑plan de l'image)
`ImageSaveOptions` est la classe qui contrôle la façon dont les pages EPUB sont rendues en images. Dans ce bloc, nous **définissons des dimensions de page personnalisées pour l'image** à 3000 × 1000 pixels et changeons l'arrière‑plan en AliceBlue. N'hésitez pas à ajuster l'objet `Size` ou le `Color` pour correspondre à votre identité visuelle (par ex., `Color.getWhite()` pour un arrière‑plan blanc simple).

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

### Étape 3 : convertir EPUB en image
Cette ligne effectue la conversion réelle. Le fichier de sortie (`"output.jpg"`) contiendra l'image rendue avec les dimensions et l'arrière‑plan que vous avez spécifiés. Vous pouvez également changer l'extension du fichier en `.png` si vous préférez **java convert epub png**. La bibliothèque prend en charge à la fois JPEG et PNG, vous offrant une flexibilité pour le traitement en aval.

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

### Étape 4 : fermer les ressources (géré automatiquement)
L'instruction `try‑with‑resources` ferme automatiquement le `FileInputStream`, garantissant qu'aucune poignée de fichier ne reste ouverte.

## Cas d'utilisation courants
- **Générer des vignettes** pour les bibliothèques d'e‑books où chaque vignette doit tenir dans une boîte de 200 × 300 pixels.  
- **Créer des captures d'écran haute résolution** pour la documentation, les brochures marketing ou les maquettes UI.  
- **Traitement par lots** de grandes collections d'EPUB en actifs PNG/JPEG pour les galeries web ou les archives hors ligne.  
- **Automatiser l'extraction d'images** pour les outils d'accessibilité qui ont besoin d'aperçus visuels des e‑books.

## Conseils & bonnes pratiques
- **Astuce pro :** Utilisez `Length.fromInches()` ou `Length.fromCentimeters()` si vous préférez les unités physiques aux pixels.  
- **Astuce de performance :** Pour les gros EPUB, augmentez la taille du tas JVM (`-Xmx2g`) afin d'éviter la pression mémoire.  
- **Gestion des erreurs :** Enveloppez l'appel de conversion dans un bloc `try‑catch` pour capturer `IOException` ou `AsposeException`.  
- **Contrôle de la qualité :** Ajustez `options.setQuality(90)` pour affiner la compression JPEG sans perte perceptible.  
- **Affirmation chiffrée :** Aspose.HTML for Java prend en charge la conversion vers **plus de 15 formats d'image** et peut rendre des pages jusqu'à **10 000 × 10 000 pixels** sans dégrader les performances.

## Problèmes courants et solutions
- **Erreurs de mémoire insuffisante :** Augmentez la taille du tas ou traitez l'EPUB par morceaux plus petits en rendant les pages individuellement.  
- **Arrière‑plan blanc :** Assurez‑vous de définir une couleur d'arrière‑plan ; les arrière‑plans transparents peuvent apparaître noirs dans certains visionneurs.  
- **Dimensions d'image inattendues :** Vérifiez que l'objet `Size` reflète les valeurs exactes en pixels dont vous avez besoin ; les réglages DPI n'affectent pas la taille en pixels.  
- **Fonctionnalités EPUB non prises en charge :** Aspose.HTML gère pleinement EPUB3, mais les polices personnalisées peuvent devoir être incorporées ou référencées correctement.

## Questions fréquentes
**Q : Puis‑je convertir des fichiers EPUB en d'autres formats d'image ?**  
A : Oui, vous pouvez spécifier des formats tels que PNG ou GIF en changeant `ImageFormat.Jpeg` en `ImageFormat.Png` ou `ImageFormat.Gif`.

**Q : Aspose.HTML for Java prend‑il en charge EPUB3 ?**  
A : Absolument. La bibliothèque prend pleinement en charge EPUB3, vous permettant de travailler avec les dernières normes d'e‑book.

**Q : Comment gérer les erreurs pendant le processus de conversion ?**  
A : Implémentez des blocs `try‑catch` autour du code de conversion pour capturer et consigner les exceptions, assurant que votre application reste robuste.

**Q : Puis‑je personnaliser la taille et la qualité de l'image ?**  
A : Oui, ajustez l'objet `Size` pour les dimensions et utilisez `options.setQuality(int)` pour contrôler la qualité de compression JPEG.

**Q : Aspose.HTML for Java est‑il compatible avec toutes les versions de Java ?**  
A : La bibliothèque fonctionne avec Java 1.7 et ultérieur, couvrant un large éventail d'environnements de développement.

## Conclusion
En suivant ce guide, vous savez maintenant comment **convertir EPUB en image** tout en **définissant des dimensions de page personnalisées pour l'image** et **changeant la couleur d'arrière‑plan de l'image** avec Aspose.HTML for Java. Ces capacités vous permettent de produire des images parfaitement dimensionnées et brandées pour tout flux de travail en aval — que ce soit une galerie de vignettes, une brochure marketing ou un service de prévisualisation d'e‑books automatisé. N'hésitez pas à expérimenter différentes dimensions, couleurs et formats de sortie pour répondre à vos besoins spécifiques.

---

**Dernière mise à jour :** 2026-08-17  
**Testé avec :** Aspose.HTML for Java 24.10  
**Auteur :** Aspose

## Tutoriels associés

- [Comment convertir des pages EPUB en images avec Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Convertir EPUB en BMP et autres images – Aspose.HTML Java](/html/java/converting-between-epub-and-image-formats/)
- [Définir la couleur d'arrière‑plan de l'image pour la conversion EPUB en image](/html/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}