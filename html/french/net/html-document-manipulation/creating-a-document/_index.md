---
title: Créer un document en .NET avec Aspose.HTML
linktitle: Créer un document dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Exploitez la puissance d'Aspose.HTML pour .NET. Apprenez à créer, manipuler et optimiser facilement des documents HTML et SVG. Découvrez des exemples étape par étape et des FAQ.
weight: 14
url: /fr/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document en .NET avec Aspose.HTML


Dans le monde en constante évolution du développement Web, il est essentiel de garder une longueur d'avance. Aspose.HTML pour .NET fournit aux développeurs une boîte à outils robuste pour travailler avec des documents HTML. Que vous partiez de zéro, que vous chargiez à partir d'un fichier, que vous tiriez d'une URL ou que vous manipuliez des documents SVG, cette bibliothèque offre la polyvalence dont vous avez besoin.

Dans ce guide étape par étape, nous allons nous plonger dans les principes fondamentaux de l'utilisation d'Aspose.HTML pour .NET, en veillant à ce que vous soyez bien équipé pour utiliser cet outil puissant dans vos projets de développement Web. Avant de plonger dans les détails, passons en revue les prérequis et les espaces de noms nécessaires pour démarrer votre parcours.

## Prérequis

Pour suivre avec succès ce tutoriel et exploiter la puissance d'Aspose.HTML pour .NET, vous aurez besoin des prérequis suivants :

- Une machine Windows avec .NET Framework ou .NET Core installé.
- Un éditeur de code comme Visual Studio.
- Connaissances de base de la programmation C#.

Maintenant que vous avez mis en place vos prérequis, commençons.

## Importation d'espaces de noms

Avant de commencer à utiliser Aspose.HTML pour .NET, vous devez importer les espaces de noms nécessaires. Ces espaces de noms contiennent des classes et des méthodes essentielles pour travailler avec des documents HTML. Vous trouverez ci-dessous une liste des espaces de noms que vous devez importer :

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Une fois ces espaces de noms importés, vous êtes maintenant prêt à plonger dans les exemples étape par étape.

## Créer un document HTML à partir de zéro

### Étape 1 : Initialiser un document HTML vide

```csharp
// Initialiser un document HTML vide.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Créez un élément de texte et ajoutez-le au document
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Enregistrez le document sur le disque.
    document.Save("document.html");
}
```

Dans cet exemple, nous commençons par créer un document HTML vide et y ajoutons un texte « Hello World ! ». Nous enregistrons ensuite le document dans un fichier.

## Créer un document HTML à partir d'un fichier

### Étape 1 : Préparez un fichier « document.html »

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Étape 2 : Charger à partir d'un fichier « document.html »

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Écrivez le contenu du document dans le flux de sortie.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Ici, nous préparons un fichier avec le contenu « Hello World ! » puis nous le chargeons en tant que document HTML. Nous imprimons le contenu du document sur la console.

## Créer un document HTML à partir d'une URL

### Étape 1 : Charger un document à partir d’une page Web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Écrivez le contenu du document dans le flux de sortie.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Dans cet exemple, nous chargeons un document HTML directement depuis une page Web et affichons son contenu.

## Créer un document HTML à partir d'une chaîne

### Étape 1 : Préparez un code HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Étape 2 : Initialiser le document à partir de la variable de chaîne

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Enregistrez le document sur le disque.
    document.Save("document.html");
}
```

Ici, nous créons un document HTML à partir d'une variable de chaîne et l'enregistrons dans un fichier.

## Créer un document HTML à partir d'un MemoryStream

### Étape 1 : créer un objet de flux de mémoire

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Écrivez le code HTML dans l'objet mémoire
    sw.Write("<p>Hello World!</p>");
    // Régler la position au début
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Initialiser le document à partir du flux mémoire
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Enregistrez le document sur le disque.
        document.Save("document.html");
    }
}
```

Dans cet exemple, nous créons un document HTML à partir d’un flux mémoire et l’enregistrons dans un fichier.

## Travailler avec des documents SVG

### Étape 1 : Initialiser le document SVG à partir d'une chaîne

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Écrivez le contenu du document dans le flux de sortie.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Ici, nous créons et affichons un document SVG à partir d'une chaîne.

## Chargement d'un document HTML de manière asynchrone

### Étape 1 : Créer l’instance du document HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Étape 2 : Abonnez-vous à l'événement « ReadyStateChange »

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Vérifiez la valeur de la propriété « ReadyState ».
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Étape 3 : Naviguer de manière asynchrone à l'Uri spécifié

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Dans cet exemple, nous chargeons un document HTML de manière asynchrone et gérons l'événement « ReadyStateChange » pour afficher le contenu une fois le chargement terminé.

## Gestion de l'événement « OnLoad »

### Étape 1 : Créer l’instance du document HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Étape 2 : Abonnez-vous à l'événement « OnLoad »

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Étape 3 : Naviguer de manière asynchrone à l'Uri spécifié

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Cet exemple illustre le chargement d'un document HTML de manière asynchrone et la gestion de l'événement « OnLoad » pour afficher le contenu une fois l'opération terminée.

## En conclusion

Dans le monde dynamique du développement Web, il est essentiel de disposer des bons outils. Aspose.HTML pour .NET vous offre les moyens de créer, de manipuler et de traiter efficacement des documents HTML et SVG. Ce guide complet vous a présenté les éléments essentiels, vous permettant d'exploiter la puissance d'Aspose.HTML pour .NET dans vos projets.

## FAQ

### Q1 : Qu'est-ce qu'Aspose.HTML pour .NET ?

A1 : Aspose.HTML pour .NET est une puissante bibliothèque .NET qui permet aux développeurs de travailler avec des documents HTML et SVG. Elle offre une large gamme de fonctionnalités, de la création de documents à partir de zéro à l'analyse et à la manipulation de fichiers HTML et SVG existants.

### Q2 : Puis-je utiliser Aspose.HTML pour .NET avec .NET Core ?

A2 : Oui, Aspose.HTML pour .NET est compatible avec .NET Framework et .NET Core, ce qui en fait un choix polyvalent pour les applications .NET modernes.

### Q3 : Aspose.HTML pour .NET est-il adapté au scraping et à l'analyse Web ?

A3 : Absolument ! Aspose.HTML pour .NET est un excellent choix pour les tâches de scraping et d'analyse Web, grâce à sa capacité à charger des documents HTML à partir d'URL et de chaînes. Vous pouvez extraire des données, effectuer des analyses, etc.

### Q4 : Comment puis-je accéder au support pour Aspose.HTML pour .NET ?

 A4 : Si vous rencontrez des problèmes ou avez des questions lors de l'utilisation d'Aspose.HTML pour .NET, vous pouvez visiter le[Forum Aspose](https://forum.aspose.com/) pour le soutien et l'assistance de la communauté et des experts Aspose.

### A5 : Où puis-je trouver une documentation détaillée et des options de téléchargement ?

A5 : Pour une documentation complète et un accès aux options de téléchargement, vous pouvez vous référer aux liens suivants :

- [Documentation](https://reference.aspose.com/html/net/)
- [Télécharger](https://releases.aspose.com/html/net/)
- [Acheter](https://purchase.aspose.com/buy)
- [Essai gratuit](https://releases.aspose.com/)
- [Licence temporaire](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
