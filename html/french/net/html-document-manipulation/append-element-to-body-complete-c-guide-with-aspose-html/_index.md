---
category: general
date: 2026-02-11
description: Ajouter un élément au corps du document avec Aspose.HTML en C#. Apprenez
  à créer un élément paragraphe, à définir le poids de la police en gras, à choisir
  la police Arial et à spécifier la taille de police CSS — le tout dans un seul tutoriel.
draft: false
keywords:
- append element to body
- create paragraph element
- set font weight bold
- set font family arial
- define css font size
language: fr
og_description: Ajouter un élément au corps avec Aspose.HTML. Ce tutoriel montre comment
  créer un élément paragraphe, définir le poids de la police en gras, définir la famille
  de police Arial et définir la taille de police CSS.
og_title: Ajouter un élément au corps – Guide complet C#
tags:
- Aspose.HTML
- C#
- DOM manipulation
title: Ajouter un élément au corps – Guide complet C# avec Aspose.HTML
url: /fr/net/html-document-manipulation/append-element-to-body-complete-c-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un élément au corps – Guide complet C# avec Aspose.HTML

Vous avez déjà eu besoin d'**append element to body** d'un document HTML depuis C# et vous vous êtes demandé pourquoi les exemples semblent toujours à moitié cuits ? Vous n'êtes pas seul. Dans de nombreux extraits de démarrage rapide, vous verrez un paragraphe ajouté, mais les détails de style — comme mettre le texte en **set font weight bold** ou utiliser **set font family arial** — sont omis.  

Dans ce tutoriel, nous parcourrons un scénario réel : créer une balise `<p>`, définir son style (y compris **define css font size**), et enfin **append element to body** avec Aspose.HTML. À la fin, vous disposerez d'un fichier HTML entièrement fonctionnel que vous pourrez insérer dans n'importe quelle page web, et vous comprendrez les raisons derrière chaque ligne de code.

## Ce que vous apprendrez

- Comment **create paragraph element** programmétiquement.
- Les étapes exactes pour **set font weight bold** et **set font family arial** en utilisant l'énumération `WebFontStyle`.
- Comment **define css font size** en points pour une typographie précise.
- La façon la plus propre de **append element to body** sans concaténation manuelle de chaînes.
- Astuces, cas limites, et un exemple complet exécutable que vous pouvez copier‑coller.

Aucune bibliothèque externe au-delà d'Aspose.HTML n'est requise, et le code fonctionne avec .NET 6+ (ou .NET Framework 4.7.2). Commençons.

---

## Étape 1 – Installer Aspose.HTML et configurer le projet

Tout d'abord, assurez-vous d'avoir le package NuGet Aspose.HTML :

```bash
dotnet add package Aspose.HTML
```

> Astuce : Utilisez la dernière version stable (au moment de la rédaction, **23.9.0**) pour bénéficier des corrections de bugs et des nouvelles fonctionnalités CSS.

Créez une nouvelle application console (ou intégrez‑la dans un projet existant) et ajoutez les directives `using` suivantes :

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Ces espaces de noms vous donnent accès à `HTMLDocument`, `CSSStyleDeclaration` et à l'énumération `WebFontStyle` dont nous aurons besoin plus tard.

## Étape 2 – Définir le style CSS : famille de police, taille, poids et italique

Pourquoi définir un objet de style plutôt que d'écrire une chaîne brute d'attribut `style` ? Parce que `CSSStyleDeclaration` valide les noms de propriétés, gère la conversion d'unités et rend les modifications futures indolores.

```csharp
// Step 2: Build a CSS style block
var paragraphStyle = new CSSStyleDeclaration();

// Set the font family to Arial – this satisfies the “set font family arial” requirement
paragraphStyle.FontFamily = "Arial";

// Define the font size in points; “define css font size” is clearer than using pixels for print‑like output
paragraphStyle.FontSize = new CSSLength(14, CSSLengthUnit.Point);

// Make the text bold – fulfills “set font weight bold”
paragraphStyle.FontWeight = WebFontStyle.Bold;

// Optional: add italic for visual flair
paragraphStyle.FontStyle = WebFontStyle.Italic;
```

> **Pourquoi les points ?** Les points sont indépendants du dispositif, garantissant la même taille visuelle à l'écran et à l'impression. Si vous avez besoin d'un design réactif, remplacez `CSSLengthUnit.Point` par `CSSLengthUnit.Px` ou `%`.

## Étape 3 – Créer un nouveau document HTML

Aspose.HTML vous fournit une API propre, similaire au DOM, qui reflète les navigateurs. Considérez `HTMLDocument` comme l'objet racine que vous obtiendriez de `document` en JavaScript.

```csharp
// Step 3: Initialize an empty HTML document
var htmlDoc = new HTMLDocument();
```

À ce stade, le document contient la structure minimale `<html><head></head><body></body></html>`, prête à être manipulée.

## Étape 4 – Créer l'élément paragraphe et appliquer le style

Nous allons maintenant réellement **create paragraph element**. La méthode `CreateElement` renvoie un `IHTMLElement` que nous pouvons enrichir avec des attributs et du contenu interne.

```csharp
// Step 4: Build the <p> element
var paragraph = htmlDoc.CreateElement("p");

// Apply the previously built CSS style; CssText converts the declaration to a valid style string
paragraph.SetAttribute("style", paragraphStyle.CssText);

// Insert the visible text
paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";
```

Si vous inspectez `paragraphStyle.CssText`, vous verrez quelque chose comme :

```
font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;
```

