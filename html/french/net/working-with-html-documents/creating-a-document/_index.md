---
title: Créer un document HTML dans .NET avec Aspose.HTML
linktitle: Créer un document HTML dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Apprenez à créer des documents HTML dans .NET à l'aide d'Aspose.HTML, à partir de zéro ou à partir d'URL. Un didacticiel complet pour les développeurs Web.
weight: 10
url: /fr/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document HTML dans .NET avec Aspose.HTML


Dans le domaine du développement Web et de la manipulation de données, il est indispensable de disposer d'un outil puissant pour créer, modifier et travailler avec des documents HTML. Aspose.HTML pour .NET est l'un de ces outils qui peut simplifier vos tâches liées au HTML. Dans ce didacticiel complet, nous découvrirons comment créer des documents HTML à l'aide d'Aspose.HTML pour .NET étape par étape. Avant de nous plonger dans les exemples, examinons quelques prérequis.

## Prérequis

Avant de vous lancer dans ce voyage, assurez-vous de disposer des prérequis suivants :

1. Visual Studio : assurez-vous que Visual Studio est installé sur votre système.

2. Aspose.HTML pour .NET : Téléchargez et installez la bibliothèque Aspose.HTML pour .NET. Vous pouvez trouver le lien de téléchargement[ici](https://releases.aspose.com/html/net/).

3. Connaissances de base de C# : Familiarisez-vous avec les bases du langage de programmation C#.

Maintenant que nous avons couvert les prérequis, commençons par créer des documents HTML.

## Importation d'espaces de noms

Tout d'abord, vous devez importer les espaces de noms nécessaires pour utiliser Aspose.HTML dans votre projet C#. Ajoutez les directives using suivantes à votre fichier de code :

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Créer un document SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Effectuez des actions sur le document SVG ici...
    }
}
```

 Dans cet exemple, nous créons un document SVG en fournissant le contenu SVG et une URL de base.`SVGDocument` La classe d'Aspose.HTML pour .NET vous permet de manipuler des documents SVG sans effort.

## Créer un document HTML à partir de zéro

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Effectuez des actions sur le document HTML ici...
    }
}
```

 Cet exemple montre comment créer un document HTML à partir de zéro.`HTMLDocument`La classe fournit une toile vierge pour votre contenu HTML.

## Créer un document HTML à partir d'un fichier local

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Effectuez des actions sur le document HTML ici...
    }
}
```

 Si vous avez un fichier HTML existant sur votre système local, vous pouvez le charger à l'aide de l'`HTMLDocument` classe, comme le montre cet exemple.

## Créer un document HTML à partir d'une URL distante

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://votre.site.com/"))
    {
        // Effectuez des actions sur le document HTML ici...
    }
}
```

Il peut arriver que vous ayez besoin de travailler avec du contenu HTML hébergé sur un serveur distant. Cet exemple montre comment créer un document HTML à partir d'une URL distante.

## Créer un document HTML à partir d'une URL distante (alternative)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://votre.site.com/")))
    {
        // Effectuez des actions sur le document HTML ici...
    }
}
```

Cette approche alternative montre également comment créer un document HTML à partir d’une URL distante à l’aide d’un constructeur différent.

## Créer un document HTML à partir d'un contenu HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Effectuez des actions sur le document HTML ici...
    }
}
```

Si vous avez du contenu HTML dans un format de chaîne, vous pouvez créer un document HTML avec celui-ci, comme illustré dans cet exemple.

## Créer un document HTML à partir d'un flux

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Effectuez des actions sur le document HTML ici...
        }
    }
}
```

Dans cet exemple, nous montrons comment créer un document HTML à partir de données d'un flux de mémoire. Cela peut être utile lorsque vous avez du contenu HTML dans un flux et que vous souhaitez le manipuler.

## Conclusion

Aspose.HTML pour .NET fournit un ensemble d'outils puissants pour créer et travailler avec des documents HTML dans vos applications .NET. Avec les exemples fournis dans ce didacticiel, vous pouvez facilement commencer à créer des documents HTML, qu'il s'agisse de zéro, de fichiers locaux, d'URL distantes ou de contenu HTML existant.

 Vous avez des questions ou besoin d'aide ? Visitez le forum de la communauté Aspose.HTML pour obtenir de l'aide à l'adresse[https://forum.aspose.com/](https://forum.aspose.com/).

## FAQ

### Q1 : L'utilisation d'Aspose.HTML pour .NET est-elle gratuite ?
 A1 : Aspose.HTML pour .NET propose un essai gratuit, mais pour une utilisation complète, vous devrez acheter une licence. Vous trouverez plus de détails à l'adresse[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2 : Comment puis-je obtenir une licence temporaire pour Aspose.HTML pour .NET ?
 A2 : Si vous avez besoin d'un permis temporaire, vous pouvez en obtenir un à[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3 : Où puis-je trouver la documentation pour Aspose.HTML pour .NET ?
A3 : La documentation est disponible à l'adresse[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4 : Existe-t-il d’autres bibliothèques Aspose pour le développement .NET ?
 A4 : Oui, Aspose propose une gamme de bibliothèques pour divers formats de fichiers et tâches de manipulation de documents. Découvrez leurs offres sur[https://products.aspose.com/](https://products.aspose.com/).

### Q5 : Puis-je utiliser Aspose.HTML pour .NET dans mes applications Web ?
A5 : Oui, Aspose.HTML pour .NET est compatible avec les applications Web, ce qui en fait un choix polyvalent pour les projets de bureau et Web.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
