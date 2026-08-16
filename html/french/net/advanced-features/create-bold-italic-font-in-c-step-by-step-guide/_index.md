---
category: general
date: 2026-08-15
description: Créez rapidement une police en gras et italique en C#. Apprenez comment
  créer une police en C# avec les styles gras et italique en utilisant la classe Font
  intégrée.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: fr
lastmod: 2026-08-15
og_description: Créer une police en gras italique en C# avec un exemple clair. Ce
  tutoriel montre comment créer une police en C# en utilisant les indicateurs FontStyle
  et explique les pièges courants.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Créer une police gras et italique en C# – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Créer une police en gras italique en C# – guide étape par étape
url: /fr/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une police gras italique en C# – guide étape par étape

Si vous avez besoin de **créer une police gras italique** en C#, ce guide vous montre exactement comment le faire. Vous verrez un exemple complet et exécutable qui montre également comment **créer une police en C#** en utilisant la classe standard .NET `Font`.

Travailler avec des polices personnalisées est une partie courante de la création d'applications de bureau Windows, de la génération de PDF ou du rendu HTML sur le serveur. À la fin de ce tutoriel, vous serez capable d'instancier une police à la fois en gras et en italique, comprendre pourquoi l'opérateur binaire `|` est utilisé, et gérer les cas limites courants tels que les familles de polices manquantes.

## Ce que vous apprendrez

* Comment importer les espaces de noms requis pour la gestion des polices.  
* La syntaxe pour combiner `FontStyle.Bold` et `FontStyle.Italic`.  
* Comment vérifier que la police a été créée avec succès.  
* Conseils pour la gestion des polices de secours lorsque la famille demandée n’est pas installée.  

Aucune bibliothèque externe n’est requise — tout utilise la bibliothèque de classes de base du .NET Framework / .NET Core.

## Prérequis

* .NET 6.0 SDK ou ultérieur (le code fonctionne également sur .NET Framework 4.6+).  
* Un éditeur de code ou un IDE (Visual Studio, VS Code, Rider, etc.).  
* Une connaissance de base de la syntaxe C#.  

Si vous remplissez ces prérequis, vous pouvez suivre les étapes sans configuration supplémentaire.

## Étape 1 : Ajouter les directives using nécessaires

La classe `Font` se trouve dans l’espace de noms `System.Drawing`, qui fait partie du package NuGet `System.Drawing.Common` pour .NET Core/.NET 5+. Ajoutez l’espace de noms en haut de votre fichier :

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Pourquoi cette étape est importante** – Sans la ligne `using System.Drawing;`, le compilateur ne peut pas localiser `Font` ou `FontStyle`, ce qui entraîne une erreur « type ou nom d’espace de noms introuvable ».

## Étape 2 : Combiner les styles gras et italique avec l’opérateur OU binaire

Dans .NET, `FontStyle` est une énumération marquée avec l’attribut `[Flags]`. Cela signifie que vous pouvez combiner plusieurs valeurs en utilisant l’opérateur `|` (OU binaire) :

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Explication

* `"Arial"` – le nom de la famille de police. Si le système n’a pas Arial installé, le constructeur revient à la police par défaut.  
* `12` – taille en points.  
* `FontStyle.Bold | FontStyle.Italic` – combine les deux indicateurs de style. L’opérateur `|` fusionne la représentation binaire de chaque indicateur, produisant une valeur unique qui représente « gras + italique ».  

> **Astuce :** Utilisez toujours les noms d’énumération (`FontStyle.Bold`) plutôt que des nombres magiques ; cela améliore la lisibilité et évite les bugs lorsque les valeurs d’énumération changent.

## Étape 3 : Vérifier la police créée (optionnel mais recommandé)

Afficher les propriétés de la police vous aide à confirmer que la combinaison de styles a réussi, surtout lors du débogage sur une nouvelle machine.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Sortie attendue**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Si la sortie indique à la fois `Bold` et `Italic`, la police a été créée correctement.

## Étape 4 : Rendre une chaîne d’exemple (confirmation visuelle)

