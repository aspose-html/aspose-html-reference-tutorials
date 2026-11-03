---
category: general
date: 2026-07-08
description: Apprenez comment activer l'anticrénelage lors du rendu de HTML en PNG
  avec Aspose HTML. Ce guide couvre également la conversion du HTML en image et l’enregistrement
  du HTML au format PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- render html to png
- convert html to image
- save html as png
- aspose html to png
language: fr
lastmod: 2026-07-08
og_description: Comment activer l'anticrénelage lors du rendu HTML en PNG avec Aspose
  HTML. Suivez ce tutoriel étape par étape pour convertir le HTML en image et enregistrer
  le HTML au format PNG.
og_image_alt: Screenshot of HTML rendered to PNG with antialiasing enabled – how to
  enable antialiasing
og_title: Comment activer l'anticrénelage du rendu HTML en PNG – Guide Aspose
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  headline: How to Enable Antialiasing Rendering HTML to PNG
  type: TechArticle
- description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  name: How to Enable Antialiasing Rendering HTML to PNG
  steps:
  - name: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
    text: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
  - name: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
    text: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
  - name: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
    text: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
  - name: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
    text: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
  - name: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
    text: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
  type: HowTo
tags:
- Aspose
- C#
- Image Rendering
title: Comment activer l'anticrénelage lors du rendu HTML en PNG
url: /fr/net/rendering-html-documents/how-to-enable-antialiasing-rendering-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer l'anticrénelage lors du rendu HTML en PNG

Vous êtes-vous déjà demandé **comment activer l'anticrénelage** en transformant une page web en une image PNG nette ? Vous n'êtes pas seul — de nombreux développeurs rencontrent des problèmes lorsque le rendu apparaît en dents de scie ou flou. La bonne nouvelle, c’est qu’avec Aspose.HTML vous pouvez lisser ces bords en quelques lignes de code seulement. Dans ce tutoriel, nous parcourrons les étapes exactes pour rendre du HTML en PNG, convertir du HTML en image, et enfin **enregistrer le HTML en PNG** avec l’anticrénelage activé.

> **Ce que vous obtiendrez :** un exemple complet, prêt à l’exécution en C#, une explication de chaque option, et des astuces pour gérer les cas particuliers comme les polices personnalisées ou les pages volumineuses.

## Comment activer l'anticrénelage lors du rendu HTML en PNG

La première chose à comprendre est **pourquoi l'anticrénelage est important**. Lorsque le moteur de rendu dessine des formes ou du texte, il approxime les courbes avec des pixels. Sans anticrénelage, ces approximations créent des artefacts en escalier — particulièrement visibles sur les lignes diagonales ou les polices fines. Activer l'anticrénelage indique au moteur de mélanger les pixels voisins, produisant ainsi un résultat visuel plus lisse.

Ci‑dessous se trouve le code principal qui montre **comment activer l'anticrénelage** à l’aide de `ImageRenderingOptions` d’Aspose.HTML. Nous le décortiquerons étape par étape afin que vous voyiez exactement ce que chaque ligne fait.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// Step 1: Create an in‑memory HTML document
HTMLDocument htmlDoc = new HTMLDocument("<html><body><h1>Sample</h1></body></html>");

// Step 2: Define the desired font style (bold + italic)
WebFontStyle fontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

// Step 3: Configure image rendering options – enable antialiasing for smoother graphics
ImageRenderingOptions imageOpts = new ImageRenderingOptions();
imageOpts.UseAntialiasing = true;

// Step 4: Configure text rendering options – enable hinting for clearer text
TextOptions textOpts = new TextOptions();
textOpts.UseHinting = true;

// Step 5: Combine rendering and text options into PNG save options
ImageSaveOptions pngSaveOpts = new ImageSaveOptions(SaveFormat.Png)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts
};

