---
category: general
date: 2026-02-16
description: Apprenez à exécuter du JavaScript dans Java avec CompletableFuture, à
  retarder le JS et à évaluer le code asynchrone. Guide complet étape par étape pour
  l'évaluation asynchrone de JavaScript.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: fr
og_description: Maîtrisez comment exécuter du JavaScript depuis Java, retarder le
  JS et évaluer du code asynchrone avec CompletableFuture dans ce tutoriel complet.
og_title: Comment exécuter du JavaScript de manière asynchrone avec CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Comment exécuter du JavaScript de manière asynchrone avec CompletableFuture
url: /fr/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter du JavaScript de manière asynchrone avec CompletableFuture

Vous vous êtes déjà demandé **comment exécuter du JavaScript** à l'intérieur d'une application Java sans bloquer le thread principal ? Peut-être devez‑vous appeler un petit script qui récupère des données, mais vous ne voulez pas que votre interface se fige. La bonne nouvelle, c’est que les bibliothèques Java modernes vous permettent d’évaluer du JavaScript **de façon asynchrone**, et vous pouvez même introduire des délais comme dans un navigateur. Dans ce guide, nous vous montrons un exemple complet et exécutable qui utilise le `ScriptEngine` d’Aspose HTML avec `CompletableFuture` pour **comment exécuter du javascript** et récupérer le résultat en Java.

Nous couvrirons également **comment utiliser CompletableFuture**, **comment retarder le JS**, et **comment évaluer du code async** afin que vous puissiez **évaluer du JavaScript de manière asynchrone** dans n’importe quel projet Java. À la fin, vous disposerez d’un modèle solide que vous pourrez copier‑coller, ajuster et intégrer dans des systèmes plus grands.

---

## Ce que vous allez apprendre

- Configurer un `ScriptEngine` Java capable d’exécuter du JavaScript moderne ES2022.  
- Écrire une fonction `async` incluant un délai (`how to delay js`).  
- Appeler `evaluateAsync` et recevoir un `CompletableFuture` (`how to use completablefuture`).  
- Récupérer le résultat une fois que la promesse JavaScript est résolue (`how to evaluate async`).  
- Conseils pour la gestion des erreurs, la gestion des threads et l’extension du modèle.

Aucun outil de construction externe n’est requis au-delà du JAR Aspose HTML for Java, que vous pouvez placer dans votre classpath. Plongeons‑y.

## Étape 1 : Comment exécuter du JavaScript – Initialiser le moteur de script

Tout d’abord. La bibliothèque Aspose HTML fournit une classe `ScriptEngine` qui peut exécuter du code JavaScript. Considérez‑la comme un petit moteur Chromium fonctionnant à l’intérieur de votre JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Pourquoi c’est important :** En instanciant `ScriptEngine`, nous obtenons un environnement sandboxé où le JavaScript moderne (y compris `async/await`) fonctionne immédiatement. Aucun besoin de lancer un processus Node externe.

## Étape 2 : Comment retarder le JS – Écrire une fonction async avec un minuteur basé sur Promise

Le `setTimeout` de JavaScript est la méthode classique pour suspendre l’exécution. Dans le code moderne, nous l’enveloppons dans une `Promise` afin de pouvoir le `await`. C’est exactement ce que nous ferons dans la chaîne de script.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Comment retarder le js :** L’assistant `delay` crée une promesse qui se résout après `ms` millisecondes. En l’`await`‑ant, la fonction se met en pause sans bloquer le thread Java.

## Étape 3 : Comment évaluer de façon async – Exécuter le script et obtenir un CompletableFuture

Au lieu de la méthode synchrone `evaluate`, nous appelons `evaluateAsync`. Elle renvoie immédiatement un `CompletableFuture<Object>` qui sera complété lorsque la promesse JavaScript sera résolue.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Comment évaluer de façon async :** `evaluateAsync` fait le pont entre la boucle d’événements JavaScript et le `CompletableFuture` de Java. C’est le cœur de **evaluate javascript asynchronously**.

