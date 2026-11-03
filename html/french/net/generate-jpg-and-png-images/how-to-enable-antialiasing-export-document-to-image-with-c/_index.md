---
category: general
date: 2026-04-06
description: Apprenez comment activer l'anticrénelage, définir la largeur et la hauteur
  de l'image, et enregistrer le document au format PNG en C# – un guide rapide pour
  exporter un document en image.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: fr
og_description: Comment activer l'anticrénelage lors de l'exportation d'un document
  en image. Ce guide vous montre comment définir la largeur de l'image, la hauteur
  de l'image et enregistrer le document au format PNG.
og_title: Comment activer l'anticrénelage – Exporter le document en image
tags:
- C#
- ImageRendering
- Antialiasing
title: Comment activer l'anticrénelage – Exporter le document en image avec C#
url: /fr/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage – Exporter un document en image en C#

Vous vous êtes déjà demandé **comment activer l'anticrénelage** lors de la conversion d'un document en image ? Peut‑être avez‑vous essayé un appel rapide à `Save` et le résultat était dentelé, surtout sur les lignes diagonales. La bonne nouvelle, c’est que vous n’avez pas besoin d’être un magicien du graphisme — juste quelques lignes de C# et les bonnes options.

Dans ce tutoriel, nous allons parcourir la définition de la largeur de l’image, la hauteur de l’image, puis **enregistrer le document au format PNG** afin que vous puissiez **exporter le document en image** avec des bords lisses. À la fin, vous disposerez d’un extrait prêt à l’emploi qui génère un PNG net de 800 × 600 avec l’anticrénelage activé.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.7+)  
- Une référence à une bibliothèque de rendu qui prend en charge `ImageRenderingOptions` (par ex., Aspose.Words, Syncfusion, ou toute API exposant des propriétés similaires)  
- Une compréhension de base de la syntaxe C#  

Pas d’installation lourde — ajoutez simplement le package NuGet et vous êtes prêt.

## Étape 1 : Installer la bibliothèque de rendu

Tout d’abord, ajoutez le package à votre projet. Si vous utilisez Aspose.Words, exécutez :

```bash
dotnet add package Aspose.Words
```

> **Astuce :** Gardez la version de la bibliothèque à jour ; la dernière version (en avril 2026) apporte des améliorations de performances pour l’anticrénelage.

## Étape 2 : Créer l’objet Document

Chargez ou créez le document que vous souhaitez rendre. Voici un exemple minimal qui construit un document d’une page avec un paragraphe simple :

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

La classe `Document` est le point d’entrée ; tout ce que vous rendez provient d’elle. Dans les projets réels, vous chargerez probablement un .docx existant :

```csharp
// Document doc = new Document("input.docx");
```

## Étape 3 : Définir les options de rendu (largeur, hauteur, anticrénelage)

Nous répondons maintenant à la question centrale : **comment activer l'anticrénelage**. L’objet `ImageRenderingOptions` vous permet de basculer le lissage et de contrôler les dimensions.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Remarquez les commentaires : ils mentionnent explicitement **set image width**, **set image height**, et **UseAntialiasing** — les trois paramètres qui comptent le plus lorsque vous voulez un PNG soigné.

### Pourquoi l'anticrénelage est important

Sans anticrénelage, les lignes diagonales et les courbes apparaissent en escalier parce que le moteur de rendu considère chaque pixel comme allumé ou éteint. L’activer mélange les pixels de bord, produisant un adoucissement visuel similaire à ce que l’on voit dans un éditeur photo. Le compromis est une légère augmentation du temps de traitement, mais pour la plupart des exportations orientées UI, c’est négligeable.

## Étape 4 : Enregistrer le document au format PNG (Exporter le document en image)

Avec les options prêtes, nous **enregistrons enfin le document au format PNG**. La méthode `Save` prend le chemin du fichier et les options que nous venons de configurer.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

C’est tout — votre document devient maintenant un PNG de 800 × 600 avec l’anticrénelage appliqué. Si vous ouvrez `output.png`, vous verrez du texte net, des lignes lisses et aucun artefact dentelé.

### Vérifier le résultat

Vous pouvez rapidement vérifier le fichier dans n’importe quel visualiseur d’images. Recherchez :

- Les dimensions correctes (800 × 600)  
- Aucun bord en escalier visible sur le texte ou les formes  
- Un arrière‑plan transparent si votre document ne contenait pas de couleur de fond (la plupart des bibliothèques utilisent le blanc par défaut)

Si l’image apparaît dentelée, assurez‑vous que `UseAntialiasing = true` n’est pas écrasé ailleurs.

## Étape 5 : Cas particuliers & variantes

### Modifier le format de sortie

Vous voulez un JPEG au lieu d’un PNG ? Changez simplement l’extension du fichier et, éventuellement, ajustez la compression :

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Exporter plusieurs pages

Lorsque le document source comporte plusieurs pages, le moteur crée par défaut un fichier image distinct par page. Vous pouvez parcourir les pages :

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Enregistrer dans un flux (par ex., réponse HTTP)

Si vous construisez une API web, vous pouvez renvoyer le PNG directement :

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller, qui intègre chaque étape décrite :

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

L’exécution de ce programme produit `output.png` dans le répertoire de l’exécutable. Ouvrez‑le et vous verrez un PNG lisse de 800 × 600 — exactement ce que nous voulions obtenir.

## Questions fréquentes & dépannage

- **Et si l’image paraît floue ?**  
  Le flou peut survenir lorsque vous agrandissez une petite page source. Gardez la taille de la page source proche des dimensions cibles, ou augmentez le DPI via `imageOptions.Resolution` (par ex., `Resolution = 300`).

- **Cela fonctionne‑t‑il sur .NET Framework ?**  
  Oui. La même API existe dans le framework classique ; il suffit de référencer le DLL approprié.

- **Puis‑je contrôler la couleur d’arrière‑plan ?**  
  Absolument. Définissez `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` avant l’enregistrement.

- **L’anticrénelage est‑il accéléré par le matériel ?**  
  La plupart des bibliothèques effectuent l’anticrénelage en logiciel. Si vous avez besoin d’une accélération GPU, cherchez un moteur de rendu qui le supporte explicitement.

## Conclusion

Nous avons couvert **comment activer l'anticrénelage** lors de **l'exportation d'un document en image**, parcouru **set image width** et **set image height**, et montré les étapes exactes pour **save document as PNG**. L’extrait ci‑dessus est prêt pour la production, et vous pouvez maintenant l’adapter à JPEG, PDF multi‑pages, ou même diffuser l’image directement vers un client.

Ensuite, vous pourriez explorer l’ajout de filigranes, l’ajustement du DPI pour une sortie imprimable, ou l’intégration de cette logique dans un point de terminaison ASP.NET Core. Les mêmes principes s’appliquent — il suffit de remplacer le chemin de fichier par un flux de réponse.

Bon codage, et profitez de ces images nettes et antialiasées !

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}