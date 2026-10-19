---
category: general
date: 2026-10-19
description: Définir le device pixel ratio en Java à l'aide du sandbox Aspose.HTML.
  Apprenez comment définir la largeur et la hauteur de l'écran et obtenir le titre
  de la page java avec un exemple complet et exécutable.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Obtenir le titre de la page java avec le sandbox Aspose.HTML. Ce guide
  vous montre comment définir la largeur et la hauteur de l'écran et le device pixel
  ratio en Java en quelques étapes simples.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Obtenir le titre de la page java – set device pixel ratio dans le tutoriel
  sandbox Java
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Obtenir le titre de la page java – set device pixel ratio dans le tutoriel
  sandbox Java
url: /fr/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir le titre de la page java – définir le ratio de pixels du dispositif dans le tutoriel sandbox Java

Vous avez déjà eu besoin de **définir le ratio de pixels du dispositif** lors du test d’un site réactif en Java ? Vous n’êtes pas le seul. De nombreux développeurs se heurtent à un problème lorsque la page est parfaite sur le bureau mais se casse sur les téléphones à haute résolution DPI. Bonne nouvelle ? Avec le sandbox d’Aspose.HTML, vous pouvez émuler un iPhone X (ou tout autre appareil) directement depuis votre code Java—sans navigateur requis.

Dans ce guide, nous parcourrons **comment définir la largeur et la hauteur de l’écran**, configurer le **ratio de pixels du dispositif**, et enfin **obtenir le titre de la page java** pour vérifier que tout a été rendu correctement. À la fin, vous disposerez d’un programme autonome que vous pourrez intégrer à n’importe quel projet et commencer à tester les mises en page mobiles instantanément.

## Réponses rapides
- **Comment définir le ratio de pixels du dispositif en Java ?** Utilisez `SandboxOptions.setDevicePixelRatio(double)` avant de créer le sandbox.  
- **Quelle méthode renvoie le titre de la page ?** Appelez `htmlDocument.getTitle()` sur le `HTMLDocument` chargé.  
- **Puis-je émuler d’autres appareils ?** Oui—créez un nouveau `SandboxOptions` avec la largeur, la hauteur et le ratio de pixels souhaités.  
- **Ai‑je besoin d’un pilote de navigateur ?** Non, le sandbox d’Aspose.HTML est sans tête et s’exécute uniquement en Java.  
- **Quelle version d’Aspose.HTML est requise ?** La version 23.7 ou ultérieure prend en charge toutes les fonctionnalités d’émulation mobile.

## Qu’est‑ce que get page title java ?
`get page title java` est l’opération consistant à récupérer l’élément `<title>` d’un document HTML à l’aide de code Java. Cela vous permet de confirmer qu’une page chargée dans un contexte de dispositif virtuel a rendu le titre attendu. Récupérer le titre est une étape courante dans la validation automatisée afin de s’assurer que la bonne page a été chargée après l’application des paramètres d’émulation du dispositif.

## Pourquoi utiliser le sandbox Aspose.HTML pour l’émulation mobile ?
Aspose.HTML prend en charge **plus de 30** formats d’entrée et de sortie—y compris HTML, CSS, SVG et PDF—et peut rendre les pages sans lancer de navigateur complet. Son sandbox traite des sites de plusieurs centaines de pages tout en maintenant l’utilisation de la mémoire en dessous de 200 Mo, ce qui le rend idéal pour les pipelines CI.

## Prérequis

- Java 8 ou plus récent (le code compile également avec JDK 11)  
- Bibliothèque Aspose.HTML pour Java (version 23.7 ou ultérieure) – vous pouvez la récupérer depuis Maven Central  
- Un IDE ou une configuration simple en ligne de commande `javac`  
- Accès Internet pour l’URL de démonstration (`https://responsive.example.com`)

Aucun framework supplémentaire, pas de Selenium, juste du Java pur et Aspose.HTML.

## Comment définir la largeur et la hauteur de l’écran ainsi que le ratio de pixels du dispositif en Java

