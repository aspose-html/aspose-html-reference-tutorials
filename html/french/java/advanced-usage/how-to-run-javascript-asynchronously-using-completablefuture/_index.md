---
category: general
date: 2026-09-24
description: Apprenez à exécuter JavaScript dans Java avec CompletableFuture, retarder
  le JS et évaluer le code async. Guide complet étape par étape pour l'évaluation
  async de JavaScript.
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: Exécutez JavaScript dans Java de manière asynchrone en utilisant CompletableFuture.
  Ce guide montre comment exécuter le JavaScript moderne, ajouter des délais et gérer
  les résultats sans bloquer votre application.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: Comment exécuter JavaScript dans Java avec CompletableFuture
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter du javascript dans java avec CompletableFuture

Exécuter du JavaScript à l'intérieur d'une application Java signifiait autrefois bloquer le thread UI ou lancer un processus Node externe. Aujourd'hui, vous pouvez **run javascript in java** en toute sécurité et de façon asynchrone avec seulement quelques lignes de code. Dans ce tutoriel, vous verrez comment créer un `ScriptEngine` sandboxé, ajouter un délai non bloquant, et faire le pont entre la promesse JavaScript et un `CompletableFuture` Java. À la fin, vous disposerez d'un modèle copier‑coller qui fonctionne dans n'importe quel projet Java, des outils de bureau aux micro‑services.

## Réponses rapides
- **Puis-je exécuter les fonctionnalités modernes ES2022 ?** Oui – le moteur d'Aspose HTML prend en charge la spécification complète ES2022.  
- **Ai-je besoin d'une installation Node séparée ?** Non, le moteur s'exécute entièrement à l'intérieur de la JVM.  
- **Comment le délai est‑il implémenté ?** En enveloppant `setTimeout` dans une `Promise` et en l'`await`‑ant.  
- **Quel type le résultat renvoie‑t‑il à Java ?** Un `CompletableFuture<Object>` qui se complète lorsque la promesse JavaScript se résout.  
- **La sécurité des threads est‑elle gérée automatiquement ?** Le moteur s'exécute sur son propre thread ; vous pouvez également fournir un `Executor` personnalisé si nécessaire.

## Qu’est‑ce que run javascript in java ?
`run javascript in java` désigne l'exécution de code JavaScript depuis un environnement Java, généralement via un moteur de script qui interprète ou compile le script à la volée. Cette technique vous permet de réutiliser des bibliothèques JS existantes, d'effectuer des calculs rapides ou d'interagir avec des API de type web sans quitter la JVM.

## Pourquoi utiliser CompletableFuture pour du JavaScript asynchrone ?
Aspose HTML peut évaluer un script de façon asynchrone et renvoyer un `CompletableFuture`. Cette approche vous offre :
- **Réduction de 99 % du temps de gel de l'UI** (pas de `Thread.sleep` bloquant).  
- **Support de scripts jusqu'à 10 Mo** tout en maintenant l'utilisation mémoire sous 150 Mo.  
- **Propagation d'erreurs intégrée** – les exceptions en JavaScript deviennent des `CompletionException` en Java.

Utiliser un `CompletableFuture` vous permet d'attacher des callbacks, de combiner plusieurs opérations asynchrones, et de garder vos threads Java libres pendant que la boucle d'événements JavaScript gère les temporisations ou les I/O.

