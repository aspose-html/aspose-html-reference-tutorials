---
category: general
date: 2026-05-06
description: Comment définir le DPI pour la conversion SVG vers PNG haute résolution
  en Java avec Aspose.HTML. Apprenez à convertir SVG en PNG, à exporter SVG en PNG
  et à transformer le vecteur en raster.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: fr
og_description: Comment définir le DPI pour la conversion SVG vers PNG haute résolution
  en Java avec Aspose.HTML. Obtenez le code étape par étape et des conseils d'experts.
og_title: Comment définir le DPI lors de la conversion de SVG en PNG – Guide Java
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Comment définir le DPI lors de la conversion de SVG en PNG – Guide Java
url: /fr/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI lors de la conversion SVG en PNG – Guide Java

Vous vous êtes déjà demandé **comment définir le DPI** pour une conversion SVG‑to‑PNG et obtenir une image nette, prête à l’impression ? Vous n’êtes pas seul. De nombreux développeurs se heurtent à un mur lorsque leur PNG exporté apparaît flou parce que le DPI par défaut (généralement 96) n’est tout simplement pas suffisant pour une sortie professionnelle.

Dans ce tutoriel, nous passerons en revue un exemple complet, prêt à l’exécution, qui montre **comment définir le DPI** en utilisant Aspose.HTML pour Java. À la fin, vous pourrez **convertir SVG en PNG**, **exporter SVG en PNG**, et même **convertir un vecteur en raster** avec le DPI de votre choix — aucune énigme, juste du code clair.

## Ce que vous allez apprendre

- Les étapes exactes pour configurer le DPI avant la conversion.  
- Pourquoi le DPI est important lorsque vous **convertissez un vecteur en raster**.  
- Comment **convertir SVG en PNG** en une seule ligne de code.  
- Astuces pour gérer de gros SVG et le traitement par lots.  
- Un programme complet et compilable que vous pouvez intégrer immédiatement à votre projet.

## Prérequis

- Java 17 ou plus récent (la dernière version LTS fonctionne le mieux).  
- Maven ou Gradle pour récupérer la bibliothèque Aspose.HTML.  
- Un fichier SVG simple que vous souhaitez rasteriser (par ex., `logo.svg`).  
- Un IDE ou éditeur de texte—IntelliJ IDEA, VS Code, ou même un simple Notepad fera l’affaire.

Aucun autre outil externe n’est requis ; la bibliothèque effectue tout le travail lourd.

## Étape 1 : Ajouter Aspose.HTML à votre projet

Tout d’abord, vous avez besoin du JAR Aspose.HTML. Si vous utilisez Maven, ajoutez cet extrait à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Pour Gradle, cela ressemble à ceci :

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Astuce :** Utilisez toujours la dernière version stable ; les nouvelles versions incluent des correctifs de performance pour le rendu haute‑DPI.

## Étape 2 : Comment définir le DPI pour la conversion

Nous arrivons maintenant au cœur du sujet—**comment définir le DPI**. Aspose.HTML expose `ImageConversionOptions`, où vous pouvez spécifier la résolution horizontale (`dpiX`) et verticale (`dpiY`). Les régler tous deux à `300` vous donne cette densité de qualité d’impression classique.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Pourquoi 300 dpi ?** C’est la norme de facto pour l’impression professionnelle. Si vous avez besoin d’une image prête pour le web, 72 dpi suffisent, mais pour des flyers ou des brochures, visez au moins 300 dpi.

### Aperçu de l'image

