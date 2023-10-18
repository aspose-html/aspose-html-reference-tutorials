---
title: Observateur de mutation DOM avec Aspose.HTML pour Java
linktitle: DOM Mutation Observer - Observation des ajouts de nœuds
second_title: Traitement HTML Java avec Aspose.HTML
description: Découvrez comment utiliser Aspose.HTML pour Java pour implémenter un observateur de mutation DOM dans ce guide étape par étape. Surveillez et réagissez efficacement aux changements du DOM.
type: docs
weight: 11
url: /fr/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Êtes-vous un développeur Java cherchant à observer et à réagir aux modifications apportées au modèle objet de document (DOM) d'un document HTML ? Aspose.HTML pour Java fournit une solution puissante pour cette tâche. Dans ce guide étape par étape, nous explorerons comment utiliser Aspose.HTML pour Java pour créer un document HTML et observer les ajouts de nœuds avec un Mutation Observer. Ce didacticiel vous guidera tout au long du processus, en décomposant chaque exemple en plusieurs étapes. À la fin, vous serez en mesure d’implémenter facilement les DOM Mutation Observers dans vos projets Java.

## Conditions préalables

Avant de nous lancer dans l'utilisation d'Aspose.HTML pour Java, assurons-nous que vous disposez des prérequis nécessaires :

1. Environnement de développement Java : assurez-vous que le kit de développement Java (JDK) est installé sur votre système.

2.  Aspose.HTML pour Java : vous devrez télécharger et installer Aspose.HTML pour Java. Vous pouvez trouver le lien de téléchargement[ici](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment) : utilisez votre IDE Java préféré, tel que IntelliJ IDEA ou Eclipse, pour écrire et exécuter du code Java.

## Importer des packages

Pour démarrer avec Aspose.HTML pour Java, vous devez importer les packages requis dans votre code Java. Voici comment procéder :

```java
// Importer les packages nécessaires
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Créer un document HTML vide
HTMLDocument document = new HTMLDocument();
```

Maintenant que vous avez importé les packages requis, passons au guide étape par étape pour implémenter un DOM Mutation Observer en Java.

## Étape 1 : Créer une instance d'observateur de mutation

Tout d’abord, vous devez créer une instance Mutation Observer. Cet observateur surveillera les changements dans le DOM et exécutera une fonction de rappel lorsque des mutations se produisent.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

Dans cette étape, nous créons un observateur avec une fonction de rappel qui imprime un message lorsque des nœuds sont ajoutés au DOM.

## Étape 2 : configurer l'observateur

Maintenant, configurons l'observateur avec les options souhaitées. Nous souhaitons observer les changements dans la liste des enfants et les changements dans les sous-arbres, ainsi que les changements dans les données des personnages.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Transmettez le nœud cible pour observer avec la configuration spécifiée
observer.observe(document.getBody(), config);
```

 Ici, nous définissons le`config` objet pour permettre d'observer les modifications des données de la liste des enfants, du sous-arbre et des caractères. On passe ensuite le nœud cible (dans ce cas, le nœud du document`<body>`) et la configuration à l'observateur.

## Étape 3 : modifier le DOM

Nous allons maintenant apporter quelques modifications au DOM pour déclencher l'observateur. Nous allons créer un élément de paragraphe et l'ajouter au corps du document.

```java
// Créez un élément de paragraphe et ajoutez-le au corps du document
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Créez un texte et ajoutez-le au paragraphe
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Dans cette étape, nous créons un élément de paragraphe HTML et l'ajoutons au corps du document. Ensuite, nous créons un nœud de texte avec le contenu « Hello World » et l'ajoutons au paragraphe.

## Étape 4 : Attendre les observations (de manière asynchrone)

Puisque les mutations sont observées de manière asynchrone, nous devons attendre un moment pour permettre à l’observateur de capturer les changements. Nous utiliserons`synchronized` et`wait` à cet effet, comme indiqué ci-dessous.

```java
// Puisque les mutations fonctionnent en mode asynchrone, attendez quelques secondes
synchronized (this) {
    wait(5000);
}
```

Ici, nous attendons 5 secondes pour nous assurer que l'observateur a une chance de capturer d'éventuelles mutations.

## Étape 5 : Arrêtez d’observer

Enfin, lorsque vous avez fini d'observer, il est indispensable de déconnecter l'observateur pour libérer des ressources.

```java
// Arrêtez d'observer
observer.disconnect();
```

Avec cette étape, vous avez terminé l’observation et pouvez nettoyer les ressources.

## Conclusion

Dans ce didacticiel, nous avons parcouru le processus d'utilisation d'Aspose.HTML pour Java pour implémenter un observateur de mutation DOM. Vous avez appris à créer un observateur, à le configurer, à apporter des modifications au DOM, à attendre des observations et à arrêter d'observer. Vous disposez désormais des compétences nécessaires pour appliquer les observateurs de mutations DOM dans vos projets Java afin de surveiller et de réagir efficacement aux modifications apportées au DOM des documents HTML.

Si vous avez des questions ou rencontrez des problèmes, n'hésitez pas à demander de l'aide au[Forum Aspose.HTML](https://forum.aspose.com/) . De plus, vous pouvez accéder au[Documentation](https://reference.aspose.com/html/java/) pour des informations détaillées sur Aspose.HTML pour Java.

## FAQ

### Q1 : Qu’est-ce qu’un observateur de mutation DOM ?

A1 : Un observateur de mutation DOM est une fonctionnalité JavaScript qui vous permet de surveiller les modifications dans le modèle objet de document (DOM) d'un document HTML. Il permet de réagir aux ajouts, suppressions ou modifications de nœuds DOM en temps réel.

### Q2 : Puis-je utiliser Aspose.HTML pour Java dans mes projets commerciaux ?

 A2 : Oui, vous pouvez utiliser Aspose.HTML pour Java dans des projets commerciaux. Vous pouvez trouver des informations sur les licences et les achats[ici](https://purchase.aspose.com/buy).

### Q3 : Existe-t-il un essai gratuit disponible pour Aspose.HTML pour Java ?

 A3 : Oui, vous pouvez bénéficier d'un essai gratuit d'Aspose.HTML pour Java.[ici](https://releases.aspose.com/). Cela vous permet d’explorer ses fonctionnalités et capacités avant de faire un achat.

### Q4 : Quel est l'avantage d'observer les changements dans les données des personnages avec Mutation Observer ?

A4 : L'observation des modifications des données de caractères est utile pour les scénarios dans lesquels vous souhaitez surveiller et réagir aux modifications du contenu textuel des éléments HTML. Par exemple, vous pouvez l'utiliser pour suivre et répondre aux entrées des utilisateurs dans les formulaires Web.

### Q5 : Comment puis-je disposer des ressources lorsque j'utilise Aspose.HTML pour Java ?

 A5 : Il est important de libérer des ressources lorsque vous avez terminé. Dans notre exemple, nous avons utilisé`document.dispose()` pour nettoyer les ressources associées au document HTML. Assurez-vous de supprimer tous les objets et ressources que vous créez pour éviter les fuites de mémoire.