## Étape 4 : Comment utiliser CompletableFuture – Attacher un callback et bloquer pour la démo

Nous attachons maintenant un callback avec `thenAccept` pour afficher le résultat, et nous bloquons le thread principal juste assez longtemps pour que la démo se termine.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Pourquoi nous appelons `get()` :** Dans une application réelle, vous continueriez probablement le traitement ailleurs. Ici nous bloquons pour que l’exemple reste autonome.

## Vue d’ensemble visuelle

![Diagramme montrant comment exécuter du JavaScript de manière asynchrone avec CompletableFuture](https://example.com/diagram.png "Comment exécuter du JavaScript – Flux asynchrone")

*Texte alternatif :* **Diagramme montrant comment exécuter du JavaScript de manière asynchrone avec CompletableFuture** – l’image illustre le flux de Java vers le moteur de script, le délai async, et la complétion du CompletableFuture.

## Pièges courants & bonnes pratiques (Comment évaluer async en toute sécurité)

| Piège | Ce qui se passe | Solution |
|-------|----------------|----------|
| Oublier de retourner la promesse | `evaluateAsync` se résout immédiatement avec `undefined` | S’assurer que la dernière ligne du script est la promesse (`fetchMessage();`) |
| Utiliser `Thread.sleep` bloquant dans JS | Bloque la boucle d’événements du moteur, annule l’asynchronisme | Utiliser le pattern de promesse `delay` (comme montré) |
| Ignorer les exceptions | Le Future se complète de façon exceptionnelle, mais vous ne le voyez jamais | Attacher `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Ne pas fermer le moteur | Fuite de ressources dans les applications de longue durée | Appeler `scriptEngine.dispose()` lorsqu’il n’est plus nécessaire |

## Étendre le modèle (Comment utiliser CompletableFuture dans des projets réels)

Vous pouvez chaîner plusieurs appels JavaScript async, les combiner avec d’autres futures, ou même les exécuter sur un `Executor` personnalisé. Voici un rapide aperçu :

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Comment utiliser CompletableFuture :** En passant un `Executor`, vous contrôlez le pool de threads, gardant l’interface réactive et évitant la famine de threads.

## Résultat attendu

Exécutez la classe `JsAsyncDemo` et vous devriez voir :

```
JS result: Hello from async JS!
```

La pause de 500 ms n’est pas visible dans la console, mais vous pouvez ajouter des horodatages pour vérifier le délai si vous le souhaitez.

## Récapitulatif – Comment exécuter du JavaScript avec CompletableFuture

Nous avons commencé par **comment exécuter du javascript** dans Java, écrit une fonction `async` qui **comment retarder le js**, l’avons exécutée avec `evaluateAsync` (**comment évaluer async**), et capturé le résultat en utilisant un **comment utiliser completablefuture**. L’ensemble du flux démontre **evaluate javascript asynchronously** dans un modèle propre et réutilisable.

## Et après ?

- **Intégrer avec des clients HTTP :** Récupérer des données depuis un endpoint REST dans le JS async et les renvoyer à Java.  
- **Utiliser plusieurs scripts :** Chaîner plusieurs appels `evaluateAsync` pour des pipelines complexes.  
- **Changer de moteur :** Le même modèle fonctionne avec Nashorn, GraalVM ou d’autres runtimes JavaScript — il suffit de remplacer `ScriptEngine`.

N’hésitez pas à expérimenter avec des délais plus longs, des scripts générant des erreurs, ou même des modules WebAssembly. Le ciel est la limite lorsque vous combinez les primitives de concurrence de Java avec le JavaScript moderne.

### Des questions ?

Si quelque chose n’est pas clair — peut‑être vous vous demandez comment gérer une promesse rejetée ou comment passer des variables de Java au script — laissez un commentaire ci‑dessous. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}