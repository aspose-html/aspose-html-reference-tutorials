---
category: general
date: 2026-05-31
description: Désactivez les images externes lors du rendu d’une page Web en PNG en
  Java avec Aspose HTML. Apprenez à charger la page Web en toute sécurité dans un
  bac à sable et à enregistrer le document HTML au format PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: fr
og_description: Désactiver les images externes lors du rendu d’une page Web en PNG
  en Java. Ce guide étape par étape montre comment charger une page Web dans un bac
  à sable et enregistrer le document HTML en PNG.
og_title: Désactiver les images externes lors du rendu d'une page Web en PNG en Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Désactiver les images externes lors du rendu d’une page Web en PNG en Java
url: /fr/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Désactiver les images externes lors du rendu d'une page Web en PNG avec Java

Vous avez déjà eu besoin de **désactiver les images externes** lorsque vous rendez une page Web en PNG avec Java ? Peut-être que vous créez un service de vignettes qui doit rester isolé d'Internet public, ou vous voulez simplement garantir qu'aucune image tierce ne fuit pendant la conversion. Dans tous les cas, vous êtes au bon endroit.

Dans ce tutoriel, nous allons parcourir le chargement d’une page Web dans un sandbox, désactiver la récupération d’images externes, puis enregistrer le document HTML en fichier PNG — le tout avec Aspose.HTML for Java. À la fin, vous disposerez d’un exemple prêt à l’emploi, ainsi que de plusieurs astuces pratiques pour éviter les pièges habituels.

## Ce que vous apprendrez

- **Comment rendre du HTML en image Java** en utilisant `Converter` d’Aspose.HTML.
- Les étapes exactes pour **charger une page web dans un sandbox** avec une fenêtre d’affichage personnalisée et DPI.
- La configuration nécessaire pour **désactiver les images externes** tout en rendant la page.
- Comment **enregistrer le document HTML en PNG** (ou tout autre format supporté) sur le disque.
- Gestion des cas limites, conseils de performance et astuces de dépannage.

### Prérequis

- Java 8 ou plus récent installé (le code fonctionne également avec JDK 11+).
- Maven ou Gradle pour récupérer la bibliothèque Aspose.HTML for Java.
- Une connaissance de base de la syntaxe Java et de la gestion des exceptions.
- Une connexion Internet pour le chargement initial de la page (à moins que vous ne serviez le HTML localement).

> **Conseil pro :** Si vous travaillez derrière un proxy d'entreprise, définissez les propriétés JVM `http.proxyHost` et `http.proxyPort` avant d'exécuter l'exemple.

---

## Étape 1 : Configurer votre projet et ajouter Aspose.HTML

Tout d'abord, ajoutez la dépendance Aspose.HTML. Si vous utilisez Maven, insérez ceci dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Pour Gradle, l’équivalent est :

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Une fois la bibliothèque sur le classpath, vous êtes prêt à commencer à coder.

---

## Étape 2 : **Désactiver les images externes** avec un environnement Sandbox

Le cœur de la solution réside dans `DocumentSandbox`. En passant `false` pour le drapeau *allowExternalImages*, nous indiquons à Aspose.HTML d’ignorer les balises `<img>` pointant vers des URL en dehors du sandbox. C’est le mécanisme exact qui **désactive les images externes**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Pourquoi c’est important :** Sans le sandbox, le moteur de rendu tenterait de télécharger chaque image référencée par la page, ce qui peut être lent, peu fiable, voire représenter un risque de sécurité. Mettre le drapeau à `false` garantit un passage de rendu propre et autonome.

---

## Étape 3 : **Charger la page Web dans le Sandbox**  

Nous pointons maintenant Aspose.HTML vers l’URL que nous voulons capturer. Le constructeur `HTMLDocument` accepte l’instance du sandbox, appliquant automatiquement les restrictions que nous venons de définir.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Si la page dépend fortement de scripts externes pour la mise en page, vous pourriez remarquer du contenu manquant parce que nous avons également désactivé les scripts. Dans ce cas, basculez le drapeau `allowExternalScripts` à `true` tout en gardant `allowExternalImages` à `false`.

---

## Étape 4 : **Rendre la page Web en PNG**  

Avec le document chargé, le convertir en image se fait en une seule ligne grâce à `Converter.convert`. L’objet `ImageSaveOptions` vous permet de choisir le format de sortie ; ici nous optons pour PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Le fichier résultant, `sandboxed.png`, contient un instantané de la page **sans aucune image externe** — seules les SVG inline ou les graphiques encodés en base64 restent, le cas échéant.

