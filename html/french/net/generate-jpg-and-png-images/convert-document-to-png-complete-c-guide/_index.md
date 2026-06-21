---
category: general
date: 2026-02-19
description: Apprenez à convertir un document en PNG, à définir les dimensions de
  l'image et à ajuster la qualité de l'image en C# avec un exemple simple étape par
  étape.
draft: false
keywords:
- convert document to png
- set image dimensions
- save rendered image
- adjust image quality
- set custom image size
language: fr
og_description: Convertir un document en PNG en C# en définissant les dimensions de
  l'image, en ajustant la qualité et en enregistrant l'image rendue — le tout dans
  un seul tutoriel.
og_title: Convertir un document en PNG – Guide complet C#
tags:
- C#
- Image Rendering
- Document Processing
title: Convertir le document en PNG – Guide complet C#
url: /fr/net/generate-jpg-and-png-images/convert-document-to-png-complete-c-guide/
---

CODE_BLOCK_0}} etc. Keep them.

Translate headings, paragraphs, list items, table contents, blockquotes, etc.

Be careful with markdown formatting.

Let's produce the translated version.

Check for any URLs: none present except maybe in code? No.

Make sure to keep the shortcodes exactly as they are.

Let's translate:

Title: "# Convert Document to PNG – Complete C# Guide" => "# Convertir un document en PNG – Guide complet C#"

Similarly other headings.

Translate sentences.

Also note "RTL formatting if needed" but French is LTR, ignore.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir un document en PNG – Guide complet C#

Vous avez déjà eu besoin de **convertir un document en PNG** sans savoir quels réglages vous donnent un rendu net et correctement dimensionné ? Vous n'êtes pas seul. Dans de nombreux projets—rapports, vignettes ou aperçus web—obtenir les bonnes dimensions et la bonne qualité d'image est crucial, et le code ci‑dessous montre exactement comment le faire.

Dans ce tutoriel, nous allons parcourir le chargement d’un document, la configuration des **dimensions de l’image**, le réglage de la **qualité de l’image**, puis enfin **enregistrer l’image rendue** sur le disque. À la fin, vous verrez également comment **définir une taille d’image personnalisée** pour n’importe quel scénario.

## Ce que vous allez apprendre

- Comment charger un document avec une bibliothèque de rendu .NET populaire (Aspose.Words for .NET est utilisé, mais les concepts s’appliquent à des API similaires).  
- Le processus pas‑à‑pas pour **convertir un document en PNG** tout en contrôlant la largeur, la hauteur et l’antialiasing.  
- Les façons de **définir les dimensions de l’image** et **d’ajuster la qualité de l’image** pour des applications où les performances sont critiques.  
- Comment **enregistrer l’image rendue** en toute sécurité et gérer les documents multi‑pages.  
- Des astuces pour les cas particuliers, comme le rendu d’une page spécifique ou la gestion de gros fichiers.

> **Prérequis :** SDK .NET 6+ , Visual Studio 2022 (ou tout autre IDE), et le package NuGet Aspose.Words for .NET. Si vous utilisez un moteur de rendu différent, remplacez simplement la classe `ImageRenderingOptions` par l’équivalent de votre bibliothèque.

---

## Étape 1 – Convertir un document en PNG avec la taille souhaitée

La première chose à faire est de créer une instance `ImageRenderingOptions` et d’indiquer au moteur de rendu la taille exacte du PNG. C’est ici que **définir les dimensions de l’image** entre en jeu.

```csharp
using System;
using System.Drawing.Imaging;               // For ImageFormat
using Aspose.Words;                         // Core document API
using Aspose.Words.Rendering;               // Image rendering helpers

class Program
{
    static void Main()
    {
        // Load the source document (DOCX, PDF, etc.)
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Create an ImageRenderingOptions instance
        ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions();

        // Configure the image size, format, and quality
        imageRenderOptions.Width = 1024;                     // width in pixels
        imageRenderOptions.Height = 768;                     // height in pixels
        imageRenderOptions.OutputFormat = ImageFormat.Png;  // PNG output
        imageRenderOptions.UseAntialiasing = true;           // smoother edges

        // Render the first page to a PNG file
        document.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);
    }
}
```