La classe `SandboxOptions` vous permet de spécifier les dimensions d’écran et la densité de pixels du dispositif virtuel. Pour émuler un appareil mobile spécifique, vous devez configurer le sandbox avec la largeur, la hauteur et le ratio de pixels du dispositif souhaités. En créant un objet `SandboxOptions` et en définissant ces propriétés, le moteur de rendu traitera la page comme si elle était affichée sur cet appareil, garantissant que les media queries CSS et le redimensionnement des images se comportent correctement.

Créez une instance de `SandboxOptions`, définissez la largeur à **375**, la hauteur à **812**, et le ratio de pixels du dispositif à **3.0**. Ensuite, transmettez ces options à un nouveau `Sandbox`. Cela configure entièrement le dispositif virtuel avant le chargement de toute page.

La classe `SandboxOptions` définit la taille d’écran et la densité de pixels du dispositif virtuel. C’est le point d’entrée pour tout scénario d’émulation mobile.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Pourquoi c’est important :**  
> L’appel `setDevicePixelRatio` met à l’échelle tout—des images au rendu des polices—de sorte que la page pense qu’elle est sur un vrai téléphone. Si vous l’omettez, la mise en page peut revenir aux media queries CSS de type bureau, contrecarrant l’objectif du test mobile.

## Comment créer l’instance du sandbox

La classe `Sandbox` représente un environnement de navigateur sans tête qui rend le HTML en utilisant les options définies précédemment. Après avoir configuré `SandboxOptions`, créez une instance de `Sandbox` avec ces options pour obtenir un contexte de rendu isolé. Ce sandbox agit comme un navigateur léger, appliquant la taille d’écran et la densité de pixels que vous avez spécifiées, et peut être réutilisé pour plusieurs chargements de pages tout en gardant l’environnement propre.

Instanciez un `Sandbox` avec les `SandboxOptions` préalablement configurés. Le sandbox se comporte comme un petit navigateur sans tête qui respecte les dimensions et le ratio de pixels que vous avez définis.

L’objet `Sandbox` est le moteur de rendu isolé d’Aspose.HTML qui s’exécute sans interface utilisateur. Il garantit que chaque test s’exécute dans un environnement propre.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Astuce :** Vous pouvez réutiliser le même objet `Sandbox` pour plusieurs chargements de pages ; il suffit de changer l’URL et le sandbox conservera les mêmes caractéristiques du dispositif.

## Comment charger la page dans le sandbox

La classe `HTMLDocument` représente un fichier HTML analysé en mémoire, offrant un accès au DOM et des capacités de rendu. Avec le sandbox prêt, créez un `HTMLDocument` en passant l’URL cible et l’instance du sandbox. Cela charge et rend la page en utilisant les paramètres du dispositif virtuel, vous permettant d’interagir avec le DOM ou d’extraire des informations telles que le titre.

Créez un `HTMLDocument` en passant l’URL cible et l’instance `Sandbox`. Cela force le document à se rendre en utilisant le dispositif virtuel que vous avez défini précédemment.

La classe `HTMLDocument` représente un fichier HTML analysé en mémoire et fournit des méthodes pour la manipulation du DOM et l’extraction des métadonnées.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Si l’URL est inaccessible ou que la page contient des erreurs, Aspose.HTML lèvera une exception. Pour du code de production, vous envelopperiez cela dans un `try‑catch` et enregistreriez l’échec, mais le tutoriel reste simple.

## Comment vérifier avec get page title java

La méthode `getTitle()` renvoie le contenu de l’élément `<title>` du document HTML sous forme de chaîne simple. Lire le titre est le contrôle de cohérence le plus rapide. Après le chargement de la page, appelez `htmlDocument.getTitle()` pour récupérer le texte du titre. Cette vérification simple confirme que la page a été rendue correctement sous les paramètres du dispositif émulé et offre un moyen rapide de valider la navigation ou les changements de contenu dans les tests automatisés.

Appelez `htmlDocument.getTitle()` sur le document chargé et affichez le résultat. Si le sandbox a correctement appliqué le **ratio de pixels du dispositif**, le titre correspondra à ce que vous verriez sur un vrai iPhone X.

La méthode `getTitle()` renvoie le contenu de l’élément `<title>` sous forme de chaîne simple, vous permettant de valider le rendu sans inspection visuelle.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Sortie attendue (exemple) :**  

