---
category: general
date: 2026-02-10
description: Apprenez à utiliser un pool de threads fixe en Java pour compter les
  images dans les fichiers HTML, exécuter des tâches simultanément en Java et fermer
  correctement le service d’exécution.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: fr
og_description: Maîtrisez l’utilisation d’un pool de threads fixe en Java pour compter
  les images, traiter les fichiers en parallèle et arrêter le service d’exécution
  en toute sécurité.
og_title: 'Pool de threads fixe Java : compter les images dans des fichiers parallèles'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool : compter les images dans des fichiers parallèles'
url: /fr/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Tutoriel de comptage d'images en parallèle

Vous êtes‑vous déjà demandé comment **java fixed thread pool** à travers des dizaines de fichiers HTML et obtenir rapidement le nombre d'images ? Peut‑être avez‑vous regardé un répertoire de pages, pensé « Je dois savoir combien de balises `<img>` chaque fichier possède », puis réalisé qu’une boucle monothread prendrait une éternité.  

The good news is you don’t need to write a custom thread manager or wrestle with low‑level `Thread` objects. In this guide we’ll show you exactly **comment compter les images** using a *java fixed thread pool*, run tasks concurrently java, and gracefully **shutdown executor service** when the work is done.  

Nous couvrirons tout, de la configuration du pool, la préparation de la liste de fichiers, la soumission de tâches parallèles, la gestion des cas limites, à la vérification de la sortie. À la fin, vous disposerez d’un programme prêt à l’exécution qui démontre **java parallel file processing** de manière propre et maintenable.  

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Java 17 ou plus récent (le code utilise le mot‑clé `var` pour plus de concision, mais vous pouvez rétrograder si besoin).
- Aspose.HTML for Java sur votre classpath – vous pouvez le récupérer depuis Maven Central :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Un petit nombre de fichiers HTML que vous souhaitez analyser (le tutoriel suppose qu’ils se trouvent dans `YOUR_DIRECTORY/`).
- Un IDE ou un outil de construction avec lequel vous êtes à l’aise – IntelliJ IDEA, VS Code, ou simplement `javac` fonctionne très bien.

C’est tout. Aucun serveur supplémentaire, pas de Docker, juste du Java pur et une petite bibliothèque tierce.

## Étape 1 : Créer un java fixed thread pool

Un *java fixed thread pool* vous fournit un ensemble limité de threads de travail qui se réutilisent pour chaque tâche soumise. Cela évite le surcoût de création constante de nouveaux threads et limite le niveau de concurrence, ce qui est crucial lors de la lecture de fichiers depuis le disque.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** Si vous avez un ordinateur portable quad‑core, quatre threads maintiennent chaque cœur occupé sans sur‑saturation. Sur un serveur avec plus de cœurs, vous pouvez augmenter le nombre, mais rappelez‑vous que chaque thread ouvrira un handle de fichier, donc trop de threads peuvent épuiser les limites du système d’exploitation.

## Étape 2 : Lister les fichiers HTML que vous souhaitez analyser

Le prochain élément de **java parallel file processing** consiste simplement à construire un tableau (ou `List`) de chemins de fichiers. Dans un projet réel, vous pourriez parcourir un répertoire de façon récursive, filtrer par extension, ou lire les chemins depuis une base de données. Voici l’approche directe :

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Si vous devez gérer un ensemble dynamique, remplacez le tableau statique par quelque chose comme :

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Ce fragment démontre **java parallel file processing** pour n’importe quel nombre de fichiers sans modifier le reste du code.

## Étape 3 : Soumettre des tâches à **run tasks concurrently java**

Voici le cœur du tutoriel – nous allons **run tasks concurrently java** en soumettant une lambda pour chaque fichier. Chaque tâche charge le document HTML avec Aspose.HTML, interroge tous les éléments `<img>` et affiche le nombre.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Why use a lambda?** Elle rend le code concis et évite de créer une classe `Runnable` séparée. La lambda capture automatiquement `filePath`, ainsi chaque tâche travaille sur son propre fichier.

### Comment **compter les images** efficacement

