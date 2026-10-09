---
category: general
date: 2026-10-09
description: Créer une instance de ImageRenderingOptions pour activer l’anticrénelage
  et améliorer la qualité du rendu graphique dans les applications .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: fr
lastmod: 2026-10-09
og_description: Créez une instance d'ImageRenderingOptions pour activer l'anticrénelage
  et obtenir un rendu graphique plus fluide dans .NET. Suivez le guide étape par étape.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Créer une instance d'ImageRenderingOptions – améliorer la qualité graphique
  dans .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Créer une instance d’ImageRenderingOptions pour le rendu graphique de haute
  qualité
url: /fr/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une instance d'imagerenderingoptions pour un rendu graphique de haute qualité

Si vous devez **créer une instance d'imagerenderingoptions** pour produire des graphiques plus fluides, ce guide vous montre exactement comment faire. En configurant antialiasing, vous éliminez les bords dentelés et obtenez un rendu de qualité professionnelle sans bibliothèques supplémentaires.

Vous apprendrez comment instancier `ImageRenderingOptions`, activer antialiasing et attacher les options à un moteur de rendu tel qu'Aspose.Slides ou System.Drawing. Le tutoriel suppose que vous êtes familier avec la syntaxe de base de C# et que vous disposez d'un environnement de développement .NET prêt.

## Prérequis

- .NET 6.0 ou supérieur (l'API est disponible dans .NET Standard 2.0+)
- Une référence à l'assembly contenant `ImageRenderingOptions` (par ex., `Aspose.Slides.NET`)
- Un IDE tel que Visual Studio 2022 ou VS Code avec l'extension C#
- Compréhension de base des pipelines de rendu graphique

## Étape 1 : Créer une instance d'imagerenderingoptions

La première opération consiste à allouer un nouvel objet `ImageRenderingOptions`. Cet objet agit comme un conteneur pour tous les indicateurs liés au rendu.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Créer l'instance vous donne un contrôle complet sur la façon dont les graphiques vectoriels sont rasterisés. Vous pouvez ensuite activer ou désactiver des fonctionnalités spécifiques telles que antialiasing, le mode de rendu du texte ou la compression d'image.

## Étape 2 : Activer antialiasing pour améliorer le rendu graphique

Antialiasing lisse la transition entre les couleurs des pixels, réduisant l'effet d'escalier sur les lignes diagonales ou courbes. La propriété plus ancienne `SmoothingMode` est obsolète ; `UseAntialiasing` est l'approche moderne et recommandée.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Définir `UseAntialiasing` sur `true` indique au moteur de rendu d'appliquer un filtre de haute qualité lors de la rasterisation. Ce drapeau fonctionne à la fois pour les formes vectorielles et le texte, garantissant une fidélité visuelle constante sur la diapositive.

### Pourquoi ne pas utiliser SmoothingMode ?

`SmoothingMode` appartient à `System.Drawing.Graphics` et n'affecte que le dessin GDI+. Lorsque vous rendez des diapositives ou des PDF via Aspose.Slides, `ImageRenderingOptions.UseAntialiasing` est le seul indicateur respecté par la bibliothèque. Utiliser la propriété plus récente garantit la compatibilité future et élimine les comportements inattendus sur les plateformes non Windows.

## Étape 3 : Appliquer les options à une opération de rendu

Une fois l'instance `ImageRenderingOptions` configurée, transmettez‑la à la méthode qui effectue le rendu réel. Ci‑dessous se trouve un exemple complet et exécutable qui charge une présentation, rend la première diapositive en PNG et enregistre l'image avec antialiasing activé.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Explication des lignes clés**

- `new Presentation("sample.pptx")` charge le fichier source.  
- `GetThumbnail(2f, 2f, imgOptions)` crée un bitmap de la diapositive à deux fois le DPI par défaut tout en appliquant les options de rendu que vous avez configurées.  
- Le PNG résultant (`slide1_antialiased.png`) affiche des courbes et du texte lisses grâce à `UseAntialiasing = true`.

### Résultat attendu

Ouvrez `slide1_antialiased.png` dans n'importe quel visualiseur d'images. Comparé à un rendu sans antialiasing, vous remarquerez :

- Les coins arrondis des formes apparaissent sans étapes dentelées.  
- Les bords du texte sont nets mais adoucis, éliminant les artefacts pixelisés.  
- La qualité visuelle globale correspond à ce que vous verriez dans la vue PowerPoint originale.

## Étape 4 : Ajustements optionnels pour un rendu graphique avancé

Bien que antialiasing soit le drapeau le plus courant, `ImageRenderingOptions` propose des contrôles supplémentaires :

| Propriété | Objectif | Valeur typique |
|----------|---------|---------------|
| `UseHighQualityRendering` | Active le rendu sous‑pixel pour le texte | `true` |
| `PixelFormat` | Détermine la profondeur de couleur du bitmap de sortie | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Définit le format d'image cible (PNG, JPEG, etc.) | `Export.SaveFormat.Png` |

Vous pouvez chaîner ces paramètres :

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Astuce :** Lors de la génération de PDF à grande échelle ou de PNG haute résolution, conservez `UseAntialiasing` activé mais surveillez l'utilisation de la mémoire. Antialiasing ajoute une surcharge de traitement supplémentaire, qui peut être perceptible sur les machines peu puissantes.

## Pièges courants et comment les éviter

1. **Oublier de passer les options** – Les méthodes de rendu qui acceptent `ImageRenderingOptions` ignoreront antialiasing si vous appelez la surcharge sans le paramètre d'options. Utilisez toujours la méthode `GetThumbnail` à trois paramètres ou une méthode équivalente.  
2. **Mélanger SmoothingMode avec ImageRenderingOptions** – Définir `Graphics.SmoothingMode` n'a aucun effet sur le rendu Aspose.Slides. Comptez uniquement sur `UseAntialiasing`.  
3. **Utiliser une version de bibliothèque obsolète** – `ImageRenderingOptions` a été introduit dans Aspose.Slides 20.5. Assurez‑vous que votre paquet NuGet est à jour ; sinon la classe peut être manquante ou ne pas contenir la propriété `UseAntialiasing`.

## Conclusion

Vous savez maintenant comment **créer une instance d'imagerenderingoptions**, activer antialiasing et intégrer les options dans un flux de travail de rendu. Cette approche garantit un rendu graphique plus fluide, remplace le paramètre hérité `SmoothingMode` et fonctionne de manière cohérente sur les plateformes .NET.

À partir de là, vous pouvez explorer des indicateurs de rendu supplémentaires, expérimenter différentes échelles DPI ou combiner la technique avec l'export PDF pour des actifs de qualité imprimable. Maîtriser `ImageRenderingOptions` est une pierre angulaire de la programmation graphique .NET haute fidélité.

---

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un PNG à partir de HTML – Guide complet de rendu C#](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Créer une image à partir de HTML en C# – Guide complet étape par étape](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Créer du texte sur canvas – Guide complet du rendu de texte sur les images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}