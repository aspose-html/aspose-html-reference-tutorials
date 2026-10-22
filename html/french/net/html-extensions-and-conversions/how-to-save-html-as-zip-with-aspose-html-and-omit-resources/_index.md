---
category: general
date: 2026-10-21
description: Apprenez à enregistrer du HTML au format ZIP avec Aspose.HTML, à convertir
  du HTML en ZIP et à supprimer les ressources pour obtenir un package propre.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: fr
lastmod: 2026-10-21
og_description: Enregistrez le HTML au format ZIP avec Aspose.HTML, apprenez comment
  convertir le HTML en ZIP et supprimer les ressources pour une archive légère.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Enregistrez le HTML au format ZIP avec Aspose.HTML – omettez les ressources
  en une seule étape
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Comment enregistrer du HTML en ZIP avec Aspose.HTML et omettre les ressources
url: /fr/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer du HTML en ZIP avec Aspose.HTML et omettre les ressources

Si vous devez **enregistrer du HTML en ZIP** tout en supprimant les fichiers externes, ce guide présente une solution complète, prête à l’emploi. À la fin du tutoriel, vous serez capable de **convertir du HTML en ZIP**, de contrôler les ressources conservées et de produire une archive propre qui ne contient que le balisage principal.

De nombreux scénarios d’automatisation web nécessitent d’emballer une page pour une utilisation hors ligne, une pièce jointe email ou un archivage. Inclure des images, des polices ou des scripts gonfle souvent l’archive inutilement. Les étapes ci‑dessous expliquent **comment omettre les ressources** et **comment supprimer les ressources** de la sortie, afin que le ZIP résultant reste léger.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou version ultérieure installé  
- Une licence Aspose.HTML for .NET (ou une évaluation gratuite)  
- Un environnement de développement C# de base (Visual Studio, VS Code ou Rider)  

Aucun package NuGet supplémentaire n’est requis au-delà de `Aspose.Html`.

## Étape 1 : Créer un gestionnaire de ressources personnalisé

Le cœur de **comment omettre les ressources** réside dans une sous‑classe de `ResourceHandler`. Aspose.HTML appelle ce gestionnaire pour chaque ressource externe (images, CSS, scripts). En retournant un flux vide, vous indiquez effectivement au convertisseur d’ignorer la ressource.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Pourquoi c’est important :** Le comportement par défaut copie chaque fichier lié dans le ZIP, ce qui peut doubler ou tripler la taille du fichier. Surcharger `HandleResource` vous donne un contrôle fin sans modifier le HTML original.

## Étape 2 : Charger le document HTML

Chargez le fichier source avec `HTMLDocument`. Le constructeur accepte un chemin de fichier, une URL ou un flux. Dans cet exemple, nous lisons un fichier local nommé `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Si votre HTML réside en mémoire ou provient d’une requête web, vous pouvez passer un `MemoryStream` ou une chaîne URL à la place. L’API fonctionne de la même manière.

## Étape 3 : Configurer les options d’enregistrement

Créez une instance de `HtmlSaveOptions` et affectez le gestionnaire personnalisé créé à l’Étape 1. Cela indique à Aspose.HTML d’utiliser le gestionnaire chaque fois qu’il rencontre une ressource.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Vous pouvez également ajuster d’autres options ici, comme `CompressImages = false` si vous souhaitez conserver les données d’image tout en omettant les autres actifs. L’exemple conserve les paramètres de compression par défaut.

## Étape 4 : Enregistrer le document en tant qu’archive ZIP

Enfin, invoquez `Save` avec le chemin cible et les options configurées. Le fichier de sortie sera un `.zip` contenant `index.html` (ou le nom de fichier original) et **aucune ressource externe**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Résultat attendu

- `output.zip` → contient un seul fichier `index.html`.  
- Toutes les images, fichiers CSS et références JavaScript sont omis, car le gestionnaire personnalisé a renvoyé un flux vide pour chacun.  

Vous pouvez vérifier l’archive en l’ouvrant avec n’importe quel visualiseur ZIP. La page HTML référencera toujours les URL originales, mais ces fichiers ne seront pas présents dans l’archive, ce qui maintient le paquet minimal.

## Exemple complet et exécutable

Voici le programme complet que vous pouvez copier, coller et exécuter. Remplacez `YOUR_DIRECTORY` par un chemin de dossier réel sur votre machine.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

L’exécution de ce programme produit le fichier ZIP décrit précédemment. Vous pouvez désormais distribuer la page HTML sans regrouper d’actifs inutiles.

## Variations courantes et cas limites

| Scénario | Ajustement |
|----------|------------|
| **Conserver les images mais supprimer CSS/JS** | Dans `CustomResourceHandler`, inspectez `info.MimeType`. Retournez un `MemoryStream` uniquement pour `text/css` et `application/javascript`. |
| **Conserver les polices externes** | Retournez le flux original pour les types MIME `font/woff2`, sinon retournez un flux vide. |
| **Générer un ZIP avec un nom d’entrée personnalisé** | Utilisez la surcharge `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)` pour spécifier un nom de fichier racine différent. |
| **Convertir plusieurs fichiers HTML en un seul ZIP** | Parcourez chaque fichier, créez un `HTMLDocument` séparé, et ajoutez chacun au même `ZipArchive` manuellement en utilisant `System.IO.Compression`. |

Ces variations illustrent **comment supprimer sélectivement les ressources**, vous offrant un contrôle total sur la taille finale de l’archive.

## Astuces professionnelles

- **Valider le résultat** : après l’enregistrement, ouvrez le ZIP et chargez `index.html` dans un navigateur. Les ressources manquantes apparaîtront comme des liens brisés, confirmant que le gestionnaire a fonctionné.  
- **Performance** : retourner un `MemoryStream` vide est peu coûteux, mais si vous avez des milliers d’actifs, envisagez de mettre en cache la décision (par ex., un `HashSet<string>` des types MIME à ignorer).  
- **Licences** : la version d’évaluation gratuite d’Aspose.HTML ajoute un commentaire filigrane dans le HTML. Déployez une version sous licence pour le supprimer en production.  

## Conclusion

Vous savez maintenant comment **enregistrer du HTML en ZIP**, **convertir du HTML en ZIP** et **supprimer les ressources** à l’aide d’Aspose.HTML pour .NET. En implémentant un `ResourceHandler` personnalisé, vous pouvez omettre les fichiers indésirables et garder l’archive légère. Expérimentez la logique du gestionnaire pour ne conserver que les ressources réellement nécessaires, et intégrez ce modèle dans des pipelines d’automatisation plus vastes.

---

**Étapes suivantes**

- Explorez d’autres fonctionnalités de `HtmlSaveOptions` telles que `EmbedImages` pour intégrer les images directement dans le HTML.  
- Combinez cette approche avec `Aspose.PDF` pour convertir le même HTML en PDF après la création du ZIP.  
- Examinez les scénarios côté serveur où vous générez le ZIP à la demande et le diffusez vers un client sans l’écrire sur le disque.  

Bonne programmation !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment utiliser ZipArchive – Enregistrer le HTML et les ressources dans un fichier ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Comment enregistrer du HTML en C# – Gestionnaires de ressources personnalisés & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Comment enregistrer du HTML en ZIP en C# – Guide complet Aspose.HTML](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}