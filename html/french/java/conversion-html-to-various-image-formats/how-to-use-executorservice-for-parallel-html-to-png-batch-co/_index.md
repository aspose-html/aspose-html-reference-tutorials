---
category: general
date: 2026-02-21
description: Comment utiliser ExecutorService pour convertir rapidement du HTML en
  PNG. Apprenez à convertir en lot des fichiers HTML avec des tâches parallèles en
  Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: fr
og_description: Comment utiliser ExecutorService pour convertir en lot des fichiers
  HTML en PNG. Guide étape par étape avec un exemple Java complet.
og_title: Comment utiliser ExecutorService pour la conversion parallèle de HTML en
  PNG
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Comment utiliser ExecutorService pour la conversion par lots parallèle de HTML
  en PNG
url: /fr/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

We must keep the final shortcodes unchanged.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser ExecutorService pour la conversion par lots HTML‑vers‑PNG en parallèle

Vous vous êtes déjà demandé **comment utiliser ExecutorService** lorsque vous avez un dossier rempli de pages HTML qui doivent devenir des images PNG ? Vous n'êtes pas le seul—de nombreux développeurs rencontrent ce problème lorsque leur pipeline de reporting web se bloque sur une boucle de conversion monothread.  

Bonne nouvelle ? En quelques lignes de Java et avec le puissant `Converter` d’Aspose.HTML, vous pouvez créer un pool de threads de travail, fournir chaque fichier HTML au convertisseur, et voir les images apparaître en parallèle. Dans ce tutoriel, nous aborderons également les bases de **convert html to png**, vous montrerons comment **run parallel tasks**, et vous fournirons un script **batch convert html files** prêt à l’emploi.

## Prérequis

- Java 17 ou supérieur (le code utilise l’API moderne `java.nio.file`).  
- Bibliothèque Aspose.HTML for Java dans votre classpath. Vous pouvez la récupérer depuis Maven Central :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Un répertoire contenant les fichiers source `.html` et un dossier de sortie vide.  
- Une quantité modeste de RAM—chaque conversion s’exécute dans son propre thread, donc la taille du pool doit correspondre au nombre de cœurs CPU dont vous disposez.

> **Astuce :** Si vous êtes sur une machine avec hyper‑threading, `Runtime.getRuntime().availableProcessors()` renvoie généralement le nombre optimal de cœurs.

## Étape 1 – Définir les chemins d’entrée et de sortie

Tout d’abord, nous devons indiquer à Java où se trouvent les fichiers HTML et où les PNG doivent être enregistrés. L’utilisation d’objets `Path` rend le code indépendant de la plateforme.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Pourquoi c’est important :** Créer le répertoire de sortie à l’avance évite le `FileNotFoundException` lorsque le premier thread de travail tente d’écrire un fichier.

## Étape 2 – Créer un pool de threads à taille fixe

Le cœur de **how to use ExecutorService** réside dans la création d’un pool adapté à votre matériel. Un pool *fixe* garantit que nous ne créerons pas plus de threads que nous ne pouvons réellement exécuter.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Explication :** `ExecutorService` abstrait la gestion des threads de bas niveau. En utilisant `newFixedThreadPool`, nous laissons la JVM réutiliser les threads, ce qui réduit la surcharge liée à la création et à la destruction constantes de ceux‑ci.

## Étape 3 – Soumettre une tâche de conversion par fichier HTML

Nous parcourons maintenant le répertoire d’entrée, sélectionnons chaque fichier `*.html`, et le transmettons au pool. Chaque tâche est une petite lambda qui appelle `Converter.convert`.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Que se passe-t-il en coulisses ?

1. `DirectoryStream` lit les noms de fichiers de façon paresseuse, de sorte que l’utilisation de la mémoire reste faible même avec des milliers de fichiers.  
2. La lambda capture `htmlFile` et `outputDir`—pas besoin d’une classe `Runnable` séparée.  
3. `Converter.convert` est un appel bloquant qui lit le HTML, le rend, et écrit un PNG. Comme chaque appel s’exécute dans son propre thread, plusieurs fichiers sont traités simultanément—exactement le comportement attendu lorsque vous **run parallel tasks**.

