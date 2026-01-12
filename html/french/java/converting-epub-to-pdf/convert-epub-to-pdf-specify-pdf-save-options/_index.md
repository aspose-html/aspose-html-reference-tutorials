---
date: 2026-01-02
description: Apprenez à convertir des fichiers EPUB en PDF en Java avec Aspose.HTML
  tout en définissant une taille de page PDF personnalisée et d’autres options d’enregistrement
  PDF.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Taille de page PDF personnalisée : spécifier les options d’enregistrement
  PDF pour EPUB vers PDF'
url: /fr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Taille de page PDF personnalisée : spécification des options d’enregistrement PDF pour EPUB vers PDF

## Introduction

Aspose.HTML for Java facilite la **conversion d’EPUB en PDF** et vous offre un contrôle complet sur le résultat, y compris la définition d’une **taille de page PDF personnalisée**. Dans ce guide pas à pas, nous passerons en revue tout ce dont vous avez besoin — de la préparation de votre environnement à l’ajustement de `PdfSaveOptions` afin que le PDF généré corresponde exactement aux dimensions de page requises. Que vous construisiez une chaîne de publication, une plateforme d’e‑learning ou que vous ayez simplement besoin d’automatiser la conversion de documents, vous trouverez ici des techniques utiles.

## Quick Answers
- **Quel est le but principal de ce tutoriel ?** Convertir un fichier EPUB en PDF tout en appliquant une taille de page PDF personnalisée.  
- **Quelle bibliothèque est utilisée ?** Aspose.HTML for Java.  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite est disponible ; une licence commerciale est requise pour la production.  
- **Puis‑je changer la couleur d’arrière‑plan ?** Oui, en utilisant `PdfSaveOptions`.  
- **Java 8+ est‑il pris en charge ?** Absolument — tout environnement Java moderne fonctionne.

## Qu’est‑ce qu’une taille de page PDF personnalisée ?

Une taille de page PDF personnalisée vous permet de définir la largeur et la hauteur exactes de chaque page du PDF de sortie, au lieu de vous reposer sur des formats standards comme A4 ou Letter. Cela est particulièrement utile pour les livres numériques, les flyers ou tout scénario où la mise en page visuelle doit correspondre à un design précis.

## Pourquoi utiliser Aspose.HTML pour la conversion d’EPUB en PDF ?

- **Haute fidélité :** préserve les mises en page complexes, les polices et les images.  
- **Contrôle fin :** ajustez la taille de page, l’arrière‑plan, les marges, etc. via `PdfSaveOptions`.  
- **Multiplateforme :** fonctionne sous Windows, Linux et macOS avec le même code Java.  
- **Performance :** moteur de rendu optimisé pour des conversions rapides.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **Environnement de développement Java :** JDK 8 ou supérieur installé et configuré.  
- **Aspose.HTML for Java :** téléchargez le JAR le plus récent depuis le [site web](https://releases.aspose.com/html/java/).  
- **Fichier EPUB :** un document `.epub` que vous souhaitez convertir.  

Maintenant que tout est prêt, plongeons dans les étapes réelles de conversion.

## Étape 1 : Ouvrir le fichier EPUB

Tout d’abord, nous devons ouvrir le fichier EPUB à l’aide d’un `FileInputStream`. Ce flux sera transmis au convertisseur ultérieurement.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Étape 2 : Définir les options d’enregistrement PDF

C’est ici que nous définissons la **taille de page PDF personnalisée** et la couleur d’arrière‑plan optionnelle. Ajustez les valeurs en pixels pour correspondre aux dimensions souhaitées.

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

### Astuce pro :
- **Pixels vs. Points :** `Length.fromPixels` convertit les pixels d’écran en points PDF (1 point = 1/72 pouce). Choisissez des valeurs qui reflètent la taille imprimée finale dont vous avez besoin.

## Étape 3 : Convertir l’EPUB en PDF

Avec le flux d’entrée et les options personnalisées prêts, invoquez le convertisseur. Le PDF de sortie sera enregistré à l’emplacement que vous spécifiez.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Code source complet

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
| **Les pages PDF sont blanches** | Le flux d’entrée est fermé avant la conversion | Gardez le bloc `try‑with‑resources` ouvert jusqu’après `convertEPUB`. |
| **Dimensions de page incorrectes** | Utilisation de pixels qui ne correspondent pas à la taille d’impression désirée | Convertissez les pouces souhaités en points (`1 pouce = 72 points`) puis en pixels avec `Length.fromPixels`. |
| **Polices manquantes** | Polices non intégrées dans l’EPUB | Assurez‑vous que les polices sont emballées dans l’EPUB ou installées sur la machine hôte. |

## Foire aux questions (FAQ)

### Aspose.HTML for Java est‑il une bibliothèque gratuite ?
Aspose.HTML for Java est une bibliothèque commerciale, mais vous pouvez obtenir une version d’essai gratuite depuis leur [site web](https://releases.aspose.com/).

### Quels formats EPUB sont pris en charge pour la conversion ?
Aspose.HTML for Java prend en charge la conversion de divers formats EPUB, assurant la compatibilité avec la plupart des documents EPUB.

### Puis‑je personnaliser davantage la sortie PDF ?
Oui, vous pouvez personnaliser la sortie PDF en ajustant la configuration de la page, la couleur d’arrière‑plan et d’autres paramètres dans `PdfSaveOptions`.

### Existe‑t‑il des limitations à la version d’essai d’Aspose.HTML for Java ?
La version d’essai peut comporter certaines limitations ; il est recommandé de consulter la documentation pour plus de détails.

### Où puis‑je obtenir du support pour Aspose.HTML for Java ?
Vous pouvez trouver des réponses à vos questions et demander de l’aide sur le [forum Aspose.HTML](https://forum.aspose.com/).

---

**Dernière mise à jour :** 2026-01-02  
**Testé avec :** Aspose.HTML for Java 24.11 (dernière version au moment de la rédaction)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}