---
date: 2025-12-10
description: Apprenez à utiliser Aspose pour gérer les liens brisés en Java, convertir
  du HTML en PNG et charger un document HTML en Java avec Aspose.HTML pour Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Comment utiliser les gestionnaires de messages Aspose.HTML en Java
url: /fr/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser les gestionnaires de messages Aspose.HTML en Java

## Introduction
Dans ce tutoriel, **how to use aspose** pour gérer les ressources manquantes dans le HTML est démonstration étape par étape. Nous créerons un document HTML simple qui référence une image manquante, attacherons un gestionnaire de messages personnalisé, et vous montrerons comment **load html document java** tout en gérant gracieusement les liens cassés. À la fin, vous verrez également comment **convert html to png** avec Aspose.HTML, vous offrant une vue complète de la conversion HTML‑vers‑image en Java.

## Réponses rapides
- **Quel est le mais principal d'un gestionnaire de messages?** Intercepter les opérations réseau et réagir aux codes d'état tels que les ressources manquantes.
- **Aspose.HTML peut‑il convertir du HTML en PNG?** Oui, en utilisant `Converter.convertHTML` vous pouvez effectuer la conversion HTML vers image.
- **Ai‑je besoin d’une licence pour cet exemple?** Une licence temporaire supprime les limites d’évaluation; une licence permanente est requise pour la production.
- **Quelle version de Java est prise en charge ?** Tout JDK8+ (le tutoriel utilise JDK11).
- **Est‑il possible de gérer plusieurs liens cassés?** Absolument – ​​vous pouvez chaîner plusieurs gestionnaires pour gérer différents scénarios.

