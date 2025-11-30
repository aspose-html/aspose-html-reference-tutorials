---
date: 2025-11-30
description: Apprenez comment ajouter un élément au corps et surveiller les changements
  du DOM en Java en utilisant le Mutation Observer d’Aspose.HTML. Comprend les étapes
  pour créer un document HTML en Java et déconnecter le Mutation Observer.
language: fr
linktitle: Append Element to Body - Observing Node Additions
second_title: Java HTML Processing with Aspose.HTML
title: Ajouter un élément au corps avec Aspose.HTML pour Java en utilisant un observateur
  de mutations du DOM
url: /java/advanced-usage/dom-mutation-observer-observing-node-additions/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un élément au corps avec Aspose.HTML pour Java à l'aide d'un observateur de mutation du DOM

Si vous êtes un développeur Java qui doit **ajouter un élément au corps** tout en surveillant chaque changement qui se produit dans le DOM, vous êtes au bon endroit. Aspose.HTML pour Java rend simple la **création d'objets HTML document Java**, l'attachement d'un observateur de mutation, et la réaction instantanée lorsque des nœuds sont ajoutés, supprimés ou modifiés. Dans ce tutoriel pas à pas, nous parcourrons l’ensemble du processus — de la configuration du document à la **déconnexion propre de l'observateur de mutation** — afin que vous puissiez surveiller les changements du DOM en toute confiance dans vos applications Java.

## Réponses rapides
- **Que fait un observateur de mutation ?** Il surveille l'arbre DOM et vous notifie des ajouts, suppressions ou modifications d'attributs de nœuds.  
- **Quelle bibliothèque fournit cela en Java ?** Aspose.HTML pour Java inclut une API d'observateur de mutation complète.  
- **Ai‑je besoin d’une licence pour la production ?** Oui, une licence Aspose.HTML valide est requise pour une utilisation commerciale.  
- **Puis‑je observer les changements des nœuds texte ?** Absolument — définissez `characterData` à `true` dans la configuration de l'observateur.  
- **Comment arrêter l'observateur ?** Appelez `observer.disconnect()` une fois le suivi terminé.

## Qu’est‑ce que « ajouter un élément au corps » dans le contexte d’Aspose.HTML ?
Ajouter un élément à la balise `<body>` signifie insérer programmétiquement un nouveau nœud (comme un `<p>` ou `<div>`) dans la zone principale du document. Lorsqu’il est combiné avec un observateur de mutation, vous pouvez détecter instantanément cette insertion et déclencher une logique personnalisée — idéal pour la génération dynamique de HTML, les tests ou les scénarios de rendu côté serveur.

## Pourquoi utiliser un observateur de mutation en Java ?
- **Surveillance en temps réel :** Réagissez aux modifications du DOM dès qu’elles surviennent.  
- **Code plus propre :** Aucun besoin de sondage manuel ou de gestion d’événements complexes.  
- **Cohérence multiplateforme :** Fonctionne de la même façon que vous rendiez le HTML dans un navigateur ou sur le serveur.  
- **Performance :** Les observateurs sont efficaces et s’exécutent de manière asynchrone, libérant votre thread principal.

## Prérequis
1. **Java Development Kit (JDK)** – version 8 ou supérieure.  
2. **Aspose.HTML pour Java** – téléchargez la dernière version depuis le site officiel.  
3. **IDE** – IntelliJ IDEA, Eclipse ou tout éditeur compatible Java.  

