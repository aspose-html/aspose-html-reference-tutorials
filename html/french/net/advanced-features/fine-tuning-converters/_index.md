---
title: Ajustement précis des convertisseurs dans .NET avec Aspose.HTML
linktitle: Ajustement précis des convertisseurs dans .NET
second_title: API de manipulation HTML Aspose.HTML .NET
description: Découvrez comment convertir du HTML en PDF, XPS et images avec Aspose.HTML pour .NET. Tutoriel étape par étape avec des exemples de code et des FAQ.
weight: 16
url: /fr/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajustement précis des convertisseurs dans .NET avec Aspose.HTML


## Introduction

Aspose.HTML pour .NET est une bibliothèque puissante qui permet aux développeurs de manipuler et de convertir des documents HTML dans divers formats. Que vous ayez besoin de convertir du HTML en PDF, XPS ou en images, ou d'effectuer d'autres tâches liées au HTML, Aspose.HTML fournit un ensemble d'outils robustes pour vous aider à accomplir votre travail.

Dans ce didacticiel, nous allons explorer certaines fonctionnalités essentielles d'Aspose.HTML pour .NET et fournir des explications étape par étape pour chaque exemple. À la fin de ce didacticiel, vous aurez une solide compréhension de la façon d'utiliser Aspose.HTML pour .NET dans vos applications .NET.

## Prérequis

Avant de plonger dans les exemples, assurez-vous que les conditions préalables suivantes sont remplies :

