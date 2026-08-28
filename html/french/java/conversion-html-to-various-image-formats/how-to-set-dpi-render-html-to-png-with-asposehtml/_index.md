---
category: general
date: 2026-01-14
description: Comment définir le DPI lors de la conversion d’une URL en PNG. Apprenez
  à rendre du HTML en PNG, à définir la taille du viewport et à enregistrer du HTML
  en PNG en utilisant Aspose.HTML en Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: fr
og_description: Comment définir le DPI lors de la conversion d’une URL en PNG. Guide
  étape par étape pour rendre le HTML en PNG, contrôler la taille du viewport et enregistrer
  le HTML en PNG avec Aspose.HTML.
og_title: Comment définir le DPI – Rendre le HTML en PNG avec AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: Comment définir le DPI – Rendre le HTML en PNG avec AsposeHTML
url: /fr/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment définir le DPI – Rendu HTML en PNG avec AsposeHTML

Vous vous êtes déjà demandé **comment définir le DPI** pour une image de type capture d'écran générée à partir d'une page web ? Peut‑être avez‑vous besoin d'un PNG à 300 DPI pour l'impression, ou d'une vignette basse résolution pour une application mobile. Dans les deux cas, l'astuce consiste à indiquer au moteur de rendu le DPI logique souhaité, puis le laisser faire le travail lourd.  

Dans ce tutoriel, nous prendrons une URL en direct, la rendrons en fichier PNG, **définirons la taille du viewport**, ajusterons le DPI, et enfin **enregistrerons le HTML en PNG** — le tout avec Aspose.HTML pour Java. Aucun navigateur externe, aucun outil en ligne de commande encombrant — juste du code Java propre que vous pouvez intégrer à n'importe quel projet Maven ou Gradle.

> **Astuce :** Si vous ne cherchez qu'une vignette rapide, vous pouvez garder le DPI à 96 DPI (la valeur par défaut pour la plupart des écrans). Pour des actifs prêts à l'impression, montez-le à 300 DPI ou plus.

