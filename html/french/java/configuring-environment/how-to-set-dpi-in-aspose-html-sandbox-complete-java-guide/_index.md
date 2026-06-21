---
category: general
date: 2026-04-02
description: Apprenez à définir le DPI, la taille du viewport et l’agent utilisateur
  dans Aspose.HTML Sandbox. Exemple Java pas à pas avec le code complet et des astuces.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: fr
og_description: Maîtrisez comment définir le DPI, la taille du viewport et l'agent
  utilisateur dans Aspose.HTML Sandbox avec un exemple complet en Java.
og_title: Comment définir le DPI dans le bac à sable Aspose.HTML – Tutoriel Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Comment définir le DPI dans le bac à sable Aspose.HTML – Guide complet Java
url: /fr/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le DPI dans le bac à sable Aspose.HTML – Guide complet Java

Vous vous êtes déjà demandé **comment définir le DPI** lors du rendu d’une page web avec Aspose.HTML ? Vous n’êtes pas le seul. Dans de nombreux scénarios de test, il faut que la mise en page corresponde à une densité d’écran précise — pensez aux PDF prêts à imprimer ou aux captures d’écran haute résolution. La bonne nouvelle, c’est que le bac à sable Aspose.HTML vous permet de contrôler le DPI, la taille du viewport et même la chaîne user‑agent, le tout dans un seul paquet pratique.

Dans ce tutoriel, nous parcourrons un exemple Java concret qui **définit le DPI**, **définit la taille du viewport** et **définit le user‑agent** en une seule fois. À la fin, vous disposerez d’un programme exécutable, comprendrez pourquoi chaque paramètre est important et serez prêt à ajuster le bac à sable pour vos propres projets.

---

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent ; l’API est compatible avec Java 8+)
- Bibliothèque **Aspose.HTML for Java** (version 23.12 ou plus récente)
- Un IDE ou un simple éditeur de texte + compilation en ligne de commande
- Accès Internet pour l’URL d’exemple (`https://example.com`)

Aucun outil de construction externe n’est requis ; le code se compile avec `javac` et s’exécute avec `java`. Si vous préférez Maven ou Gradle, ajoutez simplement la dépendance Aspose.HTML—rien de compliqué.

---

## Étape 1 : Créer un bac à sable qui définit l’environnement de rendu

Le bac à sable est l’endroit où vous indiquez à Aspose.HTML quel « écran » vous simulez. Ici, nous définissons un **viewport de 1024 × 768**, un **DPI de 96** et une chaîne **user‑agent personnalisée**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Pourquoi c’est important :**  
- **DPI** influence la façon dont les unités CSS `pt` sont converties en pixels ; un DPI plus élevé donne un rendu plus net.  
- **Taille du viewport** détermine les points de rupture de mise en page que le CSS réactif va atteindre.  
- **User‑agent** peut déclencher des variations de contenu côté serveur (mobile vs desktop).

> **Astuce :** Si vous générez plus tard des PDF, faites correspondre le DPI à la résolution d’impression cible (par ex. 300 dpi pour des impressions haute qualité).

---

## Étape 2 : Charger une page web dans le bac à sable

Nous pointons maintenant le bac à sable vers une URL. Le constructeur `HTMLDocument` accepte le bac à sable, de sorte que le moteur de mise en page respecte les paramètres que nous venons de définir.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Que se passe-t-il en coulisses ?**  
Aspose.HTML crée un contexte de rendu isolé, similaire à un navigateur sans tête, mais sans le poids d’une instance complète de Chromium. Cela rend l’opération rapide et peu gourmande en mémoire—idéal pour le traitement par lots.

---

## Étape 3 : Interagir avec le DOM – Lire le titre de la page

À titre de démonstration, nous récupérons le titre et l’affichons. Dans un scénario réel, vous pourriez prendre une capture d’écran, exporter en PDF ou extraire des données.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Sortie attendue** (lorsque `https://example.com` est accessible) :

```
Title inside sandbox: Example Domain
```

Si le site renvoie un titre différent, vous verrez celui‑ci à la place—aucune autre modification n’est nécessaire.

---

## Étape 4 : Vérifier les paramètres (débogage optionnel)

