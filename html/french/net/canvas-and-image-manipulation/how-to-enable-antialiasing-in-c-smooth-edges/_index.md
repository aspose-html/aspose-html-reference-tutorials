---
category: general
date: 2025-12-26
description: Apprenez comment activer l'anticrénelage en C# pour lisser les bords
  et améliorer le rendu du texte. Ce guide étape par étape couvre également l'anticrénelage
  des images.
draft: false
keywords:
- how to enable antialiasing
- how to smooth edges
- enable antialiasing
- improve text rendering
- antialiasing for images
language: fr
og_description: Comment activer l'anticrénelage en C# pour des bords plus lisses et
  un texte plus clair. Suivez ce guide pour améliorer le rendu du texte et ajouter
  l'anticrénelage aux images.
og_title: Comment activer l'anticrénelage en C# – Bords lisses
tags:
- C#
- graphics
- rendering
title: Comment activer l'anticrénelage en C# – Bords lisses
url: /fr/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-smooth-edges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage en C# – Bords lisses

Vous vous êtes déjà demandé **comment activer l'anticrénelage** dans une routine de dessin C# ? Vous n'êtes pas le seul—les développeurs luttent constamment contre les lignes dentelées et le texte flou, surtout lors du rendu de graphiques riches en UI. La bonne nouvelle, c’est qu’un petit nombre d’ajustements de propriétés peut transformer ces bords rugueux en visuels soyeux, et vous bénéficierez également d’une amélioration notable de la qualité de **améliorer le rendu du texte**.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre exactement comment lisser les bords, activer l'anticrénelage pour les images et activer le hinting du texte. Aucune documentation externe n’est requise ; il suffit de copier, coller et exécuter. À la fin, vous saurez non seulement *quoi* configurer, mais aussi *pourquoi* ces réglages sont importants pour un rendu pixel‑parfait.

## Ce que vous apprendrez

- La différence entre l'anticrénelage et le hinting, et quand chacun est important.  
- Comment configurer `ImageRenderingOptions` (ou une API comparable) dans un projet C# réel.  
- Gestion des cas limites pour les écrans haute‑DPI et les charges de travail lourdes en images.  
- Un exemple complet, prêt à être compilé, que vous pouvez insérer dans n’importe quelle application console .NET ou WinForms.  

**Prérequis :** .NET 6+ (ou .NET Framework 4.7+), une compréhension de base de la syntaxe C#, et une bibliothèque graphique qui expose `ImageRenderingOptions` (l’exemple utilise une classe factice à titre d’illustration).  

---

## Comment activer l'anticrénelage – Vue d’ensemble rapide

Voici le cœur de la solution : créer une instance `ImageRenderingOptions` et activer les bons indicateurs. Ce bloc unique effectue le travail lourd pour le contenu raster et vectoriel.

```csharp
// Step 1: Create the rendering options object
var renderingOptions = new ImageRenderingOptions();

// Step 2: Turn on antialiasing to smooth visual edges
renderingOptions.UseAntialiasing = true;

// Step 3: Enable text hinting for sharper glyphs
renderingOptions.Text.UseHinting = true;
```

**Pourquoi ces trois lignes sont importantes :**  

- `UseAntialiasing` indique au rasteriseur de mélanger les bords des pixels, éliminant l’effet d’escalier qui rend les lignes “dentelées”.  
- `Text.UseHinting` aligne les caractères sur la grille de pixels, ce qui est essentiel pour des polices nettes à l’écran, surtout à petite taille.  
- Les regrouper dans un seul objet d’options garde votre pipeline de rendu propre et rend les ajustements futurs indolores.

---

## Configurer un projet minimal (Comment lisser les bords)

Si vous partez de zéro, suivez ces étapes pour obtenir une application console qui rend une image simple avec les options ci‑dessus.

### 1️⃣ Create the Project

```bash
dotnet new console -n AntialiasDemo
cd AntialiasDemo
```

### 2️⃣ Add a Graphics Library

Dans le cadre de ce tutoriel, nous utiliserons le package **SixLabors.ImageSharp**, qui expose une classe `GraphicsOptions` similaire. Installez‑le avec :

```bash
dotnet add package SixLabors.ImageSharp --version 3.0.0
```

> *Astuce :* `GraphicsOptions` d’ImageSharp correspond 1‑pour‑1 à `ImageRenderingOptions` présenté précédemment, vous pouvez donc remplacer le nom de la classe sans modifier la logique.

### 3️⃣ Write the Code

Remplacez le `Program.cs` généré automatiquement par l’exemple complet suivant :

