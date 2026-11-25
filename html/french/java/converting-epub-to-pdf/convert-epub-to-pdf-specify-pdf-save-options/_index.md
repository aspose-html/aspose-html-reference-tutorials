---
date: 2026-05-30
description: Apprenez comment convertir EPUB en PDF en Java avec Aspose.HTML tout
  en définissant une taille de page PDF personnalisée et d'autres options d'enregistrement
  PDF.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Spécification des options d'enregistrement PDF pour EPUB vers PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Taille de page PDF personnalisée - Spécification des options d'enregistrement
  PDF pour EPUB vers PDF
url: /fr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Taille de page PDF personnalisée : spécification des options d’enregistrement PDF pour EPUB vers PDF

## Introduction

Aspose.HTML for Java facilite la **conversion d’EPUB en PDF** et vous donne un contrôle total sur la sortie, y compris la définition d’une **taille de page PDF personnalisée**. Dans ce guide étape par étape, nous passerons en revue tout ce dont vous avez besoin — de la préparation de votre environnement à l’ajustement de `PdfSaveOptions` afin que le PDF généré corresponde exactement aux dimensions de page que vous exigez. Que vous construisiez une chaîne de publication, une plateforme d’apprentissage en ligne, ou que vous ayez simplement besoin d’automatiser la conversion de documents, vous trouverez les techniques présentées ici précieuses.

## Réponses rapides
- **Quel est le but principal de ce tutoriel ?** Convertir un fichier EPUB en PDF tout en appliquant une taille de page PDF personnalisée.  
- **Quelle bibliothèque est utilisée ?** Aspose.HTML for Java.  
- **Ai-je besoin d’une licence ?** Une version d’essai gratuite est disponible ; une licence commerciale est requise pour la production.  
- **Puis-je changer la couleur d’arrière‑plan ?** Oui, en utilisant `PdfSaveOptions`.  
- **Java 8+ est‑il pris en charge ?** Absolument — tout runtime Java moderne fonctionne.

## Qu’est‑ce qu’une taille de page PDF personnalisée ?

Une taille de page PDF personnalisée vous permet de définir la largeur et la hauteur exactes de chaque page du PDF de sortie, au lieu de vous fier à des tailles standard comme A4 ou Letter. Vous pouvez définir les dimensions en points (1 point = 1/72 pouce) ou les convertir depuis des pixels, vous offrant ainsi un contrôle pixel‑parfait sur la mise en page finale. Cela est idéal pour les e‑books, les flyers ou tout design qui doit correspondre à un format prédéfini sans post‑traitement manuel.

## Pourquoi utiliser Aspose.HTML pour la conversion d’EPUB en PDF ?

Aspose.HTML convertit les EPUB en PDF en deux lignes de code tout en préservant les mises en page complexes, les polices intégrées et les images haute résolution. Il prend en charge **plus de 50 formats d’entrée et de sortie**, peut rendre des PDF jusqu’à **2 000 pages** sans charger le fichier complet en mémoire, et fonctionne sous Windows, Linux et macOS avec des résultats identiques. La bibliothèque offre également des options de sauvegarde PDF granulaire, vous permettant d’ajuster la taille de page, la couleur d’arrière‑plan, les marges et les paramètres de compression — le tout depuis Java.

