---
category: general
date: 2026-02-13
description: Apprenez à créer un gestionnaire de ressources personnalisé en C# pour
  convertir du HTML en archive ZIP, en créant le zip en mémoire avec Aspose.HTML –
  guide étape par étape.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: fr
og_description: Découvrez la solution C# complète pour utiliser un gestionnaire de
  ressources personnalisé afin de convertir du HTML en archive ZIP directement en
  mémoire.
og_title: Gestionnaire de ressources personnalisé – Convertir HTML en ZIP depuis la
  mémoire
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Gestionnaire de ressources personnalisé en C# – Convertir le HTML en archive
  ZIP depuis la mémoire
url: /fr/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gestionnaire de ressources personnalisé – Convertir HTML en archive ZIP depuis la mémoire

Vous avez déjà eu besoin d’un **custom resource handler** pour récupérer chaque image, fichier CSS ou script qu’une page HTML charge, puis compresser le tout sans toucher le disque ? Vous n’êtes pas le seul. Dans de nombreux scénarios d’automatisation web ou de génération d’e‑mails, vous souhaitez que la page entière soit empaquetée en un seul fichier portable, et vous préférez tout garder en RAM pour la rapidité et la sécurité.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre exactement comment **convertir HTML zip archive** en utilisant un **custom resource handler** puis **create zip from memory** avec `System.IO.Compression` de .NET. À la fin, vous disposerez d’une méthode autonome que vous pourrez intégrer dans n’importe quel projet C# utilisant Aspose.HTML.

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (package NuGet `Aspose.HTML`)  
- Connaissances de base des streams et de la classe `ZipArchive`

Aucun outil externe, aucun fichier temporaire, uniquement du traitement pur en mémoire.

## Étape 1 : définir le Custom Resource Handler

Le cœur de la solution est une classe qui hérite de `Aspose.Html.ResourceHandler`. Sa tâche est de fournir un nouveau `Stream` pour chaque ressource externe demandée par le moteur HTML. En renvoyant un nouveau `MemoryStream` à chaque fois, nous gardons les données isolées et prêtes à être empaquetées ultérieurement.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Pourquoi c’est important :**  
Si vous laissez Aspose.HTML écrire les ressources sur le disque, vous devrez les nettoyer par la suite. Un gestionnaire en mémoire élimine la surcharge d’I/O et rend le code sûr pour les environnements sandboxés (par ex., Azure Functions).

## Étape 2 : charger votre document HTML

Ensuite, indiquez à Aspose.HTML le fichier HTML que vous souhaitez empaqueter. Le document peut être sur le disque, une URL, ou même une chaîne brute. Ici, nous utilisons un chemin de fichier pour plus de simplicité.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Astuce :** Si votre HTML référence des ressources relatives, assurez‑vous que le `input.html` se trouve dans le même dossier que ces actifs, sinon le gestionnaire ne pourra pas les localiser.

## Étape 3 : connecter le gestionnaire et enregistrer dans un MemoryStream