## Étape 4 – Fermer le pool proprement

Après que toutes les tâches soient mises en file d’attente, nous indiquons au pool d’arrêter d’accepter de nouveaux travaux et d’attendre que tout se termine. Si quelque chose se bloque, le délai d’attente s’interrompra après une heure, ce qui est généreux pour la plupart des jobs par lots.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Cas particulier :** Si vous avez des fichiers HTML exceptionnellement volumineux, vous pourriez vouloir augmenter le délai d’attente ou surveiller l’utilisation de la mémoire. Ajouter `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` force le thread appelant à exécuter les tâches excédentaires, évitant ainsi `RejectedExecutionException`.

## Exemple complet, prêt à l’exécution

Voici le programme complet, copiable‑collable dans un seul fichier `ParallelBatchConversion.java`.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Sortie attendue

L’exécution du programme affiche une ligne pour chaque conversion réussie :

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Si un fichier échoue, vous verrez une ligne d’erreur avec le message d’exception, ce qui rend le débogage simple.

## Comment étendre ce modèle

- **Différents formats d’image :** Remplacez l’extension `.png` par `.jpg` ou `.bmp` et ajustez les options de conversion Aspose en conséquence.  
- **Nombre de threads dynamique :** Pour des charges de travail I/O‑bound, vous pourriez augmenter la taille du pool (`availableProcessors() * 2`).  
- **Suivi de progression :** Remplacez `System.out.println` par une bibliothèque de barre de progression thread‑safe comme `jline` ou consignez dans un fichier.  
- **Gestion des erreurs :** Collectez les chemins échoués dans une `List<Path>` et réessayez après la fin de la boucle principale.

## Questions fréquentes

**Q : Cela fonctionne-t-il sous Windows et Linux ?**  
R : Oui. `java.nio.file` abstrait le système de fichiers sous‑jacent, donc le même code s’exécute sans modification sur tout OS supportant Java.

**Q : Que se passe-t-il si j’ai plus de 10 000 fichiers HTML ?**  
R : L’itérateur `DirectoryStream` lit les entrées de façon paresseuse, donc la mémoire reste basse. Assurez‑vous simplement que votre disque dispose de suffisamment d’espace libre pour la sortie PNG.

**Q : Puis‑je limiter la mémoire utilisée par chaque conversion ?**  
R : Aspose.HTML vous permet de configurer le moteur de rendu via `HtmlLoadOptions` et `ImageSaveOptions`. Vous pouvez définir une taille maximale de bitmap ou activer le rendu basse qualité pour garder la consommation RAM sous contrôle.

## Conclusion

Nous avons parcouru **how to use ExecutorService** pour **batch convert html files** en images PNG, expliqué pourquoi un pool à taille fixe est le point idéal pour le rendu CPU‑bound, et vous avons fourni un programme Java complet, copiable‑collable. En suivant les étapes ci‑dessus, vous transformerez une boucle lente monothread en un pipeline rapide et évolutif capable de gérer des milliers de fichiers avec une seule commande.

Prêt pour le prochain défi ? Essayez de remplacer `Converter.convert` par l’export PDF d’Aspose pour **convert html to pdf**, ou intégrez cette logique dans un microservice Spring Boot qui accepte les requêtes de téléchargement‑et‑conversion. L’idée principale—utiliser `ExecutorService` pour **run parallel tasks**—reste la même, et vous la trouverez utile dans d’innombrables scénarios de traitement par lots.

Bon codage, et que vos threads restent toujours vivants ! 

![diagramme d’utilisation d’executorservice](placeholder.png "Diagramme illustrant le flux de travail du pool de threads pour la conversion parallèle HTML‑vers‑PNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}