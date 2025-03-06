---
title: Convertir EPUB en image dans .NET avec Aspose.HTML
linktitle: Convertir EPUB en image dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez comment convertir un EPUB en images à l'aide d'Aspose.HTML pour .NET. Tutoriel étape par étape avec des exemples de code et des options personnalisables.
weight: 11
url: /fr/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir EPUB en image dans .NET avec Aspose.HTML


À l'ère du numérique, la capacité à manipuler et à convertir différents formats de documents est une compétence précieuse. Aspose.HTML pour .NET est un outil puissant qui permet aux développeurs de travailler sans effort avec des documents HTML et EPUB. Dans ce didacticiel, nous allons nous plonger dans le monde d'Aspose.HTML pour .NET et vous guider tout au long du processus de conversion de documents EPUB en différents formats d'image. Nous allons décomposer chaque exemple en plusieurs étapes, en expliquant chaque étape tout au long du processus.

## Prérequis

Avant de plonger dans le monde d'Aspose.HTML pour .NET, vous devez vous assurer que vous disposez des conditions préalables suivantes :

1. Visual Studio : assurez-vous que Visual Studio est installé sur votre système. Vous pouvez le télécharger à partir du site Web.

2.  Aspose.HTML pour .NET : vous pouvez obtenir la bibliothèque sur le site Web d'Aspose[ici](https://releases.aspose.com/html/net/).

3. Votre répertoire de données : préparez un répertoire dans lequel vous stockez vos fichiers EPUB et où les images de sortie seront enregistrées.

4. Connaissances de base de C# : la familiarité avec la programmation C# est essentielle pour comprendre et implémenter les exemples de code fournis dans ce didacticiel.

## Importer les espaces de noms nécessaires

Avant de commencer à travailler avec Aspose.HTML pour .NET, vous devez importer les espaces de noms requis dans votre code C#. Ces espaces de noms donnent accès aux fonctionnalités d'Aspose.HTML pour .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Maintenant que nous avons mis en place les prérequis et les espaces de noms, passons aux exemples étape par étape.

## Conversion d'EPUB en JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Ouvrez un fichier EPUB existant pour le lire.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Appelez la méthode ConvertEPUB pour convertir le fichier EPUB en image.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Mesures

1. Fournissez le chemin d'accès à votre fichier EPUB dans la variable dataDir.
2. Ouvrez le fichier EPUB pour le lire à l'aide d'un FileStream.
3. Appelez la méthode ConvertEPUB, en passant le flux EPUB, une ImageSaveOptions spécifiant le format de sortie (JPEG) et le nom du fichier de sortie (« output.jpg »).
5. Le fichier EPUB est converti en image JPEG.

Dans cet exemple, nous ouvrons un fichier EPUB, lisons son contenu et le convertissons en un format d'image JPEG. L'image de sortie est enregistrée sous le nom « output.jpg ».

## Conversion d'EPUB en PNG

Vous pouvez facilement convertir des fichiers EPUB en différents formats d'image tels que PNG, BMP, GIF et TIFF en utilisant des structures de code similaires. Voici un exemple de conversion au format PNG :

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Mesures
1. Ouvrez le fichier EPUB pour le lire à l'aide d'un FileStream.
2. Initialisez un objet ImageSaveOptions avec le format de sortie souhaité (dans ce cas, PNG).
3. Appelez la méthode ConvertEPUB en passant le flux EPUB, les options d’enregistrement de l’image et le nom du fichier de sortie.
4. Le fichier EPUB est converti au format d'image spécifié.

## Spécifier les options d'enregistrement de l'image

Vous pouvez personnaliser la sortie de l'image en spécifiant des options telles que la taille de la page et la couleur d'arrière-plan. Voici un exemple :

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Mesures

1.  Indiquez le chemin d'accès à votre fichier EPUB dans le`dataDir` variable.
2.  Ouvrez le fichier EPUB pour le lire à l'aide d'un`FileStream`.
3.  Créer un`ImageSaveOptions` objet et spécifiez le format de sortie souhaité (JPEG).
4. Personnalisez la taille de la page et la couleur d'arrière-plan, si nécessaire.
5.  Appelez le`ConvertEPUB`méthode, en passant le flux EPUB, les options d'enregistrement de l'image et le nom du fichier de sortie.
6. Le fichier EPUB est converti en image avec les options spécifiées.

## Spécifier un fournisseur de flux personnalisé

Si vous devez manipuler le flux de sortie, vous pouvez utiliser un fournisseur de flux personnalisé. Voici un exemple :

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Code source de la classe MemoryStreamProvider.

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
                // Cette méthode est appelée lorsque la création de plusieurs flux de sortie est requise. Par exemple lors du rendu HTML vers une liste de fichiers image (JPG, PNG, etc.)
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

### Mesures
1.  Indiquez le chemin d'accès à votre fichier EPUB dans le`dataDir` variable.
2.  Ouvrez le fichier EPUB pour le lire à l'aide d'un`FileStream`.
3.  Créer un`MemoryStreamProvider` pour gérer les flux de sortie personnalisés.
4.  Appelez le`ConvertEPUB` méthode, en passant le flux EPUB, les options d'enregistrement de l'image (JPEG) et le fournisseur de flux personnalisé.
5. Parcourez les flux de mémoire dans le fournisseur personnalisé et enregistrez-les dans des fichiers individuels.
6. Cet exemple vous permet de manipuler et d'enregistrer plusieurs flux de sortie selon vos besoins.

## Conclusion

Aspose.HTML pour .NET est une bibliothèque polyvalente qui simplifie le travail avec les documents EPUB et HTML. Avec la possibilité de convertir des documents EPUB en divers formats d'image et des options personnalisables, elle offre une large gamme d'applications pour les développeurs.

---

## Questions fréquemment posées

### 1. Où puis-je télécharger Aspose.HTML pour .NET ?

 Vous pouvez télécharger Aspose.HTML pour .NET à partir de la page des versions[ici](https://releases.aspose.com/html/net/).

### 2. Comment puis-je obtenir une licence temporaire pour Aspose.HTML pour .NET ?

 Pour obtenir une licence temporaire, visitez la page des licences temporaires[ici](https://purchase.aspose.com/temporary-license/).

### 3. Où puis-je trouver une assistance supplémentaire pour Aspose.HTML pour .NET ?

 Pour toute question ou problème, vous pouvez demander de l'aide à la communauté Aspose sur le forum d'assistance[ici](https://forum.aspose.com/).

### 4. Puis-je convertir des documents EPUB en d’autres formats comme PDF ou XPS ?

Oui, vous pouvez utiliser Aspose.HTML pour .NET pour convertir des documents EPUB en différents formats, notamment PDF et XPS.

### 5. Aspose.HTML pour .NET convient-il aussi bien aux projets à petite et à grande échelle ?

Absolument ! Aspose.HTML pour .NET est conçu pour être évolutif, ce qui en fait un excellent choix pour les projets de toutes tailles.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
