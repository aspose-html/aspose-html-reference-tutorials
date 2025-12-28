---
category: general
date: 2025-12-27
description: Apprenez comment activer l'anticrénelage lors de la conversion de DOCX
  en PNG ou JPG. Ce guide étape par étape couvre également la conversion de DOCX en
  PNG et la conversion de DOCX en JPG.
draft: false
keywords:
- how to enable antialiasing
- convert docx to png
- convert docx to jpg
- how to convert docx
- how to render docx
language: fr
og_description: Comment activer l'anticrénelage lors de la conversion de fichiers
  DOCX en PNG ou JPG. Suivez ce guide complet pour obtenir un rendu fluide et de haute
  qualité.
og_title: Comment activer l'anticrénelage lors de la conversion de DOCX en PNG/JPG
tags:
- C#
- Document Rendering
- Image Processing
title: Comment activer l'anticrénelage lors de la conversion de DOCX en PNG/JPG
url: /fr/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage lors de la conversion de DOCX en PNG/JPG

Vous vous êtes déjà demandé **comment activer l'anticrénelage** pour que vos images DOCX converties soient nettes plutôt que dentelées ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent transformer un document Word en PNG ou JPG et se retrouvent avec des bords flous sur les lignes et le texte. Bonne nouvelle ? En quelques lignes de C#, vous pouvez transformer ce rendu approximatif en graphiques pixel‑parfait—sans aucun éditeur d'images tiers.

Dans ce tutoriel, nous parcourrons l’ensemble du processus de **convert docx to png** et **convert docx to jpg** en utilisant une bibliothèque de rendu moderne. Vous apprendrez non seulement *comment convertir docx* mais aussi *comment rendre docx* avec l'anticrénelage et le hinting activés, afin que chaque courbe et chaque caractère soient lisses. Aucune expérience préalable en programmation graphique n’est requise ; il vous suffit d’une configuration C# basique et d’un fichier DOCX que vous souhaitez transformer en image.

---

## Ce dont vous aurez besoin

- **.NET 6+** (ou .NET Framework 4.6+ si vous préférez le runtime classique)  
- Un fichier **DOCX** que vous souhaitez rendre (placez‑le dans un dossier nommé `input` pour la démonstration)  
- Le package NuGet **Aspose.Words for .NET** (ou toute bibliothèque exposant `Document`, `ImageRenderingOptions` et `ImageDevice`). Installez‑le avec :

```bash
dotnet add package Aspose.Words
```

C’est tout—aucun outil de traitement d’image supplémentaire n’est requis.

---

## Étape 1 : Charger le document DOCX (how to convert docx)

Tout d'abord, nous avons besoin d'un objet `Document` qui représente le fichier source. Considérez‑le comme la version numérique de votre fichier Word que la bibliothèque peut lire et manipuler.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

// Load the DOCX you want to render
Document sourceDoc = new Document("input/input.docx");
```

> **Pourquoi c’est important :** Charger le document est la base pour *how to render docx*. Si le fichier ne peut pas être lu, aucune des étapes suivantes ne fonctionnera, nous commençons donc ici.

---

## Étape 2 : Configurer les options de rendu d’image (enable antialiasing)

Voici la partie magique — activer l'anticrénelage et le hinting. L'anticrénelage adoucit les bords dentelés que l’on voit habituellement sur les lignes diagonales, tandis que le hinting améliore la clarté du petit texte.

```csharp
// Set up rendering options with antialiasing and hinting
ImageRenderingOptions renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,                // <‑‑ smooth graphics
    Text = { UseHinting = true }           // <‑‑ sharper text
};
```

> **Astuce :** Si vous avez besoin d’un gain de performance sur des documents volumineux, vous pouvez désactiver `UseAntialiasing`, mais la qualité visuelle diminuera de façon notable.

---

## Étape 3 : Choisir le format de sortie – PNG ou JPG (convert docx to png / convert docx to jpg)

La classe `ImageDevice` détermine où les pages rendues sont enregistrées. En échangeant `ImageSaveOptions`, vous pouvez produire soit du PNG (sans perte) soit du JPG (compressé). Ci-dessous, nous créons deux appareils distincts afin que vous puissiez générer les deux formats en une seule exécution.

```csharp
// PNG device – lossless, ideal for screenshots or further editing
ImageDevice pngDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = "output/page_{0}.png"   // {0} will be replaced by page number
    }
};

// JPG device – smaller file size, good for web thumbnails
ImageDevice jpgDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
    {
        OutputFileName = "output/page_{0}.jpg",
        JpegQuality = 90          // 0‑100, higher = better quality
    }
};
```

> **Pourquoi les deux ?** PNG préserve chaque pixel, ce qui est parfait lorsque vous avez besoin d’une fidélité exacte (par ex., impression). JPG, en revanche, compresse l’image, ce qui la rend plus rapide à charger sur un site web.

---

## Étape 4 : Rendre les pages du document en images (how to render docx)

Avec les appareils prêts, nous demandons au `Document` de rendre chaque page. La bibliothèque parcourra automatiquement toutes les pages et les enregistrera en utilisant le modèle de nommage que nous avons défini.

```csharp
// Render to PNG
sourceDoc.RenderTo(pngDevice);