## Prérequis
Avant de plonger dans le guide étape par étape, déterminez‑nous que vous avez tout ce qu’il faut:
1. Java Development Kit (JDK) : Assurez-vous d’avoir le JDK installé sur votre système. Vous pouvez le télécharger depuis le [site d’Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML pour Java : Vous devez disposer d’Aspose.HTML pour Java installé. Vous pouvez le télécharger depuis la [page des releases Aspose](https://releases.aspose.com/html/java/).
3. IDE : Utilisez votre environnement de développement Java préféré (IDE) comme IntelliJ IDEA, Eclipse ou NetBeans.
4. Connaissances de base en Java: Une familiarité avec la programmation Java est essentielle pour suivre efficacement ce tutoriel.
5. Licence temporaire : Si vous utilisez la version d’essai d’Aspose.HTML, envisagez d’obtenir une [licence temporaire](https://purchase.aspose.com/temporary-license/) afin d’éviter toute limitation pendant le développement.

## Importer des packages
Avant de commencer, assurez‑vous d’avoir les packages nécessaires importés dans votre projet Java. Voici les imports essentiels dont vous aurez besoin :
```java
import java.io.IOException;
```
Ces imports vous donnent accès aux classes et méthodes requises pour gérer les opérations réseau, créer des documents HTML et effectuer la conversion HTML‑vers‑PNG.

## Étape 1 : Préparer le code HTML
La première chose dont nous avons besoin est un extrait HTML simple qui référence un fichier image. Nous référencerons délibérément une image qui n’existe pas afin de déclencher le mécanisme de gestion des erreurs.
```java
String code = "<img src='missing.jpg'>";
```
Ce code crée une balise `<img>` qui pointe vers `missing.jpg`. Comme l’image est manquante, le service réseau renverra un code d’état différent de 200, que notre gestionnaire personnalisé interceptera.

## Étape 2 : Écrire le code HTML dans un fichier
Ensuite, nous devons persister l’extrait HTML afin qu’Aspose.HTML puisse le charger en tant que document.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
En utilisant un `FileWriter` nous enregistrons le HTML dans **document.html**. Ce fichier devient la source pour l’étape **load html document java** ultérieure.

## Étape 3 : Créer un gestionnaire de messages personnalisé
Construisons maintenant un gestionnaire de messages personnalisé qui réagit lorsque l’image ne peut pas être trouvée. Le gestionnaire vérifie le code d’état HTTP et affiche un message convivial.
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
La méthode `invoke` examine `context.getResponse().getStatusCode()`. Si ce n’est pas **200**, nous affichons un avertissement clair indiquant que le fichier est manquant. L’appel final `invoke(context);` transmet le contrôle au gestionnaire suivant dans la chaîne.

## Étape 4 : Configurer le service réseau
Pour que Aspose.HTML prenne en compte notre gestionnaire, nous l’enregistrons auprès du service réseau via la classe `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Ici nous créons une instance `Configuration`, récupérons le `INetworkService`, et ajoutons notre gestionnaire personnalisé à sa collection. Cela garantit que le gestionnaire s’exécute lors de toute requête réseau, comme le chargement d’images.

## Étape 5 : Charger le document HTML
Avec la configuration prête, nous pouvons maintenant charger le fichier HTML que nous avons créé précédemment. Cette étape montre **load html document java** tandis que l’image manquante déclenche notre gestionnaire.
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
Le constructeur `HTMLDocument` reçoit à la fois le chemin du fichier et la `configuration` personnalisée. Lorsque le document analyse la balise `<img>`, le service réseau tente de récupérer `missing.jpg`, reçoit un 404, et notre gestionnaire affiche l’avertissement.

## Étape 6 : Convertir le HTML en PNG
Pour illustrer les capacités plus larges d’Aspose.HTML, nous convertirons le document chargé en une image PNG. Il s’agit d’un scénario classique de **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` prend le `HTMLDocument`, des `ImageSaveOptions` optionnelles (où vous pouvez définir le DPI, la qualité, etc.), et le nom du fichier de sortie. Le résultat est une image raster du HTML rendu.

## Étape 7 : Nettoyage des ressources
Une gestion correcte des ressources est essentielle dans toute application Java. Nous libérons à la fois la `Configuration` et le `HTMLDocument` afin d’éviter les fuites de mémoire.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
En plaçant le nettoyage dans un bloc `finally`, nous garantissons son exécution même si une exception survient plus tôt.

## Pourquoi utiliser des gestionnaires de messages ?
Les gestionnaires de messages vous offrent un contrôle fin sur les opérations réseau telles que **handle Broken Links Java**. Au lieu de laisser la bibliothèque échouer silencieusement, vous pouvez journaliser, réessayer, remplacer les ressources ou fournir du contenu de secours—rendant votre traitement HTML robuste et prêt pour la production.

## Problèmes courants et solutions
- **Récursion du gestionnaire** – Assurez-vous d'appeler `invoke(context);` une seule fois pour éviter les boucles infinies.
- **Licence manquante** – Sans licence valide, la conversion peut produire une image filigranée.
- **Erreurs de chemin de fichier** – Utiliser des chemins absolus ou définir correctement le répertoire de travail lors du chargement de `document.html`.

## Questions fréquemment posées

**Q : Puis‑je chaîner plusieurs gestionnaires de messages ?**  
R : Oui, vous pouvez ajouter plusieurs gestionnaires à la collection `network.getMessageHandlers()` ; ils seront exécutés dans l’ordre d’ajout.

**Q : Le gestionnaire fonctionne‑t‑il également pour les ressources CSS ou script ?**  
R : Absolument — toute requête réseau effectuée par le moteur HTML (images, CSS, JS, polices) passe par le gestionnaire.

**Q : Comment modifier la requête HTTP avant son envoi ?**  
R : Implémentez un gestionnaire qui modifie `context.getRequest()` avant d’appeler `invoke(context)`.

**Q : Existe‑t‑il un moyen de supprimer l’avertissement pour des URL spécifiques ?**  
R : Dans le gestionnaire, inspectez `context.getRequest().getRequestUri()` et sautez conditionnellement le journal.

**Q : Quelle version d’Aspose.HTML est requise pour ces API ?**  
R : Le code fonctionne avec Aspose.HTML for Java 22.10 et versions ultérieures.

## Conclusion
Et voilà — un guide complet sur **how to use aspose** les gestionnaires de messages en Java. Nous avons couvert la création d’un fichier HTML, le branchement d’un gestionnaire personnalisé pour **handle broken links java**, le chargement du document, et la réalisation de **convert html to png**. Avec ce modèle, vous pouvez gérer en toute confiance les ressources manquantes, appliquer des politiques personnalisées et étendre les capacités réseau d’Aspose.HTML dans n’importe quelle application Java.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}