## Prérequis
- **Environnement de développement Java :** JDK 8 ou version ultérieure installé et configuré.  
- **Aspose.HTML for Java :** Téléchargez le JAR le plus récent depuis le [site web](https://releases.aspose.com/html/java/).  
- **Fichier EPUB :** Un document `.epub` que vous souhaitez convertir.  

Maintenant que tout est prêt, plongeons dans les étapes réelles de conversion.

## Comment convertir un EPUB en PDF avec une taille de page personnalisée ?

`FileInputStream` est une classe Java qui lit les octets bruts d’un fichier.  
`PdfSaveOptions` est une classe d’Aspose.HTML qui configure les paramètres de sortie PDF tels que la taille de page et la couleur d’arrière‑plan. Chargez votre EPUB avec un `FileInputStream`, configurez `PdfSaveOptions` pour spécifier les dimensions exactes de la page, puis appelez le convertisseur. Le flux de travail en trois étapes suivant effectue la conversion en moins d’une minute pour des tailles d’e‑book typiques, et il s’adapte aux collections plus importantes avec peu de modifications de code.

### Étape 1 : Ouvrir le fichier EPUB

Tout d’abord, créez un `FileInputStream` qui pointe vers votre source `.epub`. Garder le flux ouvert jusqu’à la fin de la conversion évite les erreurs de « page blanche ».

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Étape 2 : Définir les options d’enregistrement PDF

`PdfSaveOptions` est la classe de configuration d’Aspose.HTML qui contrôle les paramètres de sortie PDF tels que la taille de page, la couleur d’arrière‑plan et les marges.  
`Length.fromPixels` convertit les pixels d’écran en points PDF (1 point = 1/72 pouce), vous permettant de spécifier les dimensions dans des unités de pixel familières.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Astuce :
- **Pixels vs. Points :** `Length.fromPixels` convertit les pixels d’écran en points PDF (1 point = 1/72 pouce). Choisissez des valeurs qui reflètent la taille imprimée finale dont vous avez besoin.

### Étape 3 : Convertir l’EPUB en PDF

Avec le flux d’entrée et les options personnalisées prêts, invoquez le convertisseur. Le PDF de sortie sera enregistré à l’emplacement que vous spécifiez, en conservant les dimensions exactes de page que vous avez définies.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` est une méthode qui active le traitement parallèle des pages lors de la conversion PDF.

## Code source complet

L’exemple complet et exécutable combine les trois étapes ci‑dessus dans une seule classe Java. Remplacez les chemins factices par vos propres emplacements de fichiers.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Les pages PDF sont blanches** | Flux d’entrée fermé avant la conversion | Gardez le bloc `try‑with‑resources` ouvert jusqu’après `convertEPUB`. |
| **Dimensions de page incorrectes** | Utilisation de pixels qui ne correspondent pas à la taille d’impression souhaitée | Convertissez les pouces souhaités en points (`1 inch = 72 points`) puis en pixels à l’aide de `Length.fromPixels`. |
| **Polices manquantes** | Polices non intégrées dans l’EPUB | Assurez‑vous que les polices sont incluses dans l’EPUB ou installez‑les sur la machine hôte. |
| **Ralentissement des performances sur les gros livres** | Rendu de chaque page séquentiellement | Activez le rendu multithread via `PdfSaveOptions.setEnableParallelProcessing(true)` pour un traitement plus rapide des EPUB de plus de 500 pages. |

## Questions fréquemment posées (FAQ)

**Q : Aspose.HTML for Java est‑il une bibliothèque gratuite ?**  
R : Aspose.HTML for Java est une bibliothèque commerciale, mais vous pouvez obtenir une version d’essai gratuite depuis leur [site web](https://releases.aspose.com/).

**Q : Quels formats EPUB sont pris en charge pour la conversion ?**  
R : Aspose.HTML for Java prend en charge EPUB 2.0, EPUB 3.0 et EPUB 3.1, gérant les livres ré‑flottants et à mise en page fixe avec un support complet du CSS.

**Q : Puis‑je personnaliser davantage la sortie PDF ?**  
R : Oui, vous pouvez personnaliser la sortie PDF en ajustant la configuration de la page, la couleur d’arrière‑plan, le niveau de compression et d’autres paramètres dans `PdfSaveOptions`.

**Q : Y a‑t‑il des limitations à la version d’essai d’Aspose.HTML for Java ?**  
R : La version d’essai peut ajouter un filigrane aux premières pages et limite la taille maximale du fichier à 10 Mo ; achetez une licence pour supprimer ces restrictions.

**Q : Où puis‑je obtenir du support pour Aspose.HTML for Java ?**  
R : Vous pouvez trouver des réponses à vos questions et demander de l’aide sur le [forum Aspose.HTML](https://forum.aspose.com/).

---

**Dernière mise à jour :** 2026-05-30  
**Testé avec :** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Auteur :** Aspose

## Tutoriels associés

- [Ajuster la taille de page PDF avec Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Comment convertir un EPUB en PDF avec Java – Utilisation d’Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Convertir EPUB en PDF et images avec Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}