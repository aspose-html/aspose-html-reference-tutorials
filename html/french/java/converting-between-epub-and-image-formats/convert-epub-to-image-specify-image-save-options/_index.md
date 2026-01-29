---
date: 2025-12-25
description: Apprenez à convertir des fichiers EPUB en images avec Aspose.HTML pour
  Java et à définir une taille de page personnalisée. Ce guide étape par étape couvre
  les prérequis, les importations de packages et le processus de conversion.
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Convertir EPUB en image avec Aspose.HTML pour Java – Définir une taille de
  page personnalisée
url: /fr/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir EPUB en image avec Aspose.HTML pour Java – Définir une taille de page personnalisée

Dans le monde en constante évolution du développement web, Aspose.HTML for Java se présente comme un outil puissant, et aujourd’hui nous nous concentrerons sur **comment définir une taille de page personnalisée** lors de la conversion d’un EPUB en image. Ce guide vous accompagne à travers l’ensemble du processus — de l’installation des bibliothèques requises à l’ajustement de la couleur de fond de l’image — afin que vous puissiez **convertir EPUB en image** exactement comme vous le souhaitez.

## Réponses rapides
- **Que signifie « définir une taille de page personnalisée » ?** Cela vous permet de définir la largeur et la hauteur de chaque page d’image générée.  
- **Puis-je changer la couleur de fond de l’image ?** Oui, vous pouvez spécifier n’importe quelle couleur en utilisant `ImageSaveOptions`.  
- **Quels formats sont pris en charge ?** JPEG, PNG, GIF, et plus via `ImageFormat`.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour les tests ; une licence commerciale est requise pour la production.  
- **Quelle version de Java est requise ?** Java 1.7 ou ultérieure est entièrement prise en charge.

## Qu’est‑ce que « définir une taille de page personnalisée » dans la conversion d’EPUB en image ?
Définir une taille de page personnalisée signifie que vous contrôlez les dimensions de l’image rendue (par ex., 3000 × 1000 pixels). Cela est utile lorsque vous avez besoin de captures d’écran haute résolution d’e‑books ou lorsque vous souhaitez que la sortie corresponde à une mise en page spécifique.

## Pourquoi définir une taille de page personnalisée et changer la couleur de fond de l’image ?
Les tailles de page personnalisées vous offrent une flexibilité pour différentes cibles d’affichage — écrans mobiles, PDF prêts à imprimer ou vignettes web. Modifier la couleur de fond vous aide à harmoniser la marque ou à améliorer la lisibilité des images contenant des éléments transparents.

## Prérequis

Avant de commencer notre parcours pour **convertir epub en image**, assurez‑vous de disposer de ce qui suit :

1. **Environnement Java** – Un kit de développement Java installé sur votre machine. Si vous n’avez pas encore Java, vous pouvez le télécharger depuis [ici](https://www.java.com).
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

### Étape 1 : Ouvrir un fichier EPUB existant en lecture

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

Ici nous ouvrons l’EPUB source. Remplacez `"input.epub"` par le chemin vers votre fichier e‑book.

### Étape 2 : Initialiser ImageSaveOptions avec des paramètres personnalisés (définir une taille de page personnalisée & changer la couleur de fond de l’image)

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

Dans ce bloc, nous **définissons une taille de page personnalisée** à 3000 × 1000 pixels et changeons le fond en AliceBlue. N’hésitez pas à ajuster le `size` ou le `Color` selon votre projet (par ex., `Color.getWhite()` pour un fond blanc simple).

### Étape 3 : Convertir EPUB en image

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

Cette ligne effectue la conversion réelle. Le fichier de sortie (`"output.jpg"`) contiendra l’image rendue avec les dimensions et le fond que vous avez spécifiés. Vous pouvez également changer l’extension du fichier en `.png` si vous préférez **java convert epub png**.

### Étape 4 : Fermer les ressources (géré automatiquement)

L’instruction `try‑with‑resources` ferme automatiquement le `FileInputStream`, garantissant qu’aucune poignée de fichier ne reste ouverte.

## Cas d’utilisation courants

- **Générer des vignettes** pour les bibliothèques d’e‑books.  
- **Créer des captures d’écran haute résolution** pour la documentation ou le marketing.  
- **Traitement par lots** de grandes collections d’EPUB en actifs PNG/JPEG pour les galeries web.  

## Astuces et bonnes pratiques

- **Astuce pro :** Utilisez `Length.fromInches()` ou `Length.fromCentimeters()` si vous préférez les unités physiques aux pixels.  
- **Astuce performance :** Pour les gros EPUB, envisagez d’augmenter la taille du tas JVM (`-Xmx2g`) afin d’éviter la pression mémoire.  
- **Gestion des erreurs :** Enveloppez l’appel de conversion dans un bloc `try‑catch` pour capturer `IOException` ou `AsposeException`.  

## Questions fréquentes

**Q : Puis‑je convertir des fichiers EPUB en d’autres formats d’image ?**  
R : Oui, vous pouvez spécifier des formats tels que PNG ou GIF en changeant `ImageFormat.Jpeg` en `ImageFormat.Png` ou `ImageFormat.Gif`.

**Q : Aspose.HTML for Java prend‑il en charge EPUB3 ?**  
R : Absolument. La bibliothèque prend pleinement en charge EPUB3, vous permettant de travailler avec les dernières normes d’e‑book.

**Q : Comment gérer les erreurs pendant le processus de conversion ?**  
R : Implémentez des blocs `try‑catch` autour du code de conversion pour capturer et consigner les exceptions, assurant que votre application reste robuste.

**Q : Puis‑je personnaliser la taille et la qualité de l’image ?**  
R : Oui, ajustez l’objet `Size` pour les dimensions et utilisez `options.setQuality(int)` pour contrôler la qualité de compression JPEG.

**Q : Aspose.HTML for Java est‑il compatible avec toutes les versions de Java ?**  
R : La bibliothèque fonctionne avec Java 1.7 et ultérieur, couvrant un large éventail d’environnements de développement.

---

**Dernière mise à jour :** 2025-12-25  
**Testé avec :** Aspose.HTML for Java 24.10  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}