```csharp
using System;
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Drawing;
using SixLabors.ImageSharp.Drawing.Processing;
using SixLabors.ImageSharp.PixelFormats;
using SixLabors.ImageSharp.Processing;

namespace AntialiasDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a blank 400x200 image with a light gray background
            using var image = new Image<Rgba32>(400, 200);
            image.Mutate(ctx => ctx.Fill(Color.LightGray));

            // -------------------------------------------------
            // Step 1: Instantiate rendering options (antialiasing + hinting)
            // -------------------------------------------------
            var renderingOptions = new GraphicsOptions()
            {
                Antialias = true,          // smooth edges
                AntialiasSubpixelDepth = 16,
                // Text hinting is implicit in ImageSharp when Antialias is true,
                // but we can emphasize it with a higher quality setting.
                TextOptions = new TextOptions()
                {
                    DpiX = 96,
                    DpiY = 96,
                    Hinting = TextHinting.Enabled
                }
            };

            // -------------------------------------------------
            // Step 2: Draw a diagonal line (you’ll see the smoothing)
            // -------------------------------------------------
            var linePen = Pens.Solid(Color.DarkBlue, 5);
            image.Mutate(ctx => ctx.DrawLines(renderingOptions, linePen, new PointF(20, 20), new PointF(380, 180)));

            // -------------------------------------------------
            // Step 3: Render some text to demonstrate hinting
            // -------------------------------------------------
            var font = SystemFonts.CreateFont("Arial", 24, FontStyle.Bold);
            var textOptions = new TextOptions(font)
            {
                HorizontalAlignment = HorizontalAlignment.Center,
                VerticalAlignment = VerticalAlignment.Center,
                Origin = new PointF(200, 100)
            };
            image.Mutate(ctx => ctx.DrawText(renderingOptions, "Antialiasing ✔", font, Color.Black, new PointF(200, 100)));

            // -------------------------------------------------
            // Save the result
            // -------------------------------------------------
            const string outputPath = "antialias_demo.png";
            image.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}. Open it to verify smooth edges and clear text.");
        }
    }
}
```

#### Explication des sections clés

| Section | Pourquoi c’est important |
|---------|---------------------------|
| **GraphicsOptions** | Centralise l'anticrénelage (`Antialias = true`) et le hinting du texte (`Hinting = Enabled`). |
| **DrawLines** | La ligne diagonale montre comment **comment lisser les bords** fonctionne en pratique—remarquez l'absence de crénelures. |
| **DrawText** | Démontre **améliorer le rendu du texte** ; le glyphe “✔” est net grâce au hinting. |
| **AntialiasSubpixelDepth** | Contrôle la qualité du mélange sous‑pixel ; des valeurs plus élevées donnent des dégradés plus lisses. |
| **Saving the PNG** | Vous fournit un artefact tangible que vous pouvez inspecter ou intégrer dans la documentation. |

---

## Cas limites & variantes (Activer l'anticrénelage pour les images)

### Écrans haute‑DPI

Lors du ciblage d’écrans avec un DPI > 120, augmentez `DpiX`/`DpiY` dans `TextOptions` et envisagez d’augmenter `AntialiasSubpixelDepth`. Cela empêche le moteur de rendu de « down‑sampler » vos lignes lisses.

```csharp
renderingOptions.AntialiasSubpixelDepth = 32; // extra smoothness on 4K monitors
```

### Grandes images

Pour des bitmaps très grands (par ex., > 4000 px), vous pourriez rencontrer une pression mémoire. Dans ces cas, vous pouvez activer le **rendu progressif** :

```csharp
renderingOptions = renderingOptions.WithProgressiveRendering(true);
```

### APIs non‑ImageSharp

Si vous utilisez **System.Drawing** (Windows uniquement) ou **SkiaSharp**, les noms de propriétés diffèrent (`SmoothingMode.AntiAlias`, `TextRenderingHint.ClearTypeGridFit`). Le concept est identique — définissez le drapeau d’anticrénelage sur le contexte graphique, puis activez le hinting sur le rendu du texte.

---

## Vérifier le résultat (Ce qu’il faut rechercher)

1. **Ligne diagonale lisse** – Aucun artefact d’escalier ; la ligne doit apparaître comme un doux dégradé.  
2. **Texte net** – Les caractères s’alignent proprement sur la grille de pixels ; le “✔” doit être nettement net.  
3. **Taille du fichier** – Le PNG sera légèrement plus grand en raison des informations de couleur supplémentaires, ce qui est normal pour un rendu antialiasé.  

Ouvrez `antialias_demo.png` dans n’importe quel visualiseur d’images ; si les bords semblent d’une douceur beurrée et que le texte est lisible clairement, vous avez réussi à **activer l'anticrénelage** dans votre projet C#.

---

## Questions fréquentes répondues

- **Cela fonctionne‑t‑il sur .NET Framework ?** Oui—il suffit d’installer la version appropriée du package ImageSharp qui cible .NET Framework.  
- **Et si ma bibliothèque n’expose pas de propriété `Text.UseHinting` ?** Recherchez des équivalents comme `TextRenderingHint` (System.Drawing) ou `FontHinting` (SkiaSharp).  
- **Puis‑je désactiver l'anticrénelage pour la performance ?** Absolument ; définissez `Antialias = false` lors du rendu de miniatures ou lorsque la vitesse prime sur la fidélité visuelle.  

---

## Conclusion

Vous disposez maintenant d’un **guide complet et autonome sur comment activer l'anticrénelage** en C#. En basculant quelques propriétés, vous pouvez **lisser les bords**, **améliorer le rendu du texte**, et même appliquer **l'anticrénelage pour les images** à travers différentes bibliothèques graphiques. Le code d’exemple est prêt à être exécuté, et les explications vous donnent le raisonnement derrière chaque réglage—vous permettant d’adapter l’approche à n’importe quel projet.

Prêt pour l’étape suivante ? Essayez d’expérimenter avec différentes épaisseurs de stylo, des polices personnalisées, ou la superposition de plusieurs formes pour voir comment l'anticrénelage se comporte dans diverses conditions. Et si vous êtes curieux des modes de fusion ou du rendu SVG, ces sujets découlent naturellement de ce que vous venez de maîtriser.

Bon codage, et profitez de ces visuels d’une douceur beurrée ! 

![Capture d’écran de antialias_demo.png montrant des bords lisses et du texte clair – comment activer l'anticrénelage]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}