// Step 6: Save the HTML document as a PNG image using the configured options
htmlDoc.Save("YOUR_DIRECTORY/sample.png", pngSaveOpts);
```

### Pourquoi chaque élément est important

1. **HTMLDocument** – fonctionne entièrement en mémoire, vous n’avez donc pas besoin de fichiers `.html` physiques. Idéal pour les conversions à la volée.  
2. **WebFontStyle** – montre que vous pouvez styliser le texte avant le rendu ; la combinaison gras‑italique n’est qu’une démonstration.  
3. **ImageRenderingOptions.UseAntialiasing** – ce drapeau répond à **comment activer l'anticrénelage** ; réglez‑le sur `true` et le rasteriseur lissera les bords.  
4. **TextOptions.UseHinting** – le hinting améliore la clarté des glyphes, surtout à petite taille. C’est un bon complément à l’anticrénelage.  
5. **ImageSaveOptions** – regroupe les options de rendu et de texte, puis indique à Aspose de générer un fichier PNG.

## Rendre du HTML en PNG avec Aspose

Maintenant que vous savez **comment activer l'anticrénelage**, parlons de la vision d’ensemble du **rendu HTML en PNG**. Aspose.HTML se charge du travail lourd :

- **Mise en page automatique** – le moteur analyse le CSS, calcule les modèles de boîtes et positionne les éléments comme le ferait un navigateur.  
- **Contrôle de la résolution** – vous pouvez spécifier le DPI via `ImageRenderingOptions.Resolution`, ce qui est pratique pour les impressions haute résolution.  
- **Gestion de l’arrière‑plan** – définissez `imageOpts.BackgroundColor` si vous avez besoin d’un canevas transparent ou coloré.

Voici un petit ajustement qui ajoute un DPI personnalisé :

```csharp
imageOpts.Resolution = new SizeF(300, 300); // 300 DPI for print‑quality PNG
```

> **Astuce pro :** si vous convertissez une page contenant des ressources externes (images, polices), assurez‑vous de définir `htmlDoc.BaseUrl` sur le dossier contenant ces actifs. Sinon le moteur de rendu les ignorera.

## Convertir du HTML en image – Options avancées

L’expression **convertir HTML en image** implique souvent plus que le simple PNG. Aspose prend en charge JPEG, BMP, TIFF et même GIF. Changer de format est aussi simple que de modifier l’énumération `SaveFormat` :

```csharp
ImageSaveOptions jpegOpts = new ImageSaveOptions(SaveFormat.Jpeg)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts,
    Quality = 90 // JPEG quality (0‑100)
};

htmlDoc.Save("sample.jpg", jpegOpts);
```

Lorsque vous avez besoin d’une sortie adaptée aux vecteurs, pensez à `SvgSaveOptions`. Le même pipeline de rendu s’applique, vous obtenez donc un anticrénelage cohérent quel que soit le format.

### Cas particulier : pages très longues

Si votre HTML dépasse la hauteur d’un écran typique, Aspose créera, par défaut, une image unique très haute. Cela peut exploser la consommation mémoire. Pour atténuer ce problème, vous pouvez diviser le document en plusieurs pages :

```csharp
var pageHeight = 1080; // pixels
var totalHeight = htmlDoc.DocumentElement.ScrollHeight;
for (int offset = 0; offset < totalHeight; offset += pageHeight)
{
    imageOpts.Viewport = new RectangleF(0, offset, htmlDoc.DocumentElement.ScrollWidth, pageHeight);
    htmlDoc.Save($"page_{offset / pageHeight}.png", pngSaveOpts);
}
```

## Enregistrer le HTML en PNG – L’étape finale

À ce stade, vous avez vu **comment activer l'anticrénelage**, vous avez appris à **rendre du HTML en PNG**, et vous avez exploré les options de **conversion du HTML en image**. L’acte final—**enregistrer le HTML en PNG**—est déjà illustré dans l’extrait original, mais encapsulons‑le dans une méthode réutilisable :

```csharp
public static void SaveHtmlAsPng(string html, string outputPath, bool antialias = true)
{
    // Create document
    var doc = new HTMLDocument(html);

    // Rendering options
    var imgOpts = new ImageRenderingOptions
    {
        UseAntialiasing = antialias,
        Resolution = new SizeF(96, 96) // default screen DPI
    };

    // Text options
    var txtOpts = new TextOptions { UseHinting = true };

    // Combine into save options
    var saveOpts = new ImageSaveOptions(SaveFormat.Png)
    {
        RenderingOptions = imgOpts,
        TextOptions = txtOpts
    };

    // Save
    doc.Save(outputPath, saveOpts);
}
```

Vous pouvez maintenant appeler `SaveHtmlAsPng("<html>…</html>", @"C:\temp\output.png")` depuis n’importe où dans votre projet. Le paramètre `antialias` vous permet de basculer la fonction de lissage des bords, vous donnant un contrôle complet sur **comment activer l'anticrénelage** à l’exécution.

## Aspose HTML en PNG – Exemple complet fonctionnel

Voici une application console autonome qui réunit tous les éléments. Copiez‑collez, ajustez le placeholder `YOUR_DIRECTORY`, puis exécutez avec .NET 6 ou une version ultérieure.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment utiliser Aspose pour rendre HTML en PNG – Guide étape par étape](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Comment rendre HTML en PNG avec Aspose – Guide complet](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Rendre HTML en PNG dans .NET avec Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}