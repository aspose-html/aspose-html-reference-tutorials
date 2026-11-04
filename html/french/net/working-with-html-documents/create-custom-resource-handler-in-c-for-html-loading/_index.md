---
category: general
date: 2026-08-15
description: Créer un gestionnaire de ressources personnalisé en C# pour gérer les
  ressources HTML telles que les images et le CSS. Apprenez HTMLLoadOptions, les flux
  mémoire et le chargement de HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: fr
lastmod: 2026-08-15
og_description: Créer un gestionnaire de ressources personnalisé en C# pour contrôler
  la diffusion des ressources HTML. Ce tutoriel montre la configuration de HTMLLoadOptions,
  la gestion des flux mémoire et le chargement de HTMLDocument avec une logique personnalisée.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Créer un gestionnaire de ressources personnalisé en C# – guide complet pour
  la gestion des ressources HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Créer un gestionnaire de ressources personnalisé en C# pour le chargement HTML
url: /fr/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un gestionnaire de ressources personnalisé en C# pour le chargement HTML

Si vous devez **créer un gestionnaire de ressources personnalisé** pour les fichiers HTML, ce guide vous montre exactement comment faire. Vous apprendrez à intercepter les images, les CSS et d’autres actifs lors du chargement d’un document HTML, en utilisant `HTMLLoadOptions` et un flux basé sur la mémoire.

Le tutoriel couvre tout ce qui est nécessaire pour implémenter un gestionnaire réutilisable, configurer les options de chargement et vérifier que les ressources sont correctement capturées. Aucun document externe n’est requis — seulement le code ci‑dessous et les explications.

## Prérequis

- .NET 6.0 ou version ultérieure
- Connaissances de base en C#
- Une référence à la bibliothèque de traitement HTML qui fournit `HTMLDocument`, `HtmlLoadOptions` et `ResourceHandler` (par ex., GroupDocs.Viewer for .NET)

## Vue d’ensemble de la solution

Nous allons :

1. **Créer un gestionnaire de ressources personnalisé** en sous‑classant `ResourceHandler`.
2. Configurer `HTMLLoadOptions` pour utiliser ce gestionnaire.
3. Charger un fichier HTML avec `HTMLDocument` pendant que le gestionnaire fournit un flux pour chaque ressource.
4. (Optionnel) Stocker les ressources reçues sur le disque pour vérification.

Chaque étape comprend le code source complet et le raisonnement qui la sous-tend.

## Étape 1 : Définir la classe du gestionnaire de ressources personnalisé

Créer un gestionnaire personnalisé signifie surcharger `HandleResource` afin que la bibliothèque puisse écrire les octets de la ressource dans un flux que vous contrôlez. L’utilisation d’un `MemoryStream` garde les données en mémoire, ce qui est idéal pour les tests ou un traitement ultérieur.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Pourquoi c’est important :**  
La surcharge de `HandleResource` vous donne un contrôle total sur l’endroit où les données de la ressource sont envoyées. Si vous avez besoin plus tard de mettre en cache des images, de transformer du CSS ou de journaliser l’utilisation des ressources, vous pouvez remplacer le `MemoryStream` par n’importe quelle implémentation de flux personnalisée.

## Étape 2 : Configurer `HTMLLoadOptions` pour utiliser le gestionnaire

`HTMLLoadOptions` vous permet d’insérer le gestionnaire dans le pipeline de chargement. En définissant la propriété `ResourceHandler`, vous indiquez au visualiseur d’appeler `MyHandler` pour chaque actif externe.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Pourquoi c’est important :**  
Sans affecter `ResourceHandler`, le visualiseur écrirait les ressources à son emplacement par défaut (souvent un dossier temporaire). En spécifiant votre propre gestionnaire, vous **créez un gestionnaire de ressources personnalisé** qui correspond à la stratégie de stockage de votre application.

## Étape 3 : Charger le document HTML avec les options configurées

Chargez maintenant le fichier HTML. Le visualiseur appellera `MyHandler.HandleResource` pour chaque ressource rencontrée.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

À ce stade, le contenu HTML est analysé et toutes les ressources externes ont été diffusées dans les tampons mémoire fournis par `MyHandler`.

## Étape 4 (optionnelle) : Accéder aux ressources capturées

Si vous devez inspecter ou persister les ressources, vous pouvez modifier `MyHandler` afin de stocker chaque `MemoryStream` dans un dictionnaire indexé par le nom de la ressource.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Après le chargement, vous pouvez parcourir `handler.Resources` et écrire chaque élément sur le disque :

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Pourquoi c’est important :**  
Le stockage des ressources permet un post‑traitement tel que l’optimisation d’images, la minification de CSS ou l’archivage. Cela fournit également une vérification concrète que la logique de **créer un gestionnaire de ressources personnalisé** fonctionne comme prévu.

## Étape 5 : Nettoyage

Tant `HTMLDocument` que les flux doivent être libérés pour libérer les ressources non gérées.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Exemple complet exécutable

Voici un programme autonome qui montre toutes les étapes, de la définition de la classe à l’extraction des ressources.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Sortie attendue**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

La console répertorie chaque ressource que le visualiseur a diffusée via votre gestionnaire personnalisé, confirmant que le flux de travail **créer un gestionnaire de ressources personnalisé** a réussi.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|---------|
| *Et si une ressource est volumineuse (par ex., image haute résolution) ?* | Remplacez le `MemoryStream` par un `FileStream` pointant vers un dossier temporaire. Cela évite une consommation excessive de mémoire. |
| *Puis‑je filtrer les ressources par type ?* | Dans `HandleResource`, examinez `info.MimeType` ou `info.Extension` et retournez `null` pour les types indésirables. Retourner `null` indique au visualiseur d’ignorer la ressource. |
| *La sécurité des threads est‑elle requise ?* | Si la même instance de gestionnaire est utilisée pour plusieurs chargements concurrents, protégez le dictionnaire `Resources` avec un verrou ou utilisez une collection concurrente. |
| *Comment gérer les URL relatives ?* | `ResourceInfo` contient l’URL d’origine ; vous pouvez la combiner avec le chemin de base du fichier HTML pour résoudre les références relatives avant de les stocker. |

## Conclusion

Vous savez maintenant comment **créer un gestionnaire de ressources personnalisé** en C# pour le chargement HTML, configurer `HTMLLoadOptions`, capturer les actifs diffusés et nettoyer correctement. Ce modèle vous donne un contrôle total sur la gestion des ressources, ouvrant des scénarios tels que le traitement d’images à la volée, la réécriture de CSS ou le stockage sécurisé.

Ensuite, explorez des sujets connexes comme le **chargement de HTMLDocument** avec différentes options de rendu, ou étendez le gestionnaire à des implémentations **C# resource handler** qui écrivent directement vers le stockage cloud. Expérimentez avec la méthode `HandleResource` du gestionnaire pour l’adapter au flux de travail de ressources propre à votre projet.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer du HTML à partir d’une chaîne en C# – Guide du gestionnaire de ressources personnalisé](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Gestionnaire de ressources personnalisé en C# – Tutoriel de conversion HTML en ZIP](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Comment enregistrer du HTML en C# – Guide complet avec un gestionnaire de ressources personnalisé](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}