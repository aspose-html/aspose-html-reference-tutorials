---
category: general
date: 2026-04-03
description: Apprenez à utiliser le sandbox dans Aspose.HTML Java pour définir l'agent
  utilisateur, définir la taille et obtenir instantanément la taille du viewport.
  Code complet, explications et astuces inclus.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: fr
og_description: Apprenez à utiliser le sandbox dans Aspose.HTML Java pour définir
  l'agent utilisateur, définir la taille et obtenir instantanément la taille du viewport.
  Guide complet avec du code et les meilleures pratiques.
og_title: Comment utiliser Sandbox – définir l'agent utilisateur et obtenir la taille
  du viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Comment utiliser Sandbox – définir l'agent utilisateur et obtenir la taille
  du viewport
url: /fr/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser le bac à sable – Définir l'agent utilisateur et obtenir la taille du viewport

Vous vous êtes déjà demandé **comment utiliser le bac à sable** lors du rendu HTML avec Aspose.HTML for Java ? Peut‑être avez‑vous rencontré des difficultés pour simuler une taille d’écran précise ou devez‑vous usurper une chaîne d’agent‑utilisateur afin que la page se comporte comme si elle était visitée depuis un navigateur mobile.  

Bonne nouvelle : l’API sandbox vous permet de faire exactement cela, et vous pouvez également récupérer la taille du viewport calculée après le chargement de la page. Dans ce tutoriel, nous allons créer un sandbox, définir la taille, définir un agent utilisateur personnalisé, charger une page distante, puis lire les dimensions du viewport. À la fin, vous saurez **comment définir la taille**, **comment obtenir le viewport**, et pourquoi ces étapes sont essentielles pour un rendu headless fiable.

> **Gain rapide** : vous disposerez d’une classe Java exécutable qui affichera quelque chose comme `Viewport: 1280×800` en quelques secondes.

---

## Ce dont vous avez besoin

- **Aspose.HTML for Java** version 24.6 ou plus récente (l’API utilisée a été introduite dans la version 24.5).  
- Un kit de développement Java 17+ (tout JDK récent convient).  
- Un IDE ou un simple éditeur de texte — aucun plugin spécial requis.  
- Un accès Internet si vous souhaitez charger une URL externe telle que `https://example.com`.

C’est tout. Aucun wizard Maven/Gradle n’est obligatoire ; vous pouvez déposer les JARs sur le classpath manuellement si vous le préférez.  

---

## Comment utiliser le bac à sable – Vue d’ensemble

Le sandbox isole le moteur de rendu du système d’exploitation hôte, vous permettant de définir un écran virtuel (largeur, hauteur, DPI) et une chaîne **user agent** personnalisée. Pensez‑y comme à une petite fenêtre de navigateur qui vit entièrement en mémoire. Lorsque vous interrogez ensuite le `HTMLDocument` pour sa vue par défaut, le moteur renvoie la **taille du viewport** qu’il a calculée à partir des paramètres du sandbox.  

Voici le flux à haut niveau :

1. **Créer** un `DocumentSandbox` et configurer la largeur, la hauteur, le DPI et l’agent‑utilisateur.  
2. **Charger** un `HTMLDocument` à l’intérieur de ce sandbox.  
3. **Interroger** la vue par défaut du document pour obtenir la taille du viewport.  

Passons en revue chaque étape.

---

## Étape 1 : Créer un sandbox et définir la taille

Tout d’abord, nous démarrons un sandbox et lui indiquons la taille de l’écran virtuel. C’est ici que vous répondez à la question **comment définir la taille** pour un rendu sans tête.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Astuce** : si vous testez une mise en page réactive, essayez une largeur étroite comme `360` pour émuler un téléphone, ou une large comme `1920` pour un bureau. Le sandbox respecte le DPI que vous avez défini, donc un écran à haute densité (par ex., 144 DPI) influencera les media‑queries qui utilisent `device-pixel-ratio`.

---

## Étape 2 : Définir l’agent utilisateur pour le sandbox

Pourquoi se soucier d’un **user agent** personnalisé ? Certains sites livrent un balisage ou des scripts différents selon le navigateur déclaré. En appelant `setUserAgent`, vous pouvez faire croire à la page qu’elle est visitée depuis Chrome, Firefox ou un appareil mobile.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Maintenant, la page pensera qu’elle s’affiche sur un iPhone. Si vous devez **revenir à l’agent utilisateur** par défaut, réutilisez simplement la chaîne précédente : « AsposeHTML/24.6 … ».

---

## Étape 3 : Charger un document HTML dans le sandbox

Le sandbox étant prêt, nous pouvons charger n’importe quelle URL ou fichier HTML local. Le constructeur `HTMLDocument` accepte le sandbox comme second argument, liant ainsi les deux.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Le bloc `try‑with‑resources` garantit que le document est correctement libéré, libérant les ressources natives qu’Aspose.HTML alloue en arrière‑plan.

---

## Étape 4 : Obtenir la taille du viewport depuis le document

Voici le moment tant attendu : récupérer la **taille du viewport** que le moteur de rendu a calculée. Cela répond à **comment obtenir le viewport** après le rendu de la page.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Lorsque vous exécuterez le programme, vous devriez voir quelque chose comme :

```
Viewport: 1280×800
```

Si vous avez modifié les dimensions du sandbox à l’Étape 1, les nombres affichés refléteront ces nouvelles valeurs — idéal pour des tests automatisés qui vérifient les points de rupture réactifs.

---

## Exemple complet fonctionnel

Voici la classe complète, prête à être exécutée. Copiez‑collez‑la dans un fichier nommé `SandboxExample.java`, ajoutez les JARs Aspose.HTML à votre classpath, puis lancez `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Sortie attendue** (en supposant les paramètres du sandbox ci‑dessus) :

```
Viewport: 1280×800
```

Si vous définissez une largeur/hauteur différente dans le sandbox, la sortie changera en conséquence — exactement ce qu’il faut lorsqu’on teste des conceptions réactives.

---

## Cas limites et questions fréquentes

### Que se passe‑t‑il si la page utilise `window.innerWidth` au lieu des media queries CSS ?

La taille d’écran virtuelle du sandbox influence à la fois la mise en page CSS et la valeur JavaScript `window.innerWidth/innerHeight`. Ainsi, **comment obtenir le viewport** via JavaScript renverra les mêmes chiffres que vous voyez dans la console Java.

### Puis‑je exécuter plusieurs sandboxes en parallèle ?

Oui. Chaque instance de `DocumentSandbox` est indépendante, vous pouvez donc créer un pool de threads, attribuer à chaque thread son propre sandbox avec des dimensions différentes, et rendre des dizaines de pages simultanément. Veillez simplement à ce que les JARs soient thread‑safe (ils le sont).

### Le réglage du DPI affecte‑t‑il le redimensionnement des images ?

Absolument. Un DPI plus élevé fait que chaque pixel CSS correspond à plusieurs pixels d’appareil, ce qui peut rendre les images haute résolution plus nettes. Si vous testez des ressources de type retina, essayez `sandbox.setDeviceDpi(144)`.

### Comment gérer les certificats HTTPS auto‑signés ?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}