**Pourquoi c’est important :**  
- **Width & Height** vous permettent de **définir une taille d’image personnalisée** sans devoir redimensionner ensuite, ce qui préserve la netteté.  
- **UseAntialiasing** est le drapeau clé pour **ajuster la qualité de l’image** — activez‑le pour des bords plus lisses, désactivez‑le pour un rendu plus rapide.  
- Rendre directement en PNG garantit une profondeur de couleur sans perte, idéale pour les vignettes UI.

> **Astuce pro :** Si vous avez besoin d’un DPI (dots per inch) plus élevé, définissez `imageRenderOptions.Resolution = 300;` avant le rendu. Un DPI plus haut améliore la qualité d’impression mais augmente la taille du fichier.

## Étape 2 – Définir les dimensions de l’image et ajuster la qualité

Parfois, la taille de page par défaut ne convient pas. Vous pouvez vouloir une vignette paysage pour une galerie web ou une icône carrée pour une application mobile. C’est là que vous **définissez les dimensions de l’image** manuellement.

```csharp
// Example: Create a square 500×500 PNG with high quality
imageRenderOptions.Width = 500;
imageRenderOptions.Height = 500;
imageRenderOptions.UseAntialiasing = true;   // high‑quality rendering
imageRenderOptions.OutputFormat = ImageFormat.Png;
```

**Que se passe‑t‑il en coulisses ?**  
Le moteur de rendu met à l’échelle les données vectorielles de la page originale selon la grille de pixels que vous spécifiez. Comme le PNG est sans perte, le redimensionnement n’introduira pas d’artefacts de compression, mais le drapeau **ajuster la qualité de l’image** (antialiasing) détermine la douceur des bords. Désactiver l’antialiasing peut accélérer le traitement par lots lorsque vous générez des centaines de vignettes.

### Quand ajuster la qualité

| Scénario | Réglage recommandé |
|----------|---------------------|
| Aperçu en temps réel (ex. UI) | `UseAntialiasing = false` |
| Assets finaux pour le marketing | `UseAntialiasing = true` |
| Conversion par lots importante | Expérimentez avec `Resolution` et `UseAntialiasing` pour équilibrer vitesse et clarté |

## Étape 3 – Enregistrer l’image rendue sur le disque

Une fois les options configurées, la dernière étape consiste à **enregistrer l’image rendue**. La méthode `RenderToImage` crée le fichier pour vous, mais vous devez tout de même vérifier le chemin de sortie et gérer les éventuelles erreurs d’E/S.

```csharp
try
{
    string outputPath = "YOUR_DIRECTORY/output.png";
    document.RenderToImage(outputPath, imageRenderOptions);
    Console.WriteLine($"✅ Successfully saved PNG to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Failed to save PNG: {ex.Message}");
}
```

**Pourquoi l’envelopper dans un try/catch ?**  
Les permissions de fichier, l’espace disque ou un chemin invalide peuvent générer des exceptions. En les interceptant, vous évitez le plantage du service — particulièrement important dans les API web qui convertissent des documents à la volée.

### Vérifier le résultat

Ouvrez le fichier généré avec n’importe quel visualiseur d’images. Vous devez voir un PNG dont la largeur et la hauteur correspondent à celles que vous avez définies, avec des bords lisses si l’antialiasing était activé. Si les dimensions semblent incorrectes, revérifiez que vous n’avez pas inversé `Width` et `Height`.

## Optionnel – Définir une taille d’image personnalisée pour différents scénarios

Parfois, vous avez besoin d’une série d’images à différentes résolutions (vignettes, moyen, grand). Au lieu de coder en dur chaque taille, parcourez un tableau d’objets de dimensions.