-  Aspose.HTML pour .NET : la bibliothèque Aspose.HTML pour .NET doit être installée. Vous pouvez la télécharger à partir du[lien de téléchargement](https://releases.aspose.com/html/net/).

-  Licence temporaire (facultatif) : Si vous n'avez pas de licence valide, vous pouvez obtenir une licence temporaire auprès de[ici](https://purchase.aspose.com/temporary-license/).

Explorons maintenant quelques cas d’utilisation courants avec Aspose.HTML pour .NET.

## Importer des espaces de noms

Dans votre code C#, commencez par importer les espaces de noms nécessaires :

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Convertir HTML en PDF

### Étape 1 : préparer le code HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer un périphérique PDF et spécifier le fichier de sortie

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Étape 4 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple convertit un extrait HTML en document PDF. Vous pouvez personnaliser le code HTML et le fichier de sortie selon vos besoins.

## Définir une taille de page personnalisée

### Étape 1 : préparer le code HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer des options de rendu PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Étape 5 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple montre comment définir une taille de page personnalisée pour le document PDF résultant.

## Ajuster la résolution

### Étape 1 : Préparez le code HTML et enregistrez-le dans un fichier

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Étape 3 : Créer des options de rendu PDF pour une basse résolution

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie pour la basse résolution

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Étape 5 : Rendu HTML en PDF pour une faible résolution

```csharp
document.RenderTo(device);
```

### Étape 6 : Créer des options de rendu PDF pour une haute résolution

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Étape 7 : Créer un périphérique PDF et spécifier les options et le fichier de sortie pour la haute résolution

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Étape 8 : Rendu HTML en PDF pour une haute résolution

```csharp
document.RenderTo(device);
```

Cet exemple illustre comment ajuster la résolution lors du rendu HTML en PDF, en tenant compte des écrans basse et haute résolution.

## Spécifier la couleur d'arrière-plan

### Étape 1 : Préparez le code HTML et enregistrez-le dans un fichier

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Étape 3 : Initialiser les options de rendu PDF avec la couleur d'arrière-plan

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Étape 5 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple montre comment spécifier une couleur d'arrière-plan lors de la conversion de HTML en PDF.

## Définir les tailles de page gauche et droite

### Étape 1 : préparer le code HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer des options de rendu PDF avec des tailles de page gauche et droite

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Étape 5 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple montre comment définir différentes tailles de page pour les pages de gauche et de droite lors de la conversion de HTML en PDF.

## Ajuster la taille de la page au contenu

### Étape 1 : préparer le code HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer des options de rendu PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Étape 5 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple montre comment ajuster la taille de la page au contenu le plus large lors de la conversion de HTML en PDF.

## Spécifier les autorisations PDF

### Étape 1 : préparer le code HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer des options de rendu PDF avec des autorisations

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Étape 4 : Créer un périphérique PDF et spécifier les options et le fichier de sortie

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Étape 5 : Convertir du HTML en PDF

```csharp
document.RenderTo(device);
```

Cet exemple montre comment spécifier les autorisations et le cryptage lors de la conversion de HTML en PDF protégé.

## Spécifier les options spécifiques à l'image

### Étape 1 : préparer le code HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Créer des options de rendu d’image

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Étape 4 : Créer un périphérique d'image et spécifier les options et le fichier de sortie

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Étape 5 : Rendre le code HTML en image

```csharp
document.RenderTo(device);
```

Cet exemple montre comment convertir du HTML en image avec des options de rendu spécifiques, telles que le format, la résolution et le mode de lissage.

## Spécifier les options de rendu XPS

### Étape 1 : préparer le code HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : créer des options de rendu XPS avec la taille de la page

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Étape 4 : créer un périphérique XPS et spécifier les options et le fichier de sortie

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Étape 5 : Rendu HTML en XPS

```csharp
document.RenderTo(device);
```

Cet exemple montre comment convertir HTML en XPS avec une taille de page et des options de rendu personnalisées.

## Combiner plusieurs documents HTML en PDF

### Étape 1 : préparer le code HTML pour plusieurs documents

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Étape 2 : Créer des documents HTML à fusionner

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Étape 3 : Initialiser le moteur de rendu HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Étape 4 : Créer un périphérique PDF pour la sortie fusionnée

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Étape 5 : fusionner des documents HTML en PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Cet exemple montre comment combiner plusieurs documents HTML en un seul fichier PDF à l'aide d'Aspose.HTML pour .NET.

## Définir le délai d'expiration du rendu

### Étape 1 : Préparez le code HTML avec JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Étape 2 : Initialiser le document HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Étape 3 : Initialiser le moteur de rendu HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Étape 4 : créer un périphérique PDF et définir le délai de rendu

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Étape 5 : Rendre HTML en PDF avec délai d'attente

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Cet exemple montre comment définir un délai d'expiration de rendu lors de la conversion de HTML en PDF, ce qui peut être utile lors du traitement de contenu dynamique ou de scripts de longue durée.

## Conclusion

Aspose.HTML pour .NET est une bibliothèque polyvalente qui permet aux développeurs de travailler efficacement avec des documents HTML. Dans ce didacticiel, nous avons abordé divers exemples, des conversions HTML de base en PDF aux fonctionnalités plus avancées telles que les tailles de page personnalisées, les résolutions et les autorisations. En suivant ces exemples, vous pouvez exploiter tout le potentiel d'Aspose.HTML pour .NET dans vos applications .NET.

 Si vous avez des questions ou avez besoin d'aide supplémentaire, n'hésitez pas à visiter le[Forum Aspose.HTML](https://forum.aspose.com/) pour obtenir du soutien et des conseils.

## FAQ

### Q1. Qu'est-ce qu'Aspose.HTML pour .NET ?
   
A1 : Aspose.HTML pour .NET est une bibliothèque .NET qui permet aux développeurs de manipuler et de convertir des documents HTML par programmation. Elle offre une large gamme de fonctionnalités pour travailler avec du contenu HTML, notamment la conversion HTML en PDF, XPS et d'images, ainsi que des options de rendu avancées.

### Q2. Où puis-je télécharger Aspose.HTML pour .NET ?

 A2 : Vous pouvez télécharger Aspose.HTML pour .NET à partir du[lien de téléchargement](https://releases.aspose.com/html/net/).

### Q3. Ai-je besoin d'une licence pour utiliser Aspose.HTML pour .NET ?

A3 : Bien que vous puissiez utiliser Aspose.HTML pour .NET sans licence, il est recommandé d'obtenir une licence pour une utilisation en production afin de déverrouiller toutes les fonctionnalités et de supprimer les filigranes ou les limitations.

### Q4. Comment puis-je protéger mes fichiers PDF générés avec Aspose.HTML pour .NET ?

A4 : Vous pouvez spécifier les autorisations PDF et les paramètres de chiffrement lors du rendu HTML au format PDF à l'aide d'Aspose.HTML pour .NET. Cela vous permet de contrôler qui peut accéder aux fichiers PDF résultants et les modifier.

### Q5. Puis-je convertir du HTML en d'autres formats comme XPS ou des images ?

A5 : Oui, Aspose.HTML pour .NET prend en charge la conversion de HTML en différents formats, notamment PDF, XPS et images (par exemple, JPEG). Vous pouvez personnaliser les paramètres de conversion pour répondre à vos besoins spécifiques.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
