---
category: general
date: 2026-02-14
description: Comment définir le DPI pour la conversion SVG en PNG avec Java. Exporter
  un PNG haute résolution, apprendre à convertir SVG en PNG et utiliser une bibliothèque
  Java de conversion d'images.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: fr
og_description: Comment définir le DPI pour la conversion SVG en PNG avec Java. Ce
  guide vous montre comment exporter des PNG haute résolution et utiliser une bibliothèque
  de conversion d'images Java.
og_title: Comment définir le DPI lors de la conversion de SVG en PNG avec Java
tags:
- java
- image-conversion
- svg
- png
title: Comment définir le DPI lors de la conversion de SVG en PNG avec Java
url: /fr/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI lors de la conversion SVG en PNG avec Java

Vous vous êtes déjà demandé **comment définir le DPI** pour une conversion SVG‑vers‑PNG afin que le résultat soit net sur une affiche prête à imprimer ? Vous n'êtes pas le seul. Dans de nombreux projets—pensez aux flyers marketing, aux maquettes UI ou aux diagrammes techniques—obtenir un PNG haute résolution à partir d'un SVG est indispensable.  

Dans ce tutoriel, nous passerons en revue les étapes exactes pour **convertir SVG en PNG**, **exporter un PNG haute résolution**, et, surtout, contrôler le DPI à l'aide de la bibliothèque Aspose.HTML for Java. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quelle application Java, que vous développiez un outil de bureau ou un service backend.

## Ce dont vous avez besoin

