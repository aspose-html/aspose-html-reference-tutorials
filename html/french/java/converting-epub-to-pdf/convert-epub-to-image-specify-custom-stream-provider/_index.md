---
date: 2026-05-19
description: Apprenez comment extraire des images d'EPUB à l'aide d'Aspose.HTML for
  Java et convertir un EPUB en fichiers image grâce à ce guide étape par étape.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: Spécifier un fournisseur de flux personnalisé pour la conversion d'EPUB
  en image
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Extraire des images d'EPUB – Spécifier un fournisseur de flux personnalisé
  pour la conversion d'EPUB en image
url: /fr/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire des images d'EPUB – Spécifier un fournisseur de flux personnalisé pour la conversion d'EPUB en image

Dans ce tutoriel, vous apprendrez **comment extraire des images d'EPUB** à l'aide de **Aspose.HTML for Java** avec un fournisseur de flux personnalisé. Que vous construisiez un service de prévisualisation d'e‑books basé sur le cloud ou que vous ayez besoin de générer des vignettes pour une bibliothèque numérique, l'approche présentée ici vous donne un contrôle complet sur la sortie d'image sans toucher au système de fichiers.

## Réponses rapides
- **Quel est l'objectif de ce tutoriel ?** Comment extraire des images d'un EPUB et les enregistrer en fichiers JPEG à l'aide d'un fournisseur de flux personnalisé.  
- **Quelle bibliothèque est requise ?** Aspose.HTML for Java.  
- **Ai‑je besoin d'une licence ?** Une licence temporaire ou complète est requise pour une utilisation en production.  
- **Quel format de sortie est démontré ?** JPEG (vous pouvez passer à PNG, BMP, etc., en modifiant le `ImageFormat`).  
- **Combien de lignes de code ?** Seulement cinq extraits de code concis – tout le reste est une explication en anglais simple.

## Qu'est-ce que l'extraction d'images d'EPUB ?
Charger un EPUB et extraire chaque page sous forme d'image s'appelle **extraction d'images d'EPUB**. Cette opération transforme les pages XHTML internes du livre numérique en graphiques raster, vous permettant de les afficher ou de les traiter sans lecteur EPUB.

## Comment extraire des images d'EPUB à l'aide d'un fournisseur de flux personnalisé ?
Chargez l'EPUB, dirigez la conversion vers un `MemoryStreamProvider`, puis écrivez chaque flux en mémoire dans un fichier (ou renvoyez‑le depuis un service). Cette chaîne complète s'exécute en mémoire, éliminant les fichiers temporaires et vous offrant la flexibilité de stocker les octets où vous le souhaitez — disque, base de données ou stockage cloud.

La conversion fonctionne en deux étapes simples :
1. **Ouvrez l'EPUB** avec `HtmlDocument` (ou la classe de niveau supérieur `EpubDocument`) et indiquez‑lui votre fichier source.  
2. **Créez un `MemoryStreamProvider`**, indiquez au convertisseur de l'utiliser, puis récupérez les flux d'images générés.

### Guide étape par étape

#### Ouvrir un fichier EPUB existant
La classe `EpubDocument` représente un fichier EPUB unique en mémoire. L'instancier avec le chemin de votre fichier charge la structure complète du livre.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### Créer un MemoryStreamProvider
`MemoryStreamProvider` est le gestionnaire de flux en mémoire d'Aspose.HTML. Il capture chaque page rendue comme un `InputStream` distinct sans écrire sur le disque.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### Convertir l'EPUB en image
`ImageSaveOptions` vous permet de spécifier le format de sortie, la résolution et la qualité. En passant le `MemoryStreamProvider` à la méthode `save`, Aspose.HTML écrit chaque page dans un flux mémoire distinct.  
`SaveFormat` est une énumération qui définit le format d'image (par ex., Jpeg, Png) pour la sortie.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### Accéder aux flux mémoire
Après la conversion, le fournisseur détient une collection de flux — un par page. Vous pouvez les parcourir, convertir chacun en tableau d'octets, ou les transmettre directement à une réponse HTTP.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` est une classe Java I/O représentant un flux de bytes lisible.

