---
category: general
date: 2026-03-04
description: Comment mettre en évidence le HTML en recherchant du texte dans le HTML
  et en enveloppant chaque correspondance avec une balise <mark>. Guide Java étape
  par étape pour remplacer le texte par des éléments <mark>.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: fr
og_description: Comment mettre en évidence du HTML en recherchant du texte dans le
  HTML et en enveloppant les correspondances avec une balise <mark>. Exemple complet
  en Java pour remplacer le texte par une balise <mark>.
og_title: Comment surligner le HTML – Rechercher du texte et le remplacer par <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Comment surligner du HTML – Rechercher du texte et le remplacer par <mark>
url: /fr/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment mettre en évidence le HTML – Rechercher du texte et remplacer par `<mark>`

Vous vous êtes déjà demandé **comment mettre en évidence le HTML** lorsqu’un certain mot apparaît plusieurs fois ? Peut‑être que vous créez un site de documentation, un moteur de blog, ou que vous avez simplement besoin de mettre en avant le nom d’une marque sur une page statique. Bonne nouvelle ? C’est assez simple une fois que vous savez comment rechercher du texte dans le HTML et envelopper les résultats avec un élément `<mark>`.

Dans ce tutoriel, nous allons parcourir une solution Java complète qui charge un fichier HTML, recherche un mot cible, remplace chaque occurrence par une balise `<mark>`, puis enregistre la version mise en évidence. À la fin, vous serez capable de **highlight word in HTML**, **highlight occurrences of word**, et même **replace text with mark** sans casser le balisage environnant.

> **Ce dont vous aurez besoin**  
> • Java 17 ou supérieur (le code fonctionne aussi avec les versions antérieures)  
> • Bibliothèque Aspose.HTML for Java (version d’essai gratuite ou copie sous licence)  
> • Un fichier HTML simple que vous souhaitez traiter  

Si vous avez ces bases, plongeons‑y.  

![Capture d’écran montrant la sortie HTML mise en évidence – comment mettre en évidence le html](/images/highlight-html-example.png "exemple de comment mettre en évidence le html")

## Étape 1 – Charger le document HTML (How to Highlight HTML)

Tout d’abord, nous devons charger le fichier source en mémoire. La classe `Document` d’Aspose.HTML effectue tout le travail lourd, en analysant le balisage dans une structure semblable à un DOM que nous pouvons interroger.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Pourquoi c’est important :** Charger le document nous fournit un modèle d’objet propre, ce qui nous permet de manipuler en toute sécurité les nœuds de texte sans craindre de casser des balises ou des attributs. Cela normalise également les espaces, ce qui rend l’étape ultérieure de **search text in html** plus fiable.

## Étape 2 – Rechercher du texte dans le HTML pour le mot cible

Maintenant que le document est prêt, nous allons rechercher chaque occurrence du mot que nous voulons mettre en avant. La méthode `searchText` renvoie une liste d’objets `TextMatch`, chacun décrivant où se trouve la correspondance dans le DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Astuce :** La recherche est sensible à la casse par défaut. Si vous avez besoin d’une recherche insensible à la casse, convertissez à la fois le texte du document et `searchTerm` dans la même casse avant d’appeler `searchText`, ou utilisez une approche basée sur les expressions régulières fournie par la bibliothèque.

## Étape 3 – Remplacer le texte par `<mark>` (Highlight Word in HTML)

Pour chaque correspondance, nous reconstruirons le texte du nœud contenant, en injectant un élément `<mark>` autour du mot exact. Cela garantit que nous n’affectons que le texte cible et laissons le reste du HTML intact.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Explication :**  
- `getStartOffset`/`getEndOffset` nous donnent les positions exactes des caractères de la correspondance à l’intérieur de son nœud parent.  
- En découpant le texte original (`textBefore` et `textAfter`) nous conservons tout le reste exactement tel qu’il était.  
- Envelopper la correspondance avec `<mark>` est la méthode canonique pour **replace text with mark** et obtenir un surlignage natif du navigateur sans CSS supplémentaire.

