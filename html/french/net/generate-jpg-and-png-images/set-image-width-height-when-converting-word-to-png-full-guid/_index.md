---
category: general
date: 2026-05-22
description: Définissez la largeur et la hauteur de l'image lors de la conversion
  d'un document Word en PNG. Apprenez à exporter un docx en image avec un rendu haute
  qualité grâce à un tutoriel étape par étape.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: fr
og_description: Définissez la largeur et la hauteur de l'image lors de la conversion
  d'un document Word en PNG. Ce tutoriel montre comment exporter un docx en image
  avec des paramètres haute qualité.
og_title: Définir la largeur et la hauteur de l'image lors de la conversion de Word
  en PNG – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Définir la largeur et la hauteur de l'image lors de la conversion de Word en
  PNG – Guide complet
url: /fr/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la largeur et la hauteur d'une image lors de la conversion de Word en PNG – Guide complet

Vous êtes-vous déjà demandé comment **définir la largeur et la hauteur d'une image** tout en **convertissant Word en PNG** ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsque l'exportation par défaut donne une image floue ou aux mauvaises dimensions, puis ils passent des heures à chercher une solution qui fonctionne réellement.

Dans ce tutoriel, nous parcourrons une solution propre, de bout en bout, qui montre **comment rendre des documents Word** en images PNG, vous permettant de **sauvegarder un docx en PNG** avec un contrôle précis de la largeur‑hauteur et un antialiasing de haute qualité. À la fin, vous disposerez d’un extrait de code prêt à l’emploi, d’une compréhension solide des options de l’API et de quelques astuces professionnelles pour éviter les pièges courants.

## Ce que vous allez apprendre

- Charger un fichier `.docx` avec Aspose.Words for .NET.  
- **Définir la largeur et la hauteur d’une image** avec `ImageRenderingOptions`.  
- **Exporter un docx en image** (PNG) avec l’antialiasing activé.  
- Comment **convertir Word en PNG** pour une page unique ou l’ensemble du document.  
- Astuces pour gérer les documents volumineux, les considérations DPI et les chemins de système de fichiers.

Aucun outil externe, aucune gymnastique de ligne de commande désordonnée—juste du code C# pur que vous pouvez intégrer dans n’importe quel projet .NET.

---

## Prérequis

Avant de commencer, assurez‑vous de disposer de ce qui suit :

| Prérequis | Pourquoi c’est important |
|-----------|---------------------------|
| **.NET 6.0+** (ou .NET Framework 4.7.2) | Aspose.Words prend en charge les deux, mais les runtimes plus récents offrent de meilleures performances. |
| **Aspose.Words for .NET** package NuGet (`Install-Package Aspose.Words`) | Fournit la classe `Document` et le moteur de rendu. |
| Un **document Word** (`.docx`) que vous souhaitez transformer en PNG. | La source que vous allez convertir. |
| Connaissances de base en C# – vous comprendrez les instructions `using` et l’initialisation d’objets. | Facilite la courbe d’apprentissage. |

Si le package NuGet vous manque, exécutez ceci dans la console du gestionnaire de packages :

```powershell
Install-Package Aspose.Words
```

C’est tout—une fois le package installé, vous êtes prêt à coder.

---

## Étape 1 : Charger le document source

La toute première chose à faire est d’indiquer à la bibliothèque le fichier Word que vous voulez transformer.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Pourquoi c’est important :** La classe `Document` lit l’ensemble du package Word en mémoire, vous donnant accès aux pages, aux styles et à tout le reste. Si le chemin est incorrect, vous obtiendrez une `FileNotFoundException`, alors vérifiez que le fichier existe et que le chemin utilise des antislashs échappés (`\\`) ou une chaîne verbatim (`@`).  

> **Astuce pro :** Enveloppez l’appel de chargement dans un bloc `try/catch` si le fichier peut être absent à l’exécution.

---

## Étape 2 : Configurer les options de rendu d’image (Définir la largeur et la hauteur)

Voici le cœur du tutoriel : **comment définir la largeur et la hauteur d’une image** afin que le PNG résultant ne soit ni étiré ni pixelisé. La classe `ImageRenderingOptions` vous offre un contrôle granulaire sur les dimensions, le DPI et le lissage.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Explication des propriétés clés :**

