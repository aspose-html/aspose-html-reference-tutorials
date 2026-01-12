---
category: general
date: 2025-12-29
description: Comment compresser rapidement du HTML en C# avec Aspose.HTML – enregistrer
  le HTML dans un zip à l’aide d’un ZipResourceHandler personnalisé. Apprenez étape
  par étape.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: fr
og_description: Comment compresser du HTML en C# rapidement avec Aspose.HTML. Suivez
  ce guide pour enregistrer le HTML dans un zip et créer une archive zip avec une
  gestion personnalisée des ressources.
og_title: Comment compresser du HTML en C# – Enregistrer le HTML dans un zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Comment compresser du HTML en C# – Enregistrer le HTML dans un zip
url: /fr/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment zipper du HTML en C# – Enregistrer le HTML dans un zip

Zipper du HTML en C# est un besoin fréquent lorsque vous souhaitez empaqueter des pages web pour une utilisation hors ligne. Que vous regroupiez une seule page avec ses images ou que vous exportiez un site complet, **saving HTML to zip** permet de garder tout bien organisé et portable. Dans ce tutoriel, nous parcourrons une solution complète, prête à l’emploi, qui non seulement zippe le code HTML mais diffuse également chaque ressource référencée directement dans l’archive.

Vous apprendrez à :

* Créer une archive zip programmatique avec `System.IO.Compression` de .NET.
* Brancher un `ResourceHandler` personnalisé dans Aspose.HTML afin que les ressources aillent directement dans le zip.
* Gérer les cas particuliers comme les fichiers zip existants et les gros actifs binaires.

Aucun outil externe requis — juste C#, Aspose.HTML et quelques lignes de code.

## Ce qu’il vous faut

Avant de commencer, assurez‑vous d’avoir :

* **.NET 6+** (le code fonctionne également avec .NET Framework 4.6.2 et versions ultérieures).
* **Aspose.HTML for .NET** – vous pouvez obtenir une version d’essai gratuite sur le site d’Aspose ou utiliser une copie sous licence.
* Un environnement de développement (Visual Studio, VS Code, Rider—ce que vous préférez).

C’est tout. Aucun package NuGet supplémentaire en dehors de `System.IO.Compression` (fourni avec .NET) et `Aspose.HTML`.

## Étape 1 : Configurer le projet et les imports

Créez un nouveau projet console (ou ajoutez le code à un projet existant). Ajoutez les directives `using` requises en haut de votre fichier :

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Astuce :** Si vous utilisez Visual Studio, l’IDE proposera d’ajouter le package NuGet manquant pour `Aspose.Html`. Acceptez‑le, et vous êtes prêt à démarrer.

## Étape 2 : Implémenter un ZipResourceHandler personnalisé

Aspose.HTML appelle un `ResourceHandler` chaque fois qu’il doit écrire une ressource (comme une image, un fichier CSS ou un script). En surchargeant `HandleResource`, nous pouvons décider exactement où chaque ressource sera placée. Le gestionnaire ci‑dessous crée une entrée zip qui reflète le chemin logique de la ressource, puis renvoie un flux d’écriture pointant directement sur cette entrée.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Pourquoi c’est important :**  
Au lieu d’écrire les ressources dans un dossier temporaire puis de zipper le dossier, ce gestionnaire diffuse les données à la volée, économisant les entrées/sorties disque et limitant l’utilisation de la mémoire. Il garantit également que la hiérarchie interne du zip correspond aux chemins relatifs du HTML, ce que les navigateurs attendent lorsqu’on dézippe et ouvre la page.

## Étape 3 : Préparer l’archive zip

Nous allons maintenant ouvrir (ou créer) le fichier zip cible. Le drapeau `FileMode.Create` écrase tout fichier existant—idéal pour des builds répétables. Si vous préférez conserver une archive existante, passez à `FileMode.OpenOrCreate` et gérez les entrées dupliquées en conséquence.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Cas particulier :** Si le processus se bloque avant que le bloc `using` ne libère l’archive, vous pourriez vous retrouver avec un zip corrompu. Exécuter le code dans un `try/catch` et supprimer le fichier partiellement créé en cas d’échec constitue une protection simple.

## Étape 4 : Construire le document HTML avec une ressource intégrée

À titre d’exemple, nous créerons une petite page HTML qui référence une image nommée `image.png`. Dans un scénario réel, vous chargeriez le HTML depuis un fichier ou une chaîne provenant d’une base de données.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Si vous avez de véritables fichiers image sur le disque, vous pouvez les ajouter manuellement au zip avant d’enregistrer le HTML, ou laisser Aspose.HTML les récupérer via le gestionnaire (par ex., depuis une URL). Le gestionnaire que nous avons écrit fonctionne à la fois pour les chemins locaux et les URLs distantes.

## Étape 5 : Configurer les options de sauvegarde pour utiliser le ZipResourceHandler

Nous indiquons maintenant à Aspose.HTML d’utiliser notre gestionnaire personnalisé lors de l’écriture des ressources. La classe `HTMLSaveOptions` vous permet également de spécifier le nom du fichier de sortie à l’intérieur du zip (par défaut, c’est `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Étape 6 : Enregistrer le document – Tout est diffusé dans le zip

Enfin, invoquez `Save`. Aspose.HTML analyse le markup, localise la balise `<img>`, appelle `HandleResource` pour `image.png`, et écrit à la fois le fichier HTML et l’image dans la même archive zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Lorsque les blocs `using` se terminent, le `ZipArchive` finalise le fichier, le rendant prêt à être distribué.

### Exemple complet fonctionnel

Voici le programme complet assemblé. Copiez‑collez‑le dans `Program.cs` et exécutez—aucune modification supplémentaire n’est nécessaire.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Résultat attendu :** Après exécution, `output.zip` contient deux entrées :

```
index.html
image.png
```

Si vous dézippez le fichier et ouvrez `index.html` dans un navigateur, l’image s’affiche correctement car le chemin relatif est préservé.

## Questions fréquentes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}