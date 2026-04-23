---
category: general
date: 2026-04-23
description: Apprenez comment définir le DPI pour une conversion SVG vers PNG ultra‑haute
  qualité en Java avec Aspose. Comprend du code étape par étape, des astuces et la
  gestion des cas limites.
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: fr
og_description: Maîtrisez la façon de définir le DPI pour la conversion SVG en PNG
  avec Aspose HTML en Java. Code complet, explications et conseils de bonnes pratiques.
og_title: Comment définir le DPI lors de la conversion de SVG en PNG – Tutoriel Java
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Comment définir le DPI lors de la conversion de SVG en PNG avec Aspose – Guide
  Java
url: /fr/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI lors de la conversion SVG en PNG avec Aspose – Guide Java

Vous vous êtes déjà demandé **comment définir le DPI** pour un PNG cristallin provenant d'un SVG ? Peut‑être que vous construisez une chaîne de branding et avez besoin du logo à 600 dpi pour l’impression, ou vous voulez simplement que l’image raster soit nette sur des écrans haute résolution. La bonne nouvelle, c’est que vous n’avez pas besoin d’y deviner — Aspose HTML for Java le rend très simple.

Dans ce tutoriel, nous allons parcourir **comment définir le DPI** pendant que vous **convertissez SVG en PNG** à l’aide de la bibliothèque Aspose. Vous obtiendrez un exemple de code complet, prêt à être exécuté, une explication de chaque option de configuration, et une poignée de conseils pratiques pour des projets réels. Aucun référentiel externe requis — tout ce dont vous avez besoin se trouve ici.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

- Java 17 (ou tout JDK récent) installé.  
- Maven ou Gradle pour gérer les dépendances (nous montrerons l’extrait Maven).  
- Un fichier SVG que vous souhaitez rasteriser (par ex., `logo.svg`).  
- Une compréhension de base de la syntaxe Java — rien de compliqué, juste le traditionnel `public static void main`.

Si l’un de ces éléments manque, procurez‑le‑vous d’abord ; le reste du guide suppose qu’ils sont déjà en place.

## Dépendance Maven

Ajoutez la dépendance Aspose HTML for Java à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Les utilisateurs de Gradle peuvent remplacer cet extrait par la ligne équivalente `implementation "com.aspose:aspose-html:23.12"`.

## Étape 1 : Créer l’objet d’options de conversion

La première chose à faire est d’instancier `SvgConversionOptions`. Cet objet contient chaque réglage que vous pourriez vouloir — DPI, couleur d’arrière‑plan, mise à l’échelle, etc.

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

Pourquoi c’est important : sans définir explicitement le DPI, Aspose utilise par défaut 96 dpi, ce qui convient au web mais est loin d’être prêt pour l’impression. En créant l’objet d’options, vous obtenez un contrôle total sur le processus de rasterisation.

## Étape 2 : Définir le DPI souhaité

Nous répondons maintenant à la question centrale : **comment définir le DPI**. La méthode `setDpi(int)` attend un entier simple ; les valeurs typiques vont de 72 dpi (faible résolution) à 1200 dpi (ultra‑haute résolution). Pour la plupart des travaux d’impression, 300 dpi est le point idéal ; pour les logos qui doivent être agrandis, 600 dpi est un choix sûr.

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **Astuce :** les valeurs de DPI qui ne sont pas multiples de 72 peuvent parfois produire des dimensions de pixels non entières. Si vous avez besoin d’une taille de pixel exacte, calculez `pixel = inches * DPI` au préalable et ajustez le `viewBox` du SVG en conséquence.

## Étape 3 : Gérer la transparence avec une couleur d’arrière‑plan

Les SVG contiennent souvent des zones transparentes. PNG prend en charge la transparence, mais si vous ciblez un flux de travail d’impression qui attend un arrière‑plan opaque, vous voudrez le remplacer. La méthode `setBackgroundColor(String)` accepte n’importe quelle chaîne de couleur compatible CSS.

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

Vous pouvez également utiliser `#FFFFFF`, `rgb(255,255,255)`, ou même `transparent` si vous *voulez* conserver le canal alpha.

## Étape 4 : Effectuer la conversion

Une fois les options configurées, la conversion proprement dite se résume à un appel statique unique à `Converter.convert`. Fournissez le chemin du SVG d’entrée, le chemin de sortie PNG souhaité, et l’objet d’options.

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

C’est tout — Aspose se charge d’analyser le SVG, d’appliquer le redimensionnement DPI, de remplir l’arrière‑plan, et d’écrire le fichier PNG sur le disque.

## Exemple complet, exécutable

Ci‑dessous se trouve la classe Java complète que vous pouvez copier‑coller dans un fichier nommé `SvgToPngHighRes.java`. Remplacez `YOUR_DIRECTORY` par le chemin réel de votre dossier.

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### Résultat attendu