---

## Étape 5 : Vérifier la sortie et déboguer les problèmes courants

Après avoir exécuté le programme, ouvrez `sandboxed.png` avec n’importe quel visualiseur d’images. Vous devriez voir la mise en page, le texte et le style CSS, mais tous les éléments `<img src="http://…">` seront vides (souvent rendus comme un rectangle blanc ou tout simplement omis).

### Problèmes typiques et comment les résoudre

| Symptom | Likely cause | Fix |
|---|---|---|
| Page blanche | L’URL cible a bloqué la requête (ex. : Cloudflare) | Ajoutez les en‑têtes appropriés à l’agent‑utilisateur du sandbox ou utilisez un proxy. |
| Polices manquantes | Les fichiers de police sont hébergés à l’extérieur | Installez les polices localement ou intégrez‑les via `@font-face` avec des data URIs. |
| Décalage de mise en page | Le CSS référence des feuilles de style externes qui ont été bloquées | Réglez `allowExternalScripts` à `true` *uniquement* pour le chargement du CSS, puis relancez. |
| `java.lang.OutOfMemoryError` | Rendu d’une page très grande à haute résolution DPI | Réduisez la taille de la fenêtre d’affichage ou le DPI, ou augmentez le heap JVM (`-Xmx2g`). |

---

## Étape 6 : Étendre l’exemple – Enregistrer dans d’autres formats

Le même code fonctionne pour JPEG, BMP ou même PDF. Il suffit de changer l’énumération `SaveFormat` :

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Si vous avez besoin d’un PDF à la place, remplacez `ImageSaveOptions` par `PdfSaveOptions` et ajustez l’extension du fichier en conséquence.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le **programme complet et exécutable**. Créez une nouvelle classe Java, collez le code, assurez‑vous que le répertoire `output` existe, puis lancez‑le.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Sortie attendue** (console) :

```
PNG image saved to: output/sandboxed.png
```

Ouvrez `sandboxed.png` — vous verrez la page rendue **sans aucune image externe**.

---

## Questions fréquentes

**Q : Puis‑je toujours afficher les images intégrées dans le HTML ?**  
R : Oui. Les URIs `data:` inline ou les images encodées en base64 sont traitées comme faisant partie du document et apparaîtront dans le PNG.

**Q : Et si je dois garder certaines images externes tout en bloquant d’autres ?**  
R : Le sandbox fonctionne comme un commutateur tout‑ou‑rien. Pour un contrôle fin, téléchargez vous‑même les images autorisées, intégrez‑les en tant que data URIs, puis effectuez le rendu.

**Q : Cette approche fonctionne‑t‑elle sur des serveurs sans affichage (headless) ?**  
R : Absolument. Aspose.HTML est une bibliothèque pure Java ; elle ne nécessite aucun serveur d’affichage ni moteur de navigateur.

**Q : En quoi cela diffère‑t‑il de Selenium ou Puppeteer ?**  
R : Selenium pilote un vrai navigateur, ce qui est lourd et plus difficile à sandboxer. Aspose.HTML rend le HTML directement en mémoire, offrant des performances déterministes et des contrôles de sécurité plus simples comme **désactiver les images externes**.

---

## Conclusion

Vous disposez maintenant d’une recette complète, de bout en bout, pour **désactiver les images externes lors du rendu d’une page Web en PNG avec Java**. En tirant parti de `DocumentSandbox`, vous obtenez un contrôle strict sur les ressources externes autorisées, garantissant à la fois sécurité et reproductibilité. Vous pouvez maintenant expérimenter avec différentes tailles de fenêtre d’affichage, réglages DPI ou formats de sortie — chaque ajustement ouvre de nouvelles possibilités pour générer des vignettes, des aperçus ou des instantanés d’archives.

Prêt pour le prochain défi ? Essayez de rendre un lot d’URL en parallèle, ou intégrez cette logique dans un micro‑service Spring Boot qui renvoie des PNG à la demande. Le ciel est la limite quand on combine la flexibilité d’Aspose.HTML avec les outils de concurrence de Java.

Bon codage, et n’oubliez pas de partager vos succès dans les commentaires !

## Que devriez‑vous apprendre ensuite ?

- [Comment utiliser Aspose pour rendre du HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Comment rendre du HTML en PNG avec Aspose – Guide complet](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Comment modifier le CSS – Édition avancée du CSS externe avec Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}