Aspose.HTML analyse le fichier une fois, construit un DOM, puis `querySelectorAll("img")` s’exécute en O(n) où *n* est le nombre de nœuds. Pour la plupart des pages HTML, c’est négligeable. Si vous aviez besoin d’une approche plus rapide, uniquement en streaming (par ex., pour des fichiers de plusieurs gigaoctets), vous pourriez passer à un analyseur SAX, mais cela sacrifierait la simplicité recherchée.

## Étape 4 : Fermer correctement **shutdown executor service**

N’oubliez jamais de fermer le pool, sinon votre JVM continuera à tourner indéfiniment. Le modèle ci‑dessous est la façon recommandée de **shutdown executor service** tout en attendant que toutes les tâches se terminent :

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**What if a task hangs?** L’appel `shutdownNow()` tente d’interrompre les threads en cours d’exécution. Si votre logique de comptage d’images respecte l’interruption (ce qui n’est pas bloqué par Aspose.HTML sur les I/O), le pool se terminera proprement. Ce modèle est la référence pour toute utilisation de **java fixed thread pool**.

## Étape 5 : Vérifier la sortie

Lancez le programme depuis votre IDE ou via la ligne de commande :

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Une sortie typique ressemble à :

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Si vous voyez les comptes affichés dans un ordre quelconque, c’est normal – les threads terminent à des moments différents. L’essentiel est que chaque fichier soit pris en compte et que le programme se termine proprement après la séquence d’arrêt.

## Exemple complet fonctionnel (prêt à copier‑coller)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Résultat attendu

L’exécution du fragment affiche chaque chemin de fichier suivi du nombre de balises `<img>` qu’il contient, puis la JVM se ferme. Aucun thread persistant, aucune fuite de mémoire.

## Pièges courants & Astuces pro

- **Pitfall:** Utiliser `newCachedThreadPool()` au lieu d’un pool *fixed*. Cela crée des threads illimités, ce qui peut épuiser les descripteurs de fichiers sur de gros lots. Restez avec `newFixedThreadPool`.
- **Pro tip:** Si vos fichiers HTML sont volumineux, envisagez d’augmenter le tas (`-Xmx2g`) ou de passer à un analyseur en streaming. Pour la plupart des pages marketing, le tas par défaut suffit.
- **Pitfall:** Oublier d’appeler `shutdown()` – votre application restera bloquée après l’affichage des résultats. La méthode `shutdownAndAwaitTermination` ci‑dessus le gère de façon robuste.
- **Pro tip:** Enregistrez l’heure de début et de fin de chaque tâche si vous avez besoin de métriques de performance. Un simple `System.nanoTime()` avant et après la construction de `HTMLDocument` indique la durée de l’analyse.
- **Pitfall:** Codage en dur du nombre de threads. Utilisez `Runtime.getRuntime().availableProcessors()` pour choisir une valeur par défaut sensée :

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Sujets connexes que vous pourriez explorer ensuite

- **run tasks concurrently java** avec `CompletableFuture` pour des pipelines plus expressifs.
- Persister les comptes d’images dans une base de données pour des tableaux de bord analytiques.
- Utiliser **java parallel file processing** avec l’API `java.nio.file.Files.walk` combinée aux streams.
- Implémenter un `ThreadFactory` personnalisé pour donner aux threads des noms significatifs (facilite le débogage).

## Conclusion

Nous venons de parcourir un exemple complet et autonome qui montre comment un **java fixed thread pool** peut être exploité pour **how to count images** sur plusieurs fichiers HTML, tout en démontrant la bonne façon de **shutdown executor service**. Le modèle s’adapte bien – remplacez le tableau de fichiers par une liste dynamique, augmentez la taille du pool, et vous obtenez une solution robuste pour toute charge de travail **java parallel file processing**.

Essayez‑le, ajustez le nombre de threads, et ajoutez éventuellement une exportation CSV des résultats. Le ciel est la limite lorsque vous combinez une base solide de concurrence avec une bibliothèque pratique comme Aspose.HTML. Bon codage !  

![java fixed thread pool diagram](image.png){alt="diagramme du java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}