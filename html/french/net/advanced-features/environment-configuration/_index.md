---
title: Configuration de l'environnement dans .NET avec Aspose.HTML
linktitle: Configuration de l'environnement dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez comment travailler avec des documents HTML dans .NET à l'aide d'Aspose.HTML pour des tâches telles que la gestion des scripts, les styles personnalisés, le contrôle de l'exécution JavaScript, etc. Ce didacticiel complet fournit des exemples étape par étape et des FAQ pour vous aider à démarrer.
weight: 10
url: /fr/net/advanced-features/environment-configuration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configuration de l'environnement dans .NET avec Aspose.HTML


Dans le monde numérique d'aujourd'hui, la création et la manipulation de documents HTML constituent une tâche fondamentale pour de nombreux développeurs. Que vous créiez une application Web ou que vous ayez besoin de convertir du HTML en d'autres formats tels que PDF ou images, Aspose.HTML pour .NET est un outil puissant à avoir dans votre boîte à outils. Dans ce didacticiel, nous explorerons divers aspects d'Aspose.HTML pour .NET, notamment les prérequis, l'importation d'espaces de noms et des exemples étape par étape avec des explications détaillées.

## Prérequis

Avant de nous lancer dans l’utilisation d’Aspose.HTML pour .NET, vous devez vous assurer que les conditions préalables suivantes sont remplies :

1. Visual Studio : assurez-vous que Visual Studio est installé sur votre machine de développement. Aspose.HTML pour .NET est conçu pour fonctionner de manière transparente avec Visual Studio.