```
Title under sandbox: Responsive Demo – Mobile View
```

Si vous voyez le titre affiché, vous avez réussi à **définir le ratio de pixels du dispositif**, **définir la largeur et la hauteur de l’écran**, et **obtenir le titre de la page** en Java.

## Exemple complet et exécutable

Ci-dessous se trouve le programme complet que vous pouvez copier‑coller dans un fichier nommé `SandboxDemo.java`. Assurez‑vous que les JARs Aspose.HTML sont dans votre classpath (option `-cp`) avant de compiler.

La classe `SandboxDemo` regroupe toutes les étapes précédentes en un seul exemple exécutable.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Compilez et exécutez :

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Vous devriez voir le titre affiché dans la console, confirmant que la page a été rendue avec le **ratio de pixels du dispositif** souhaité.

## Questions fréquentes & cas limites

**Q : Puis‑je changer le ratio de pixels à l’exécution ?**  
R : Oui—créez un nouveau `SandboxOptions` avec une valeur différente de `setDevicePixelRatio` et instanciez un nouveau `Sandbox`. Réutiliser le même sandbox après avoir modifié ses options n’est pas supporté.

**Q : Et si je dois tester plusieurs appareils ?**  
R : Parcourez une liste de `SandboxOptions` (par ex., iPhone 8, Pixel 4) et exécutez la même logique de chargement et de récupération du titre pour chacun.

**Q : Cela fonctionne‑t‑il avec des sites HTTPS possédant des certificats auto‑signés ?**  
R : Aspose.HTML respecte le magasin de confiance SSL par défaut de Java. Ajoutez le certificat au keystore JVM ou, uniquement pour les tests, désactivez la vérification (non recommandé en production).

**Q : Comment capturer une capture d’écran au lieu du simple titre ?**  
R : L’API `HTMLDocument` propose des méthodes `save` qui peuvent exporter la page rendue en PNG ou JPEG. Utilisez `htmlDoc.save("output.png", SaveFormat.PNG);` après le chargement.

**Q : Le sandbox est‑il thread‑safe ?**  
R : Chaque instance de `Sandbox` est isolée, mais vous devez éviter de partager une même instance entre plusieurs threads sans synchronisation.

## Vue d’ensemble visuelle

![Diagramme montrant la définition du ratio de pixels du dispositif dans le sandbox mobile](https://example.com/images/sandbox-diagram.png "diagramme du ratio de pixels du dispositif")

[Diagramme montrant la définition du ratio de pixels du dispositif dans le sandbox mobile](https://example.com/images/sandbox-diagram.png "diagramme du ratio de pixels du dispositif")

*L’illustration ci‑dessus montre le flux depuis la configuration de `SandboxOptions` (incluant **définir la largeur et la hauteur de l’écran** et **définir le ratio de pixels du dispositif**) jusqu’au chargement d’une URL et à l’extraction du titre.*

## Conclusion

Vous savez maintenant **comment définir le ratio de pixels du dispositif** en Java, comment **définir la largeur et la hauteur de l’écran** pour une émulation mobile précise, et comment **obtenir le titre de la page java** pour confirmer que le rendu a réussi. Ce flux de travail compact élimine le besoin de navigateurs lourds lors des tests UI automatisés et s’intègre parfaitement aux pipelines CI.

Prêt pour l’étape suivante ? Essayez d’exporter la page rendue en image, ou expérimentez le débogage des media queries CSS en basculant le `devicePixelRatio` entre 1.0 et 3.0. Vous pouvez également explorer les fonctionnalités de conversion PDF d’Aspose.HTML pour capturer une version imprimable de la vue mobile.

Bon codage, et que vos mises en page mobiles restent toujours nettes—quelle que soit la densité de pixels !

---

**Dernière mise à jour :** 2026-10-19  
**Testé avec :** Aspose.HTML 23.7 for Java  
**Auteur :** Aspose

## Tutoriels associés

- [Obtenir le titre HTML Java – rendre la page dans le sandbox avec largeur d’écran](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Créer le sandbox Aspose Html – guide complet Java](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Définir le ratio de pixels du dispositif en Java – guide complet](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}