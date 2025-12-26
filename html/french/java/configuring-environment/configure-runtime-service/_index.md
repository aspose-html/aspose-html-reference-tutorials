---
date: 2025-12-10
description: Apprenez à définir le délai d’attente dans Aspose.HTML pour Java, à configurer
  le service d’exécution pour convertir le HTML en PNG, à prévenir les boucles infinies
  et à améliorer les performances.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Comment définir le délai d'expiration dans le service d'exécution Aspose.HTML
  pour Java
url: /fr/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir un délai d'attente dans le service d'exécution d'Aspose.HTML pour Java

## Introduction
Si vous cherchez **how to set timeout** pour les scripts lors de l'utilisation d'Aspose.HTML pour Java, vous êtes au bon endroit. Contrôler l'exécution des scripts non seulement empêche les boucles infinies, mais vous aide également à **convert html to png** plus rapidement et à garder votre application réactive. Dans ce tutoriel, nous parcourrons les étapes exactes pour configurer le Runtime Service, limiter l'exécution des scripts et finalement produire une image PNG à partir de HTML sans bloquer votre programme.

## Réponses rapides
- **Que fait le Runtime Service ?** Il vous permet de contrôler le temps d'exécution des scripts et de gérer les ressources lors du traitement du HTML.
- **Comment définir le délai d'attente pour JavaScript ?** Utilisez `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.
- **Puis-je empêcher les boucles infinies ?** Oui – le délai d'attente interrompt les boucles qui dépassent la limite définie.
- **Cela affecte-t-il la conversion HTML‑vers‑PNG ?** Non, la conversion se poursuit une fois le script terminé ou interrompu par le délai d'attente.
- **Quelle version d'Aspose.HTML est requise ?** La dernière version disponible sur la page de téléchargement d'Aspose.

## Prérequis
Avant de Sous-marin dans les détails, assurez-vous de disposer de ce qui suit :

1. **Java Development Kit (JDK)** – installez‑le depuis [site Web d'Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. **Aspose.HTML for Java Library** – récupérez la dernière version sur la [Aspose releases page](https://releases.aspose.com/html/java/).
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans conviendront parfaitement.
4. **Connaissances de base de Java et HTML** – indispensable pour suivre les extraits de code.

## Importer des packages
Tout d'abord, importez les classes dont vous aurez besoin. L'import `java.io.IOException` est requis pour la gestion des fichiers.

```java
import java.io.IOException;
```

## Étape 1 : Créer un fichier HTML avec du code JavaScript
Nous allons commencer par générer un fichier HTML simple contenant une boucle JavaScript. Cette boucle s'exécuterait indéfiniment si nous n'imposions pas de délai d'attente, ce qui en fait une démonstration parfaite pour le Runtime Service.

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

## Étape 2 : Configurer l’objet de configuration
Ensuite, créez une instance de `Configuration`. Cet objet constitue la colonne vertébrale de tous les services Aspose.HTML, y compris le Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Étape 3 : Configurer le service d’exécution
Voici où nous appliquons réellement **how to set timeout**. En récupérant le `IRuntimeService` depuis la configuration, nous pouvons définir une limite d'exécution JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` limite l'exécution du script à **5 seconds**, empêchant ainsi efficacement **preventing infinite loops**.  
- Cela **limits script execution** également pour tout code lourd côté client.

## Étape 4 : Charger le document HTML avec la configuration
Chargez maintenant le fichier HTML en utilisant la configuration qui contient notre règle de délai d'attente.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Le document respecte le délai d'attente défini précédemment, de sorte que la boucle infinie sera arrêtée après 5 secondes.

## Étape 5 : Convertir le HTML en PNG
Avec le document chargé en toute sécurité, nous pouvons **convert html to png**. La conversion n'intervient qu'après la fin du script ou son interruption par le délai d'attente.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` indique à Aspose.HTML de produire une image PNG.  
- Le fichier résultant, **runtime-service_out.png**, montre le HTML rendu sans blocage.

## Étape 6 : Nettoyage des ressources
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

- Une disposition correcte est essentielle pour les applications à long terme.

## Conclusion
Vous venez d'apprendre **how to set timeout** pour l'exécution JavaScript dans Aspose.HTML pour Java, comment **prevent infinite loops**, et comment **convert html to png** en toute sécurité. En configurant le Runtime Service, vous obtenez un contrôle granulaire du comportement des scripts, ce qui se traduit par des temps de démarrage plus rapides et des conversions plus fiables. Expérimentez avec différentes valeurs de délai d'attente pour répondre à vos charges de travail spécifiques, et vous constaterez une amélioration notable des performances.

## Questions fréquemment posées

**Q : Quel est l'objectif du service d'exécution dans Aspose.HTML pour Java ?**
R : Il vous permet de contrôler le temps d'exécution des scripts, aidant à **empêcher les boucles infinies** et à garder les conversions réactives.

**Q : Comment puis-je télécharger Aspose.HTML pour Java ?**
R : Obtenez la dernière version depuis la [page des versions](https://releases.aspose.com/html/java/).

**Q : Est-il nécessaire de supprimer les objets `document` et `configuration` ?**
R : Oui, la libération des ressources natives et empêche les fuites de mémoire.

**Q : Puis-je définir le délai d'expiration JavaScript sur une valeur autre que 5 secondes ?**
R : Absolument – ​​modifiez l'argument de `TimeSpan.fromSeconds()` selon la limite qui convient à votre scénario.

**Q : Où puis-je trouver de l'aide si je rencontre des problèmes ?**
R : Consultez le [forum Aspose.HTML](https://forum.aspose.com/c/html/29) pour obtenir de l'aide de la communauté et du personnel.

---

**Dernière mise à jour :** 2025-12-10
**Testé avec :** Aspose.HTML pour Java 24.11 (dernière version)
**Auteur :** Aspose 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}