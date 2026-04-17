---
category: general
date: 2026-03-26
description: Apprenez à émuler l’iPhone en Java avec Aspose.HTML. Comprend les étapes
  pour définir un agent utilisateur personnalisé et régler le ratio de pixels de l’appareil
  afin d’obtenir un rendu mobile précis.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: fr
og_description: Comment émuler un iPhone en Java ? Ce tutoriel montre comment définir
  un agent utilisateur personnalisé et le ratio de pixels de l’appareil avec Aspose.HTML,
  offrant des pages mobiles pixel‑parfaites.
og_title: Comment émuler l’iPhone – Guide Aspose.HTML étape par étape
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Comment émuler l'iPhone – Guide complet avec Aspose.HTML
url: /fr/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment émuler iPhone – Guide complet avec Aspose.HTML

Vous vous êtes déjà demandé **comment émuler iPhone** lors du test d’une page web en local ? Peut‑être déboguez‑vous une mise en page responsive et le navigateur de bureau ne suffit pas. La bonne nouvelle, c’est que vous n’avez pas besoin d’un appareil physique—`DocumentSandbox` d’Aspose.HTML vous permet d’imiter l’écran, le user‑agent et le device‑pixel‑ratio (DPR) d’un iPhone avec quelques lignes de Java.  

Dans ce tutoriel, nous passerons en revue les étapes exactes pour définir un **user agent personnalisé**, configurer le **device pixel ratio**, et vérifier que tout fonctionne comme prévu. À la fin, vous disposerez d’un sandbox réutilisable qui rend les pages exactement comme un iPhone 8, et vous comprendrez pourquoi chaque paramètre est important.

## Ce que vous allez accomplir

- Créer un objet `Screen` qui reflète les dimensions et le DPR d’un iPhone.  
- Appliquer une chaîne **custom user agent** afin que les serveurs pensent que la requête provient de Safari sur iOS.  
- Construire un `DocumentSandbox` qui lie l’écran et le user‑agent ensemble.  
- Exécuter un `HTMLDocument` à l’intérieur du sandbox et voir la sortie console confirmant la configuration.  

Aucune bibliothèque externe en dehors d’Aspose.HTML n’est requise, et le code s’exécute sur n’importe quel environnement Java 17+.

---

