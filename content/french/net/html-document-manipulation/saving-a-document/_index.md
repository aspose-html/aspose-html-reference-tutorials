---
title: Enregistrer un document dans .NET avec Aspose.HTML
linktitle: Enregistrer un document dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez la puissance d'Aspose.HTML pour .NET avec notre guide étape par étape. Apprenez à créer, manipuler et convertir des documents HTML et SVG
type: docs
weight: 16
url: /fr/net/html-document-manipulation/saving-a-document/
---

À l'ère du numérique, la création et la manipulation de documents HTML et SVG sont essentielles pour de nombreux développeurs de logiciels et entreprises. Aspose.HTML pour .NET est une bibliothèque puissante qui simplifie ces tâches, offrant diverses fonctionnalités pour travailler avec HTML, SVG et plus encore. Dans ce guide complet, nous allons plonger dans les éléments essentiels d'Aspose.HTML pour .NET, en décomposant chaque exemple en étapes faciles à suivre. Que vous soyez un développeur chevronné ou que vous débutiez, vous trouverez ce guide inestimable pour exploiter les capacités d'Aspose.HTML.

## Prérequis

Avant de nous lancer dans ce voyage, assurons-nous que vous avez tout ce dont vous avez besoin :

- Environnement de développement : assurez-vous que Visual Studio ou tout autre environnement de développement .NET est installé sur votre ordinateur.

- Aspose.HTML pour .NET : vous devez obtenir la bibliothèque Aspose.HTML pour .NET. Vous pouvez la télécharger à partir de[ici](https://releases.aspose.com/html/net/).

- Connaissance de C# : La connaissance du langage de programmation C# est bénéfique mais pas obligatoire. Ce guide est conçu pour être adapté aux débutants.

## Importer un espace de noms

Pour commencer à utiliser Aspose.HTML pour .NET, vous devez importer les espaces de noms nécessaires dans votre projet. Dans votre code C#, incluez l'espace de noms suivant :

### Étape 1 : Importer l'espace de noms Aspose.HTML
```csharp
using Aspose.Html;
```

Cet espace de noms vous donnera accès à diverses fonctionnalités de manipulation HTML et SVG.

## HTML vers fichier

### Étape 1 : Initialiser un document HTML vide
```csharp
// Initialiser un document HTML vide.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Créez un élément de texte et ajoutez-le au document
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Enregistrez le code HTML dans le fichier sur le disque.
    document.Save("document.html");
}
```

Dans cet exemple, nous créons un document HTML et y ajoutons un texte simple « Hello World ! ». Nous enregistrons ensuite le document HTML dans un fichier sur le disque.

## HTML sans fichier lié

### Étape 1 : Préparez un fichier HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Ici, nous créons un fichier HTML de base avec un lien d'ancrage vers un autre fichier.

### Étape 2 : charger « document.html » dans la mémoire
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Créer une instance d'options d'enregistrement
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Définissez la profondeur de traitement maximale sur 0 pour couper les fichiers HTML liés.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Enregistrer le document
    document.Save(@".\html-to-file-example\document.html", options);
}
```

Dans cet exemple, nous chargeons un document HTML en mémoire, définissons la profondeur de traitement maximale pour couper les fichiers liés et enregistrons le document. 

## Conversion HTML en MHTML

### Étape 1 : Préparez un fichier HTML simple
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Tout comme dans l’exemple 2, nous créons un fichier HTML de base avec un lien d’ancrage vers un autre fichier.

### Étape 2 : chargez « document.html » dans la mémoire et enregistrez-le au format MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Enregistrer le document au format MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Ici, nous chargeons le document HTML en mémoire et l'enregistrons au format MHTML.

## Conversion HTML en Markdown

### Étape 1 : Préparez un code HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 Dans cette étape, nous définissons un extrait de code HTML contenant un`<H2>` élément.

### Étape 2 : Initialiser le document à partir du code HTML et l'enregistrer au format Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Enregistrez le document en tant que fichier Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Nous créons un document HTML à partir de l'extrait de code et l'enregistrons sous forme de fichier Markdown.

## SVG vers fichier

### Étape 1 : Préparez un code SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' hauteur='80' largeur='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Ici, nous créons un code SVG qui dessine un graphique simple et coloré.

### Étape 2 : Initialiser un document SVG à partir du code et l'enregistrer sur le disque
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Enregistrez le fichier SVG sur le disque
    document.Save("document.svg");
}
```

Dans cette étape, nous créons un document SVG à partir du code et l’enregistrons sous forme de fichier SVG.

## Conclusion

Aspose.HTML pour .NET est une bibliothèque polyvalente qui simplifie la gestion des documents HTML et SVG dans vos applications .NET. Dans ce guide, nous avons abordé cinq exemples essentiels, décomposant chacun en instructions étape par étape. Que vous créiez, manipuliez ou convertissiez des documents, Aspose.HTML vous couvre. En suivant ces étapes, vous êtes sur la bonne voie pour maîtriser cet outil puissant.

## FAQ

### Q1 : Qu'est-ce qu'Aspose.HTML pour .NET ?

A1 : Aspose.HTML pour .NET est une bibliothèque .NET qui fournit une large gamme de fonctionnalités pour travailler avec des documents HTML et SVG, notamment la création, la manipulation et la conversion.

### Q2 : Où puis-je télécharger Aspose.HTML pour .NET ?

 A2 : Vous pouvez télécharger Aspose.HTML pour .NET à partir de[ici](https://releases.aspose.com/html/net/).

### Q3 : Aspose.HTML pour .NET convient-il aux débutants ?

A3 : Oui, Aspose.HTML pour .NET peut être utilisé aussi bien par les débutants que par les développeurs expérimentés. Les exemples de ce guide sont conçus pour être adaptés aux débutants.

### Q4 : Puis-je convertir du HTML vers d’autres formats à l’aide d’Aspose.HTML pour .NET ?

A4 : Oui, Aspose.HTML pour .NET prend en charge la conversion vers divers formats, notamment MHTML et Markdown, comme indiqué dans les exemples.

### Q5 : Où puis-je obtenir de l'aide pour Aspose.HTML pour .NET ?

 A5 : Vous pouvez trouver de l'aide et des réponses à vos questions dans le forum de la communauté Aspose.HTML[ici](https://forum.aspose.com/).