2.  Aspose.HTML pour .NET : vous pouvez télécharger la bibliothèque Aspose.HTML pour .NET à partir du site Web. Utilisez le lien suivant pour accéder à la page de téléchargement :[Télécharger Aspose.HTML pour .NET](https://releases.aspose.com/html/net/).

3.  Installation et licence : Après avoir téléchargé la bibliothèque, suivez les instructions d'installation fournies dans la documentation. Vous aurez peut-être également besoin d'une licence valide pour utiliser certaines des fonctionnalités avancées. Vous pouvez obtenir une licence sur le site Web d'Aspose :[Acheter la licence Aspose.HTML](https://purchase.aspose.com/buy).

4.  Essai gratuit : Si vous souhaitez tester Aspose.HTML avant d'acheter une licence, vous pouvez obtenir une version d'essai gratuite à partir de ce lien :[Essai gratuit d'Aspose.HTML](https://releases.aspose.com/).

Maintenant que vous disposez des prérequis nécessaires, passons à la section suivante où nous importerons les espaces de noms requis.

## Importer des espaces de noms

Pour travailler efficacement avec Aspose.HTML pour .NET, vous devez importer les espaces de noms appropriés dans votre projet. Ci-dessous, nous allons lister les espaces de noms dont vous avez besoin pour les exemples que nous allons aborder :

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Avec ces espaces de noms importés, vous pouvez accéder aux fonctionnalités fournies par Aspose.HTML pour .NET.

## Désactiver l'exécution des scripts

Commençons par un exemple simple de désactivation de l'exécution de script dans un document HTML et de conversion de celui-ci en PDF. Suivez ces étapes :

1. Créez un extrait de code HTML et enregistrez-le dans un fichier nommé « document.html ».

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Initialisez la configuration Aspose.HTML, en marquant « scripts » comme une ressource non fiable.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Initialiser un document HTML avec la configuration spécifiée
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertir HTML en PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

Dans cet exemple, nous avons empêché l'exécution de scripts dans le document HTML, garantissant ainsi la sécurité lors de sa conversion en PDF. Passons maintenant à l'exemple suivant.

## Spécifier la feuille de style de l'utilisateur

Parfois, vous souhaiterez peut-être appliquer des styles personnalisés aux éléments d'un document HTML. Voici comment procéder à l'aide d'Aspose.HTML pour .NET :

1. Créez un extrait de code HTML et enregistrez-le dans un fichier nommé « document.html ».

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Définissez une couleur personnalisée pour le`<span>` élément utilisant une feuille de style utilisateur.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Initialiser un document HTML avec la configuration spécifiée
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertir HTML en PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 Dans cet exemple, nous avons appliqué un style personnalisé à la`<span>` élément, en définissant sa couleur de texte sur vert. Aspose.HTML pour .NET vous permet de manipuler les styles en toute simplicité.

## Délai d'exécution JavaScript expiré

Lorsque vous travaillez avec du code JavaScript qui peut prendre du temps, il est essentiel de définir un délai d'attente pour éviter une exécution indéfinie. Voici comment procéder :

1. Créez un extrait de code HTML avec une boucle sans fin et enregistrez-le dans un fichier nommé « document.html ».

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Définissez un délai d’exécution JavaScript sur 10 secondes.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Initialiser un document HTML avec la configuration spécifiée
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Attendez que tous les scripts soient terminés/annulés et convertissez HTML en PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Dans cet exemple, nous avons limité le temps d'exécution JavaScript à 10 secondes, garantissant que le script ne s'exécute pas indéfiniment, ce qui pourrait potentiellement entraîner des problèmes de performances.

## Gestionnaire de messages personnalisé

Parfois, vous devrez peut-être gérer des messages d'erreur ou des ressources manquantes lors du chargement d'un document HTML. Voici un exemple de création d'un gestionnaire de messages personnalisé :

1. Créez un extrait de code HTML avec une référence de fichier image manquante et enregistrez-le dans un fichier nommé « document.html ».

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Ajoutez un gestionnaire de messages d’erreur au service réseau pour enregistrer les demandes ayant échoué.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Initialiser un document HTML avec la configuration spécifiée
    // Lors du chargement du document, l'application va tenter de charger l'image, et nous verrons le résultat de cette opération dans la console.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertir HTML en PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Dans cet exemple, nous avons ajouté un gestionnaire de messages personnalisé (`LogMessageHandler`) pour enregistrer des informations sur les requêtes ayant échoué. Cela peut être particulièrement utile pour déboguer et gérer les ressources manquantes avec élégance.

## Conclusion

Aspose.HTML pour .NET est une bibliothèque polyvalente qui permet aux développeurs de travailler efficacement avec des documents HTML. Dans ce didacticiel, nous avons abordé les concepts essentiels et fourni des exemples étape par étape pour les tâches courantes, notamment la gestion des scripts, la personnalisation des feuilles de style, le contrôle de l'exécution JavaScript et la gestion des messages personnalisés.

En suivant les étapes décrites dans ce didacticiel, vous pouvez exploiter la puissance d’Aspose.HTML pour .NET pour créer, manipuler et convertir des documents HTML dans vos applications .NET en toute confiance.

## FAQ

### Q1 : Puis-je utiliser Aspose.HTML pour .NET sans acheter de licence ?

A1 : Oui, vous pouvez essayer Aspose.HTML pour .NET avec une version d’essai gratuite, mais certaines fonctionnalités avancées peuvent nécessiter une licence valide.

### Q2 : Comment puis-je obtenir une licence pour Aspose.HTML pour .NET ?

 A2 : Vous pouvez acheter une licence sur le site Web d'Aspose :[Acheter la licence Aspose.HTML](https://purchase.aspose.com/buy).

### Q3 : Dans quels formats puis-je convertir des documents HTML à l’aide d’Aspose.HTML pour .NET ?

A3 : Aspose.HTML pour .NET prend en charge la conversion vers divers formats, notamment PDF, images, etc.

### Q4 : Existe-t-il une communauté ou un forum d'assistance pour Aspose.HTML pour .NET ?

 A4 : Oui, vous pouvez trouver de l'aide et du support sur les forums Aspose :[Forum d'assistance Aspose.HTML](https://forum.aspose.com/).

### Q5 : Aspose.HTML pour .NET fournit-il de la documentation et des tutoriels ?

 A5 : Oui, vous pouvez accéder à la documentation ici :[Documentation Aspose.HTML pour .NET](https://reference.aspose.com/html/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
