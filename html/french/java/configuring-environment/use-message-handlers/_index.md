---
date: 2026-02-10
description: Apprenez à utiliser Aspose pour gérer les liens brisés en Java, convertir
  du HTML en PNG et charger un document HTML en Java avec Aspose.HTML pour Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Convertir le HTML en PNG avec les gestionnaires de messages Aspose.HTML en
  Java
url: /fr/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir du HTML en PNG avec les gestionnaires de messages Aspose.HTML en Java

## Introduction
Dans ce tutoriel, vous découvrirez **comment convertir du HTML en PNG** tout en gérant gracieusement les ressources manquantes à l'aide d'Aspose.HTML pour Java. Nous parcourrons la création d'une petite page HTML qui pointe vers une image inexistante, le branchement d'un **gestionnaire de messages personnalisé** pour **intercepter les requêtes réseau**, la configuration du **service réseau**, le chargement du document, et enfin l'exécution de la **conversion HTML en image**. À la fin, vous disposerez d'un modèle solide pour **gérer les liens cassés java** et obtenir une sortie PNG de haute qualité—parfait pour les rapports, les vignettes ou les aperçus d'e‑mail.

## Quick Answers
- **Que fait un gestionnaire de messages ?** Il intercepte les opérations réseau (comme les requêtes d'images) et vous permet de réagir aux codes d'état tels que 404.  
- **Aspose.HTML peut‑il convertir du HTML en PNG ?** Oui—`Converter.convertHTML` effectue la conversion en un seul appel.  
- **Ai‑je besoin d'une licence pour cet exemple ?** Une licence temporaire supprime les limites d'évaluation ; une licence permanente est requise pour une utilisation en production.  
- **Quelle version de Java fonctionne ?** Toute version JDK 8+ (l'exemple s'exécute sur JDK 11).  
- **Puis‑je configurer le service réseau ?** Absolument—utilisez `configuration.getService(INetworkService.class)` pour ajouter votre gestionnaire.

## Prerequisites
Avant de plonger, assurez‑vous d'avoir les éléments suivants prêts :

1. **Java Development Kit (JDK)** – téléchargez‑le depuis le [site Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – obtenez la bibliothèque sur la [page des releases Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans fonctionnent parfaitement.  
4. **Connaissances de base en Java** – vous devez être à l'aise avec les classes, le try‑with‑resources et la gestion des exceptions.  
5. **Licence temporaire** – si vous êtes en période d'essai, procurez‑vous une [licence temporaire](https://purchase.aspose.com/temporary-license/) pour éviter les filigranes.

## Import Packages
Tout d'abord, importez la classe Java I/O dont nous aurons besoin pour la gestion des fichiers. Le reste des classes Aspose est référencé avec leurs noms pleinement qualifiés plus tard, ce qui maintient la liste d'importations propre.

```java
import java.io.IOException;
```

## Step 1: Prepare the HTML Code
Nous créons un extrait HTML minimal qui référence délibérément une image manquante. Cela déclenchera notre gestionnaire lorsque le moteur tentera de récupérer la ressource.

```java
String code = "<img src='missing.jpg'>";
```

## Step 2: Write the HTML Code to a File
Ensuite, nous persistons l'extrait dans *document.html*. L'utilisation d'un bloc try‑with‑resources garantit que le `FileWriter` est correctement fermé.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Step 3: Write a Custom Message Handler
Nous construisons maintenant un **gestionnaire de messages personnalisé** qui vérifie le statut HTTP de chaque requête réseau. Si la réponse n'est pas `200`, nous enregistrons un avertissement convivial. Notez l'appel à `invoke(context);` à la fin—cela transmet la requête au gestionnaire suivant dans la chaîne, évitant ainsi la récursion.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Step 4: Configure the Network Service
Pour que Aspose.HTML prenne en compte notre gestionnaire, nous récupérons le **service réseau** depuis une instance `Configuration` et ajoutons le gestionnaire à sa collection. C’est l’étape où nous **configurons le service réseau** pour un comportement personnalisé.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Step 5: Load the HTML Document
Avec la configuration prête, nous chargeons *document.html*. Le moteur utilise désormais notre service réseau, de sorte que la requête d'image manquante est interceptée par le gestionnaire que nous venons d’ajouter.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Step 6: Convert HTML to PNG
Voici le cœur du processus de **conversion HTML en image**. La méthode `Converter.convertHTML` prend le `HTMLDocument` chargé, des `ImageSaveOptions` optionnels (où vous pouvez ajuster le DPI ou la qualité), et le nom du fichier de sortie.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Step 7: Clean Up Resources
Une bonne pratique Java impose de libérer toutes les ressources natives. Le bloc `finally` garantit que la `Configuration` est disposée même si une exception se propage.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Why Use Message Handlers?
Les gestionnaires de messages vous offrent un **contrôle granulaire** sur chaque requête réseau—qu’il s’agisse d’une image, d’un CSS, d’un JavaScript ou d’un fichier de police. Au lieu de laisser la bibliothèque échouer silencieusement, vous pouvez consigner les ressources manquantes, fournir du contenu de secours, ou même réessayer la requête. Cela rend votre pipeline de traitement HTML **robuste**, **prêt pour la production**, et plus facile à déboguer.

## Common Issues and Solutions
- **Récursion du gestionnaire** – Appelez `invoke(context);` une seule fois pour éviter les boucles infinies.  
- **Licence manquante** – Sans licence valide, le PNG de sortie contiendra un filigrane.  
- **Chemins de fichiers incorrects** – Utilisez des chemins absolus ou définissez correctement le répertoire de travail lors du chargement de `document.html`.  
- **Types de ressources non pris en charge** – Assurez‑vous que la ressource que vous souhaitez intercepter (image, CSS, etc.) est réellement demandée par le moteur HTML.

## Frequently Asked Questions

**Q : Puis‑je chaîner plusieurs gestionnaires de messages ?**  
R : Oui, vous pouvez ajouter plusieurs gestionnaires à la collection `network.getMessageHandlers()` ; ils seront exécutés dans l'ordre d'ajout.

**Q : Le gestionnaire fonctionne‑t‑il également pour les ressources CSS ou script ?**  
R : Absolument—toute requête réseau effectuée par le moteur HTML (images, CSS, JS, polices) passe par le gestionnaire.

**Q : Comment modifier la requête HTTP avant son envoi ?**  
R : Implémentez un gestionnaire qui modifie `context.getRequest()` avant d’appeler `invoke(context)`.

**Q : Existe‑t‑il un moyen de supprimer l’avertissement pour des URL spécifiques ?**  
R : À l'intérieur du gestionnaire, inspectez `context.getRequest().getRequestUri()` et ignorez conditionnellement le log.

**Q : Quelle version d’Aspose.HTML est requise pour ces API ?**  
R : Le code fonctionne avec Aspose.HTML for Java 22.10 et versions ultérieures.

## Conclusion
Vous disposez maintenant d’un exemple complet, de bout en bout, de **comment convertir du HTML en PNG** tout en utilisant un **gestionnaire de messages personnalisé** pour **intercepter les requêtes réseau** et **gérer les liens cassés java**. En configurant le service réseau, en chargeant le document et en invoquant le convertisseur, vous pouvez générer de manière fiable des vignettes PNG ou des captures d’écran pleine page dans n’importe quelle application Java.

---

**Last Updated:** 2026-02-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}