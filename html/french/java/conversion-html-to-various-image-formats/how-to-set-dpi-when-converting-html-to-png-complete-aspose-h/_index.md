---
category: general
date: 2026-06-29
description: Apprenez à définir le DPI et la résolution d’image lors de la conversion
  de HTML en PNG avec Aspose HTML Converter. Exemple Java étape par étape inclus.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: fr
og_description: Comment définir le DPI dans la conversion HTML d’Aspose. Ce guide
  vous montre comment convertir une page HTML en image PNG haute résolution en Java.
og_title: Comment définir le DPI lors de la conversion de HTML en PNG – Tutoriel Aspose
  HTML
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Comment définir le DPI lors de la conversion de HTML en PNG – Guide complet
  Aspose HTML
url: /fr/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI lors de la conversion HTML en PNG – Guide complet Aspose HTML

Vous êtes‑vous déjà demandé **comment définir le DPI** pour un PNG que vous générez à partir d’une page HTML ? Dans de nombreux scénarios de reporting ou d’automatisation de captures d’écran, le 96 dpi par défaut n’est tout simplement pas assez net. La bonne nouvelle, c’est qu’Aspose.HTML pour Java vous donne un contrôle total sur la simulation d’écran et la résolution d’image, vous permettant d’augmenter le DPI à 300 ou même 600 en quelques lignes de code.

Dans ce tutoriel, nous parcourrons un exemple Java réel qui **convertit une page HTML en PNG** tout en définissant explicitement le **DPI** et la **résolution d’image**. À la fin, vous disposerez d’une classe prête à l’emploi, comprendrez pourquoi chaque paramètre est important et saurez comment l’ajuster pour différents cas d’utilisation, comme les impressions haute résolution ou les vignettes web.

> **Aperçu rapide :** Les étapes principales sont (1) créer un `Sandbox` qui simule un écran, (2) définir son DPI, (3) configurer `ImageConversionOptions` avec la résolution souhaitée, et (4) appeler `Converter.convert`. Aucun outil externe, aucune gymnastique en ligne de commande — juste du Java pur.

## Prérequis

Avant de plonger, assurez‑vous d’avoir :

