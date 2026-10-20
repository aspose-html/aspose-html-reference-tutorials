---
date: 2026-05-14
description: Apprenez comment définir le délai d'attente dans Aspose.HTML pour Java,
  configurer le Runtime Service pour la conversion html en png, empêcher les boucles
  infinies et améliorer les performances.
keywords:
- html to png conversion
- convert html to png
- java html processing
- prevent infinite loops java
- control script execution
linktitle: Configurer le Runtime Service dans Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-05-14'
  description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  headline: How to Set Timeout for html to png conversion in Aspose.HTML for Java
    Runtime Service
  type: TechArticle
- description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  name: How to Set Timeout for html to png conversion in Aspose.HTML for Java Runtime
    Service
  steps:
  - name: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
    text: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
  - name: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
  - name: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
    text: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
  - name: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
    text: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
  type: HowTo
- questions:
  - answer: It lets you control script execution time, helping to **prevent infinite
      loops** and keep conversions responsive.
    question: What is the purpose of the Runtime Service in Aspose.HTML for Java?
  - answer: Get the latest version from the [releases page](https://releases.aspose.com/html/java/).
    question: How can I download Aspose.HTML for Java?
  - answer: Yes, disposing releases native resources and prevents memory leaks.
    question: Is it necessary to dispose of the `document` and `configuration` objects?
  - answer: Absolutely – change the `TimeSpan.fromSeconds()` argument to whatever
      limit fits your scenario.
    question: Can I set the JavaScript timeout to a value other than 5 seconds?
  - answer: Visit the [Aspose.HTML forum](https://forum.aspose.com/c/html/29) for
      community and staff assistance.
    question: Where can I find help if I run into issues?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Comment définir le délai d'attente pour la conversion html en png dans Aspose.HTML
  pour Java Runtime Service
url: /fr/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir un délai d'attente pour la conversion html en png avec Aspose.HTML pour le service d'exécution Java

## Introduction
Si vous cherchez à **définir un délai d'attente** pour les scripts lors de l'utilisation d'Aspose.HTML pour Java, vous êtes au bon endroit. Contrôler l'exécution des scripts permet non seulement d'éviter les boucles infinies, mais aussi d'accélérer la **conversion html en png** et de garder votre application réactive. Dans ce tutoriel, nous parcourrons les étapes exactes pour configurer le Runtime Service, limiter l'exécution des scripts et, en fin de compte, produire une image PNG à partir de HTML sans bloquer votre programme.

## Réponses rapides
- **À quoi sert le Runtime Service ?** Il vous permet de contrôler le temps d'exécution des scripts et de gérer les ressources lors du traitement du HTML.  
- **Comment définir le délai d'attente pour JavaScript ?** Récupérez `IRuntimeService` depuis la configuration et appelez `setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Puis-je empêcher les boucles infinies ?** Oui – le délai d'attente interrompt les boucles qui dépassent la limite définie.  
- **Cela affecte-t-il la conversion html en png ?** Non, la conversion se poursuit une fois le script terminé ou interrompu par le délai d'attente.  
- **Quelle version d'Aspose.HTML est requise ?** La dernière version disponible sur la page de téléchargement d'Aspose.

## Comment définir un délai d'attente pour la conversion html en png avec le Runtime Service d'Aspose.HTML
Chargez le Runtime Service, définissez un `TimeSpan` (par ex., 5 secondes) à l'aide de `TimeSpan.fromSeconds`, puis appliquez‑le via `setJavaScriptTimeout`. Cela limite l'exécution JavaScript, arrête les boucles incontrôlées et garantit que la conversion se termine de manière prévisible sans consommer indéfiniment les ressources CPU, tout en permettant aux scripts normaux de s'exécuter jusqu'à leur achèvement.

## Prérequis
Avant de plonger dans les détails, assurez‑vous de disposer de :

1. **Java Development Kit (JDK)** – installez‑le depuis [le site d'Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – téléchargez la dernière version depuis la [page des releases Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans conviendront.  
4. **Connaissances de base en Java & HTML** – essentielles pour suivre les extraits de code.

## Importer les packages
Les instructions d'importation font entrer les classes nécessaires de Java et d'Aspose.HTML dans le scope, permettant la gestion des fichiers et la configuration du service.  
`java.io.IOException` est une exception levée lorsqu'une opération d'E/S échoue ou est interrompue.

```java
import java.io.IOException;
```

## Étape 1 : Créer un fichier HTML avec du code JavaScript
Créer un fichier HTML contenant une boucle JavaScript montre un scénario de script potentiellement infini, que nous arrêterons ensuite à l'aide d'un délai d'attente.  
`java.io.FileWriter` est une classe permettant d'écrire des fichiers texte sur le disque.

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

## Étape 2 : Configurer l'objet Configuration
La classe `Configuration` contient les paramètres de tous les services Aspose.HTML, y compris le Runtime Service, et sert de point central pour les options personnalisées.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Étape 3 : Configurer le Runtime Service
`IRuntimeService` offre le contrôle de l'exécution des scripts, comme la définition de délais d'attente, afin de protéger l'environnement hôte contre le code incontrôlé.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` limite l'exécution du script à **5 secondes**, empêchant ainsi les boucles infinies.  
- Cela **limite également l'exécution des scripts** pour tout code client lourd.

## Étape 4 : Charger le document HTML avec la configuration
La classe `Document` charge et représente une page HTML avec la configuration appliquée, garantissant que la règle de délai d'attente est respectée pendant l'analyse.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Le document respecte le délai d'attente défini précédemment, de sorte que la boucle sans fin sera arrêtée après 5 secondes.

## Étape 5 : Convertir le HTML en PNG
`ImageSaveOptions` spécifie le format de sortie et les options de rendu pour la conversion d'image, permettant une **conversion html en png** propre une fois le script terminé ou interrompu.

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
Appeler `dispose()` libère les ressources natives utilisées par les objets Aspose.HTML, évitant les fuites de mémoire dans les applications à longue exécution.

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

- Une libération correcte est essentielle pour les applications à longue durée de vie.

## Pourquoi c'est important
Un délai d'attente protège votre pipeline de conversion en terminant les scripts à exécution prolongée, ce qui empêche le blocage des threads et réduit le temps de traitement global, surtout dans les services multi‑locataires. Avec une limite de 5 secondes, vous conservez le comportement normal de la page tout en coupant les scripts abusifs ou défectueux, ce qui conduit à des performances de conversion html en png plus prévisibles.

## Pièges courants et dépannage
- **Délai trop court** – Les pages complexes avec de nombreuses ressources peuvent nécessiter une limite plus longue. Augmentez la valeur du `TimeSpan` si vous observez des terminaisons prématurées.  
- **Oubli de la libération** – Négliger l'appel à `dispose()` peut entraîner des fuites de mémoire native, surtout lors du traitement de nombreux documents en boucle.  
- **Objet de configuration incorrect** – Récupérez toujours le `IRuntimeService` depuis la même instance `Configuration` que vous utilisez pour charger le document ; sinon le délai d'attente ne sera pas appliqué.

## Questions fréquentes

**Q : Quel est le rôle du Runtime Service dans Aspose.HTML pour Java ?**  
R : Il vous permet de contrôler le temps d'exécution des scripts, aidant à **empêcher les boucles infinies** et à garder les conversions réactives.

**Q : Comment télécharger Aspose.HTML pour Java ?**  
R : Obtenez la dernière version depuis la [page des releases](https://releases.aspose.com/html/java/).

**Q : Est‑il nécessaire de libérer les objets `document` et `configuration` ?**  
R : Oui, la libération libère les ressources natives et prévient les fuites de mémoire.

**Q : Puis‑je définir le délai d'attente JavaScript à une valeur différente de 5 secondes ?**  
R : Absolument – modifiez l'argument de `TimeSpan.fromSeconds()` selon la limite qui convient à votre scénario.

**Q : Où puis‑je trouver de l'aide en cas de problème ?**  
R : Visitez le [forum Aspose.HTML](https://forum.aspose.com/c/html/29) pour obtenir de l'aide de la communauté et du personnel.

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Créer un fichier HTML Java & configurer le service réseau (Aspose.HTML)](/html/java/configuring-environment/setup-network-service/)
- [Comment définir un délai d'attente – Gérer le délai d'attente réseau dans Aspose.HTML pour Java](/html/java/message-handling-networking/network-timeout/)
- [Convertir HTML en PNG avec Aspose.HTML pour Java](/html/java/conversion-html-to-various-image-formats/convert-html-to-png/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}