// Render to JPG
sourceDoc.RenderTo(jpgDevice);
```

Après l’exécution du code, vous trouverez une série de fichiers comme `page_0.png`, `page_1.png`, … et `page_0.jpg`, `page_1.jpg` dans le dossier `output`. Chaque image aura l’anticrénelage appliqué, de sorte que les lignes sont lisses et le texte est cristallin.

---

## Étape 5 : Vérifier le résultat (expected output)

Ouvrez l’une des images générées. Vous devriez voir :

- **Des courbes lisses** sur les formes et les graphiques (pas d’artefacts en escalier).  
- **Un texte net et lisible** même à petite taille de police, grâce au hinting.  
- **Des couleurs cohérentes** entre PNG et JPG (bien que le JPG puisse montrer de légers artefacts de compression si vous réduisez la qualité).

Si vous remarquez un flou, vérifiez que `UseAntialiasing` est bien réglé sur `true` et que votre DOCX source ne contient pas d’images raster basse résolution.

---

## Questions fréquentes & cas particuliers

### Et si je n’ai besoin que d’une seule page ?

Vous pouvez rendre une page spécifique en utilisant la surcharge `PageInfo` :

```csharp
// Render only the first page to PNG
sourceDoc.RenderTo(pngDevice, new PageInfo(0));
```

### Puis‑je modifier le DPI (points par pouce) pour une sortie à plus haute résolution ?

Absolument. Ajustez la propriété `Resolution` sur `ImageRenderingOptions` :

```csharp
renderingOptions.Resolution = 300; // 300 DPI for print‑quality images
```

Un DPI plus élevé signifie des fichiers plus volumineux, mais l’effet d’anticrénelage devient encore plus perceptible.

### Comment gérer de gros fichiers DOCX sans épuiser la mémoire ?

Rendez les pages une par une et libérez l’appareil après chaque itération :

```csharp
for (int i = 0; i < sourceDoc.PageCount; i++)
{
    using var singlePageDevice = new ImageDevice(renderingOptions);
    singlePageDevice.SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = $"output/page_{i}.png"
    };
    sourceDoc.RenderTo(singlePageDevice, new PageInfo(i));
}
```

### Est‑il possible de convertir vers d’autres formats comme BMP ou TIFF ?

Oui—il suffit d’échanger `SaveFormat.Png` ou `SaveFormat.Jpeg` avec `SaveFormat.Bmp` ou `SaveFormat.Tiff`. Les mêmes paramètres d’anticrénelage sont conservés.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Ci‑dessous se trouve le programme complet que vous pouvez placer dans un nouveau projet console. Il inclut toutes les instructions `using`, la gestion des erreurs et des commentaires pour plus de clarté.

```csharp
// File: Program.cs
using System;
using System.IO;
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the DOCX document (how to convert docx)
        // -------------------------------------------------
        string inputPath = Path.Combine("input", "input.docx");
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❗ Input file not found: {inputPath}");
            return;
        }

        Document sourceDoc = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure rendering options (enable antialiasing)
        // -------------------------------------------------
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            Text = { UseHinting = true },
            Resolution = 150 // optional – 150 DPI is a good balance
        };

        // -------------------------------------------------
        // 3️⃣ Set up PNG and JPG devices (convert docx to png / convert docx to jpg)
        // -------------------------------------------------
        string outputFolder = "output";
        Directory.CreateDirectory(outputFolder);

        // PNG (lossless)
        ImageDevice pngDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Png)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.png")
            }
        };

        // JPG (compressed)
        ImageDevice jpgDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.jpg"),
                JpegQuality = 90
            }
        };

        // -------------------------------------------------
        // 4️⃣ Render all pages (how to render docx)
        // -------------------------------------------------
        try
        {
            sourceDoc.RenderTo(pngDevice);
            sourceDoc.RenderTo(jpgDevice);
            Console.WriteLine($"✅ Rendering complete! Check the '{outputFolder}' folder.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ An error occurred: {ex.Message}");
        }
    }
}
```

> **Résultat :** Après compilation (`dotnet run`), vous verrez une série de fichiers PNG et JPG dans le répertoire `output`, chacun avec l’anticrénelage appliqué.

---

## Conclusion

Nous avons couvert **comment activer l'anticrénelage** lors de la **conversion de DOCX en PNG ou JPG**, parcouru les étapes exactes pour **convert docx to png**, **convert docx to jpg**, et même abordé **how to render docx** pour des besoins personnalisés

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}