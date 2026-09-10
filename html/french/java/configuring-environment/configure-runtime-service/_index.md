---
date: 2026-02-10
description: Apprenez à définir le délai d’attente dans Aspose.HTML pour Java, à configurer
  le Runtime Service pour convertir le HTML en PNG, à prévenir les boucles infinies
  et à améliorer les performances.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Comment définir le délai d’attente dans le service d’exécution Aspose.HTML
  pour Java
url: /fr/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir un délai d’attente dans Aspose.HTML pour le service d’exécution Java

## Introduction
Si vous cherchez **comment définir un délai d’attente** pour les scripts lorsque vous travaillez avec Aspose.HTML pour Java, vous êtes au bon endroit. Contrôler l’exécution des scripts permet non seulement d’éviter les boucles infinies, mais aussi d’**convertir html en png** plus rapidement et de garder votre application réactive. Dans ce tutoriel, nous parcourrons les étapes exactes pour configurer le Runtime Service, limiter l’exécution des scripts et finalement produire une image PNG à partir de HTML sans bloquer votre programme.

## Comment définir un délai d’attente dans Aspose.HTML Runtime Service
Comprendre le rôle du Runtime Service facilite la compréhension de l’importance d’un délai d’attente. Le service agit comme un bac à sable pour le code côté client, vous donnant la possibilité d’arrêter un JavaScript incontrôlé avant qu’il ne consomme tous les cycles CPU. En définissant un délai d’attente, vous protégez votre serveur contre les scénarios de déni de service et vous assurez que la **conversion html en png** se termine dans un délai prévisible.

## Réponses rapides
- **Que fait le Runtime Service ?** Il vous permet de contrôler le temps d’exécution des scripts et de gérer les ressources lors du traitement du HTML.  
- **Comment définir un délai d’attente pour JavaScript ?** Utilisez `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Puis‑je empêcher les boucles infinies ?** Oui – le délai d’attente interrompt les boucles qui dépassent la limite définie.  
- **Cela affecte‑t‑il la conversion HTML‑to‑PNG ?** Non, la conversion se poursuit une fois le script terminé ou interrompu par le délai d’attente.  
- **Quelle version d’Aspose.HTML est requise ?** La dernière version disponible sur la page de téléchargement d’Aspose.  

## Prérequis
Avant de plonger dans les détails, assurez‑vous de disposer de :

1. **Java Development Kit (JDK)** – téléchargez‑le depuis le site d’[Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML pour Java** – récupérez la dernière version sur la [page des releases Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans conviendront parfaitement.  
4. **Connaissances de base en Java & HTML** – indispensables pour suivre les extraits de code.

## Importer les packages
Tout d’abord, importez les classes dont vous aurez besoin. L’import `java.io.IOException` est requis pour la gestion des fichiers.

```java
import java.io.IOException;
```

## Étape 1 : Créer un fichier HTML avec du code JavaScript
Nous allons commencer par générer un fichier HTML simple contenant une boucle JavaScript. Cette boucle s’exécuterait indéfiniment si aucun délai d’attente n’était imposé, ce qui en fait une démonstration parfaite pour le Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Le script `while(true) {}` représente une boucle potentiellement infinie.  
- `FileWriter` écrit le contenu HTML dans **runtime-service.html**.

## Étape 2 : Configurer l’objet Configuration
Ensuite, créez une instance de `Configuration`. Cet objet constitue la colonne vertébrale de tous les services Aspose.HTML, y compris le Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Étape 3 : Configurer le Runtime Service
C’est ici que nous allons réellement **comment définir un délai d’attente**. En récupérant le `IRuntimeService` depuis la configuration, nous pouvons définir une limite d’exécution JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` limite l’exécution du script à **5 secondes**, empêchant ainsi les boucles infinies.  
- Cela **limite également l’exécution des scripts** pour tout code client lourd.

## Étape 4 : Charger le document HTML avec la configuration
Chargez maintenant le fichier HTML en utilisant la configuration qui contient notre règle de délai d’attente.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Le document respecte le délai d’attente défini précédemment, de sorte que la boucle infinie sera arrêtée après 5 secondes.

## Étape 5 : Convertir le HTML en PNG
Avec le document chargé en toute sécurité, nous pouvons **convertir html en png**. La conversion n’a lieu qu’après la fin du script ou son interruption par le délai d’attente.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` indique à Aspose.HTML de produire une image PNG.  
- Le fichier résultant, **runtime-service_out.png**, montre le HTML rendu sans blocage.

## Étape 6 : Nettoyer les ressources
Enfin, libérez les objets pour libérer la mémoire et éviter les fuites.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Une libération correcte est essentielle pour les applications à longue durée d’exécution.

## Pourquoi c’est important
Définir un délai d’attente n’est pas seulement une mesure de sécurité ; cela améliore directement la fiabilité des pipelines de **conversion html en png**. Lorsque vous intégrez Aspose.HTML dans un service web qui traite du HTML généré par les utilisateurs, un script malveillant pourrait sinon bloquer un fil d’exécution indéfiniment. Un délai d’attente modeste (par ex., 5 secondes) donne aux scripts légitimes le temps de s’exécuter tout en coupant les comportements abusifs.

## Pièges courants & dépannage
- **Délai trop court** – Les pages complexes avec de nombreuses ressources peuvent nécessiter une limite plus longue. Augmentez la valeur du `TimeSpan` si vous constatez des terminaisons prématurées.  
- **Oubli de libération** – Omettre d’appeler `dispose()` peut entraîner des fuites de mémoire native, surtout lors du traitement de nombreux documents en boucle.  
- **Objet de configuration incorrect** – Récupérez toujours le `IRuntimeService` depuis la même instance de `Configuration` que vous utilisez pour charger le document ; sinon le délai d’attente ne sera pas appliqué.

## Questions fréquentes

**Q : Quel est le rôle du Runtime Service dans Aspose.HTML pour Java ?**  
R : Il vous permet de contrôler le temps d’exécution des scripts, aidant à **prévenir les boucles infinies** et à garder les conversions réactives.

**Q : Comment télécharger Aspose.HTML pour Java ?**  
R : Obtenez la dernière version sur la [page des releases](https://releases.aspose.com/html/java/).

**Q : Est‑il nécessaire de libérer les objets `document` et `configuration` ?**  
R : Oui, la libération libère les ressources natives et évite les fuites de mémoire.

**Q : Puis‑je définir le délai d’attente JavaScript à une valeur différente de 5 secondes ?**  
R : Bien sûr – modifiez l’argument de `TimeSpan.fromSeconds()` selon la limite qui convient à votre scénario.

**Q : Où puis‑je trouver de l’aide en cas de problème ?**  
R : Consultez le [forum Aspose.HTML](https://forum.aspose.com/c/html/29) pour obtenir de l’assistance de la communauté et du personnel.

---

**Dernière mise à jour :** 2026-02-10  
**Testé avec :** Aspose.HTML pour Java 24.11 (dernière version)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}