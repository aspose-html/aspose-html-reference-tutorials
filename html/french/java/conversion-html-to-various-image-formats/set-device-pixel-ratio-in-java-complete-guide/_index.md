---
category: general
date: 2026-02-22
description: Définissez le ratio de pixels de l’appareil en Java avec le bac à sable
  Aspose.HTML. Apprenez à définir un agent utilisateur personnalisé, à obtenir le
  titre de la page en Java et à convertir du HTML en PNG dans un seul tutoriel.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: fr
og_description: Définir le ratio de pixels de l’appareil en Java avec le bac à sable
  Aspose.HTML. Ce tutoriel montre comment définir un agent utilisateur personnalisé,
  récupérer le titre de la page en Java et convertir du HTML en PNG.
og_title: Définir le ratio de pixels de l'appareil en Java – Guide complet
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Définir le ratio de pixels de l’appareil en Java – Guide complet
url: /fr/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

. Should keep as is.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le Device Pixel Ratio en Java – Guide complet

Vous vous êtes déjà demandé comment **définir le device pixel ratio** lors du rendu d’une page web depuis Java ? Vous n’êtes pas seul. De nombreux développeurs doivent émuler des écrans mobiles haute‑DPI afin que les captures d’écran soient nettes, surtout lorsqu’ils **enregistrent du html en image** pour des rapports ou des supports marketing. Dans ce tutoriel, nous allons parcourir un exemple pratique qui fait exactement cela — tout en vous montrant comment **définir un user‑agent personnalisé**, **obtenir le titre de la page java**, et **convertir du html en png** à l’aide d’Aspose.HTML.

Nous commencerons par un bref aperçu de l’API sandbox, puis nous détaillerons chaque étape de configuration, et enfin nous produirons un fichier PNG qui reproduit l’affichage d’un véritable iPhone. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet Java. Aucun outil externe requis, juste du Java pur et Aspose.HTML 7.x (ou plus récent).

---

## Prérequis

- Java 17 ou ultérieur (le code compile avec des versions antérieures mais 17 est recommandé).
- Bibliothèque Aspose.HTML for Java (téléchargeable depuis le site officiel d’Aspose ; coordonnées Maven : `com.aspose:aspose-html:23.10`).
- Un IDE ou éditeur de texte de votre choix (IntelliJ IDEA, VS Code, Eclipse… tout fonctionne).
- Accès Internet pour l’URL de démonstration (`https://example.com/responsive.html`), ou remplacez‑la par n’importe quelle page HTML publique que vous possédez.

> **Astuce :** Si vous êtes derrière un proxy, configurez les propriétés système du JVM `http.proxyHost` et `http.proxyPort` avant d’exécuter le code.

---

## Étape 1 : Définir le Device Pixel Ratio et les autres options du sandbox

La première chose dont nous avons besoin est une instance **SandboxOptions** où nous définissons la taille d’écran virtuelle et le *device pixel ratio* (DPR). Pensez au DPR comme le facteur qui indique au navigateur combien de pixels physiques correspondent à un pixel CSS. Sur un iPhone Retina, le DPR est généralement **2.0**, c’est pourquoi nous utiliserons cette valeur.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Pourquoi c’est important :** Sans définir le bon DPR, l’image rendue apparaîtra floue ou surdimensionnée parce que le rasteriseur suppose un mappage 1 : 1 pixel.

---

## Étape 2 : Définir un User‑Agent personnalisé

