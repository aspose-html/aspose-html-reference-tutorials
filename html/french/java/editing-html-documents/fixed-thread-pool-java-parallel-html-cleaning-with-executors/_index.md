---
category: general
date: 2026-01-01
description: Apprenez à utiliser un pool de threads fixe en Java pour supprimer les
  balises script des fichiers HTML. Cet exemple d’ExecutorService en Java montre comment
  charger efficacement des documents HTML.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: fr
og_description: Maîtrisez le pool de threads fixe en Java pour supprimer les balises
  script des fichiers HTML. Exemple complet d'ExecutorService en Java avec les étapes
  de chargement d'un document HTML.
og_title: Pool de threads fixe Java – Guide de nettoyage HTML parallèle
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Pool de threads fixe Java – Nettoyage HTML parallèle avec ExecutorService
url: /fr/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed thread pool java – Nettoyage parallèle de HTML avec ExecutorService

Vous avez déjà eu besoin d'un **fixed thread pool java** pour accélérer le traitement en masse de fichiers HTML ? Vous n'êtes pas seul. Lorsque vous avez des dizaines — voire des centaines — de fichiers HTML remplis d'éléments `<script>`, exécuter le travail séquentiellement peut donner l'impression de regarder la peinture sécher.  

Dans ce tutoriel, nous vous montrerons exactement comment créer un **fixed thread pool java**, charger chaque document HTML, supprimer tout le JavaScript (balises `<script>`), et enregistrer les fichiers nettoyés — le tout en parallèle à l'aide d'un **executorservice example java**. À la fin, vous disposerez d'un programme prêt à l'emploi qui supprime efficacement les balises script, et vous comprendrez pourquoi un fixed thread pool est souvent le meilleur compromis pour les charges de travail liées au CPU.

## Ce que vous allez réaliser

- Configurer un `ExecutorService` avec un nombre fixe de threads.  
- Charger les fichiers HTML en utilisant `HTMLDocument` d'Aspose.HTML.  
- Utiliser un sélecteur CSS pour **remove script tags** (ou tout autre élément indésirable).  
- Enregistrer la sortie sanitisée avec une convention de nommage claire.  
- Gérer l'arrêt et la terminaison gracieuse du pool de threads.

Pas d'outils de construction externes, pas de magie cachée — juste du Java 8+ pur et Aspose.HTML.

## Prérequis