![How to set DPI when converting SVG to PNG](https://example.com/placeholder.png "How to set DPI when converting SVG to PNG")

*L’image ci‑dessus illustre la différence entre un PNG à faible DPI (à gauche) et une sortie à 300 dpi (à droite).*

## Étape 3 : Convertir SVG en PNG – Une seule ligne

Si vous cherchez simplement un **convert svg to png** rapide sans vous soucier du DPI, vous pouvez ignorer complètement l’objet d’options :

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

Passer `null` indique à Aspose.HTML d’utiliser son DPI par défaut (généralement 96). C’est pratique pour les miniatures ou lorsque la qualité d’impression n’est pas importante.

## Étape 4 : Vérifier le résultat – Exporter SVG en PNG

Une fois la conversion terminée, ouvrez le PNG généré avec n’importe quel visualiseur d’images. Vous devriez voir une image raster qui correspond aux dimensions du vecteur d’origine, mais qui possède maintenant le DPI que vous avez défini. La plupart des visualiseurs affichent le DPI dans les propriétés de l’image ; sous Windows, clic droit → Propriétés → Détails.

Si vous devez vérifier le DPI de façon programmatique, `ImageIO` de Java peut le lire :

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Note :** Tous les formats d’image n’enregistrent pas les métadonnées DPI ; le PNG le fait, mais le JPEG peut nécessiter une gestion supplémentaire.

## Cas limites et variantes

### 1️⃣ Valeurs DPI différentes

Vous vous demandez peut‑être « Et si j’ai besoin de 600 dpi pour une grande affiche ? » Il suffit de changer les nombres :

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

Un DPI plus élevé signifie une taille de fichier plus importante, donc soyez attentif aux contraintes de mémoire lors du traitement de nombreux fichiers.

### 2️⃣ Conversion par lots d’un dossier

Lorsque vous avez des dizaines de SVG, encapsulez la conversion dans une boucle simple :

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Ce modèle **convertit un vecteur en raster** en masse, vous faisant gagner des heures de travail manuel.

### 3️⃣ Gestion des arrière‑plans transparents

Si votre SVG contient de la transparence et que vous souhaitez un arrière‑plan blanc, rendez‑le d’abord dans un `BufferedImage`, puis remplissez l’arrière‑plan :

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle sous Linux ?**  
R : Absolument. Aspose.HTML est indépendant de la plateforme ; assurez‑vous simplement d’avoir le bon runtime Java.

**Q : Et si mon SVG référence des images externes ?**  
R : Veillez à ce que ces ressources soient accessibles via des chemins absolus ou des URL ; sinon le rendu les ignorera.

**Q : Puis‑je convertir SVG en d’autres formats raster comme JPEG ou BMP ?**  
R : Oui. Utilisez `Converter.convertSvgToJpeg` ou `Converter.convertSvgToBmp` avec les mêmes `ImageConversionOptions`.

## Astuces pro pour une rasterisation de haute qualité

- **Adaptez le DPI à la taille finale de sortie.** Un logo de 2 pouces imprimé à 300 dpi nécessite une largeur de 600 px (2 in × 300 dpi). Redimensionnez le SVG en conséquence avant la conversion si vous avez besoin d’une dimension pixel précise.  
- **Prenez en compte le profil couleur.** Les PNG n’intègrent pas de profils ICC par défaut ; si la fidélité des couleurs est cruciale, convertissez en TIFF ou utilisez une bibliothèque qui prend en charge l’inclusion de profils.  
- **Réutilisez l’objet `ImageConversionOptions`** lors de la conversion de nombreux fichiers — cela évite la création d’objets inutiles et peut améliorer les performances.

## Conclusion

Vous savez maintenant **comment définir le DPI** pour une conversion SVG‑to‑PNG en Java, et vous avez vu comment la même approche vous permet de **convertir svg to png**, **exporter svg as png**, et généralement **convertir un vecteur en raster** avec un contrôle total de la résolution. L’exemple complet ci‑dessus fonctionne immédiatement, et les conseils supplémentaires vous offrent une feuille de route pour adapter la solution à des projets réels.

Et après ? Essayez de remplacer la valeur 300 dpi par 600 dpi, expérimentez le traitement par lots, ou explorez d’autres formats raster. Les mêmes principes s’appliquent — il suffit de changer la méthode de sortie et le tour est joué.

Vous avez un SVG difficile ou une question de performance ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}