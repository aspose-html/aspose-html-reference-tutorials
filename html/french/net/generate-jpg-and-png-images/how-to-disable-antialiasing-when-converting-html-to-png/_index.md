---
category: general
date: 2026-03-25
description: Apprenez comment désactiver l'anticrénelage lors de la conversion de
  HTML en PNG, garantissant un rendu pixel‑parfait. Comprend les étapes pour rendre
  le HTML en image, enregistrer le HTML en PNG et créer un PNG à partir du HTML.
draft: false
keywords:
- how to disable antialiasing
- convert html to png
- render html as image
- save html as png
- create png from html
language: fr
og_description: Découvrez la méthode étape par étape pour désactiver l'anticrénelage
  lors de la conversion de HTML en PNG, vous garantissant un rendu d'image pixel‑parfait
  à chaque fois.
og_title: Comment désactiver l'anticrénelage lors de la conversion de HTML en PNG
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Comment désactiver l'anticrénelage lors de la conversion de HTML en PNG
url: /fr/net/generate-jpg-and-png-images/how-to-disable-antialiasing-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment désactiver l'anticrénelage lors de la conversion de HTML en PNG

Vous vous êtes déjà demandé **comment désactiver l'anticrénelage** afin que votre conversion de HTML‑vers‑PNG ressemble exactement au balisage source ? Peut‑être créez‑vous un générateur de vignettes pour des composants UI et les bords flous nuisent à la fidélité visuelle. Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils essaient de **convertir du HTML en PNG** pour des captures d'écran pixel‑parfaites.

Dans ce tutoriel, nous parcourrons le processus complet de **rendu du HTML en image**, ajusterons le pipeline de rendu pour désactiver l'anticrénelage, et enfin **enregistrer le HTML en PNG** à l'aide d'Aspose.HTML pour .NET. À la fin, vous disposerez d'un extrait prêt à l'exécution qui crée un PNG net à partir de n'importe quel fichier HTML, et vous comprendrez pourquoi la désactivation de l'anticrénelage est importante pour certains scénarios sensibles au design.

## Ce dont vous aurez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+).  
- **Aspose.HTML for .NET** package NuGet (`Aspose.HTML`).  
- Un simple fichier `input.html` que vous souhaitez rasteriser.  
- Tout IDE de votre choix — Visual Studio, Rider, ou même VS Code avec l'extension C#.

Aucune bibliothèque native supplémentaire ni aucun outil externe n'est requis ; Aspose.HTML gère tout en interne.

## Étape 1 : Installer Aspose.HTML

La première chose dont vous avez besoin est la bibliothèque Aspose.HTML. Ouvrez votre terminal (ou la console du gestionnaire de packages) et exécutez :

```bash
dotnet add package Aspose.HTML
```

Ou, si vous préférez l'interface NuGet, recherchez **Aspose.HTML** et cliquez sur *Installer*. Ce package est livré avec un moteur de rendu puissant capable de produire PNG, JPEG, BMP, et plus encore.

> **Astuce :** Utilisez la dernière version stable (en mars 2026, c’est la 23.12) pour profiter des corrections de bugs liées au rendu d'images et aux contrôles d'anticrénelage.

## Étape 2 : Charger le document HTML

Une fois le package installé, vous pouvez charger le HTML que vous souhaitez transformer. La classe `HTMLDocument` abstrait le DOM et vous permet de le manipuler avant le rendu si nécessaire.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Path to your source HTML file
string inputPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Create a new HTMLDocument instance
HTMLDocument htmlDoc = new HTMLDocument(inputPath);
```

> **Pourquoi c’est important :** Charger le document en premier vous donne la possibilité d’injecter du CSS ou de corriger les URL relatives avant l’étape de rasterisation. Cela isole également le rendu du système de fichiers, rendant le code plus facile à tester.

## Étape 3 : Configurer ImageSaveOptions et désactiver l'anticrénelage

Voici le cœur du tutoriel : désactiver l'anticrénelage. Aspose.HTML expose `ImageRenderingOptions` où vous pouvez basculer `UseAntialiasing`. Le définir à `false` oblige le moteur à rendre chaque pixel exactement comme défini par les formes vectorielles, produisant un **PNG pixel‑parfait**.

```csharp
// Create ImageSaveOptions for PNG output
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach rendering options
    ImageRenderingOptions = new ImageRenderingOptions
    {
        // Disable antialiasing for a crisp raster image
        UseAntialiasing = false
    }
};
```

### Ce que fait réellement l'anticrénelage

L'anticrénelage lisse les bords des formes en mélangeant les couleurs des pixels voisins. Bien que cela soit idéal pour les photographies ou les graphiques complexes, cela peut flouter les éléments UI nets (pensez aux icônes ou au texte de petite taille). Le désactiver garantit que chaque ligne reste ultra‑net—exactement ce dont vous avez besoin lorsque vous **créez des PNG à partir de HTML** pour les tests UI ou la documentation.

## Étape 4 : Rendre et enregistrer le PNG

Maintenant que les options sont configurées, appelez `Save` sur le `HTMLDocument`. La méthode prend le chemin de sortie et les `ImageSaveOptions` configurés précédemment.

```csharp
// Destination path for the PNG file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");