| Exigence | Pourquoi c'est important |
|-------------|----------------|
| **Java 8 ou plus récent** | Nécessaire pour les expressions lambda et l'API `ExecutorService`. |
| **Aspose.HTML for Java** (télécharger depuis <https://products.aspose.com/html/java/>) | Fournit la classe `HTMLDocument` utilisée pour charger et manipuler le HTML. |
| **Un dossier contenant des fichiers HTML d'exemple** | La démo traite des fichiers comme `input1.html`, `input2.html`, etc. |
| **Un IDE ou un outil de construction en ligne de commande** (IntelliJ, Eclipse, Maven, Gradle) | Pour compiler et exécuter le code. |

Si vous n'avez pas encore ajouté Aspose.HTML à votre projet, déposez le JAR dans votre dossier `libs` et ajoutez-le au classpath, ou déclarez la dépendance Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

## Étape 1 : Créer un Fixed Thread Pool java

Un **fixed thread pool java** vous fournit un nombre prévisible de threads de travail qui restent actifs pendant toute la tâche. Cela évite le surcoût de création et de destruction constante de threads, ce qui est particulièrement utile lorsque chaque tâche est de courte durée, comme le chargement et le nettoyage d'un seul fichier HTML.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Astuce :** Choisissez la taille du pool en fonction du nombre de cœurs CPU (`Runtime.getRuntime().availableProcessors()`) plus une petite marge si les tâches impliquent des I/O.

## Étape 2 : Lister les fichiers HTML à traiter

Vous pourriez parcourir un répertoire dynamiquement, mais pour plus de clarté nous allons coder en dur un tableau. Remplacez `"YOUR_DIRECTORY"` par le chemin réel sur votre machine.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Si vous préférez une approche dynamique, `Files.list(Paths.get("YOUR_DIRECTORY"))` peut remplir le tableau automatiquement.

## Étape 3 : Soumettre une tâche de nettoyage pour chaque fichier

Chaque fichier reçoit sa propre tâche **executorservice example java**. À l'intérieur du lambda nous :

1. Ouvrons le fichier avec `HTMLDocument`.  
2. **Remove script tags** en utilisant un sélecteur CSS (`"script"`).  
3. Enregistrons la version nettoyée avec le suffixe `_clean.html`.

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Pourquoi cela fonctionne :** `querySelectorAll("script")` renvoie une collection dynamique de chaque élément `<script>`. La boucle `forEach` détache alors chaque nœud de son parent, supprimant effectivement **remove javascript html** de la source.

## Étape 4 : Arrêter le pool et attendre la fin

Une terminaison gracieuse est cruciale ; vous ne voulez pas que des threads errants restent actifs après la fin du travail.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Si vous avez de nombreux fichiers ou de gros documents, augmentez le délai d'attente à une valeur plus élevée.

## Exemple complet fonctionnel

En combinant le tout, voici le programme complet que vous pouvez copier‑coller dans `ParallelProcessingDemo.java` et exécuter.

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme, vous verrez des messages de console comme :

```
All files cleaned successfully!
```

Et dans votre répertoire, vous trouverez :

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Chaque fichier `_clean.html` sera identique à son homologue original, à l'exception de chaque bloc `<script>`.

## Questions fréquemment posées (FAQ)

**Q : Puis‑je changer la taille du pool de threads à l'exécution ?**  
R : Oui. Utilisez `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` pour une taille dynamique basée sur la machine hôte.

**Q : Que faire si mes fichiers HTML contiennent des gestionnaires d'événements en ligne (`onclick`, `onload`)?**  
R : Le sélecteur actuel ne supprime que les balises `<script>`. Pour éliminer les gestionnaires en ligne, il faudrait parcourir tous les éléments et effacer les attributs commençant par `on`. C’est une bonne extension pour un futur tutoriel.

**Q : Aspose.HTML est‑il la seule bibliothèque qui supporte `querySelectorAll` ?**  
R : Non. Des bibliothèques comme jsoup offrent également des sélecteurs CSS, mais Aspose.HTML vous fournit une API DOM complète qui reflète le comportement du navigateur, ce qui est pratique pour des tâches de nettoyage complexes.

**Q : Comment gérer des fichiers HTML très volumineux qui pourraient ne pas tenir en mémoire ?**  
R : Pour les fichiers massifs, envisagez des analyseurs en flux (par ex., Saxon pour XML) ou le traitement du fichier par morceaux. Le modèle de fixed thread pool reste applicable ; il suffit de remplacer `HTMLDocument` par une solution de streaming.

## Prochaines étapes et sujets associés

- **Remove JavaScript HTML with jsoup** – une alternative légère si vous n'avez pas besoin d'un support DOM complet.  
- **Dynamic thread pool sizing** – explorez `ThreadPoolExecutor` pour un contrôle plus fin.  
- **Batch processing with `CompletableFuture`** – combinez des futures pour des pipelines plus riches.  
- **HTML sanitization beyond scripts** – supprimez les styles, les iframes ou les attributs non sûrs.  

Tous ces éléments s'appuient sur la même base **executorservice example java** que nous avons présentée ici.

## Conclusion

Vous disposez maintenant d'un exemple solide, prêt pour la production, montrant comment utiliser un **fixed thread pool java** pour **remove script tags** d'un lot de fichiers HTML. En exploitant `ExecutorService`, chaque fichier est traité en parallèle, réduisant considérablement le temps d'exécution total. L'approche est modulaire, facile à étendre, et fonctionne avec n'importe quelle bibliothèque HTML compatible Java offrant une capacité `load html document`.

Essayez-le, ajustez la taille du pool, ou ajoutez des règles de nettoyage supplémentaires — votre prochaine aventure de traitement HTML n'est qu'à quelques lignes.

![Illustration Fixed thread pool java](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}