---
category: general
date: 2026-11-20
description: Comment activer l'anticrénelage dans les graphiques C# et définir la
  taille de la police, le style de la police de façon programmatique avec un exemple
  complet et exécutable utilisant ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: fr
lastmod: 2026-11-20
og_description: Comment activer l'anticrénelage dans les graphiques C#, définir la
  taille de la police et le style de la police de manière programmatique en utilisant
  ImageRenderingOptions – code complet et explication.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: Comment activer l'anticrénelage et définir la taille et le style de police
  par programmation en C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: Comment activer l'anticrénelage et définir la taille et le style de police
  de façon programmatique en C#
url: /fr/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage et définir la taille et le style de police de manière programmatique en C#

Activer l'anticrénelage dans les graphiques C# est une exigence fréquente lorsque vous avez besoin de bords lisses sur des formes ou du texte. Ce tutoriel vous montre comment activer l'anticrénelage, définir la taille de police et appliquer le style de police de façon programmatique à l'aide de la classe **ImageRenderingOptions**. À la fin du guide, vous disposerez d’une application console autonome qui rend du texte net et stylisé dans un fichier image.

Vous apprendrez à configurer le pipeline de rendu, choisir la bonne famille de police, ajuster la taille de police et appliquer les styles gras ou italique sans quitter votre code. La seule condition préalable est un SDK .NET récent et le package NuGet Aspose.Imaging, que l’exemple installe automatiquement.

## Prérequis

- SDK .NET 6.0 ou ultérieur (téléchargez-le depuis https://dotnet.microsoft.com/)
- Visual Studio 2022 ou tout éditeur supportant les projets .NET
- **Aspose.Imaging** package NuGet (la bibliothèque qui fournit `ImageRenderingOptions`)

Vous pouvez ajouter le package avec la commande suivante :

```bash
dotnet add package Aspose.Imaging
```

## Comment activer l'anticrénelage avec ImageRenderingOptions

`ImageRenderingOptions` est l’objet central qui contrôle la façon dont Aspose.Imaging dessine les graphiques. Définir sa propriété `UseAntialiasing` indique au rasteriseur de lisser les bords, ce qui élimine l’effet d’escalier qui apparaît lorsque l’anticrénelage est désactivé.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Activer l'anticrénelage est essentiel pour des éléments d’interface utilisateur de haute qualité, le rendu de graphiques et toute situation où la fidélité visuelle compte.

## Définir la taille de police de façon programmatique

La taille de police détermine l’envergure des glyphes dans le bitmap final. Vous pouvez la modifier en construisant un objet `Font` avec la taille en points souhaitée. L’exemple ci‑dessous fixe la taille à **24 pt**, une taille courante pour des titres lisibles.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

Vous pouvez remplacer `24` par n’importe quel entier ou nombre à virgule flottante pour répondre à vos exigences de mise en page. La classe `Font` accepte également un paramètre `GraphicsUnit` si vous avez besoin d’une dimension basée sur les pixels.

## Définir le style de police de façon programmatique

Appliquer les styles gras, italique ou souligné consiste à passer un drapeau `WebFontStyle` lors de la création du `Font`. L’énumération `WebFontStyle` combine plusieurs styles à l’aide d’une opération OU binaire.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

Si vous avez besoin d’un seul style, utilisez `WebFontStyle.Bold`, `WebFontStyle.Italic` ou `WebFontStyle.Underline`. Cette approche vous permet de **définir le style de police de façon programmatique** sans coder en dur des fichiers de police séparés.

## Exemple complet exécutable

Voici une application console complète qui réunit tous les éléments :

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Explication de chaque section

| Section | Pourquoi c’est important |
|---------|---------------------------|
| **Rendering options** | Activer `UseAntialiasing` garantit des bords lisses pour les formes vectorielles et le texte. |
| **TextOptions.UseHinting** | Le hinting améliore la lisibilité sur des rendus basse résolution en ajustant les contours des glyphes. |
| **Font construction** | Le constructeur `Font` combine **définir la taille de police** et **définir le style de police de façon programmatique** en un seul appel. |
| **Graphics object** | Passer `renderingOptions` à `Graphics` assure que chaque opération de dessin respecte l’anticrénelage et le hinting. |
| **DrawString** | Cette méthode rend le texte avec la police configurée, produisant le rendu final antialiasé. |
| **Saving** | Le format PNG préserve les données de pixels exactes sans artefacts de compression supplémentaires. |

#### Résultat attendu

L’exécution du programme crée **antialiased_text.png** qui ressemble à ceci :

![Exemple de texte antialiasé](https://example.com/antialiased_text.png "Texte antialiasé avec taille et style de police personnalisés – comment activer l'anticrénelage")

L’image montre du texte Arial gras‑italique net rendu en 24 pt avec des bords lisses, confirmant que **comment activer l'anticrénelage** a fonctionné comme prévu.

## Variations courantes et cas limites

- **Différentes familles de police** – Remplacez `"Arial"` par n’importe quel nom de police installé (par ex., `"Times New Roman"`). Si la police n’est pas disponible, Aspose.Imaging lève une `FontNotFoundException`.
- **Modification de la taille de police** – Ajustez le deuxième argument du constructeur `Font` à n’importe quelle valeur à virgule flottante. Des valeurs plus grandes augmentent la lisibilité mais peuvent nécessiter un bitmap plus grand.
- **Styles multiples** – Combinez `WebFontStyle.Underline` avec `Bold` et `Italic` à l’aide de l’opérateur `|` : `WebFontStyle.Bold | WebFontStyle.Underline`.
- **Rendu haute‑DPI** – Pour une sortie de type retina, augmentez les dimensions du bitmap (par ex., 1600 × 400) tout en conservant la même taille de police ; l’anticrénelage produira toujours des résultats lisses.
- **Désactiver l'anticrénelage** – Définissez `renderingOptions.UseAntialiasing = false;` pour comparer la différence visuelle. Le texte apparaîtra en escalier, ce qui est utile pour le débogage ou les tests de performance.

## Astuces professionnelles

- **Mettez en cache l’objet `Font`** si vous dessinez de nombreuses chaînes dans une boucle ; créer un nouveau `Font` à chaque itération ajoute une surcharge.
- **Utilisez `TextOptions.UseHinting` conjointement avec l'anticrénelage** pour le meilleur compromis entre netteté et douceur sur des images basse résolution.
- **Validez le fichier de sortie** en l’ouvrant dans un visualiseur d’images affichant les détails pixel par pixel (par ex., Photoshop ou GIMP). Cela vous aide à confirmer que l’anticrénelage a réellement été appliqué.

## Conclusion

Vous savez maintenant **comment activer l'anticrénelage** dans les graphiques C#, comment **définir la taille de police** et comment **définir le style de police de façon programmatique** à l’aide de `ImageRenderingOptions`. L’exemple complet démontre un flux de travail pratique que vous pouvez copier dans vos propres projets, que vous génériez des graphiques, créiez des miniatures d’interface ou produisiez des graphiques dynamiques pour des services web.

Ensuite, vous pourriez explorer **définir la couleur de police de façon programmatique**, ajouter des **dégradés de remplissage**, ou rendre des **formes vectorielles** avec les mêmes paramètres d’anticrénelage. Tous ces sujets s’appuient sur les bases présentées ici, vous plaçant ainsi en excellente position pour créer des graphiques de haute qualité entièrement depuis le code. Bon rendu !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment activer l'anticrénelage lors du rendu HTML vers PNG en C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [Comment activer l'anticrénelage pour le rendu d'images HTML en C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [Comment activer l'anticrénelage dans la conversion Aspose HTML vers PDF (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}