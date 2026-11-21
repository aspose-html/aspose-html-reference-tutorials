---
category: general
date: 2026-11-20
description: Apprenez à enregistrer du HTML à l'aide d'un ResourceHandler personnalisé
  en C# et également à sauvegarder du HTML dans des archives zip avec un code concis
  et prêt pour la production.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: fr
lastmod: 2026-11-20
og_description: Comment enregistrer du HTML à l'aide d'un ResourceHandler personnalisé
  en C# et éventuellement sauvegarder le HTML dans des fichiers zip — guide complet
  et fonctionnel pour les développeurs .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Comment enregistrer du HTML avec un gestionnaire de ressources personnalisé
  en C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Comment enregistrer du HTML avec un gestionnaire de ressources personnalisé
  en C#
url: /fr/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer du HTML avec un gestionnaire de ressources personnalisé en C#

Si vous avez besoin de savoir **comment enregistrer du HTML** à partir d'une chaîne en mémoire ou d'un document analysé, ce guide présente une solution complète. Utiliser un `ResourceHandler` personnalisé vous permet de contrôler le flux de destination, ce qui signifie que vous pouvez **enregistrer du HTML dans des archives zip** sans écrire de fichiers temporaires.

Vous verrez pourquoi un `ResourceHandler` est préféré à l'ancienne approche `IOutputStorage`, comment le configurer et comment l'étendre pour la compression zip. À la fin de ce tutoriel, vous pourrez intégrer le code dans n'importe quel projet .NET 6+ et l'adapter à vos propres exigences de stockage.

## Ce que vous allez créer

* Un `ResourceHandler` minimal qui renvoie un `MemoryStream`.
* Un `HtmlDocument` créé avec **HtmlAgilityPack**.
* Un appel à `doc.Save` qui écrit le HTML dans le flux fourni par le gestionnaire.
* Un wrapper optionnel qui compresse le HTML résultant dans un fichier zip.

Prérequis :

* .NET 6 SDK ou version ultérieure.
* `HtmlAgilityPack` package NuGet (`dotnet add package HtmlAgilityPack`).
* Familiarité de base avec les flux C#.

## Étape 1 : Créer un gestionnaire de ressources personnalisé (méthode principale pour **comment enregistrer du HTML**)

La classe de base `ResourceHandler` (disponible depuis la version 24.2 du SDK du visualiseur) définit une seule méthode abstraite, `HandleResource`. Implémenter cette méthode vous donne un contrôle total sur l'endroit où le HTML est écrit.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Pourquoi c'est important :** En renvoyant un `MemoryStream`, vous évitez les E/S disque, réduisez la latence et gardez le code déterministe pour les tests unitaires. Le gestionnaire est invoqué automatiquement par la méthode `Save`, vous n'avez donc jamais besoin de passer un flux explicitement.

## Étape 2 : Charger ou créer le document HTML

`HtmlAgilityPack` fournit une classe pratique `HtmlDocument` qui peut analyser une chaîne, un fichier ou un flux. Pour cet exemple, nous chargeons un littéral simple, mais le même code fonctionne avec n'importe quelle source HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Pourquoi c'est important :** Conserver le document en mémoire s'aligne avec l'approche basée sur les flux du gestionnaire personnalisé. Cela vous permet également de manipuler le DOM avant l'enregistrement, comme injecter des scripts ou corriger des balises malformées.

## Étape 3 : Enregistrer le document en utilisant le gestionnaire personnalisé

Appeler `doc.Save` avec une instance de `MyHandler` déclenche la méthode `HandleResource`. Le HTML est écrit directement dans le flux que vous avez renvoyé.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Après la fin de `Save`, le `MemoryStream` à l'intérieur de `MyHandler` contient le HTML sérialisé. Vous pouvez le récupérer ainsi :

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Résultat :** La console affiche le HTML exact que vous avez passé à `LoadHtml`. Cela prouve que vous comprenez maintenant **comment enregistrer du HTML** avec un gestionnaire personnalisé.

## Étape 4 : Étendre le gestionnaire pour **enregistrer du HTML dans un zip**

Si vous souhaitez archiver le HTML, modifiez `MyHandler` pour écrire dans un `ZipArchiveEntry`. L'espace de noms .NET `System.IO.Compression` rend cela simple.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Now use the new handler:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Pourquoi cela fonctionne :** La méthode `HandleResource` crée une entrée zip nommée `document.html`. Lorsque `doc.Save` écrit dans le flux renvoyé, les données sont compressées automatiquement. Comme le zip est construit en mémoire, vous pouvez le renvoyer depuis une API web, le joindre à un e‑mail ou le stocker dans une base de données sans toucher au système de fichiers.

## Questions fréquentes et cas particuliers

### Et si j'ai besoin de plusieurs fichiers HTML dans le même zip ?

Créez une nouvelle entrée pour chaque appel à `HandleResource`. L'argument `resourceName` contient généralement le nom de fichier, vous pouvez donc l'utiliser directement :

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Comment gérer de gros documents sans épuiser la mémoire ?

Remplacez `MemoryStream` par un `FileStream` pointant vers un fichier temporaire. Le gestionnaire renvoie alors le flux de fichier, et vous pouvez supprimer le fichier ultérieurement après la création du zip.

### Cette approche fonctionne-t-elle avec .NET Core sur Linux ?

Oui. Toutes les API utilisées (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) sont multiplateformes. Assurez-vous que le framework cible est au moins .NET 6 pour une compatibilité optimale.

### Puis-je chiffrer l'archive zip ?

`ZipArchive` ne prend en charge le chiffrement par mot de passe que via des bibliothèques tierces (par ex., `SharpZipLib`). Si le chiffrement est requis, encapsulez les octets de sortie avec une bibliothèque qui fournit le chiffrement AES avant de les envoyer au client.

## Astuces professionnelles

* **Réutilisez le gestionnaire** lors du traitement de nombreux documents en lot ; créer un nouveau `ZipArchive` pour chaque fichier ajoute une surcharge inutile.
* **Définissez `LeaveOpen: true`** sur le constructeur `ZipArchive` si vous devez lire les octets du zip pendant que l'archive est encore ouverte.
* **Validez le HTML** avant l'enregistrement en appelant `doc.OptionCheckSyntax = true;` – cela détecte les balises malformées tôt.
* **Enregistrez la taille** du zip généré ; une sortie anormalement grande indique souvent des ressources dupliquées ou une compression manquante.

## Exemple complet fonctionnel

Voici un fichier unique que vous pouvez coller dans un projet console (`dotnet new console`) et exécuter. Il montre à la fois l'enregistrement du HTML brut et la compression zip.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment enregistrer du HTML en C# avec un gestionnaire de ressources personnalisé](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Comment utiliser ZipArchive – Enregistrer du HTML et des ressources dans un fichier ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [enregistrer du html en zip avec un gestionnaire de ressources personnalisé – guide étape par étape](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}