---
title: Convertir EPUB en XPS dans .NET avec Aspose.HTML
linktitle: Convertir EPUB en XPS dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez comment convertir EPUB en XPS dans .NET à l'aide d'Aspose.HTML pour .NET. Suivez notre guide étape par étape pour des conversions sans effort.
type: docs
weight: 13
url: /fr/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Recherchez-vous un moyen simple de convertir des fichiers EPUB au format XPS dans vos applications .NET ? Aspose.HTML pour .NET fournit une solution puissante pour y parvenir sans effort. Dans ce guide étape par étape, nous vous guiderons tout au long du processus de conversion d'EPUB en XPS à l'aide d'Aspose.HTML. Commençons!

## Conditions préalables

Avant de vous lancer dans le processus de conversion EPUB vers XPS, vous devez vous assurer que les conditions préalables suivantes sont remplies :

### 1. Aspose.HTML pour la bibliothèque .NET

 Assurez-vous que la bibliothèque Aspose.HTML pour .NET est installée dans votre projet. Si vous ne l'avez pas encore fait, vous pouvez l'obtenir auprès du[Aspose.HTML pour la page de téléchargement .NET](https://releases.aspose.com/html/net/).

### 2. Saisissez le fichier EPUB

Vous aurez besoin d'un fichier EPUB que vous souhaitez convertir en XPS. Assurez-vous que vous disposez d'un fichier EPUB disponible pour la conversion.

### 3. Environnement de développement .NET

Ce guide suppose que vous disposez d’un environnement de développement .NET fonctionnel configuré sur votre ordinateur.

## Importer un espace de noms

Pour commencer, vous devez importer l'espace de noms nécessaire pour Aspose.HTML :

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Convertir EPUB en XPS

Décomposons le processus de conversion d'un fichier EPUB au format XPS en plusieurs étapes.

### Étape 1.1 : ouvrez le fichier EPUB

Tout d’abord, ouvrez le fichier EPUB existant pour le lire à l’aide d’un FileStream :

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuer le processus de conversion
}
```

### Étape 1.2 : Créer des XpsSaveOptions

Créez une instance de XpsSaveOptions. Cette étape est cruciale pour configurer la sortie XPS :

```csharp
var options = new XpsSaveOptions();
```

### Étape 1.3 : Convertir EPUB en XPS

Maintenant, appelons la méthode ConvertEPUB pour convertir l'EPUB en XPS :

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Spécifier les options XPS personnalisées

Vous pouvez personnaliser davantage la sortie XPS en spécifiant des options personnalisées telles que la taille de la page et la couleur d'arrière-plan.

### Étape 2.1 : Taille de page personnalisée et couleur d'arrière-plan

Créez une instance de XpsSaveOptions avec une taille de page et une couleur d'arrière-plan personnalisées :

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Étape 2.2 : Convertir EPUB en XPS avec des options personnalisées

Maintenant, appelez la méthode ConvertEPUB pour convertir l'EPUB en XPS avec les options personnalisées :

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Utiliser un fournisseur de flux personnalisé

Dans cette étape, nous convertirons EPUB en XPS à l'aide d'un fournisseur de flux personnalisé, vous permettant de manipuler les données résultantes.

### Étape 3.1 : Créer un MemoryStreamProvider

Créez une instance de MemoryStreamProvider :

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Continuer le processus de conversion
}
```

### Étape 3.2 : Convertir EPUB en XPS avec le fournisseur de flux

Convertissez EPUB en XPS à l'aide de MemoryStreamProvider :

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Étape 3.3 : Accéder et enregistrer le résultat

Récupérez le flux mémoire contenant les données converties et enregistrez-le dans un fichier de sortie :

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Code source de la classe MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Liste des objets MemoryStream créés lors du rendu du document
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Cette méthode est appelée lorsqu'un seul flux de sortie est requis, par exemple pour les formats XPS, PDF ou TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Cette méthode est appelée lorsque la création de plusieurs flux de sortie est requise. Par exemple lors du rendu HTML vers la liste des fichiers image (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Ici, vous pouvez libérer le flux rempli de données et, par exemple, le vider sur le disque dur
            }
            public void Dispose()
            {
                // Libérer des ressources
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Toutes nos félicitations! Vous avez converti avec succès un fichier EPUB au format XPS à l'aide d'Aspose.HTML pour .NET.

## Conclusion

Dans ce didacticiel complet, nous avons exploré comment exploiter Aspose.HTML pour .NET pour convertir des fichiers EPUB au format XPS avec diverses options de personnalisation. Que vous soyez un développeur chevronné ou tout juste débutant, Aspose.HTML simplifie le processus, vous permettant de gérer facilement les conversions EPUB vers XPS.

 Vous avez des questions ou rencontré des problèmes ? Vérifiez[Documentation Aspose.HTML](https://reference.aspose.com/html/net/) pour plus d'informations ou demandez de l'aide au[Forum communautaire Aspose.HTML](https://forum.aspose.com/).

## Questions fréquemment posées

### Qu’est-ce qu’Aspose.HTML pour .NET ?
Aspose.HTML pour .NET est une bibliothèque puissante qui permet aux développeurs de travailler avec des documents HTML, EPUB et XPS dans des applications .NET.

### Où puis-je télécharger Aspose.HTML pour .NET ?
 Vous pouvez télécharger Aspose.HTML pour .NET à partir du[page de téléchargement](https://releases.aspose.com/html/net/).

### Existe-t-il un essai gratuit disponible pour Aspose.HTML pour .NET ?
 Oui, vous pouvez bénéficier d'un essai gratuit auprès de[ici](https://releases.aspose.com/).

### Comment puis-je obtenir une licence temporaire pour Aspose.HTML pour .NET ?
 Pour obtenir un permis temporaire, visitez le[page de licence temporaire](https://purchase.aspose.com/temporary-license/).

### Où puis-je trouver plus de didacticiels et de documentation pour Aspose.HTML pour .NET ?
Explorez un large éventail de didacticiels et de documentation détaillée sur le[Documentation Aspose.HTML](https://reference.aspose.com/html/net/) page.