Les sites web servent souvent un balisage différent selon l’en‑tête **User‑Agent**. Pour que notre page se comporte comme sur un vrai iPhone, nous injectons une chaîne personnalisée qui imite Safari sur iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Cas particulier :** Certains sites inspectent également l’en‑tête `Accept-Language`. Si vous remarquez des traductions manquantes, ajoutez `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Étape 3 : Charger la page dans le sandbox et obtenir le titre

Nous lançons maintenant le sandbox avec les options que nous venons de définir. L’objet **Sandbox** isole le processus de rendu, garantissant que nos réglages de DPR et de user‑agent sont respectés.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Une fois la page chargée, récupérer le titre est aussi simple que d’appeler `getTitle()`. Cela satisfait le besoin **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Sortie console attendue**

```
Title: Responsive Demo – Mobile View
```

Si le titre est vide, revérifiez l’URL ou assurez‑vous que la page n’est pas bloquée par des politiques CORS.

---

## Étape 4 : Convertir le HTML en PNG et enregistrer le HTML en image

Aspose.HTML vous permet de rendre le DOM directement dans un fichier image. Parce que nous avons déjà fixé le DPR à 2.0, le PNG résultant aura une densité de pixels doublée, produisant une capture nette.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

La méthode `save` détecte automatiquement l’extension du fichier et choisit le rendu approprié. Si vous avez besoin d’un autre format (JPEG, BMP), il suffit de changer le nom du fichier en conséquence.

> **Et si vous avez besoin d’une taille d’image spécifique ?**  
> Utilisez `ImageSaveOptions` pour contrôler la largeur, la hauteur et la couleur de fond :

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté, qui réunit toutes les étapes. Copiez‑collez‑le dans un fichier `SandboxDemo.java`, ajoutez la dépendance Aspose.HTML, puis lancez `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

L’exécution du programme produit deux fichiers PNG :

| Fichier | Description |
|---------|-------------|
| `mobile_view.png` | Rendu par défaut avec le DPR configuré. |
| `mobile_view_custom.png` | Rendu avec largeur/hauteur explicites (utile pour des actifs à taille fixe). |

Vous pouvez ouvrir l’un ou l’autre fichier avec n’importe quel visualiseur d’images pour vérifier la sortie haute résolution.

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si la page contient du JavaScript qui modifie le DOM après le chargement ?** | Aspose.HTML exécute les scripts par défaut. Si vous avez besoin d’une capture statique avant l’exécution du script, définissez `sandboxOptions.setEnableJavaScript(false)`. |
| **Puis‑je rendre une page qui nécessite une authentification ?** | Oui. Utilisez `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` ou injectez des cookies via `sandboxOptions.getCookies().add(...)`. |
| **Le DPR est‑il limité à 2.0 ?** | Non. Vous pouvez définir n’importe quel double positif (par ex. 3.0 pour des appareils ultra‑haute‑DPI). Gardez à l’esprit qu’un DPR plus élevé génère des fichiers image plus volumineux. |
| **Comment gérer les pages avec de gros actifs (images, polices) ?** | Augmentez la limite de mémoire du sandbox avec `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (octets). Cela évite les erreurs d’out‑of‑memory sur les pages lourdes. |
| **Dois‑je fermer le sandbox manuellement ?** | Le `Sandbox` implémente `AutoCloseable`. Encapsulez‑le dans un bloc try‑with‑resources pour un nettoyage automatique. |

---

## Conclusion

Nous avons montré comment **définir le device pixel ratio** dans un sandbox Java, **définir un user‑agent personnalisé**, **obtenir le titre de la page java**, et **convertir du html en png** (effectivement **save html as image**) à l’aide d’Aspose.HTML. L’exemple complet illustre un flux de travail pratique que vous pouvez adapter pour la génération automatisée de captures d’écran, les tests de régression visuelle, ou tout scénario nécessitant une représentation pixel‑parfait d’une page web.

N’hésitez pas à expérimenter — changez le DPR à 3.0, remplacez le user‑agent par une chaîne Android, ou pointez l’URL vers un fichier HTML local. Le même schéma fonctionne pour les PDF, les SVG, ou même le rendu multi‑pages.

Si ce guide vous a été utile, explorez des sujets connexes comme **la génération de PDF avec Aspose.HTML**, **les alternatives à Chrome headless**, ou **le rendu en lot de plusieurs URL**. Bon codage, et que vos captures d’écran restent toujours ultra‑nettes !

![définir le device pixel ratio dans le sandbox Java](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}