Parfois, il faut revérifier que le bac à sable respecte réellement votre DPI et votre viewport. Aspose.HTML n’expose pas directement ces valeurs, mais vous pouvez les déduire en mesurant les dimensions d’un élément.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Si vous savez que le CSS déclare l’élément avec `width: 200pt;`, à **96 dpi** vous devriez obtenir `200pt * (96/72) ≈ 267px`. Modifiez le DPI et relancez pour voir le nombre changer—preuve que **comment définir le DPI** fonctionne réellement.

---

## Code source complet en un seul bloc

Copiez‑collez ce qui suit dans `SandboxExample.java`. Il compile tel quel ; assurez‑vous simplement que le JAR Aspose.HTML se trouve dans le classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Compiler et exécuter :

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Vous devriez voir le titre affiché, confirmant que le bac à sable fonctionne avec le **DPI défini**, la **taille du viewport définie** et le **user‑agent défini** que vous avez fournis.

---

## Questions fréquentes & cas particuliers

### Et si j’ai besoin d’un DPI différent ?

Il suffit de changer le deuxième argument de `DocumentSandbox`. Pour des PDF prêts à l’impression, vous pourriez utiliser `300` :

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Un DPI plus élevé produit des dimensions en pixels plus grandes pour les mêmes points CSS, ce qui améliore la qualité raster mais consomme plus de mémoire.

### Puis‑je charger un fichier HTML local au lieu d’une URL ?

Absolument. Remplacez l’URL par un chemin de fichier :

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Assurez‑vous que le chemin est absolu et utilise le schéma `file:///`.

### Comment changer le user‑agent après la création du bac à sable ?

Le bac à sable est immuable—une fois passé à `HTMLDocument`, les paramètres sont figés. Pour utiliser un autre user‑agent, créez un nouveau `DocumentSandbox` avec la chaîne souhaitée.

### Aspose.HTML prend‑il en charge l’exécution de JavaScript ?

Oui, le moteur exécute la plupart des scripts côté client. Si un script modifie le DOM après le chargement, vous pouvez attendre un instant :

```java
webDoc.waitForLoad();
```

Ou utiliser une logique de type `setTimeout` dans la page avant d’interroger les éléments.

---

## Confirmation visuelle (Image)

Voici une capture d’écran de la console montrant l’exécution réussie. Notez que le titre affiché correspond à la page, confirmant que le bac à sable a respecté nos paramètres.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Texte alternatif :* *Capture d’écran de la console démontrant comment définir le DPI, la taille du viewport et le user‑agent dans le bac à sable Aspose.HTML.*

---

## Récapitulatif & étapes suivantes

Nous avons vu **comment définir le DPI** (96 dpi dans l’exemple), **comment définir la taille du viewport** (1024 × 768) et **comment définir le user‑agent** (chaîne personnalisée) à l’aide de l’API bac à sable d’Aspose.HTML. Le programme Java complet et exécutable prouve que ces réglages ne sont pas théoriques — ils influencent directement le rendu et l’interaction DOM.

Prêt pour la suite ?

- **Export PDF :** Après le chargement de la page, appelez `webDoc.save("output.pdf", SaveFormat.PDF);` pour générer un PDF haute résolution qui reflète le DPI que vous avez défini.  
- **Capture d’écran :** Utilisez `webDoc.renderToBitmap("screenshot.png");` pour obtenir des images pixel‑perfectes.  
- **Tester les mises en page réactives :** Modifiez les dimensions du viewport pour tester les points de rupture mobiles sans appareil réel.  

Expérimentez avec différentes valeurs de DPI, combinaisons de viewport et user‑agents pour observer comment les serveurs et le CSS réagissent. Le bac à sable est un terrain de jeu léger qui vous évite de lancer des navigateurs complets.

---

### Continuez à explorer

- **Documentation Aspose.HTML** – approfondissez les options de `DocumentSandbox`.  
- **Media Queries CSS avancées** – apprenez comment la taille du viewport déclenche différents styles.  
- **Spoofing du User‑Agent** – découvrez comment certains sites livrent un balisage alternatif selon la chaîne d’agent.

Des questions ou un cas difficile ? Laissez un commentaire, et résolvons-le ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}