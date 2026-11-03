---
category: general
date: 2026-05-28
description: Comment utiliser Executor en Java avec un pool de threads fixe, extraire
  le texte d’un HTML et accélérer le traitement – un exemple complet de pool de threads
  Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: fr
og_description: comment utiliser l'exécuteur en Java avec un pool de threads fixe.
  Découvrez un exemple complet de pool de threads Java qui extrait efficacement le
  texte des fichiers HTML.
og_title: Comment utiliser Executor en Java – Guide du pool de threads fixe
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Comment utiliser Executor en Java – Guide du pool de threads fixe
url: /fr/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Executor en Java – Guide du pool de threads fixe

Vous vous êtes déjà demandé **comment utiliser executor** pour exécuter de nombreuses tâches simultanément sans exploser votre mémoire ? Vous n'êtes pas seul. Dans de nombreuses applications réelles, vous devez parcourir un dossier de fichiers HTML, extraire le texte du corps et le faire rapidement—c’est exactement le scénario que résout ce tutoriel.

Nous allons parcourir une implémentation **fixed thread pool java** qui extrait le texte d’un HTML, affiche le nombre de caractères de chaque fichier et se ferme proprement. À la fin, vous disposerez d’un **java thread pool example** autonome que vous pourrez intégrer à n’importe quel projet, ainsi que de quelques astuces pour personnaliser la taille du pool et gérer les cas limites.

> **Ce dont vous aurez besoin**  
> * Java 17 (ou tout JDK récent)  
> * Une petite bibliothèque d’analyse HTML – nous utiliserons *jsoup* car elle est éprouvée et zéro configuration.  
> * Une poignée de fichiers *.html* d’exemple dans le répertoire de votre choix.

---

## Comment utiliser Executor avec un pool de threads fixe

Le cœur de tout programme Java fortement concurrent est le `ExecutorService`. En créant un **fixed thread pool**, nous indiquons à la JVM de maintenir exactement N threads de travail actifs, ce qui évite le surcoût de création de threads et limite l’utilisation des ressources.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Pourquoi c’est important :*  
Si vous lanciez un nouveau `Thread` pour chaque fichier HTML, le système d’exploitation devrait planifier des dizaines de threads sur un ordinateur portable modeste, entraînant un bourrage de commutations de contexte. Un pool fixe réutilise les mêmes quatre threads, vous offrant une utilisation prévisible du CPU.

---

## Définir les fichiers HTML à traiter – Fixed Thread Pool Java

Ensuite, nous listons les fichiers que nous voulons injecter dans le pool. Dans une vraie application, vous parcourriez probablement un arbre de répertoires ; ici nous restons simples.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Astuce :* `List.of` renvoie une liste immuable, ce qui est sûr à partager entre threads sans synchronisation supplémentaire.

---

## Soumettre une tâche distincte pour chaque fichier HTML

Nous transmettons maintenant chaque chemin à l’executor. Le lambda que nous soumettons s’exécutera **en parallèle** sur l’un des quatre threads de travail.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Pourquoi nous **encapsulons** la logique dans une méthode** (`extractBodyText`) deviendra clair dans la section suivante—cela garde le lambda propre et nous permet de réutiliser le code d’extraction ailleurs.

---

## Extraire le texte du HTML – La logique principale

Voici l’assistant réutilisable qui **extrait le texte du html** à l’aide de Jsoup. Il ouvre le fichier, analyse le DOM et renvoie le texte brut du corps.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Pourquoi Jsoup ?* C’est léger, gère les balises malformées avec grâce, et ne nécessite pas de moteur de navigateur complet. La méthode lance `IOException` afin que l’appelant puisse décider comment journaliser ou récupérer—parfait pour un scénario de thread‑pool où vous ne voulez pas qu’un seul fichier défectueux termine tout l’executor.

---

## Fermer proprement l’Executor – Créer un Fixed Thread Pool

Après avoir soumis toutes les tâches, nous devons indiquer au pool d’arrêter d’accepter de nouveaux travaux et de terminer ceux déjà en file d’attente.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explication :* `shutdown()` empêche les nouvelles soumissions, tandis que `awaitTermination` bloque jusqu’à ce que chaque tâche d’analyse se termine (ou que le délai expire). Si quelque chose se bloque, `shutdownNow()` tente d’annuler les tâches en cours. Ce modèle est la façon recommandée **de créer un fixed thread pool** en toute sécurité.

---

## Exemple complet et exécutable

En réunissant tous les éléments, voici un fichier unique que vous pouvez compiler et exécuter. Il comprend les imports nécessaires, la méthode `main`, et l’assistant décrit ci‑dessus.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Sortie attendue** (en supposant que chaque fichier contienne environ 1 200 caractères de texte du corps) :

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Si un fichier est manquant ou malformé, vous verrez une trace de pile imprimée sur `stderr`, mais les autres tâches continueront sans être affectées—exactement ce que doit faire un **java thread pool example** bien comporté.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| *Et si j’ai plus de quatre fichiers ?* | Le pool mettra en file d’attente les tâches supplémentaires et les exécutera dès qu’un thread sera disponible. Aucun code supplémentaire n’est nécessaire. |
| *Dois‑je utiliser `newCachedThreadPool` à la place ?* | `newCachedThreadPool` crée des threads à la demande et peut croître de façon illimitée, ce qui est risqué pour les tâches lourdes en I/O. Un **fixed thread pool** vous offre une utilisation prévisible de la mémoire et du CPU. |
| *Comment changer la taille du pool en fonction des cœurs CPU ?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` est un schéma courant. |
| *Et si l’analyse échoue pour un fichier ?* | Le `catch (IOException e)` à l’intérieur du lambda isole l’échec, le journalise, et laisse le reste du pool continuer à travailler. |
| *Puis‑je renvoyer le texte extrait à l’appelant ?* | Oui—utilisez `Future<String>` au lieu de `submit(Runnable)`. Le code ressemblerait à `Future<String> f = executor.submit(() -> extractBodyText(path));` puis plus tard `String result = f.get();`. |

---

## Conclusion

Nous avons couvert **comment utiliser executor** pour lancer un **fixed thread pool java** qui traite une collection de fichiers HTML en parallèle, extrait leur texte du corps et indique le nombre de caractères. Le **java thread pool example** complet montre une gestion correcte des ressources, le traitement des erreurs, et une méthode d’extraction réutilisable.

Prochaines étapes ? Essayez de remplacer l’implémentation `extractBodyText` par un scraper plus sophistiqué, expérimentez avec une taille de pool plus grande, ou alimentez les résultats dans une base de données. Vous pouvez également explorer `CompletionService` pour récupérer les résultats dès qu’ils sont prêts, ce qui est pratique lorsque la taille des fichiers varie largement.

N’hésitez pas à ajuster le chemin du répertoire, ajouter plus de fichiers, ou intégrer cet extrait dans un cadre de crawling plus vaste. Le schéma de base—créer un pool, soumettre des tâches indépendantes, et fermer proprement—reste le même, quel que soit le niveau de complexité de votre charge de travail.

Bon codage, et que vos threads restent toujours actifs (jusqu’à ce que vous les arrêtiez, bien sûr) !

## Tutoriels associés

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}