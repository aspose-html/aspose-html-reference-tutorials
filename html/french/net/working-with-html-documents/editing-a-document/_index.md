---
title: Modification d'un document dans .NET avec Aspose.HTML
linktitle: Modification d'un document dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Apprenez à travailler avec des documents HTML dans .NET à l'aide d'Aspose.HTML. Ce didacticiel complet couvre la création, la manipulation et le style des documents. Commencez dès maintenant !
weight: 12
url: /fr/net/working-with-html-documents/editing-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modification d'un document dans .NET avec Aspose.HTML


Bienvenue dans notre tutoriel sur l'utilisation d'Aspose.HTML pour .NET, un outil puissant pour gérer les documents HTML dans vos applications .NET. Dans ce tutoriel, nous vous guiderons à travers les étapes essentielles pour travailler avec des documents HTML à l'aide d'Aspose.HTML. Que vous soyez un développeur expérimenté ou que vous débutiez dans le développement .NET, ce guide vous aidera à exploiter tout le potentiel d'Aspose.HTML pour vos projets.

## Prérequis

Avant de plonger dans les exemples de code, assurez-vous que les conditions préalables suivantes sont remplies :

1. Visual Studio : vous devez avoir Visual Studio installé sur votre ordinateur pour suivre les exemples.

2.  Aspose.HTML pour .NET : la bibliothèque Aspose.HTML pour .NET doit être installée. Vous pouvez la télécharger à partir de[ici](https://releases.aspose.com/html/net/).

3. Une compréhension de base de C# : une connaissance de la programmation C# sera utile, mais même si vous êtes nouveau en C#, vous pouvez toujours suivre et apprendre.

## Importer les espaces de noms nécessaires

Pour commencer à utiliser Aspose.HTML pour .NET, vous devez importer les espaces de noms requis. Voici comment procéder :

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.Dom.Css;
```

Maintenant que vous avez couvert les prérequis, décomposons chaque exemple en plusieurs étapes et expliquons chaque étape en détail.

## Exemple 1 : Créer et modifier un document HTML

```csharp
static void EditDocumentTree()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        var body = document.Body;
        // Créer un élément de paragraphe
        var p = (Aspose.Html.HTMLParagraphElement)document.CreateElement("p");
        // Définir un attribut personnalisé
        p.SetAttribute("id", "my-paragraph");
        // Créer un nœud de texte
        var text = document.CreateTextNode("my first paragraph");
        // Joindre du texte au paragraphe
        p.AppendChild(text);
        // Joindre le paragraphe au corps du document
        body.AppendChild(p);
    }
}
```

### Explication:

1.  Nous commençons par créer un nouveau document HTML en utilisant`Aspose.Html.HTMLDocument()`.

2. Nous accédons à l'élément corps du document.

3. Ensuite, nous créons un élément de paragraphe HTML (`<p>` ) en utilisant`document.CreateElement("p")`.

4.  Nous définissons un attribut personnalisé`id` pour l'élément paragraphe.

5.  Un nœud de texte est créé à l'aide de`document.CreateTextNode("my first paragraph")`.

6.  Nous attachons le nœud de texte à l'élément de paragraphe en utilisant`p.AppendChild(text)`.

7. Enfin, nous attachons le paragraphe au corps du document.

Cet exemple montre comment créer et manipuler la structure d'un document HTML.

## Exemple 2 : Suppression d'un élément d'un document HTML

```csharp
static void EditDocumentTreeWithAppendRemoveChild()
{
    using (var document = new Aspose.Html.HTMLDocument("<p>paragraph</p><div>some element to remove</div>", "about:blank"))
    {
        var body = document.Body;
        // Obtenir l'élément « div »
        var div = (Aspose.Html.HTMLDivElement)body.GetElementsByTagName("div").First();
        // Supprimer l'élément trouvé
        body.RemoveChild(div);
    }
}
```

### Explication:

1.  Nous créons un document HTML avec des éléments existants, y compris un`<p>` et un`<div>`.

2. Nous accédons à l'élément corps du document.

3.  En utilisant`body.GetElementsByTagName("div").First()` , nous récupérons le premier`<div>` élément dans le document.

4.  Nous supprimons la sélection`<div>` élément du corps du document en utilisant`body.RemoveChild(div)`.

Cet exemple montre comment manipuler et supprimer des éléments d'un document HTML existant.

## Exemple 3 : Modification du contenu HTML

```csharp
static void EditHtml()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        // Obtenir l'élément du corps
        var body = document.Body;
        // Définir le contenu de l'élément body
        body.InnerHTML = "<p>paragraph</p>";
        // Passer au premier enfant
        var node = body.FirstChild;
        System.Console.WriteLine(node.LocalName);
    }
}
```

### Explication:

1. Nous créons un nouveau document HTML.

2. Nous accédons à l'élément corps du document.

3.  En utilisant`body.InnerHTML` , nous définissons le contenu HTML du corps sur`<p>paragraph</p>`.

4.  Nous récupérons le premier élément enfant du corps en utilisant`body.FirstChild`.

5. Nous imprimons le nom local du premier élément enfant sur la console.

Cet exemple montre comment définir et récupérer le contenu HTML d'un élément dans un document HTML.

## Exemple 4 : Modification des styles d'éléments

```csharp
static void EditElementStyle()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // Obtenir l'élément à inspecter
        var element = document.GetElementsByTagName("p")[0];
        // Obtenir l'objet de vue CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // Obtenir le style calculé de l'élément
        var declaration = view.GetComputedStyle(element);
        // Obtenir la valeur de la propriété « couleur »
        System.Console.WriteLine(declaration.Color); // rvb(255, 0, 0)
    }
}
```

### Explication:

1.  Nous créons un document HTML avec CSS intégré qui définit la couleur de`<p>` éléments en rouge.

2.  Nous récupérons le`<p>` élément utilisant`document.GetElementsByTagName("p")[0]`.

3.  Nous accédons à l'objet de vue CSS et obtenons le style calculé de l'`<p>` élément.

4. Nous récupérons et imprimons la valeur de la propriété « color », qui est définie sur rouge dans le CSS.

Cet exemple montre comment inspecter et manipuler les styles CSS des éléments HTML.

## Exemple 5 : Modification du style d'un élément à l'aide d'attributs

```csharp
static void EditElementStyleUsingAttribute()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // Obtenir l'élément à modifier
        var element = (Aspose.Html.HTMLElement)document.GetElementsByTagName("p")[0];
        // Obtenir l'objet de vue CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // Obtenir le style calculé de l'élément
        var declaration = view.GetComputedStyle(element);
        // Définir la couleur verte
        element.Style.Color = "green";
        // Obtenir la valeur de la propriété « couleur »
        System.Console.WriteLine(declaration.Color); // rvb(0, 128, 0)
    }
}
```

### Explication:

1.  Nous créons un document HTML avec CSS intégré qui définit la couleur de`<p>` éléments en rouge.

2.  Nous récupérons le`<p>` élément utilisant`document.GetElementsByTagName("p")[0]`.

3.  Nous accédons à l'objet de vue CSS et obtenons le style calculé de l'`<p>` élément avant toute modification.

4.  Nous changeons la couleur de la`<p>` élément à utiliser pour le vert`element.Style.Color = "green"`.

5. Nous récupérons et imprimons la valeur mise à jour de la « couleur »

 propriété, qui est maintenant verte.

Cet exemple montre comment modifier directement le style d'un élément HTML à l'aide d'attributs.

## Conclusion

Dans ce didacticiel, nous avons abordé les principes fondamentaux de l'utilisation d'Aspose.HTML pour .NET pour créer, manipuler et styliser des documents HTML dans vos applications .NET. Nous avons exploré divers exemples, de la création d'un document HTML à la modification de sa structure et de ses styles. Grâce à ces compétences, vous pouvez gérer efficacement les documents HTML dans vos projets .NET.

 Si vous avez des questions ou avez besoin d'aide supplémentaire, n'hésitez pas à visiter le[Documentation Aspose.HTML pour .NET](https://reference.aspose.com/html/net/) ou demander de l'aide sur le[Forum Aspose](https://forum.aspose.com/).

---

## Questions fréquemment posées (FAQ)

### Qu'est-ce qu'Aspose.HTML pour .NET ?
Aspose.HTML pour .NET est une bibliothèque puissante pour travailler avec des documents HTML dans des applications .NET.

### Où puis-je télécharger Aspose.HTML pour .NET ?
 Vous pouvez télécharger Aspose.HTML pour .NET à partir de[ici](https://releases.aspose.com/html/net/).

### Existe-t-il un essai gratuit disponible ?
 Oui, vous pouvez obtenir un essai gratuit d'Aspose.HTML à partir de[ici](https://releases.aspose.com/).

### Comment puis-je acheter une licence ?
 Pour acheter une licence, visitez[ce lien](https://purchase.aspose.com/buy).

### Ai-je besoin d’une expérience préalable avec HTML pour utiliser Aspose.HTML pour .NET ?
Bien que la connaissance du HTML soit utile, vous pouvez utiliser Aspose.HTML pour .NET même si vous n'êtes pas un expert HTML.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