```csharp
var sizes = new (int width, int height)[]
{
    (200, 200),   // tiny thumbnail
    (800, 600),   // medium preview
    (1920, 1080)  // full‑HD preview
};

foreach (var (w, h) in sizes)
{
    imageRenderOptions.Width = w;
    imageRenderOptions.Height = h;
    string outFile = $"YOUR_DIRECTORY/output_{w}x{h}.png";
    document.RenderToImage(outFile, imageRenderOptions);
    Console.WriteLine($"Saved {outFile}");
}
```

**Points clés à retenir :**  

- Ce modèle vous permet de **définir une taille d’image personnalisée** à la volée, tout en gardant votre code DRY.  
- Vous pouvez également varier `UseAntialiasing` selon la taille — haute qualité pour les grandes images, rendu rapide pour les petites vignettes.  
- N’oubliez pas de libérer l’objet `Document` après utilisation (`document.Dispose();`) pour libérer les ressources natives.

---

## Gestion des documents multi‑pages

L’extrait ci‑dessus ne rend que la première page. Si votre source comporte plusieurs pages et que vous avez besoin d’un PNG pour chaque page, itérez sur `document.PageCount`.

```csharp
for (int pageIndex = 0; pageIndex < document.PageCount; pageIndex++)
{
    // Adjust options if you want per‑page customizations
    imageRenderOptions.PageIndex = pageIndex; // tells the renderer which page

    string outPath = $"YOUR_DIRECTORY/page_{pageIndex + 1}.png";
    document.RenderToImage(outPath, imageRenderOptions);
    Console.WriteLine($"Page {pageIndex + 1} saved as PNG.");
}
```

**Pourquoi utiliser `PageIndex` ?**  
Il indique au moteur de rendu quelle page peindre. Sans cela, la valeur par défaut est la page 0 (la première). Cette approche garantit que chaque page obtient son propre PNG, préservant le flux **convertir un document en png** pour les PDF, DOCX ou ODT multi‑pages.

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans une nouvelle application console. Il couvre le chargement, la configuration, le rendu, la gestion des erreurs et le support multi‑pages—le tout en un seul endroit.

```csharp
using System;
using System.Drawing.Imaging;
using Aspose.Words;
using Aspose.Words.Rendering;

class ConvertToPngDemo
{
    static void Main()
    {
        // 1️⃣ Load the source document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // 2️⃣ Prepare rendering options (set image dimensions, quality, format)
        ImageRenderingOptions opts = new ImageRenderingOptions
        {
            Width = 1024,
            Height = 768,
            OutputFormat = ImageFormat.Png,
            UseAntialiasing = true,
            Resolution = 150 // optional DPI tweak
        };

        // 3️⃣ Render each page to its own PNG file
        for (int i = 0; i < doc.PageCount; i++)
        {
            opts.PageIndex = i; // select page
            string outPath = $"YOUR_DIRECTORY/output_page_{i + 1}.png";

            try
            {
                doc.RenderToImage(outPath, opts);
                Console.WriteLine($"✅ Page {i + 1} saved → {outPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error on page {i + 1}: {ex.Message}");
            }
        }

        // Clean up
        doc.Dispose();
    }
}
```

**Résultat attendu :**  
Une série de fichiers PNG nommés `output_page_1.png`, `output_page_2.png`, … chacun de taille 1024 × 768 pixels, avec antialiasing appliqué. Ouvrez n’importe quel fichier ; l’image doit être nette, correctement proportionnée et prête pour le web ou le bureau.

---

## Conclusion

Vous savez maintenant comment **convertir un document en PNG** en C# tout en **définissant précisément les dimensions de l’image**, **ajustant la qualité de l’image**, et **enregistrant l’image rendue** de façon efficace. Que vous génériez une vignette unique ou une galerie complète, le modèle présenté ici vous donne un contrôle total sur le résultat.

Et après ? Essayez de remplacer `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}