---
category: general
date: 2026-03-04
description: Apprenez à définir le DPI lors de la conversion de HTML en PNG. Ce guide
  couvre également l'exportation de HTML au format PNG, l'enregistrement de HTML en
  PNG et la génération de PNG à partir de HTML à l'aide d'Aspose.HTML pour Java.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: fr
og_description: Comment définir le DPI pour la conversion HTML en PNG expliqué. Suivez
  le guide étape par étape pour exporter le HTML en PNG, enregistrer le HTML en PNG
  et générer un PNG à partir du HTML.
og_title: Comment définir le DPI lors de la conversion de HTML en PNG
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Comment définir le DPI lors de la conversion de HTML en PNG
url: /fr/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI lors de la conversion de HTML en PNG

Vous vous êtes déjà demandé **comment définir le DPI** pour une image raster que vous générez à partir d'une page web ? Peut-être que vous créez un outil de reporting, un service de miniatures, ou une chaîne d'assets prêts pour l'impression — chacun de ces scénarios commence généralement par un document HTML qui doit devenir un PNG haute résolution.  

Bonne nouvelle, Aspose.HTML for Java rend la **conversion de HTML en PNG** très simple, et vous pouvez contrôler le DPI avec une seule ligne de code. Dans ce tutoriel, nous parcourrons l’ensemble du processus, du chargement de votre fichier HTML à son exportation en PNG à 300 DPI, en abordant également des tâches connexes comme **export HTML as PNG**, **save HTML as PNG**, et **generate PNG from HTML**.

## Ce que vous apprendrez

- Comment configurer le DPI (dots per inch) pour l'image de sortie.
- La différence entre DPI, résolution et qualité de compression.
- Un exemple Java complet et exécutable que vous pouvez copier‑coller.
- Les pièges courants (par ex., polices manquantes, pages volumineuses) et comment les éviter.
- Astuces rapides pour ajuster le résultat lorsque vous devez **convert HTML to PNG** dans différents environnements.

### Prérequis

- Java 8 ou version ultérieure installé sur votre machine.
- Bibliothèque Aspose.HTML for Java (la dernière version en date de mars 2026). Vous pouvez la récupérer depuis Maven Central :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Un fichier `input.html` simple que vous souhaitez transformer en image PNG.

---

## Comment définir le DPI pour la conversion de HTML en PNG