![exemple de comment définir le DPI](https://example.com/images/how-to-set-dpi.png "exemple de comment définir le DPI")

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent).  
- **Aspose.HTML for Java** 24.10 ou plus récent. Vous pouvez le récupérer depuis Maven Central :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Une connexion Internet pour récupérer la page cible (l'exemple utilise `https://example.com/sample.html`).  
- Permission d'écriture sur le dossier de sortie.

C’est tout — pas de Selenium, pas de Chrome headless. Aspose.HTML effectue le rendu en‑processus, ce qui signifie que vous restez dans la JVM et évitez le surcoût du lancement d'un navigateur.

## Étape 1 – Charger le document HTML depuis une URL

Tout d'abord, nous créons une instance `HTMLDocument` pointant vers la page que nous voulons capturer. Le constructeur télécharge automatiquement le HTML, le parse, et prépare le DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Pourquoi c’est important :* En chargeant le document directement, vous évitez d'avoir besoin d'un client HTTP séparé. Aspose.HTML respecte les redirections, les cookies, et même l'authentification de base si vous intégrez les identifiants dans l'URL.

## Étape 2 – Construire un sandbox avec le DPI et la taille de la fenêtre souhaités

Un **sandbox** est la façon dont Aspose.HTML imite un environnement de navigateur. Ici, nous lui indiquons de se comporter comme un écran 1280 × 720 et, surtout, nous définissons le **device DPI**. Modifier le DPI change la densité de pixels de l'image rendue sans altérer la taille logique.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Pourquoi vous pourriez ajuster ces valeurs :*  
- **Viewport size** contrôle le comportement des media queries CSS (`@media (max-width: …)`).  
- **Device DPI** influence la taille physique de l'image lorsqu'elle est imprimée. Une image à 96 DPI convient aux écrans ; une image à 300 DPI conserve sa netteté sur papier.  

Si vous avez besoin d'une vignette carrée, changez simplement `setViewportSize(500, 500)` et gardez le DPI bas.

## Étape 3 – Choisir PNG comme format de sortie

Aspose.HTML prend en charge plusieurs formats raster (PNG, JPEG, BMP, GIF). PNG est sans perte, ce qui le rend parfait pour les captures d'écran où chaque pixel doit être préservé.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Vous pouvez également ajuster le niveau de compression (`pngOptions.setCompressionLevel(9)`) si la taille du fichier vous préoccupe.

## Étape 4 – Rendre et enregistrer l'image

Nous indiquons maintenant au document de **save** lui‑même sous forme d'image. La méthode `save` accepte un chemin de fichier et les options préalablement configurées.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Lorsque le programme se termine, vous trouverez un fichier PNG à `YOUR_DIRECTORY/sandboxed.png`. Ouvrez‑le — si vous avez défini le DPI à 300, les métadonnées de l'image le refléteront, même si les dimensions en pixels restent 1280 × 720.

## Étape 5 – Vérifier le DPI (Optionnel mais pratique)

Si vous voulez revérifier que le DPI a bien été appliqué, vous pouvez lire les métadonnées PNG avec une bibliothèque comme **metadata‑extractor** :

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Vous devriez voir `300` (ou la valeur que vous avez définie) affichée dans la console. Cette étape n’est pas requise pour le rendu, mais constitue une vérification rapide, surtout lorsque vous générez des actifs pour un flux de travail d’impression.

## Questions fréquentes & cas particuliers

### « Et si la page utilise JavaScript pour charger du contenu ? »

Aspose.HTML exécute un **subset limité** de JavaScript. Pour la plupart des sites statiques, cela fonctionne immédiatement. Si la page dépend fortement de frameworks côté client (React, Angular, Vue), vous pourriez devoir pré‑rendre la page ou utiliser un navigateur headless à la place. Cependant, la définition du DPI fonctionne de la même façon une fois le DOM prêt.

### « Puis‑je rendre un PDF au lieu d’un PNG ? »

Absolument. Remplacez `ImageSaveOptions` par `PdfSaveOptions` et changez l’extension de sortie en `.pdf`. Le réglage du DPI influence toujours l’apparence rasterisée de toute image intégrée.

### « Qu’en est‑il des captures d’écran haute résolution pour les écrans Retina ? »

Il suffit de doubler les dimensions du viewport tout en conservant le DPI à 96 DPI, ou de garder le même viewport et d’augmenter le DPI à 192. Le PNG résultant contiendra deux fois plus de pixels, vous offrant cet aspect net propre aux écrans Retina.

### « Dois‑je nettoyer les ressources ? »

`HTMLDocument` implémente `AutoCloseable`. Dans une application de production, encapsulez‑le dans un bloc try‑with‑resources :

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Cela garantit que les ressources natives sont libérées rapidement.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être exécuté. Remplacez `YOUR_DIRECTORY` par un dossier réel sur votre machine.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Exécutez la classe, et vous obtiendrez un PNG qui respecte le paramètre **comment définir le DPI** que vous avez spécifié.

## Conclusion

Nous avons parcouru **comment définir le DPI** lors du **rendu HTML en PNG**, couvert l’étape **définir la taille du viewport**, et montré comment **enregistrer le HTML en PNG** en utilisant Aspose.HTML pour Java. Les points clés sont :

- Utilisez un **sandbox** pour contrôler le DPI et le viewport.  
- Choisissez les bons **ImageSaveOptions** pour une sortie sans perte.  
- Vérifiez les métadonnées DPI si vous devez garantir la qualité d’impression.  

À partir d’ici, vous pouvez expérimenter avec différentes valeurs de DPI, des viewports plus grands, ou même traiter un lot d’URL. Vous voulez convertir tout un site web en vignettes PNG ? Il suffit de boucler sur un tableau d’URL et de réutiliser la même configuration de sandbox.

Bon rendu, et que vos captures d’écran soient toujours pixel‑perfect !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}