Vous pouvez obtenir Aspose.HTML pour Java depuis la page de téléchargement [ici](https://releases.aspose.com/html/java/).

## Importer les packages
Tout d’abord, importez les classes dont vous aurez besoin. Cela crée également un document HTML vide que nous remplirons plus tard.

```java
// Import necessary packages
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Create an empty HTML document
HTMLDocument document = new HTMLDocument();
```

## Étape 1 : Créer une instance d’observateur de mutation (mutation observer java)
Un **observateur de mutation** nécessite un rappel qui sera invoqué chaque fois qu’une mutation se produit. Dans notre rappel, nous affichons simplement un message pour chaque nœud ajouté.

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

## Étape 2 : Configurer l’observateur (monitor dom changes java)
Nous indiquons à l’observateur **quoi** surveiller : les changements de liste d’enfants, les modifications de sous‑arbre et les mises à jour de données de caractères.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Pass in the target node to observe with the specified configuration
observer.observe(document.getBody(), config);
```

## Étape 3 : Ajouter un élément au corps et déclencher l’observateur
Nous **ajoutons maintenant un élément au corps**. L’ajout d’un élément `<p>` contenant un nœud texte déclenchera l’observateur que nous avons configuré précédemment.

```java
// Create a paragraph element and append it to the document body
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Create a text and append it to the paragraph
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

## Étape 4 : Attendre les observations (asynchronous handling)
Les mutations sont signalées de façon asynchrone, nous faisons donc une pause courte pour laisser le temps à l’observateur de traiter le changement.

```java
// Since mutations are working in async mode, wait for a few seconds
synchronized (this) {
    wait(5000);
}
```

## Étape 5 : Déconnecter l’observateur (disconnect mutation observer)
Lorsque vous avez terminé la surveillance, **déconnectez toujours l’observateur de mutation** afin de libérer les ressources.

```java
// Stop observing
observer.disconnect();
```

## Pièges courants et astuces
- **N’oubliez jamais de déconnecter** – laisser des observateurs actifs peut entraîner des fuites de mémoire.  
- **Sécurité des threads :** Le rappel s’exécute sur un thread d’arrière‑plan ; utilisez une synchronisation appropriée si vous modifiez des données partagées.  
- **Observer le bon nœud :** Observer `document.getBody()` capture la plupart des changements d’interface, mais vous pouvez cibler n’importe quel élément pour une surveillance plus fine.  
- **Astuce pro :** Utilisez `config.setAttributes(true)` si vous devez également surveiller les changements d’attributs.

## Questions fréquentes

**Q : Qu’est‑ce qu’un observateur de mutation du DOM ?**  
R : C’est une API qui surveille l’arbre DOM pour détecter les ajouts, suppressions ou mises à jour d’attributs de nœuds, et transmet ces événements via un rappel.

**Q : Puis‑je utiliser Aspose.HTML pour Java dans des projets commerciaux ?**  
R : Oui, avec une licence Aspose.HTML valide. Les détails d’achat sont disponibles [ici](https://purchase.aspose.com/buy).

**Q : Existe‑t‑il une version d’essai gratuite d’Aspose.HTML pour Java ?**  
R : Absolument — téléchargez un essai depuis la [page de version](https://releases.aspose.com/).

**Q : Comment surveiller les changements de données de caractères ?**  
R : Définissez `config.setCharacterData(true)` dans la configuration de l’observateur, comme illustré à l’Étape 2.

**Q : Que faire après avoir terminé l’observation ?**  
R : Appelez `observer.disconnect()` (Étape 5) et, si vous avez créé un `HTMLDocument`, libérez‑le avec `document.dispose()` pour libérer les ressources natives.

## Conclusion
Vous avez maintenant appris comment **ajouter un élément au corps**, configurer un **observateur de mutation java**, et **surveiller les changements du DOM java** à l’aide d’Aspose.HTML pour Java. En suivant ces étapes, vous pouvez détecter et réagir de façon fiable à toute mutation du DOM dans vos applications Java côté serveur. N’hésitez pas à expérimenter avec différents types de nœuds, observations d’attributs, ou même plusieurs observateurs pour des scénarios plus complexes.

Si vous rencontrez des problèmes, la communauté est prête à aider sur le [forum Aspose.HTML](https://forum.aspose.com/). Pour des détails d’API plus approfondis, consultez la documentation officielle [Aspose.HTML pour Java](https://reference.aspose.com/html/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Dernière mise à jour :** 2025-11-30  
**Testé avec :** Aspose.HTML pour Java 24.11  
**Auteur :** Aspose