Cette chaîne est exactement ce que le navigateur interpréterait, mais nous avons évité la concaténation manuelle.

## Étape 5 – Ajouter l'élément au corps

Voici le moment que vous attendiez : **append element to body**. Cette ligne unique fait le travail lourd, insérant le `<p>` dans le nœud `<body>` du document.

```csharp
// Step 5: Append the styled paragraph to the document body
htmlDoc.Body.AppendChild(paragraph);
```

> **Alerte cas limite :** Si vous appelez `AppendChild` sur un nœud qui contient déjà l'élément, l'élément sera déplacé — et non dupliqué. Cela évite les paragraphes dupliqués accidentels lors d'une boucle.

## Étape 6 – Enregistrer le document et vérifier le résultat

Enfin, écrivez le HTML sur le disque afin de pouvoir l'ouvrir dans n'importe quel navigateur :

```csharp
// Step 6: Persist the HTML file
string outputPath = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
htmlDoc.Save(outputPath);

// Optional: launch the file automatically (works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(outputPath) { UseShellExecute = true });
```

### Résultat attendu

L'ouverture de **StyledParagraph.html** devrait afficher une seule ligne de texte :

> *Styled with WebFontStyle – bold, italic, Arial, 14pt.*

Le texte sera **bold**, **italic**, rendu en **Arial**, et de taille **14 pt**. Si vous inspectez le source, vous verrez :

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
  <p style="font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;">
    Styled with WebFontStyle – bold, italic, Arial, 14pt.
  </p>
</body>
</html>
```

C'est un document propre, conforme aux standards, créé entièrement depuis C#.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez placer dans `Program.cs`. Aucun autre fichier n'est nécessaire.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Define CSS style (font family, size, weight, style)
        var paragraphStyle = new CSSStyleDeclaration
        {
            FontFamily = "Arial",                                   // set font family arial
            FontSize = new CSSLength(14, CSSLengthUnit.Point),      // define css font size
            FontWeight = WebFontStyle.Bold,                         // set font weight bold
            FontStyle = WebFontStyle.Italic                         // optional italic for demo
        };

        // 2️⃣ Create an empty HTML document
        var htmlDoc = new HTMLDocument();

        // 3️⃣ Build a <p> element and attach the style
        var paragraph = htmlDoc.CreateElement("p");
        paragraph.SetAttribute("style", paragraphStyle.CssText);
        paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";

        // 4️⃣ Append element to body
        htmlDoc.Body.AppendChild(paragraph);

        // 5️⃣ Save the file
        string output = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
        htmlDoc.Save(output);
        Console.WriteLine($"HTML saved to: {output}");

        // Open automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(output) { UseShellExecute = true });
    }
}
```

Exécutez `dotnet run` et vous obtiendrez un fichier HTML prêt à l'emploi.

## Questions fréquentes & cas limites

### Et si je dois ajouter plusieurs paragraphes ?

Répétez simplement **Step 4** et **Step 5** à l'intérieur d'une boucle. Souvenez‑vous que chaque appel à `CreateElement("p")` renvoie un nouveau nœud, vous n'utiliserez donc pas accidentellement le même élément.

```csharp
for (int i = 1; i <= 3; i++)
{
    var p = htmlDoc.CreateElement("p");
    p.SetAttribute("style", paragraphStyle.CssText);
    p.InnerHTML = $"Paragraph {i}";
    htmlDoc.Body.AppendChild(p);
}
```

### Puis‑je utiliser des fichiers CSS externes au lieu de styles en ligne ?

Absolument. Remplacez l'attribut `style` en ligne par un nom de classe et ajoutez un bloc `<style>` ou un lien vers une feuille de style externe. L'approche en ligne est présentée ici pour plus de clarté et parce qu'elle garantit que le style accompagne l'élément lorsque vous **append element to body**.

### Qu'en est‑il des attributs spécifiques à HTML5 (par ex., `data-*`) ?

`SetAttribute` fonctionne avec n'importe quel nom d'attribut, vous pouvez donc faire :

```csharp
paragraph.SetAttribute("data-id", "12345");
```

L'attribut sera conservé dans le balisage final.

### Cela fonctionne‑t‑il sur .NET Core sous Linux ?

Oui. Aspose.HTML est multiplateforme ; assurez‑vous simplement que les dépendances natives sont installées (`libgdiplus` sur certaines distributions) si vous prévoyez de rendre le document en image plus tard.

## Conclusion

Vous disposez maintenant d'un exemple complet, de bout en bout, qui **append element to body** en utilisant Aspose.HTML en C#. Nous avons couvert comment **create paragraph element**, **set font weight bold**, **set font family arial**, et **define css font size** — le tout avec des explications claires sur l'importance de chaque étape.  

N'hésitez pas à expérimenter : changez la famille de police, modifiez l'unité de taille, ou ajoutez d'autres propriétés CSS comme `color` ou `text-shadow`. Le même schéma fonctionne pour d'autres éléments HTML (tables, images, SVG), vous permettant d'étendre cette base en générateurs de documents complets.

### Prochaines étapes

- Explorez **Aspose.HTML rendering** pour convertir le HTML en PDF ou PNG.  
- Apprenez à **inject external JavaScript** pour un comportement dynamique.  
- Combinez cette approche avec **Razor templates** pour la génération HTML côté serveur.  

Vous avez une variante que vous avez essayée ? Partagez‑la dans les commentaires, et bon codage !  

<img src="append-element-to-body.png" alt="append element to body example" width="600">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}