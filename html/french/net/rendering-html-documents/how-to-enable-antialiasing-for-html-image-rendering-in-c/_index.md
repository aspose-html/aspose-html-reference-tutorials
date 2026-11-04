---
category: general
date: 2026-09-10
description: Comment activer l'anticrénelage pour le rendu d'images HTML en C#. Apprenez
  le rendu d'images de haute qualité avec Aspose.HTML et convertissez du HTML en image
  en quelques étapes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- render html to image
- high quality image rendering
- how to render html image
language: fr
lastmod: 2026-09-10
og_description: Comment activer l'anticrénelage pour le rendu d'images HTML en C#.
  Ce guide vous montre le rendu d'images de haute qualité et comment rendre une image
  HTML avec Aspose.HTML.
og_image_alt: Diagram illustrating how to enable antialiasing in Aspose.HTML image
  rendering
og_title: Activer l'anticrénelage pour le rendu d'images HTML en C# – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to enable antialiasing for HTML image rendering in C#. Learn high
    quality image rendering with Aspose.HTML and render HTML to image in a few steps.
  headline: How to enable antialiasing for HTML image rendering in C#
  type: TechArticle
tags:
- Aspose.HTML
- C#
- image rendering
- antialiasing
title: Comment activer l'anticrénelage pour le rendu d'images HTML en C#
url: /fr/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage pour le rendu d'images HTML en C#

Si vous avez besoin de **comment activer l'anticrénelage** lors de la conversion de contenu web en bitmap, ce tutoriel vous fournit une solution complète, prête à l’emploi. Un rendu d’image de haute qualité est essentiel lorsque vous générez des vignettes, des PDF ou des captures d’écran qui doivent rester nettes sur n’importe quel affichage. À la fin de ce guide, vous serez capable de rendre du HTML en image avec des bords lisses et sans artefacts dentelés.

Nous parcourrons l’installation d’Aspose.HTML, la configuration de l’anticrénelage et l’enregistrement du résultat au format PNG. Aucun outil externe n’est requis, et le code fonctionne sous Windows, Linux et macOS. Le tutoriel aborde également les pièges courants tels que la gestion du DPI et la consommation mémoire, afin que vous puissiez adapter l’approche à du traitement par lots ou à des services web.

## Prérequis

- SDK .NET 6.0 ou ultérieur (l’exemple utilise .NET 6, mais toute version .NET Core/Framework supportant Aspose.HTML fonctionne)
- Une licence valide d’Aspose.HTML for .NET (ou une clé d’évaluation gratuite)
- Une connaissance de base du C# et de Visual Studio / VS Code
- Le package NuGet `Aspose.Html` installé :

```bash
dotnet add package Aspose.Html
```

## Étape 1 : Créer un document HTML de base

