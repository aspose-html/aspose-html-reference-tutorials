---
category: general
date: 2026-02-10
description: Définir le ratio de pixels de l’appareil en Java avec le bac à sable
  Aspose.HTML. Apprenez à définir la largeur et la hauteur de l’écran et à obtenir
  le titre de la page en Java avec un exemple complet et exécutable.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: fr
og_description: Définir le ratio de pixels de l'appareil en Java avec le bac à sable
  Aspose.HTML. Ce guide vous montre comment définir la largeur et la hauteur de l'écran
  et obtenir le titre de la page Java en quelques étapes simples.
og_title: Définir le ratio de pixels de l'appareil en Java – Tutoriel Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Définir le ratio de pixels de l’appareil en Java – Tutoriel Mobile Sandbox
url: /fr/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le device pixel ratio en Java – Tutoriel Mobile Sandbox

Vous avez déjà eu besoin de **set device pixel ratio** lors du test d'un site responsive en Java ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsque la page est parfaite sur le bureau mais se casse sur les téléphones à haute DPI. Bonne nouvelle ? Avec le sandbox d'Aspose.HTML, vous pouvez émuler un iPhone X (ou tout autre appareil) directement depuis votre code Java—aucun navigateur requis.

Dans ce guide, nous allons parcourir **how to set screen width height**, configurer le **device pixel ratio**, et enfin **get page title java** pour vérifier que tout est rendu correctement. À la fin, vous disposerez d'un programme autonome que vous pouvez intégrer à n'importe quel projet et commencer à tester les mises en page mobiles instantanément.

## Prérequis

- Java 8 ou plus récent (le code compile également avec JDK 11)  
- Bibliothèque Aspose.HTML for Java (version 23.7 ou ultérieure) – vous pouvez la récupérer depuis Maven Central  
- Un IDE ou une configuration simple en ligne de commande `javac`  
- Accès Internet pour l'URL de démonstration (`https://responsive.example.com`)

Pas de frameworks supplémentaires, pas de Selenium, juste du Java pur et Aspose.HTML.

---

## Étape 1 : Définir la largeur et la hauteur de l'écran et le device pixel ratio

La première chose dont nous avons besoin est un objet `SandboxOptions` qui indique au sandbox quel « appareil » nous simulons. Ici, nous utiliserons les dimensions de l'iPhone X (375 × 812 pixels CSS) et un **device pixel ratio** de 3.0, qui reproduit l'écran Retina à haute DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Pourquoi c'est important :**  
> L'appel `setDevicePixelRatio` met à l'échelle tout—des images au rendu des polices—de sorte que la page pense qu'elle est sur un vrai téléphone. Si vous l'omettez, la mise en page peut revenir aux requêtes média CSS de type bureau, contrecarrant le but du test mobile.

---

## Étape 2 : Créer l'instance du sandbox

Nous transformons maintenant ces options en un sandbox actif. Considérez le sandbox comme un petit navigateur sans tête qui respecte les dimensions et le pixel ratio que nous venons de définir.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Astuce pro :** Vous pouvez réutiliser le même objet `Sandbox` pour plusieurs chargements de pages ; il suffit de changer l'URL et le sandbox conservera les mêmes caractéristiques d'appareil.

---

## Étape 3 : Charger la page dans le sandbox

Avec le sandbox prêt, charger une page est aussi simple que de construire un `HTMLDocument` et de passer le sandbox comme second argument. Cela oblige le document à se rendre en utilisant l'appareil virtuel que nous avons défini précédemment.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Si l'URL est inaccessible ou que la page contient des erreurs, Aspose.HTML lèvera une exception. Pour du code de production, vous l’envelopperiez probablement dans un `try‑catch` et enregistreriez l'échec, mais pour le tutoriel nous restons simples.

---

## Étape 4 : Vérifier avec get page title java

Le contrôle de cohérence le plus rapide consiste à lire le titre du document. Si le sandbox a correctement appliqué le **device pixel ratio**, le titre sera identique à celui que vous verriez sur un vrai iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Sortie attendue (exemple) :**

```
Title under sandbox: Responsive Demo – Mobile View
```

Si vous voyez le titre affiché, vous avez réussi à **set device pixel ratio**, **set screen width height**, et **got the page title** en Java.

---

## Exemple complet et exécutable

Voici le programme complet que vous pouvez copier‑coller dans un fichier nommé `SandboxDemo.java`. Assurez-vous que les JARs Aspose.HTML sont dans votre classpath (option `-cp`) avant de compiler.

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

Compiler et exécuter :

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Vous devriez voir le titre affiché dans la console, confirmant que la page a été rendue avec le **device pixel ratio** souhaité.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| **Puis-je changer le pixel ratio à l'exécution ?** | Oui—il suffit de créer un nouveau `SandboxOptions` avec une valeur différente de `setDevicePixelRatio` et d'instancier un nouveau `Sandbox`. Réutiliser le même sandbox après avoir changé ses options n'est pas supporté. |
| **Et si je dois tester plusieurs appareils ?** | Parcourez une liste de `SandboxOptions` (par ex., iPhone 8, Pixel 4) et exécutez la même logique de chargement et de titre pour chacun. |
| **Cela fonctionne-t-il avec des sites HTTPS ayant des certificats auto‑signés ?** | Aspose.HTML respecte le magasin de confiance SSL par défaut de Java. Ajoutez le certificat au keystore du JVM ou désactivez la vérification uniquement pour les tests (non recommandé en production). |
| **Comment capturer une capture d'écran au lieu du simple titre ?** | L'API `HTMLDocument` fournit des méthodes `save` qui peuvent exporter la page rendue en PNG ou JPEG. Utilisez `htmlDoc.save("output.png", SaveFormat.PNG);` après le chargement. |
| **Le sandbox est‑il thread‑safe ?** | Chaque instance de `Sandbox` est isolée, mais vous devez éviter de partager une même instance entre plusieurs threads sans synchronisation. |

---

## Vue d'ensemble visuelle

![Diagramme montrant le set device pixel ratio dans le sandbox mobile](https://example.com/images/sandbox-diagram.png "diagramme du set device pixel ratio")

*L'illustration ci‑dessus montre le flux depuis la configuration de `SandboxOptions` (incluant **set screen width height** et **set device pixel ratio**) jusqu'au chargement d'une URL et à l'extraction du titre.*

---

## Conclusion

Vous savez maintenant **how to set device pixel ratio** en Java, comment **set screen width height** pour une émulation mobile précise, et comment **get page title java** pour confirmer que le rendu a réussi. Ce flux de travail compact élimine le besoin de navigateurs lourds lors des tests UI automatisés et s'intègre parfaitement aux pipelines CI.

Prêt pour l'étape suivante ? Essayez d'exporter la page rendue en image, ou expérimentez le débogage des media‑queries CSS en basculant le `devicePixelRatio` entre 1.0 et 3.0. Vous pouvez également explorer les fonctionnalités de conversion PDF d'Aspose.HTML pour capturer une version imprimable de la vue mobile.

Bon codage, et que vos mises en page mobiles restent toujours nettes—quelle que soit la densité de pixels !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}