Nous créons maintenant une instance du gestionnaire et indiquons à Aspose.HTML de l’utiliser via `HtmlSaveOptions.OutputStorage`. Le HTML résultant (y compris les URL de ressources réécrites) atterrit dans un `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Ce qui se passe en coulisses :**  
Lorsque `document.Save` s’exécute, Aspose.HTML demande au `MemoryResourceHandler` un flux pour chaque ressource. Comme nous renvoyons des `MemoryStream` vides, le moteur écrit les octets bruts directement en mémoire. Aucun fichier temporaire n’est créé.

## Étape 4 : assembler l’archive ZIP entièrement en mémoire

Voici la partie amusante : nous allons créer un `ZipArchive` qui vit à l’intérieur d’un autre `MemoryStream`. Cela nous permet de **create zip from memory** sans jamais toucher le système de fichiers.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Note :** La section commentée montre comment vous pourriez collecter les flux à l’intérieur de `MemoryResourceHandler`. Dans un scénario de production, vous stockeriez chaque `MemoryStream` dans un dictionnaire indexé par l’URL de la ressource originale, puis itéreriez ici pour les ajouter à l’archive.

**Pourquoi garder le ZIP en mémoire ?**  
Stocker l’archive dans un `MemoryStream` rend trivial son envoi direct à un client HTTP (`FileResult` dans ASP.NET Core) ou son téléchargement vers un stockage cloud sans fichier intermédiaire.

## Étape 5 : (Optionnel) persister le ZIP sur le disque

Si vous avez encore besoin d’un fichier physique—peut‑être pour le débogage—écrivez simplement le `zipMemoryStream` sur le disque :

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Exemple complet fonctionnel

En rassemblant tout, voici un programme unique, prêt à copier‑coller, qui **converts HTML to a ZIP archive** entièrement en mémoire.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Résultat attendu

L’exécution du programme crée `output.zip` contenant :

- `index.html` – le HTML réécrit qui pointe vers les ressources empaquetées.  
- Toutes les images, fichiers CSS et JavaScript que la page originale référençait, stockés avec leurs chemins relatifs d’origine.

Ouvrez `index.html` depuis le ZIP dans n’importe quel navigateur et vous verrez la page s’afficher exactement comme lorsqu’elle était sur le système de fichiers.

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| **Et si une ressource est très volumineuse (par ex., une vidéo) ?** | Comme tout vit en mémoire, des fichiers très gros peuvent provoquer une `OutOfMemoryException`. Dans ce cas, diffusez directement vers un fichier temporaire ou limitez la taille que vous acceptez. |
| **Do I need to handle duplicate resource URLs?** | Le dictionnaire du gestionnaire écrasera les doublons. Si vous voulez ne garder qu’une copie, vérifiez `Captured.ContainsKey` avant d’ajouter. |
| **Puis-je l’utiliser dans un contrôleur ASP.NET Core ?** | Absolument. Retournez `File(zipStream.ToArray(), "application/zip", "page.zip")` depuis une méthode d’action. |
| **Qu’en est‑il des ressources HTTPS ?** | Aspose.HTML les téléchargera automatiquement tant que le runtime fait confiance au certificat SSL. Pour les certificats auto‑signés, configurez `ServicePointManager.ServerCertificateValidationCallback`. |
| **Le gestionnaire personnalisé est‑il thread‑safe ?** | L’exemple utilise un dictionnaire statique, qui n’est *pas* thread‑safe. Enveloppez les accès dans un lock ou utilisez un `ConcurrentDictionary` si vous prévoyez de traiter de nombreux documents simultanément. |

## Astuces pro pour la production

- **Reuse the handler** uniquement pour un seul document ; créez une nouvelle instance par requête pour éviter les interférences entre utilisateurs.  
- **Dispose streams** rapidement. Même si les blocs `using` gèrent la plupart des cas, les flux stockés dans le dictionnaire doivent être libérés après la création du ZIP.  
- **Validate the HTML** avant le traitement afin de détecter un balisage malformé qui pourrait amener le gestionnaire à demander des ressources inattendues.  
- **Compress aggressively** en définissant `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` si la taille du fichier est importante.  

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **custom resource handler** votre chemin à travers une page HTML, capturer chaque ressource liée, et **create zip from memory** sans jamais toucher le disque. Le modèle présenté ici est suffisamment flexible pour les scénarios de services web, les tâches en arrière‑plan, ou même les utilitaires de bureau qui doivent livrer un bundle HTML autonome.

Essayez‑le — remplacez `YOUR_DIRECTORY/input.html` par n’importe quelle page, ajustez le gestionnaire pour stocker les ressources dans un `ConcurrentDictionary`, et vous disposerez d’un pipeline HTML‑to‑ZIP en mémoire robuste, prêt pour la production.

---

*Prêt à passer au niveau supérieur ?* Ensuite, explorez comment **convert HTML to PDF** avec Aspose.HTML, ou expérimentez le chiffrement du ZIP pour plus de sécurité. Le ciel est la limite quand vous maîtrisez le streaming en mémoire en C#. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}