- **Java 8+** (le code se compile avec n'importe quel JDK récent)
- **Aspose.HTML for Java** JARs (disponibles sur Maven Central ou le site web d'Aspose)
- Un fichier SVG que vous souhaitez rasteriser  
- Un petit brin de curiosité—rien d'autre.

Si vous êtes à l'aise avec Maven, ajoutez simplement la dépendance montrée dans la section suivante ; sinon, téléchargez les JARs manuellement et ajoutez-les à votre classpath.

## Étape 1 : Ajouter la bibliothèque Java de conversion d'images

Tout d'abord, votre projet a besoin de la **bibliothèque Java de conversion d'images** qui sait réellement lire les SVG et écrire les PNG. Aspose.HTML est un choix solide car il gère le CSS, les polices et les fonctionnalités vectorielles complexes dès le départ.

**Les utilisateurs de Maven** peuvent coller ceci dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Les adeptes de Gradle** peuvent ajouter :

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Si vous préférez la méthode manuelle, téléchargez le JAR depuis la page de téléchargement d'Aspose et placez-le dans `libs/`, puis ajoutez-le au chemin de construction de votre IDE.

> **Astuce :** Surveillez le numéro de version ; les nouvelles versions améliorent souvent la gestion du DPI et corrigent des bugs de cas limites.

## Étape 2 : Créer les options de conversion et définir le DPI souhaité

Maintenant que la bibliothèque est en place, nous devons lui indiquer *comment* nous voulons que le PNG de sortie apparaisse. C'est ici que le mot‑clé principal—**comment définir le DPI**—entre en jeu. La classe `ImageConversionOptions` vous offre un contrôle granulaire à la fois sur la résolution horizontale (`dpiX`) et verticale (`dpiY`).

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Pourquoi 300 DPI ? Pour la plupart des flux de travail d'impression, 300 points‑par‑pouce est considéré comme une « qualité d'impression ». Si vous ciblez uniquement des actifs web, vous pouvez le réduire à 72 ou 96 DPI pour garder des tailles de fichier légères.

> **Et si j'ai besoin d'un DPI différent pour la largeur et la hauteur ?**  
> Changez simplement `setDpiX` et `setDpiY` indépendamment. La bibliothèque respecte les valeurs non uniformes, ce qui est pratique pour les images anamorphiques.

## Étape 3 : Effectuer la conversion SVG‑vers‑PNG

Avec les options prêtes, la conversion réelle se fait en un seul appel statique. Nous utiliserons `java.nio.file.Paths` pour garder les choses indépendantes de la plateforme.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

C'est tout—exécutez la méthode `main` et vous trouverez un PNG net de 300 DPI dans `YOUR_DIRECTORY`. La bibliothèque met automatiquement à l'échelle les graphiques vectoriels pour correspondre au DPI que vous avez spécifié, en préservant le ratio d'aspect et la netteté du texte.

## Étape 4 : Vérifier le résultat (optionnel mais recommandé)

Une vérification rapide peut vous éviter des maux de tête plus tard. Ouvrez le PNG généré dans n'importe quel visualiseur d'images affichant les métadonnées DPI (par ex., Photoshop, GIMP, ou même l'onglet « Détails » de l'Explorateur Windows). Vous devriez voir **300 DPI** indiqué sous la résolution horizontale et verticale.

Si le fichier apparaît flou, revérifiez :

1. L'SVG original n'est pas de basse résolution dès le départ (les fichiers vectoriels sont indépendants de la résolution, mais les images raster intégrées peuvent limiter la qualité).  
2. Vous avez bien enregistré le fichier après avoir défini le DPI—parfois les IDE mettent en cache d'anciennes builds.  
3. Les options de conversion n'ont pas été écrasées ailleurs dans votre code.

## Pourquoi le DPI est important pour l'exportation de PNG haute résolution

Vous pourriez vous demander : « Pourquoi se soucier du DPI ? Le PNG n'est-il pas seulement des pixels ? » La vérité est que le DPI est une balise *métadonnée* qui indique aux applications en aval (en particulier celles orientées impression) combien de pixels correspondent à un pouce d'espace physique. Si vous fournissez un PNG 1200 × 800 à une imprimante sans métadonnées DPI appropriées, l'imprimante peut supposer une valeur par défaut (souvent 72 DPI) et agrandir l'image, ce qui entraîne un rendu flou.

Définir correctement le DPI est également un gain de performance : vous évitez d'avoir à agrandir les images raster plus tard, ce qui peut être coûteux en calcul et dégrader la qualité.

## Cas limites et pièges courants

| Situation | Ce qu’il faut surveiller | Comment corriger |
|-----------|--------------------------|------------------|
| **Le SVG contient des images bitmap intégrées** | Le bitmap intégré peut être de basse résolution, ce qui fait que le PNG final apparaît pixelisé même avec un DPI élevé. | Remplacez le bitmap par une version de résolution supérieure ou modifiez le SVG pour référencer une image externe. |
| **Valeurs DPI élevées (par ex., 1200 DPI)** | La consommation mémoire augmente fortement ; vous pourriez rencontrer une `OutOfMemoryError`. | Augmentez la taille du tas JVM (`-Xmx2g`) ou limitez le DPI à un maximum raisonnable pour votre cas d'utilisation. |
| **Pixels non carrés** | Certains écrans interprètent le DPI différemment, ce qui entraîne des images étirées. | Assurez-vous que `setDpiX` est égal à `setDpiY` sauf si vous avez une raison spécifique de les différencier. |
| **Polices manquantes** | Le texte du SVG peut revenir à une police par défaut, modifiant la mise en page. | Intégrez les polices dans le SVG ou installez les polices requises sur la machine d'exécution. |

## Résumé rapide (en une phrase)

Pour **définir le DPI** lors d'une conversion SVG‑vers‑PNG, créez un objet `ImageConversionOptions`, définissez `dpiX`/`dpiY`, et appelez `Converter.convert` de la bibliothèque Aspose.HTML Java.

## Prochaines étapes et sujets associés

- **Traitement par lots :** Parcourez un répertoire de fichiers SVG et appliquez les mêmes paramètres DPI.  
- **DPI dynamique :** Lisez un fichier de configuration ou un argument de ligne de commande pour définir le DPI à l'exécution.  
- **Bibliothèques alternatives :** Si vous ne pouvez pas utiliser Aspose, envisagez **Batik** (Apache) ou **SVG Salamander**, bien qu'elles puissent nécessiter du code supplémentaire pour gérer le DPI.  
- **Export PNG haute résolution** pour les ressources Android : combinez cette technique avec les dossiers `drawable‑hdpi`, `xhdpi`, etc., d'Android.

N'hésitez pas à expérimenter—essayez 72 DPI pour les miniatures web, 600 DPI pour les impressions grand format, ou même 150 DPI comme compromis. Le code reste identique ; seuls les nombres changent.

---

![how to set dpi](placeholder-image.png "Illustration of DPI setting in Java conversion workflow")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}