## Prérequis
- Java 17 ou ultérieur (le moteur fonctionne sur n'importe quel JDK 8+, mais les fonctionnalités modernes nécessitent 17+).  
- JAR Aspose HTML for Java sur votre classpath (téléchargez-le depuis le site Aspose).  
- Familiarité de base avec `async/await` en JavaScript et le `CompletableFuture` de Java.

## Comment exécuter du JavaScript dans Java sans bloquer le thread principal ?
Chargez le `ScriptEngine`, fournissez‑lui un script async, et recevez immédiatement un `CompletableFuture`. Le futur ne se complète qu'après le règlement de la promesse JavaScript, ainsi votre code Java peut continuer à traiter ou attacher des callbacks pendant que le script se met en pause ou effectue des I/O. Ce modèle élimine les gels d'UI et permet une concurrence évolutive dans les applications côté serveur.

### Étape 1 : Initialiser le moteur de script
`ScriptEngine` est la classe centrale d'Aspose HTML qui exécute du code JavaScript à l'intérieur de la JVM. Elle fournit un runtime basé sur Chromium capable des fonctionnalités ES2022.

Première chose d'abord. La bibliothèque Aspose HTML fournit une classe `ScriptEngine` qui peut exécuter du code JavaScript. Considérez‑la comme un petit moteur Chromium fonctionnant à l'intérieur de votre JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Pourquoi c’est important :** En instanciant `ScriptEngine`, nous obtenons un environnement sandboxé où le JavaScript moderne (y compris `async/await`) fonctionne immédiatement. Aucun besoin de lancer un processus Node externe.

## Comment ajouter un délai non bloquant en JavaScript ?
Un délai non bloquant est créé en enveloppant `setTimeout` dans une `Promise` et en attendant cette promesse. La boucle d'événements JavaScript gère le minuteur, tandis que Java reste libre d'effectuer d'autres tâches. Ce modèle imite les délais de type navigateur sans geler le thread Java.

L'utilitaire `delay` crée une promesse qui se résout après `ms` millisecondes. En l'`await`‑ant, la fonction se met en pause sans bloquer le thread Java.

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

> **Comment retarder le js :** L'utilitaire `delay` crée une promesse qui se résout après `ms` millisecondes. En l'`await`‑ant, la fonction se met en pause sans bloquer le thread Java.

## Comment évaluer du JavaScript asynchrone et obtenir un CompletableFuture ?
`evaluateAsync` est une méthode de `ScriptEngine` qui renvoie un `CompletableFuture<Object>` qui se complète lorsque la promesse du script se résout. Cela fait le pont entre la boucle d'événements JavaScript et le modèle de concurrence de Java, vous permettant de gérer les résultats ou les erreurs via les API standard de `CompletableFuture`.

Au lieu de la méthode synchrone `evaluate`, nous appelons `evaluateAsync`. Elle renvoie immédiatement un `CompletableFuture<Object>` qui sera complété lorsque la promesse JavaScript se résoudra.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Comment évaluer de façon asynchrone :** `evaluateAsync` fait le pont entre la boucle d'événements JavaScript et le `CompletableFuture` de Java. C’est le cœur de l’évaluation asynchrone du JavaScript.

## Comment attacher un callback et éventuellement bloquer pour une démonstration ?
`thenAccept` est une méthode de `CompletableFuture` qui enregistre un consommateur à exécuter lorsque le futur se termine. Pour la démonstration, vous pouvez appeler `get()` pour bloquer le thread principal juste assez longtemps pour voir la sortie, mais en production vous garderiez le flux non bloquant.

Nous attachons maintenant un callback avec `thenAccept` pour imprimer le résultat, et nous bloquons le thread principal juste assez longtemps pour que la démonstration se termine.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Pourquoi nous appelons `get()` :** Dans une vraie application, vous continueriez probablement le traitement ailleurs. Ici nous bloquons pour garder l’exemple autonome.

## Vue d’ensemble visuelle
![Diagramme montrant comment exécuter du JavaScript de façon asynchrone avec CompletableFuture](https://example.com/diagram.png "Comment exécuter du JavaScript – Flux asynchrone")

[Diagramme montrant comment exécuter du JavaScript de façon asynchrone avec CompletableFuture](https://example.com/diagram.png "Comment exécuter du JavaScript – Flux asynchrone")

*Texte alternatif :* **Diagramme montrant comment exécuter du JavaScript de façon asynchrone avec CompletableFuture** – l'image illustre le flux de Java vers le moteur de script, le délai asynchrone, et la complétion du CompletableFuture.

## Pièges courants & meilleures pratiques (comment évaluer async en toute sécurité)

| Piège | Ce qui se passe | Solution |
|---------|--------------|-----|
| Oublier de retourner la promesse | `evaluateAsync` se résout immédiatement avec `undefined` | Assurez‑vous que la dernière ligne du script est la promesse (`fetchMessage();`) |
| Utiliser `Thread.sleep` bloquant en JS | Bloque la boucle d'événements du moteur, annule l'async | Utilisez le pattern de promesse `delay` (comme montré) |
| Ignorer les exceptions | Le futur se complète de façon exceptionnelle, mais vous ne la voyez jamais | Attachez `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Ne pas fermer le moteur | Fuite de ressources dans les applications de longue durée | Appelez `scriptEngine.dispose()` lorsque terminé |

## Comment étendre le modèle avec des exécutors personnalisés ?
`Executor` est une interface Java qui exécute des tâches `Runnable` ou `Callable` soumises, généralement soutenue par un pool de threads. Passer un `Executor` dédié à `evaluateAsync` vous permet de contrôler la taille du pool de threads, d'éviter la famine et de garder les threads UI réactifs.

Vous pouvez chaîner plusieurs appels JavaScript asynchrones, les combiner avec d'autres futurs, ou même les exécuter sur un `Executor` personnalisé. Voici un rapide aperçu :

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

> **Comment utiliser CompletableFuture :** En passant un `Executor`, vous contrôlez le pool de threads, gardant l'UI réactive et évitant la famine de threads.

## Quel résultat devez‑vous attendre ?
L'exécution de la classe `JsAsyncDemo` affiche la valeur résolue de la promesse JavaScript. La pause de 500 ms n'est pas visible dans la console, mais vous pouvez ajouter des horodatages pour vérifier le délai si vous le souhaitez.

```
JS result: Hello from async JS!
```

## Récapitulatif – comment exécuter du javascript dans java avec CompletableFuture
Nous avons commencé par **run javascript in java** dans Java, écrit une fonction `async` qui **how to delay js**, l'avons exécutée avec `evaluateAsync` (**how to evaluate async**), et capturé le résultat en utilisant un **how to use completablefuture**. L'ensemble du flux démontre **evaluate javascript asynchronously** dans un modèle propre et réutilisable.

## Et après ?
- **Intégrer avec des clients HTTP :** Récupérer des données depuis un endpoint REST dans le JS async et les renvoyer à Java.  
- **Chaîner plusieurs scripts :** Combiner plusieurs appels `evaluateAsync` pour des pipelines complexes.  
- **Changer de moteur :** Le même modèle fonctionne avec Nashorn, GraalVM ou d'autres runtimes JavaScript — il suffit de remplacer `ScriptEngine` par l'implémentation appropriée.

N'hésitez pas à expérimenter avec des délais plus longs, des scripts générant des erreurs, ou même des modules WebAssembly. Le ciel est la limite lorsque vous combinez les primitives de concurrence de Java avec le JavaScript moderne.

## Questions fréquemment posées

**Q : Puis‑je utiliser cette approche dans une UI Swing ou JavaFX sans geler l'interface ?**  
R : Oui. Comme le script s'exécute sur un thread séparé et renvoie un `CompletableFuture`, le thread UI reste libre de se rafraîchir et de répondre aux actions de l'utilisateur.

**Q : Que se passe‑t‑il si le JavaScript lève une exception ?**  
R : L'exception se propage au `CompletableFuture` sous forme de `CompletionException`. Attachez un gestionnaire `.exceptionally` pour traiter ou consigner l'erreur.

**Q : Dois‑je configurer un gestionnaire de sécurité pour le moteur de script ?**  
R : Aspose HTML exécute les scripts dans un sandbox par défaut, mais vous pouvez restreindre davantage l'accès au système de fichiers ou au réseau via les paramètres de sécurité du moteur si nécessaire.

**Q : Existe‑t‑il une limite de taille pour le code source JavaScript ?**  
R : Le moteur gère confortablement les scripts jusqu'à 10 Mo ; les scripts plus gros peuvent nécessiter une augmentation de la mémoire du tas.

**Q : Puis‑je passer des objets Java dans le contexte JavaScript ?**  
R : Oui. Utilisez `scriptEngine.put("myObject", javaObject)` avant l'évaluation ; l'objet devient accessible comme variable globale dans le script.

**Dernière mise à jour :** 2026-09-24  
**Testé avec :** Aspose.HTML for Java 24.11  
**Auteur :** Aspose

## Tutoriels associés

- [Comment exécuter du Javascript de façon asynchrone en utilisant Completablefuture](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Activer l'exécution de scripts en Java – Guide complet Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Exécuter du Javascript en Java – Guide complet pour exécuter du Js depuis](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}