// Render the HTML and write the PNG file
htmlDoc.Save(outputPath, saveOptions);
```

L'exécution du code ci‑dessus générera `output.png` juste à côté de votre exécutable. Ouvrez‑le dans n'importe quel visualiseur d'images — vous devriez voir une version nette, sans anticrénelage, de `input.html`.

### Résultat attendu

| Before (Antialiasing On) | After (Antialiasing Off) |
|--------------------------|--------------------------|
| ![Sortie antialiasée](antialiased.png "exemple de désactivation de l'anticrénelage avec bords flous") | ![Sortie pixel‑parfaite](pixelperfect.png "exemple de désactivation de l'anticrénelage avec bords nets") |

*L'image de gauche montre le rendu antialiasé par défaut, tandis que l'image de droite montre le résultat net après désactivation de l'anticrénelage.*

> **Note :** Les captures d'écran ci‑dessus sont des espaces réservés ; remplacez‑les par vos propres fichiers lors de la publication.

## Étape 5 : Vérifier la sortie de manière programmatique (optionnel)

Si vous devez vous assurer que le PNG répond à certains critères (par ex., dimensions exactes ou profondeur de couleur), vous pouvez l'inspecter à l'aide de `System.Drawing` ou `SixLabors.ImageSharp`. Voici une vérification rapide avec `ImageSharp` :

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;

using (Image<Rgba32> img = Image.Load<Rgba32>(outputPath))
{
    Console.WriteLine($"Width: {img.Width}px, Height: {img.Height}px");
    // Verify that the image has no blended pixels (simple heuristic)
    // You could compare a few pixel values against expected RGBA values.
}
```

Cette étape supplémentaire est pratique lorsque vous automatisez la génération de PNG dans un pipeline CI et devez garantir la cohérence.

## Cas limites et questions fréquentes

### Et si mon HTML utilise des ressources externes ?

Si le HTML référence des CSS, des polices ou des images via des URL relatives, assurez‑vous que l'URL de base du `HTMLDocument` pointe vers le dossier contenant ces ressources :

```csharp
HTMLDocument htmlDoc = new HTMLDocument(inputPath, new Uri("file:///" + Path.GetDirectoryName(inputPath) + "/"));
```

### Puis‑je modifier le DPI ou la taille de l'image ?

Absolument. `ImageRenderingOptions` vous permet également de définir `Resolution` (points par pouce) ainsi que `Width`/`Height` :

```csharp
saveOptions.ImageRenderingOptions.Resolution = 300; // High‑resolution PNG
saveOptions.ImageRenderingOptions.Width = 800;      // Desired pixel width
saveOptions.ImageRenderingOptions.Height = 600;     // Desired pixel height
```

Gardez simplement à l'esprit qu'augmenter le DPI sans mettre à l'échelle le viewport peut produire un fichier plus volumineux avec la même taille visuelle.

### La désactivation de l'anticrénelage affecte‑t‑elle la lisibilité du texte ?

Pour la plupart des polices modernes, désactiver l'anticrénelage peut rendre le texte petit dentelé. Si vous avez besoin d'un texte net **et** de bords lisses, envisagez de rendre à une résolution plus élevée puis de réduire avec un algorithme de rééchantillonnage de haute qualité. Cette astuce préserve la lisibilité tout en vous donnant le contrôle sur la grille de pixels finale.

### Cette approche est‑elle multiplateforme ?

Oui. Aspose.HTML est purement .NET et fonctionne sous Windows, Linux et macOS. La seule nuance spécifique à la plateforme est la disponibilité des polices système ; vous devrez peut‑être intégrer des polices personnalisées dans votre HTML ou les installer sur la machine cible.

## Exemple complet fonctionnel

Ci‑dessus se trouve le programme complet et autonome que vous pouvez copier‑coller dans une application console. Il inclut toutes les instructions `using` nécessaires, la gestion des erreurs et des commentaires.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // -------------------------------------------------
                // 1️⃣ Define input and output paths
                // -------------------------------------------------
                string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
                string outputPng = Path.Combine(Environment.CurrentDirectory, "output.png");

                // -------------------------------------------------
                // 2️⃣ Load the HTML document
                // -------------------------------------------------
                // BaseUri ensures relative resources resolve correctly
                var htmlDoc = new HTMLDocument(inputHtml, new Uri("file:///" + Path.GetDirectoryName(inputHtml) + "/"));

                // -------------------------------------------------
                // 3️⃣ Configure rendering options – disable antialiasing
                // -------------------------------------------------
                var saveOptions = new ImageSaveOptions(SaveFormat.Png)
                {
                    ImageRenderingOptions = new ImageRenderingOptions
                    {
                        UseAntialiasing = false,   // 👈 The key line for pixel‑perfect output
                        // Optional: set resolution or size here
                    }
                };

                // -------------------------------------------------
                // 4️⃣ Render and save the PNG
                // -------------------------------------------------
                htmlDoc.Save(outputPng, saveOptions);
                Console.WriteLine($"✅ PNG created at: {outputPng}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Exécutez le programme, et vous verrez **output.png** apparaître à côté de l'exécutable. Ouvrez‑le — pas de bords flous, juste une copie raster pure de votre HTML.

## Conclusion

Nous avons couvert **comment désactiver l'anticrénelage** lorsque vous **convertissez du HTML en PNG**, parcouru chaque étape de configuration, et fourni un exemple complet et exécutable qui **rend le HTML en image**, **enregistre le HTML en PNG**, et vous permet de **créer des PNG à partir de HTML** avec une fidélité pixel‑parfaite.

Si vous souhaitez aller plus loin, essayez d'expérimenter avec différents formats d'image (JPEG, BMP), explorez les astuces de mise à l'échelle vecteur‑vers‑raster, ou intégrez cet extrait dans un service web qui génère des vignettes à la volée. Les mêmes principes s'appliquent que vous construisiez un générateur de documentation, un outil de tests de régression visuelle, ou un exportateur de graphiques dynamiques.

Vous avez d'autres questions sur les particularités du rendu ou les fonctionnalités d'Aspose.HTML ? Laissez un commentaire ci‑dessus, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}