![Diagramme montrant la configuration du DPI dans le code – comment définir le DPI lors de la conversion de HTML en PNG](https://example.com/images/dpi-setting.png)

L'**étape principale** qui contrôle la netteté de l'image est la propriété `Resolution` de `ImageSaveOptions`. Ci-dessous, nous décomposerons le processus en étapes faciles.

### Étape 1 : Définir les chemins d'entrée et de sortie (convert html to png)

Tout d'abord, indiquez au convertisseur où se trouve votre HTML source et où le PNG doit être écrit.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Pourquoi c'est important :** Codifier en dur les chemins est acceptable pour une démonstration, mais en production vous les récupérerez probablement depuis la configuration ou les arguments de ligne de commande. Cela rend le code flexible pour tout flux de travail **save HTML as PNG**.

### Étape 2 : Créer ImageSaveOptions et définir le DPI (how to set dpi)

Nous allons maintenant instancier `ImageSaveOptions` pour PNG et définir le DPI à 300. Le DPI détermine combien de pixels sont placés dans chaque pouce lorsque l'image est imprimée ou affichée à sa taille native.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Explication :**  
> - `setResolution(300)` indique à Aspose.HTML de rendre la page à 300 dots per inch.  
> - `setQuality(95)` est optionnel pour le PNG ; il contrôle le niveau de compression ZLIB. Vous pouvez le diminuer pour obtenir des fichiers plus petits si vous n’avez pas besoin que chaque pixel soit parfait.

### Étape 3 : Effectuer la conversion (export html as png)

Avec les options prêtes, la conversion réelle se fait en une seule ligne.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **Ce qui se passe en coulisses :** Aspose.HTML analyse le HTML, applique le CSS, met en page le DOM, rasterise la mise en page au DPI demandé, puis écrit finalement un fichier PNG. Si vous devez **generate PNG from HTML** dans un service web, vous pouvez remplacer les chemins de fichiers par des flux.

### Exemple complet fonctionnel

En rassemblant le tout, voici une classe Java complète que vous pouvez compiler et exécuter.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Exécutez le programme et vous trouverez un PNG net à 300 DPI à l'emplacement que vous avez spécifié. Ouvrez-le avec n'importe quel visualiseur d'images et vérifiez les propriétés de l'image — le DPI doit indiquer **300**.

---

## Questions fréquentes & cas limites

### Que faire si le réglage du DPI semble être ignoré ?

- **Assurez‑vous d'utiliser une version récente d'Aspose.HTML.** Les versions antérieures ignoraient `Resolution` pour le PNG.
- **Vérifiez la taille du HTML source.** Une page HTML minuscule rendue à 300 DPI peut toujours produire une petite dimension en pixels. Le DPI n'affecte que le facteur d'échelle, pas la taille inhérente de la page.

### En quoi le DPI diffère‑t‑il des dimensions de l'image ?

Le DPI est une mesure *physique* (dots per inch). La largeur/hauteur réelle en pixels est calculée comme :

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Si le corps de votre HTML fait 800 px de large, à 300 DPI le PNG de sortie sera approximativement de 2500 px de large (800 × 300 ÷ 96).

### Puis‑je utiliser d'autres formats (JPEG, BMP) tout en contrôlant le DPI ?

Absolument. Il suffit de changer `SaveFormat.PNG` en `SaveFormat.JPEG` (ou `BMP`) et de conserver `setResolution`. N'oubliez pas que le JPEG respecte également le paramètre `Quality`, qui correspond au niveau de compression.

### Qu'en est‑il des polices qui ne sont pas installées sur le serveur ?

Aspose.HTML reviendra à une police par défaut, ce qui peut modifier la mise en page. Pour garantir un rendu identique, intégrez les polices requises en utilisant `FontSettings` :

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Générer plusieurs PNG en lot

Si vous devez **generate PNG from HTML** pour de nombreux fichiers, encapsulez la logique de conversion dans une boucle et réutilisez une seule instance de `ImageSaveOptions`. Cela réduit la consommation de mémoire et accélère le traitement.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Astuces pro pour une exportation PNG de haute qualité

1. **Utilisez du CSS compatible vecteur** (par ex., `transform: scale(1)`) pour éviter les artefacts d'anti‑aliasing à haute DPI.  
2. **Définissez une couleur d'arrière‑plan** si votre HTML comporte des éléments transparents et que vous avez besoin d'un canevas opaque :

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. **Évitez les images base64 en ligne** de plus de quelques Mo — elles peuvent gonfler l'utilisation de la mémoire pendant la conversion.  
4. **Testez sur différents DPI d'écran** (par ex., moniteurs à 72 DPI vs imprimantes à 300 DPI) pour garantir que la qualité visuelle répond aux attentes.  
5. **Exploitez `setPageSize()`** si vous voulez que le PNG corresponde à une taille d'impression spécifique (A4, Letter, etc.) indépendamment des dimensions originales du HTML.

---

## Conclusion

Nous avons couvert **comment définir le DPI** lorsque vous **convertissez HTML en PNG** avec Aspose.HTML for Java, présenté un exemple complet et prêt à l'exécution, et exploré des tâches connexes comme **export HTML as PNG**, **save HTML as PNG**, et **generate PNG from HTML**. En ajustant `ImageSaveOptions.setResolution`, vous contrôlez la netteté physique du résultat, tandis que `setQuality` vous permet d'équilibrer la taille du fichier et la fidélité visuelle.

Prochaines étapes ? Essayez de remplacer le format PNG par JPEG pour voir comment la compression interagit avec le DPI, ou expérimentez le traitement par lots pour **convert HTML to PNG** à grande échelle. Vous pouvez également explorer l'ajout de filigranes ou de métadonnées personnalisées — les deux sont pris en charge par l'API riche d'Aspose.HTML.

Vous avez un scénario difficile qui n’a pas été couvert ? Laissez un commentaire, et nous le résoudrons ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}