- `Width` et `Height` – Ce sont les dimensions exactes en pixels que vous désirez. En les définissant, vous **définissez la largeur et la hauteur de l’image** directement, en écrasant la taille de page par défaut.  
- `UseAntialiasing` – Active le lissage de haute qualité pour le texte et les graphiques vectoriels, ce qui est crucial lorsque vous **convertissez Word en PNG** et que vous voulez des bords nets.  
- `Resolution` – Un DPI plus élevé produit plus de détails, surtout pour les mises en page complexes. Gardez un œil sur la consommation mémoire ; une image à 300 DPI peut être volumineuse.

> **Pourquoi ne pas se contenter de la taille par défaut ?** Le réglage par défaut utilise les dimensions physiques de la page (par ex., A4 à 96 DPI). Cela produit souvent une image de 794 × 1123 pixels—suffisant dans certains cas, mais pas quand vous avez besoin d’une vignette UI ou d’un aperçu à taille fixe.

---

## Étape 3 : Rendre et sauvegarder en PNG (Exporter le docx en image)

Avec le document chargé et les options configurées, vous pouvez enfin **exporter le docx en image**. La méthode `RenderToImage` fait le gros du travail.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Si vous souhaitez rendre **l’ensemble du document** (toutes les pages) en fichiers PNG séparés, parcourez la collection de pages :

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Que se passe‑t‑il en coulisses ?** Le moteur rasterise chaque page en utilisant les dimensions que vous avez fournies, applique l’antialiasing et écrit un flux d’octets PNG sur le disque. Comme le PNG est sans perte, vous conservez toute la fidélité de la mise en page Word d’origine.

**Résultat attendu :** Un PNG net exactement de 1024 × 768 pixels (ou la taille que vous avez définie). Ouvrez‑le avec n’importe quel visualiseur d’images et vous verrez le contenu Word rendu exactement comme dans le document original, mais désormais sous forme de bitmap.

---

## Astuces avancées & variantes

### 1. Conserver les arrière‑plans transparents

Si votre document Word contient des formes avec des arrière‑plans transparents et que vous voulez garder cette transparence, définissez `BackgroundColor` sur `Color.Transparent` :

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Rendre uniquement une plage spécifique

Parfois vous n’avez besoin que d’un paragraphe ou d’un tableau, pas de toute la page. Utilisez `DocumentVisitor` pour extraire le nœud et le rendre séparément. C’est un scénario plus avancé, mais cela montre **comment rendre du contenu Word** de façon granulaire.

### 3. Ajuster le DPI dynamiquement

Si vous avez besoin d’un DPI différent par page (par ex., haute résolution pour la page de garde), modifiez `Resolution` à l’intérieur de la boucle :

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Traitement par lots

Lorsque vous convertissez des dizaines de documents, encapsulez le flux complet dans une méthode et réutilisez la même instance de `ImageRenderingOptions`. Réutiliser l’objet d’options réduit la surcharge d’allocation.

---

## Problèmes courants & comment les éviter

| Symptom | Cause probable | Solution |
|---------|----------------|----------|
| Le PNG est flou malgré un DPI élevé | `UseAntialiasing` laissé à `false` | Définissez `UseAntialiasing = true`. |
| La taille de sortie ne correspond pas à `Width`/`Height` | DPI non pris en compte | Multipliez la taille désirée par `Resolution / 96` ou ajustez `Resolution`. |
| Exception Out‑of‑memory sur de gros documents | Rendu du document complet à 300 DPI | Rendre une page à la fois, libérer chaque image après sauvegarde. |
| Le PNG montre un fond blanc sur des images transparentes | `BackgroundColor` non défini | Définissez `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Exemple complet fonctionnel

Voici un programme autonome que vous pouvez copier‑coller dans une application console. Il montre **convertir Word en PNG**, **sauvegarder le docx en PNG**, et bien sûr **définir la largeur et la hauteur d’une image**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Exécution :** Compilez le projet, placez un `input.docx` valide au chemin indiqué, puis lancez l’application. Vous devriez obtenir un `output.png` exactement **1024 × 768** pixels, rendu avec des bords lisses.


## Tutoriels associés

- [Comment activer l’antialiasing lors de la conversion de DOCX en PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convertir docx en png – créer une archive zip c# tutoriel](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Comment utiliser Aspose pour rendre du HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}