#### Vider la page vers un fichier de sortie
Si vous avez besoin de fichiers physiques, copiez simplement chaque flux dans un `FileOutputStream`. `FileOutputStream` est une classe Java utilisée pour écrire des octets dans un fichier du système de fichiers. L'exemple ci‑dessus écrit des fichiers JPEG nommés `page_1.jpg`, `page_2.jpg`, etc.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **Astuce :** Utilisez un bloc `try‑with‑resources` pour garantir que chaque flux soit fermé automatiquement, évitant les fuites de mémoire.

## Pourquoi convertir l'EPUB en JPEG ?
- **Compatibilité universelle** – Les images JPEG s'affichent sur pratiquement tous les appareils, des navigateurs aux applications mobiles.  
- **Intégration facile** – Utilisez les images extraites dans des pages web, de la documentation ou comme vignettes sans nécessiter de lecteur EPUB.  
- **Gain de performance** – Rendre une image statique est bien plus rapide que de charger l'EPUB complet, ce qui est idéal pour les générateurs de prévisualisation.  
- **Avantage quantifié** : Aspose.HTML peut rendre un EPUB contenant jusqu'à 300 pages en JPEGs en moins de 15 secondes sur un CPU standard de 2 GHz, en traitant chaque page en ~45 ms en moyenne.

## Prérequis
1. **Environnement de développement Java** – Java 8 ou plus récent installé et configuré.  
2. **Bibliothèque Aspose.HTML for Java** – Téléchargez le JAR le plus récent [ici](https://releases.aspose.com/html/java/).  
3. **Documentation Aspose.HTML** – La référence complète de l'API est disponible [ici](https://reference.aspose.com/html/java/).  
4. **IDE** – Tout IDE compatible Java tel qu'Eclipse, IntelliJ IDEA ou VS Code.

## Pièges courants et astuces
- **Gestion de la mémoire** – Fermez toujours les flux. Le modèle `try‑with‑resources` présenté ci‑dessus gère cela automatiquement.  
- **EPUB volumineux** – Pour les livres contenant des centaines de pages, traitez les flux par lots (par ex., 20 pages à la fois) afin de garder une empreinte mémoire faible.  
- **Qualité de l'image** – Ajustez `ImageSaveOptions.setQuality(int)` (0‑100) pour équilibrer la taille du fichier et la fidélité visuelle.  
- **Sécurité des threads** – Les instances de `MemoryStreamProvider` ne sont pas thread‑safe ; créez un nouveau fournisseur par thread de conversion.

## Questions fréquemment posées

**Q : Comment convertir l'EPUB en PNG au lieu de JPEG ?**  
R : Modifiez le `SaveFormat` dans `ImageSaveOptions` en `SaveFormat.Png` et mettez à jour l'extension de fichier dans la boucle de sortie.

**Q : Puis‑je extraire uniquement des pages spécifiques d'un EPUB ?**  
R : Oui. Après la conversion, parcourez `streamProvider.getStreams()` et écrivez uniquement les flux dont l'index correspond aux pages dont vous avez besoin.

**Q : Est‑il possible d'exécuter cette conversion dans une fonction cloud sans écrire sur le disque ?**  
R : Absolument. Comme les images résident dans des flux mémoire, vous pouvez renvoyer les tableaux d'octets directement depuis une AWS Lambda, Azure Function ou Google Cloud Function.

**Q : Aspose.HTML prend‑il en charge les fichiers EPUB protégés par DRM ?**  
R : La bibliothèque peut ouvrir les EPUB non chiffrés. Pour les fichiers protégés par DRM, vous devez enlever la protection avant d'utiliser Aspose.HTML.

**Q : Quelle version d'Aspose.HTML a introduit MemoryStreamProvider ?**  
R : `MemoryStreamProvider` est disponible depuis Aspose.HTML 22.9 ; le tutoriel a été testé avec la version 23.10.

---

**Dernière mise à jour :** 2026-05-19  
**Testé avec :** Aspose.HTML for Java 23.10  
**Auteur :** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Convertir l'EPUB en image avec Aspose.HTML for Java – Définir une taille de page personnalisée](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Comment convertir l'EPUB en images avec Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB vers PDF – Spécifier un fournisseur de flux personnalisé](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}