### Cas limites & conseils

- **Multiple correspondances dans le même nœud :** La boucle traite chaque `TextMatch` séquentiellement. Comme nous remplaçons le contenu complet du nœud à chaque fois, les décalages ultérieurs changent. Aspose.HTML renvoie les correspondances dans l’ordre du document, donc le remplacement simple fonctionne dans la plupart des cas. Si vous rencontrez des correspondances qui se chevauchent, envisagez de collecter toutes les correspondances d’abord, puis de reconstruire le nœud en une seule passe.  
- **Éléments qui ne peuvent pas contenir du HTML brut :** Si le nœud parent est un bloc `<script>` ou `<style>`, insérer `<mark>` casserait la page. Vous pouvez ignorer ces nœuds en vérifiant `parentNode.getNodeName()` avant le remplacement.

## Étape 4 – Enregistrer le document mis en évidence (Highlight Occurrences of Word)

Une fois tous les remplacements effectués, nous persistons le DOM modifié sur le disque. Le fichier de sortie contiendra le balisage original plus les nouvelles balises `<mark>`, mettant effectivement en évidence **highlighting occurrences of word** “Aspose”.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Ouvrez `highlighted.html` dans n’importe quel navigateur, et vous verrez chaque « Aspose » entouré d’un fond jaunâtre (le style par défaut du `<mark>`). Si vous préférez un rendu personnalisé, ajoutez une petite règle CSS :

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Questions fréquentes (Search Text in HTML – FAQs)

**Q : Que se passe-t-il si le mot apparaît à l’intérieur d’une valeur d’attribut ?**  
R : `searchText` ne regarde que le contenu texte des nœuds, pas les chaînes d’attributs. Pour mettre en évidence les valeurs d’attributs, vous devez parcourir les éléments et inspecter manuellement les attributs.

**Q : Puis‑je mettre en évidence plusieurs mots différents en une seule passe ?**  
R : Absolument. Créez une liste de termes, parcourez‑les un par un, et exécutez la même logique de remplacement. Faites simplement attention aux correspondances qui se chevauchent.

**Q : Cela fonctionne‑t‑il avec des balises uniquement HTML5 comme `<section>` ou `<article>` ?**  
R : Oui. Aspose.HTML prend pleinement en charge les éléments modernes HTML5, donc le parcours du DOM fonctionne quel que soit le type de balise.

## Exemple complet fonctionnel (Toutes les étapes combinées)

Ci‑dessus se trouve le programme Java complet, prêt à être exécuté, qui démontre l’ensemble du flux de travail — du chargement du fichier à l’enregistrement du résultat mis en évidence.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Sortie attendue :** Ouvrez `highlighted.html` et vous verrez chaque occurrence de « Aspose » mise en évidence. Aucune autre partie de la page n’est modifiée, et le fichier reste un document HTML valide.

## Conclusion

Nous avons couvert **how to highlight HTML** en recherchant programmatique **search text in HTML**, en enveloppant chaque correspondance avec une balise `<mark>`, puis en persistant les modifications. Cette approche vous permet de **highlight word in HTML**, **highlight occurrences of word**, et **replace text with mark** sans écrire de code fragile de manipulation de chaînes.

Prochaines étapes ? Essayez d’étendre le script pour :

- Accepter le terme de recherche comme argument de ligne de commande.  
- Générer un fichier CSS qui définit une couleur de surlignage personnalisée.  
- Traiter un dossier complet de fichiers HTML en un seul lot.  

Ces variantes approfondiront votre compréhension à la fois de l’API Aspose.HTML et des modèles généraux de traitement de texte.

Si vous rencontrez des problèmes ou avez des idées d’améliorations, laissez un commentaire ci‑dessous. Bon surlignage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}