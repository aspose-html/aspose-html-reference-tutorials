---
title: Convertir EPUB en PDF dans .NET avec Aspose.HTML
linktitle: Convertir EPUB en PDF dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez comment convertir EPUB en PDF à l'aide d'Aspose.HTML pour .NET. Ce guide étape par étape couvre les options de personnalisation, les FAQ et bien plus encore pour une conversion transparente des documents.
type: docs
weight: 12
url: /fr/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Dans ce didacticiel, nous explorerons comment utiliser Aspose.HTML pour .NET pour convertir des fichiers EPUB en PDF. Aspose.HTML est une puissante bibliothèque .NET qui fournit diverses fonctionnalités pour travailler avec des documents HTML et EPUB. Nous couvrirons les conditions préalables, importerons les espaces de noms nécessaires et décomposerons plusieurs exemples, expliquant chaque étape en détail.

## Conditions préalables

Avant de commencer, assurez-vous que les conditions préalables suivantes sont remplies :

1.  Aspose.HTML pour .NET : assurez-vous que Aspose.HTML pour .NET est installé dans votre projet .NET. Vous pouvez le télécharger depuis[ici](https://releases.aspose.com/html/net/).

2. Votre répertoire de données : vous aurez besoin d'un répertoire de données dans lequel vos fichiers EPUB sont stockés.

Passons maintenant au processus étape par étape de conversion d'EPUB en PDF à l'aide d'Aspose.HTML pour .NET.

## Convertir EPUB en PDF

### Étape 1 : initialisez votre projet

Assurez-vous qu'un projet .NET est configuré et qu'Aspose.HTML pour .NET est installé.

### Étape 2 : Importer les espaces de noms requis

Dans votre fichier de code C#, importez les espaces de noms nécessaires :

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Étape 3 : ouvrez le fichier EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuer à l'étape suivante...
}
```

-  Remplacer`"Your Data Directory"` avec le répertoire réel où se trouve votre fichier EPUB.
- Ce code ouvre le fichier EPUB en lecture.

### Étape 4 : Définir les options PDF et effectuer la conversion

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Créer une instance de`PdfSaveOptions` pour spécifier les paramètres de conversion PDF.
-  Utilisez le`Converter.ConvertEPUB`méthode pour convertir l’EPUB en PDF avec les options données.
- Enregistrez le PDF résultant sous « output.pdf ».

## Spécifier les options d'enregistrement PDF

### Étape 1 : initialisez votre projet

Assurez-vous d'avoir configuré un projet .NET et d'avoir installé Aspose.HTML pour .NET.

### Étape 2 : Importer les espaces de noms requis

Importez les espaces de noms nécessaires dans votre code C# :

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Étape 3 : ouvrez le fichier EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuer à l'étape suivante...
}
```

-  Remplacer`"Your Data Directory"` avec le répertoire réel de votre fichier EPUB.
- Ouvrez le fichier EPUB pour le lire.

### Étape 4 : Personnaliser les options PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Créer une instance de`PdfSaveOptions` et personnalisez-le selon vos besoins.
- Dans cet exemple, nous définissons la taille de la page sur 3 000 pixels de largeur et 1 000 pixels de hauteur, et la couleur d'arrière-plan sur Alice Blue.

### Étape 5 : Effectuer la conversion

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Utilisez le`Converter.ConvertEPUB` méthode pour convertir l’EPUB en PDF avec les options personnalisées.
- Enregistrez le PDF résultant sous « output.pdf ».

## Utiliser un fournisseur de flux personnalisé

### Étape 1 : initialisez votre projet

Configurez un projet .NET et installez Aspose.HTML pour .NET.

### Étape 2 : Importer les espaces de noms requis

Dans votre code C#, importez les espaces de noms nécessaires :

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Étape 3 : ouvrez le fichier EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuer à l'étape suivante...
}
```

-  Remplacer`"Your Data Directory"` avec le répertoire réel de votre fichier EPUB.
- Ouvrez le fichier EPUB pour le lire.

### Étape 4 : Utiliser un fournisseur de flux personnalisé

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Continuer à l'étape suivante...
}
```

-  Créer un`MemoryStreamProvider` pour gérer le résultat de la conversion sous forme de flux mémoire.
-  Utilisez le`Converter.ConvertEPUB` méthode avec le fournisseur de flux personnalisé.

### Étape 5 : Enregistrez le résultat

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Accédez au flux mémoire contenant les données converties.
- Réglez la position du flux au début.
- Créez un fichier PDF de sortie et copiez-y le contenu du flux de mémoire.

### Code source de la classe MemoryStreamProvider. 

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
Vous avez maintenant appris à convertir des fichiers EPUB en PDF à l'aide d'Aspose.HTML pour .NET avec diverses options et possibilités de personnalisation. Aspose.HTML simplifie le processus, offrant flexibilité et contrôle sur la conversion de vos documents.

## Conclusion

Aspose.HTML pour .NET est un outil polyvalent pour convertir des fichiers EPUB en PDF, offrant des options de personnalisation pour adapter le document PDF résultant à vos besoins. Que vous ayez besoin de conversions simples ou d'une personnalisation avancée, Aspose.HTML est là pour vous.

 Si vous ne l'avez pas déjà fait, vous pouvez télécharger Aspose.HTML pour .NET à partir du[site web](https://releases.aspose.com/html/net/) et commencez à l'utiliser dans vos applications .NET dès aujourd'hui.

---

## FAQ

### L’utilisation d’Aspose.HTML pour .NET est-elle gratuite ?
    Aspose.HTML pour .NET est un produit commercial, mais un essai gratuit est disponible[ici](https://releases.aspose.com/).

### Puis-je personnaliser l’apparence du PDF converti ?
   Oui, vous pouvez personnaliser l'apparence du PDF en ajustant des options telles que la taille de la page et la couleur d'arrière-plan, comme indiqué dans l'exemple 2.

### Comment puis-je obtenir de l’assistance pour Aspose.HTML pour .NET ?
    Vous pouvez trouver du soutien et des ressources sur le[Forum Aspose.HTML](https://forum.aspose.com/).

### Existe-t-il d'autres formats que je peux convertir avec Aspose.HTML pour .NET ?
   Oui, Aspose.HTML pour .NET prend en charge divers formats de documents, notamment HTML, EPUB, etc.

### Aspose.HTML pour ..NET est-il adapté à la conversion de documents à grande échelle ?
   Aspose.HTML pour .NET est conçu pour gérer efficacement les conversions de documents à grande échelle, ce qui le rend adapté à un large éventail d'applications.