- **Java 17** (ou tout JDK récent) installé et configuré dans votre IDE.
- **Aspose.HTML for Java** library (l’artifact Maven `com.aspose:aspose-html`). Vous pouvez obtenir la dernière version depuis le [dépôt Maven d’Aspose](https://repo.aspose.com/repo) ou télécharger le JAR directement.
- Un fichier HTML simple (`page.html`) que vous souhaitez convertir en PNG. Placez‑le à un emplacement accessible, par ex., `C:/temp/page.html`.
- Une connaissance de base de la gestion des exceptions en Java—rien de compliqué.

Si l’un de ces points vous est inconnu, faites une pause et installez l’élément manquant. Le reste du guide suppose que vous êtes à l’aise avec l’ouverture d’un projet Java et l’ajout de JAR externes.

## Étape 1 : Configurer votre projet Maven (ou ajouter le JAR manuellement)

Si vous utilisez Maven, ajoutez la dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

Sinon, déposez le `aspose-html-*.jar` dans le dossier `libs` de votre projet et ajoutez‑le au chemin de construction. Cette étape ne porte pas directement sur **comment définir le DPI**, mais sans la bibliothèque vous ne pouvez pas accéder à la classe `Sandbox` qui rend le contrôle du DPI possible.

## Étape 2 : Créer un Sandbox qui simule un écran réel

Un *sandbox* est la façon d’Aspose de reproduire un environnement de navigateur. Considérez‑le comme un moniteur virtuel où vous décidez de la largeur, de la hauteur et, surtout, du **DPI**. Voici l’extrait de code qui crée un écran 1024 × 768 à 96 dpi—juste une base avant d’augmenter la résolution :

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Pourquoi un sandbox ?** Sans cela, Aspose reviendrait aux paramètres d’écran de la machine hôte, entraînant des résultats incohérents d’une machine de développement à l’autre. En verrouillant le DPI, vous garantissez que chaque conversion a le même aspect, que vous l’exécutiez sur un ordinateur portable ou sur un serveur CI.

## Étape 3 : Configurer les options de conversion d’image – Définir la résolution de l’image

Maintenant que le sandbox est prêt, nous indiquons au convertisseur quelle **résolution d’image** nous souhaitons. La classe `ImageConversionOptions` vous permet de définir le DPI du PNG de sortie indépendamment du DPI du sandbox, vous offrant ainsi deux leviers à actionner.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Astuce :** Si vous voulez un PNG à 600 dpi pour des brochures haute qualité, changez simplement `setResolution(300)` en `setResolution(600)`. Gardez à l’esprit que des valeurs DPI plus élevées augmentent la consommation de mémoire et le temps de traitement, donc testez d’abord avec une petite page.

## Étape 4 : Convertir la page HTML en PNG

Avec le sandbox et les options en place, l’étape réelle de **conversion html en png** se résume à une seule ligne :

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Si tout se passe bien, vous verrez le message de la console de l’étape suivante.

## Étape 5 : Vérifier le résultat et afficher la confirmation

Un simple `System.out.println` vous indique que le travail est terminé. Dans un projet réel, vous pourriez vouloir vérifier la taille du fichier, les dimensions, ou même ouvrir le PNG programmatiquement pour valider le DPI.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

L’exécution de la classe doit créer `page.png` dans le même dossier que votre fichier HTML. Ouvrez‑le dans un visualiseur d’images affichant le DPI (par ex., Windows Photo Viewer → Propriétés → Détails) et confirmez qu’il indique **300 dpi**.

## Exemple complet fonctionnel

En rassemblant le tout, voici une classe Java autonome que vous pouvez copier‑coller dans votre IDE :

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Rappel :** La ligne `sandbox.setDpi(96);` constitue la partie *comment définir le dpi*. Ajustez‑la pour correspondre à la densité d’écran dont vous avez besoin ; `conversionOptions.setResolution(300);` contrôle le DPI final de l’image.

## Gestion des problèmes courants

| Situation | À surveiller | Solution proposée |
|-----------|--------------|-------------------|
| **Erreurs de mémoire insuffisante** lors de l’utilisation de 600 dpi | Un DPI élevé augmente considérablement la taille du raster (par ex., 1024 × 768 @ 600 dpi ≈ 4 MP). | Réduisez les dimensions de l’écran, ou diffusez la conversion en utilisant les callbacks `ConversionProgress`. |
| **Le HTML utilise du CSS/JS externe qui ne se charge pas** | Le sandbox s’exécute en isolement ; les ressources distantes doivent être accessibles. | Fournissez des URL absolues ou intégrez le CSS directement dans le HTML. |
| **DPI incorrect dans la sortie** | Vous avez modifié `sandbox.setDpi` mais avez oublié d’ajuster `conversionOptions.setResolution`. | Assurez‑vous que les deux valeurs correspondent à votre sortie cible. |
| **FileNotFoundException** | Erreur de chemin ou permissions de fichier manquantes. | Utilisez `Paths.get(...).toAbsolutePath()` et vérifiez les droits de lecture/écriture. |

## Variantes avancées

### 1. Différents formats de sortie

Aspose.HTML ne se limite pas au PNG. Changez l’extension du fichier et utilisez une classe d’options correspondante, par ex., `JpegConversionOptions` pour les JPEG. La logique du DPI reste identique.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Détermination dynamique de la taille d’écran

Si vous avez besoin que le sandbox imite un appareil mobile, lisez les dimensions depuis un fichier de configuration :

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Exécutez avec `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326` pour émuler un affichage Retina d’iPhone.

### 3. Conversion par lot

Enveloppez l’appel de conversion dans une boucle qui parcourt un répertoire de fichiers HTML. N’oubliez pas de réutiliser les mêmes objets `Sandbox` et `ImageConversionOptions` afin d’éviter des allocations inutiles.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Résultat attendu

L’exécution de la classe avec les paramètres par défaut produit un fichier PNG d’environ **1024 × 768 pixels** à **300 dpi**. Dans la plupart des éditeurs d’image, les dimensions apparaîtront comme 1024 × 768, tandis que les métadonnées DPI indiqueront 300. Si vous imprimez l’image à une largeur de 1 pouce, vous obtiendrez une ligne nette de 300 pixels—parfait pour des flyers haute qualité.

## Résumé visuel

![comment définir le dpi dans la conversion Aspose HTML](/images/aspose-dpi-example.png "comment définir le dpi – exemple de sandbox Aspose HTML")

*La capture d’écran montre les métadonnées DPI du PNG généré (300 dpi).*

## Conclusion

Nous avons couvert **comment définir le DPI** lorsque vous **convertissez du HTML en PNG** à l’aide du **convertisseur Aspose HTML** en Java. En créant un sandbox, en configurant `ImageConversionOptions` et en appelant `Converter.convert`, vous obtenez un contrôle pixel‑parfait à la fois sur la simulation d’écran et sur la résolution finale de l’image. Que vous génériez des factures imprimables, des ressources web haute résolution ou des vignettes automatisées, le même schéma s’applique—il suffit d’ajuster le DPI et la taille de l’écran pour répondre à vos besoins.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment utiliser Aspose pour rendre du HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Comment convertir du HTML en JPEG avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Comment convertir du HTML en BMP avec Aspose.HTML pour Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}