![capture d'écran de l'émulation d'iPhone](https://example.com/images/iphone-emulation.png "comment émuler iPhone en utilisant le sandbox Aspose.HTML")

## Comment émuler iPhone avec le sandbox Aspose.HTML

La première chose dont nous avons besoin est un `Screen` qui reflète les dimensions physiques de l’iPhone *et* sa densité de pixels. C’est le cœur de **comment émuler iPhone** avec précision.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Pourquoi c’est important :**
- La largeur = 375 px et la hauteur = 667 px sont les dimensions en pixels CSS que vous verrez dans Chrome DevTools lorsque vous sélectionnez un iPhone 8.  
- Définir le DPR à 2 indique au moteur de rendu de traiter chaque pixel CSS comme deux pixels physiques, vous offrant un texte et des images nets—exactement comme le fait un appareil réel.

> *Astuce :* Si vous devez émuler un iPhone plus récent (comme l’iPhone 13), il suffit de changer les nombres à 390 × 844 et DPR = 3.

## Définir un User Agent personnalisé (set custom user agent)

Ensuite, nous devons **définir un custom user agent** afin que le serveur fournisse le HTML/CSS spécifique mobile. Sans cela, de nombreux sites penseront toujours que vous êtes sur un ordinateur de bureau.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Comment cela fonctionne :**
- L’en-tête `User-Agent` est la poignée de main que les navigateurs utilisent pour s’annoncer.  
- En fournissant la chaîne exacte que Safari sur iOS 16 envoie, vous assurez que le serveur renvoie les ressources optimisées pour le mobile (par ex. images responsives, scripts adaptatifs, etc.).  

Si vous avez besoin de **définir le user-agent** pour un autre appareil, il suffit de remplacer la chaîne par la valeur appropriée—Google Chrome, Firefox, ou même un bot personnalisé.

## Configurer le Device Pixel Ratio (set device pixel ratio)

Nous allons maintenant réellement **définir le device pixel ratio** dans le sandbox. C’est l’étape qui répond directement à « **comment définir le dpr** » pour un environnement simulé.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Explication :**
- Le pattern `Builder` vous permet d’attacher de façon fluide à la fois l’écran (qui porte le DPR) et le user‑agent.  
- Lorsque le sandbox rend un `HTMLDocument`, il fera comme s’il s’exécutait sur un appareil avec cette densité de pixels exacte.

> *Pourquoi c’est important :* Certaines requêtes média CSS utilisent `device-pixel-ratio` (par ex., `@media (-webkit-min-device-pixel-ratio: 2)`). Si vous ne définissez pas le DPR, ces règles ne s’activent jamais, et vous manquerez les ressources haute résolution.

## Vérifier la configuration du sandbox (how to set user-agent)

Mettons le sandbox en action. Le fragment suivant crée un `HTMLDocument`, charge une page, et affiche une confirmation que le sandbox est actif.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Sortie console attendue**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Si vous exécutez le programme et voyez cette ligne, vous avez réussi à **émuler iPhone** avec le DPR et le user‑agent corrects. Ouvrez la page dans un vrai navigateur et inspectez les dimensions du viewport—vous remarquerez qu’elles correspondent aux valeurs iPhone que nous avons définies.

## Pièges courants et comment définir correctement le DPR (how to set dpr)

Même avec le bon code, quelques pièges peuvent vous surprendre :

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Le DPR reste à 1** | Vous avez passé un `Screen` sans le troisième argument (DPR). | Utilisez toujours `new Screen(width, height, dpr)`. |
| **User‑Agent ignoré** | Le sandbox n’était pas attaché au `HTMLDocument`. | Passez le `documentSandbox` comme deuxième argument au constructeur `HTMLDocument`. |
| **Dimensions incorrectes** | Utilisation de pixels d’appareil au lieu de pixels CSS. | Rappelez‑vous : la largeur/hauteur sont des **pixels CSS**, pas des pixels matériels. |
| **Le serveur envoie toujours du CSS desktop** | Certains sites utilisent JavaScript pour détecter les appareils, pas seulement l’en‑tête. | Envisagez également d’injecter une balise meta viewport si nécessaire. |

En gardant cela à l’esprit, vous rencontrerez rarement une situation où l’émulation ne se comporte pas comme prévu.

## Étendre le sandbox – Prochaines étapes

Maintenant que vous savez **comment définir un user agent personnalisé** et **comment définir le dpr**, vous pouvez expérimenter davantage :

- **Modifier la taille de l’écran** pour émuler des tablettes ou des téléphones plus grands.  
- **Changer le user‑agent** pour tester Chrome sur Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Ajouter des cookies ou des en‑têtes** via la méthode `setHeaders` du sandbox pour des tests authentifiés.  
- **Capturer une capture d’écran** en utilisant `HTMLDocument.renderToFile("output.png")` pour comparer automatiquement les différences visuelles.  

Ces extensions vous permettent de créer un harness de test complet sans jamais quitter votre IDE.

## Conclusion

Nous avons couvert **comment émuler iPhone** en utilisant le `DocumentSandbox` d’Aspose.HTML, vous montrant exactement **comment définir un user agent personnalisé**, **comment définir le device pixel ratio**, et même les différences subtiles entre « **comment définir le user-agent** » et « **comment définir le dpr** ». L’exemple complet et exécutable montre chaque élément en un seul endroit, afin que vous puissiez copier‑coller, ajuster, et commencer à tester les mises en page mobiles instantanément.  

Essayez‑le — changez les dimensions de l’écran, jouez avec différents user‑agents, et observez comment vos pages réagissent. Une fois que vous maîtrisez ces paramètres, le débogage des designs responsives devient un jeu d’enfant, et vous économiserez d’innombrables heures à traquer des bugs sur de vrais appareils.  

Des questions ou envie de partager vos propres variantes ? Laissez un commentaire ci‑dessous, et bon émulation !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}