L’exécution du programme générera `logo.png` dans le même dossier. Ouvrez le fichier dans un visualiseur d’images et inspectez les **propriétés de l’image** — vous devriez voir :

- **Résolution :** 600 dpi (ou la valeur que vous avez définie)  
- **Dimensions :** mises à l’échelle selon le `viewBox` original du SVG multiplié par le facteur DPI  
- **Arrière‑plan :** blanc uni (aucun pixel transparent)

Si vous ouvrez le PNG dans un outil comme Photoshop, les métadonnées DPI seront visibles sous *Image → Taille de l’image*.

## Cas limites courants et comment les gérer

| Situation | Points d’attention | Solution recommandée |
|-----------|-------------------|----------------------|
| **Fichier SVG manquant** | `FileNotFoundException` lancé par `Converter.convert` | Validez le chemin avant la conversion avec `Files.exists(Paths.get(...))`. |
| **Fonctionnalités SVG non prises en charge** (par ex., filtres non implémentés) | Aspose peut ignorer ces fonctionnalités silencieusement | Utilisez `SvgConversionOptions.setEnableSvgFilters(true)` si vous avez besoin du support des filtres (disponible dans les versions récentes). |
| **DPI très élevé (≥1200)** | Le fichier de sortie peut devenir gigantesque (des centaines de Mo) | Envisagez le streaming du résultat ou réduisez le DPI pour les images volumineuses. |
| **Conservation de la transparence** | Vous avez défini une couleur d’arrière‑plan alors que vous vouliez garder l’alpha | Omettez `setBackgroundColor` ou passez `"transparent"` pour conserver le canal alpha d’origine. |
| **Conversion par lots** | Recréer `SvgConversionOptions` pour chaque fichier est coûteux | Créez une seule instance de `SvgConversionOptions` et réutilisez‑la dans une boucle. |

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec d’autres formats raster comme JPEG ou BMP ?**  
R : Oui. Remplacez l’extension du fichier de sortie (`.png`) par `.jpg` ou `.bmp`, et Aspose sélectionnera automatiquement l’encodeur approprié. Vous pouvez également affiner la qualité JPEG via `JpegConversionOptions`.

**Q : Puis‑je convertir des SVG stockés dans un tableau d’octets plutôt que dans un fichier ?**  
R : Absolument. Utilisez les surcharges `Converter.convert(InputStream, OutputStream, conversionOptions)` pour travailler avec des flux, ce qui est pratique pour les services web.

**Q : Le réglage du DPI est‑il identique à la mise à l’échelle de l’image ?**  
R : Le DPI est une balise de métadonnées qui indique aux imprimantes combien de pixels représentent un pouce. En interne, Aspose met à l’échelle l’image raster pour correspondre au DPI, de sorte que la taille visuelle change si vous visualisez le PNG à 100 % dans un visualiseur qui respecte le DPI.

## Astuces pro pour un code prêt pour la production

1. **Mettre en cache les options** – Si vous convertissez des dizaines de logos avec le même DPI et la même couleur d’arrière‑plan, créez `SvgConversionOptions` une seule fois et réutilisez‑le. Cela réduit la surcharge de création d’objets.  
2. **Valider les dimensions d’entrée** – Pour des SVG extrêmement grands, calculez la taille de pixel attendue (`width * DPI/96`) et arrêtez le processus si elle dépasse un seuil sûr (par ex., 20 000 px) afin d’éviter `OutOfMemoryError`.  
3. **Journaliser les métadonnées de conversion** – Enregistrez le DPI, le nom du fichier source et le horodatage dans un fichier de log ; cela simplifie le débogage ultérieur.  
4. **Sécurité des threads** – `Converter.convert` est thread‑safe, vous pouvez donc paralléliser les traitements par lots avec un `ExecutorService`.

## Résumé visuel

![exemple de réglage du DPI](image.png){: .align-center alt="exemple de réglage du DPI"}

Le diagramme ci‑dessus illustre le flux : **SVG → définir DPI & arrière‑plan → PNG**.

## Conclusion

Vous savez maintenant **comment définir le DPI** lorsque vous **convertissez SVG en PNG** avec Aspose HTML for Java. En configurant `SvgConversionOptions`, vous contrôlez la résolution, la gestion de l’arrière‑plan, et bien plus, transformant un simple fichier vectoriel en une image raster prête à l’impression en quelques lignes de code.

Passez à l’étape suivante et expérimentez :

- Conversion d’un dossier complet de SVG en boucle batch.  
- Changement du format de sortie en JPEG pour des actifs optimisés web.  
- Utilisation d’autres options de conversion Aspose comme `setScaleX/Y` pour un redimensionnement personnalisé au‑delà du DPI.

Bon codage, et que vos PNG restent toujours aussi nets que vous le désirez !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}