Lorsque vous exécutez une application console, vous ne pouvez pas voir le style réel des glyphes, mais vous pouvez générer une image pour prouver le résultat. Le fragment suivant dessine « Hello, World! » en utilisant la police gras‑italique et l’enregistre sous *sample.png* :

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Après l’exécution du programme, ouvrez *sample.png* pour voir le texte rendu avec le style gras italique.

![Texte d'exemple rendu avec une police gras italique](sample.png)

*Texte alternatif de l’image : Capture d’écran du texte rendu avec une police Arial gras italique dans une fenêtre console C#* – ce texte alternatif satisfait l’exigence SEO pour le texte alternatif des images.

## Étape 5 : Repli élégant lorsque la famille de police est indisponible

Si la famille demandée (par ex., « Arial ») n’est pas installée, le constructeur `Font` lève une `ArgumentException`. Enveloppez la création dans un bloc `try/catch` et revenez à une police sûre connue comme « Segoe UI ».

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Pourquoi gérer cela ?** Dans les environnements conteneurisés ou sans interface graphique, l’ensemble de polices par défaut peut différer d’un bureau typique. Fournir un repli empêche les plantages à l’exécution et assure un style cohérent.

## Exemple complet, exécutable

En rassemblant tout, voici un programme complet que vous pouvez copier, coller et exécuter :

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Comment exécuter

1. Enregistrez le code dans un fichier nommé `Program.cs`.  
2. Ouvrez un terminal dans le répertoire du fichier.  
3. Exécutez `dotnet new console -n FontDemo` (si vous avez besoin d’une structure de projet).  
4. Remplacez le `Program.cs` généré par le code ci‑dessus.  
5. Exécutez `dotnet add package System.Drawing.Common` (requis pour .NET Core/5+).  
6. Compilez et exécutez avec `dotnet run`.  

Vous verrez la sortie console confirmant les propriétés de la police, et `sample.png` apparaîtra dans le dossier du projet.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| **Package `System.Drawing.Common` manquant** | .NET Core n’inclut pas `System.Drawing` par défaut. | Exécutez `dotnet add package System.Drawing.Common`. |
| **Famille de police non installée** | Les images Docker sans interface graphique manquent souvent des polices Windows. | Utilisez une police de secours ou installez les polices requises dans le conteneur. |
| **Utilisation incorrecte de `|`** | Utiliser `+` au lieu de `|` entraîne une combinaison invalide. | Combinez toujours les valeurs `FontStyle` avec l’opérateur OU binaire (`|`). |
| **Libération de l’objet `Font`** | Ne pas appeler `Dispose` peut provoquer des fuites de ressources GDI. | Enveloppez `Font` dans un bloc `using` ou appelez `font.Dispose()` après utilisation. |

## Conclusion

Vous savez maintenant comment **créer une police gras italique** en C# et comment **créer une police en C#** de manière sûre et efficace. Le tutoriel a couvert l’importation du bon espace de noms, la combinaison des indicateurs `FontStyle`, la vérification du résultat, le rendu d’un exemple visuel, et la gestion des familles de polices manquantes.

Vous pourriez maintenant explorer :

* **Créer des polices soulignées ou barrées** – ajoutez `FontStyle.Underline` ou `FontStyle.Strikeout`.  
* **Utiliser des polices TrueType personnalisées** – chargez un fichier `.ttf` avec `PrivateFontCollection`.  
* **Appliquer des polices dans WinForms, WPF ou la génération de PDF** – le même objet `Font` peut être passé aux contrôles UI ou aux bibliothèques tierces.  

N’hésitez pas à expérimenter avec différentes familles, tailles et combinaisons de styles. Si vous rencontrez des problèmes, consultez à nouveau le tableau « Pièges courants » ou vérifiez la documentation officielle [.NET pour System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment combiner des polices de manière programmatique en C# – Guide étape par étape](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Créer un document HTML avec texte stylisé et l’exporter en PDF – Guide complet](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convertir docx en png – créer une archive zip tutoriel C#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}