Tout d’abord, construisez le HTML que vous souhaitez rendre. Vous pouvez charger une chaîne, un fichier ou une URL. Dans cet exemple, nous utilisons une chaîne en ligne afin que le tutoriel reste autonome.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Sample HTML – a red circle on a white background
const string htmlContent = @"
<!DOCTYPE html>
<html>
<head>
    <style>
        body { margin:0; background:#fff; }
        .circle {
            width:200px; height:200px;
            background:#e53935;
            border-radius:50%;
            margin:20px auto;
        }
    </style>
</head>
<body>
    <div class='circle'></div>
</body>
</html>";
```

Le HTML définit une forme vectorielle simple qui bénéficie de l’anticrénelage lorsqu’elle est rasterisée.

## Étape 2 : Initialiser le moteur de rendu

Aspose.HTML utilise un `HtmlRenderer` conjointement avec `ImageRenderingOptions`. C’est ici que vous **comment activer l'anticrénelage** pour le bitmap final.

```csharp
// Load the HTML into a Document object
using var document = new HTMLDocument(htmlContent, ".");

// Prepare image rendering options
var imageOptions = new ImageRenderingOptions
{
    // Primary setting for smooth edges
    UseAntialiasing = true,

    // Optional: increase DPI for higher pixel density
    // This improves perceived quality on high‑resolution screens
    DpiX = 300,
    DpiY = 300,

    // Choose PNG for lossless output
    ImageFormat = ImageFormat.Png
};
```

**Pourquoi `UseAntialiasing = true` est important** : le moteur de rendu dessine les formes vectorielles, le texte et les dégradés avec une précision sous‑pixel. Activer l’anticrénelage indique au rasteriseur de mélanger les pixels de bord avec leurs voisins, éliminant ainsi les lignes dentelées qui apparaissent lorsque `UseAntialiasing` reste à la valeur par défaut `false`. C’est le cœur du **rendu d’image de haute qualité**.

## Étape 3 : Rendre le HTML en image

Une fois les options configurées, appelez la méthode `RenderToImage`. Cette méthode renvoie un objet `Image` que vous pouvez enregistrer sur disque ou transmettre directement à une réponse.

```csharp
// Render the document to an image using the options above
using var image = document.RenderToImage(imageOptions);

// Save the image to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
image.Save(outputPath);
```

Après exécution, `output.png` contient un cercle lisse et antialiasé. Ouvrez le fichier dans n’importe quel visualiseur d’images pour vérifier le résultat.

![comment activer l'anticrénelage dans le rendu Aspose.HTML](/images/antialiasing-example.png){alt="comment activer l'anticrénelage dans le rendu Aspose.HTML"}

## Étape 4 : Vérifier la sortie haute qualité (comment rendre une image HTML)

Vous pouvez confirmer programmatique les dimensions et le DPI de l’image afin de vous assurer que le rendu répond à vos attentes.

```csharp
using System.Drawing;

// Load the saved PNG for inspection
using var bitmap = new Bitmap(outputPath);
Console.WriteLine($"Width: {bitmap.Width}px, Height: {bitmap.Height}px");
Console.WriteLine($"Horizontal DPI: {bitmap.HorizontalResolution}, Vertical DPI: {bitmap.VerticalResolution}");
```

Sortie typique de la console :

```
Width: 240px, Height: 240px
Horizontal DPI: 300, Vertical DPI: 300
```

Le DPI augmenté combiné à l’anticrénelage produit un résultat net même lorsque l’image est agrandie. Cela démontre **comment rendre une image HTML** avec une qualité professionnelle.

## Variations courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|-----------------------|
| Rendu de pages très volumineuses (p. ex. applications web plein écran) | Augmentez `ImageRenderingOptions.Width` / `Height` ou définissez `Scale` pour contrôler la consommation mémoire. |
| Besoin d’un arrière‑plan transparent | Définissez `imageOptions.BackgroundColor = Color.Transparent;` |
| Cibler JPEG pour une taille de fichier plus petite | Changez `ImageFormat` en `ImageFormat.Jpeg` et ajustez `Quality` (0‑100). |
| Exécution dans un conteneur Linux sans interface graphique | Aspose.HTML fonctionne entièrement en mode headless ; aucune dépendance supplémentaire n’est requise. |
| Vous devez désactiver l'anticrénelage pour un test UI pixel‑perfect | Définissez `UseAntialiasing = false;` – les bords seront nets mais pourront paraître dentelés. |

### Astuce pro

Lorsque vous générez un lot d’images, réutilisez une seule instance `HTMLDocument` et ne modifiez que sa propriété `Content` entre les rendus. Cela réduit le coût d’analyse du même HTML à plusieurs reprises et améliore le débit.

## Liste complète du code source

Voici le programme complet que vous pouvez copier dans un nouveau projet console et exécuter immédiatement.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment rendre le HTML en image avec C# – Guide complet](/html/english/net/rendering-html-documents/how-to-render-html-to-an-image-with-c-complete-guide/)
- [Tutoriel HTML vers Image – Rendre le HTML en PNG en C#](/html/english/net/generate-jpg-and-png-images/html-to-image-tutorial-render-html-to-png-in-c/)
- [Comment utiliser Aspose pour rendre le HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}