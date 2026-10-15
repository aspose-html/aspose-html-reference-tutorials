---
category: general
date: 2026-10-15
description: Kombinieren Sie Schriftstile in C# durch Festlegen von Schriftfamilie
  und Größe mit dem Aspose.HTML Font‑Konstruktor. Lernen Sie, schnell fett‑kursiven
  Text zu erstellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- combine font styles
- set font family
- set font size c#
- c# font constructor
- create bold italic text
language: de
lastmod: 2026-10-15
og_description: Kombinieren Sie Schriftstile in C# mit dem Aspose.HTML Font‑Konstruktor.
  Dieses Tutorial zeigt, wie man die Schriftfamilie festlegt, die Schriftgröße in
  C# setzt und fett‑kursiven Text erstellt.
og_image_alt: Screenshot of C# code that combines font styles with Aspose.HTML
og_title: Schriftstile in C# kombinieren – Schnellleitfaden mit Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  headline: How to combine font styles in C# with Aspose.HTML
  type: TechArticle
- description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  name: How to combine font styles in C# with Aspose.HTML
  steps:
  - name: Explanation
    text: '- `"Arial"` – **set font family** to Arial, a widely supported sans‑serif
      typeface. - `12` – **set font size c#** to 12 points, which is a comfortable
      default for body text. - `WebFontStyle.Bold | WebFontStyle.Italic` – this expression
      **combines font styles**. The `|` operator merges the `Bold` and'
  - name: Why this works
    text: '- `paragraph.Style.FontFamily` uses the **set font family** value from
      the `Font` instance. - `paragraph.Style.FontSize` uses the **set font size c#**
      you defined. - The explicit `FontWeight` and `FontStyle` assignments mirror
      the **combine font styles** flags, ensuring the rendered output matches t'
  - name: Pro tip on performance
    text: 'Creating many `Font` objects inside a tight loop can degrade performance.
      Cache commonly used fonts in a dictionary and reuse them:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- Font styling
title: Wie man Schriftstile in C# mit Aspose.HTML kombiniert
url: /de/net/html-document-manipulation/how-to-combine-font-styles-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Schriftartenstile in C# mit Aspose.HTML kombiniert

Wenn Sie **Schriftartenstile kombinieren** müssen in einer C#‑Anwendung, zeigt Ihnen dieser Leitfaden eine prägnante Methode, dies mit Aspose.HTML zu tun. Sie lernen, wie man die Schriftfamilie festlegt, die Schriftgröße in C# setzt und den **c#‑Schriftkonstruktor** verwendet, um fetten kursiven Text in nur wenigen Codezeilen zu erzeugen.

Entwickler fragen sich oft, ob sie für jeden Stil separate `Font`‑Objekte erstellen müssen oder ob ein einzelner Konstruktor mehrere Attribute verarbeiten kann. Die Antwort lautet, dass Sie Stile direkt beim Instanziieren der Schrift kombinieren können. Dieses Tutorial führt Sie durch den gesamten Prozess, vom Importieren des richtigen Namespaces bis zum Rendern von formatiertem Text in einem HTML‑Dokument.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Aspose.HTML für .NET installiert (NuGet‑Paket `Aspose.HTML` Version 23.9 oder neuer).
- .NET 6.0+ oder .NET Framework 4.7.2+.
- Grundlegende Kenntnisse der C#‑Syntax und objektorientierten Programmierung.

Keine zusätzlichen Drittanbieter‑Bibliotheken sind erforderlich.

## Schritt 1: Importieren des Zeichen‑Namespaces

Das Erste, was Sie tun müssen, ist **den Namespace Aspose.Html.Drawing zu importieren**, damit Sie auf die Klasse `Font` und zugehörige Zeichen‑Hilfsmittel zugreifen können.

```csharp
using Aspose.Html.Drawing;
```

> **Warum?** Die Klasse `Font` befindet sich in `Aspose.Html.Drawing`. Das Importieren dieses Namespace macht den Typ verfügbar, ohne ihn jedes Mal vollständig qualifizieren zu müssen, und hält Ihren Code sauber und lesbar.

## Schritt 2: Verwenden des C#‑Schriftkonstruktors zum Festlegen von Familie, Größe und Kombinieren von Stilen

Der **c#‑Schriftkonstruktor** akzeptiert drei Parameter: den Namen der Schriftfamilie, die Punktgröße und eine bitweise Kombination von `WebFontStyle`‑Flags. Durch die Verwendung des bitweisen ODER‑Operators (`|`) können Sie **Schriftartenstile kombinieren** wie fett und kursiv.

```csharp
// Create a Font instance that is both bold and italic
var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
```

### Erklärung

- `"Arial"` – **Schriftfamilie festlegen** auf Arial, eine weit verbreitete serifenlose Schriftart.
- `12` – **Schriftgröße in C# festlegen** auf 12 Punkt, was ein angenehmer Standard für Fließtext ist.
- `WebFontStyle.Bold | WebFontStyle.Italic` – dieser Ausdruck **kombiniert Schriftartenstile**. Der `|`‑Operator verbindet die Flags `Bold` und `Italic` zu einem einzigen Wert, sodass der Konstruktor eine Schrift erzeugt, die gleichzeitig fett *und* kursiv ist.

> **Pro‑Tipp:** Wenn Sie Unterstreichung oder Durchstreichung hinzufügen müssen, fügen Sie `WebFontStyle.Underline` bzw. `WebFontStyle.Strikethrough` im selben Ausdruck ein.

## Schritt 3: Anwenden der Schrift auf ein HTML‑Element

Da Sie nun ein `Font`‑Objekt besitzen, können Sie es auf jedes HTML‑Element anwenden, das Styling unterstützt. Im Folgenden erstellen wir ein einfaches HTML‑Dokument, fügen einen Absatz hinzu und weisen den kombinierten Stil zu.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Create a new HTML document
var document = new HTMLDocument();

// Add a paragraph element
var paragraph = document.CreateElement("p");
paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
document.Body.AppendChild(paragraph);

// Apply the Font object to the paragraph's style
paragraph.Style.FontFamily = font.Family;
paragraph.Style.FontSize = $"{font.Size}pt";
paragraph.Style.FontWeight = "bold";
paragraph.Style.FontStyle = "italic";

// Render the document to an image (optional verification step)
using (var renderer = new ImageRenderer())
{
    renderer.Render(document, "output.png");
}
```

### Warum das funktioniert

- `paragraph.Style.FontFamily` verwendet den **festgelegten Schriftfamilien**‑Wert aus der `Font`‑Instanz.
- `paragraph.Style.FontSize` verwendet die **festgelegte Schriftgröße in C#**, die Sie definiert haben.
- Die expliziten Zuweisungen `FontWeight` und `FontStyle` spiegeln die **kombinierten Schriftartenstil**‑Flags wider und stellen sicher, dass die gerenderte Ausgabe dem beabsichtigten fett‑kursiven Aussehen entspricht.

> **Randfall:** Wenn die Ziel‑Schriftfamilie keine kursiven oder fetten Varianten unterstützt, kann der Browser den Stil simulieren, was die visuelle Treue beeinträchtigen kann. Testen Sie stets mit der tatsächlichen Schrift, die Sie ausliefern wollen.

## Schritt 4: Ergebnis überprüfen

Führen Sie das Programm aus und öffnen Sie `output.png`. Sie sollten den Satz in Arial, 12 pt, mit sowohl fetter als auch kursiver Formatierung sehen. Das bestätigt, dass der **c#‑Schriftkonstruktor** die Stile korrekt kombiniert hat.

Wenn Sie das HTML lieber direkt ansehen möchten, können Sie den Rendering‑Schritt überspringen und das Dokument speichern:

```csharp
document.Save("styled.html");
```

Öffnen Sie `styled.html` in einem modernen Browser, um denselben formatierten Absatz zu sehen.

## Häufige Variationen und Tipps

| Ziel | Code‑Snippet | Hinweis |
|------|--------------|---------|
| **Nur fett** | `new Font("Arial", 12, WebFontStyle.Bold)` | Verwenden Sie ein einzelnes Flag, wenn Sie kein Kursiv benötigen. |
| **Fett, kursiv, unterstrichen** | `new Font("Arial", 12, WebFontStyle.Bold \| WebFontStyle.Italic \| WebFontStyle.Underline)` | Kombinieren Sie beliebig viele Stile. |
| **Dynamische Größe** | `var size = 14; var font = new Font("Times New Roman", size, WebFontStyle.Italic);` | Sie können die Größe zur Laufzeit berechnen. |
| **Benutzerdefinierte Schriftfamilie** | `new Font("MyCustomFont", 10, WebFontStyle.Bold)` | Stellen Sie sicher, dass die benutzerdefinierte Schrift dem Rendering‑Engine zur Verfügung steht (z. B. über `@font-face`). |

### Pro‑Tipp zur Performance

Das Erzeugen vieler `Font`‑Objekte innerhalb einer engen Schleife kann die Leistung mindern. Zwischenspeichern Sie häufig genutzte Schriften in einem Dictionary und verwenden Sie sie erneut:

```csharp
var fontCache = new Dictionary<string, Font>();
string key = "Arial_12_BoldItalic";

if (!fontCache.TryGetValue(key, out var cachedFont))
{
    cachedFont = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
    fontCache[key] = cachedFont;
}
```

## Vollständiges ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können. Es demonstriert den gesamten Ablauf vom Importieren des Namespace bis zum Rendern des formatierten Textes.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // Step 1: Import Aspose.Html.Drawing (already done via using statements)

        // Step 2: Create a Font that combines bold and italic
        var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);

        // Step 3: Build a simple HTML document
        var document = new HTMLDocument();
        var paragraph = document.CreateElement("p");
        paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
        document.Body.AppendChild(paragraph);

        // Apply font settings
        paragraph.Style.FontFamily = font.Family;
        paragraph.Style.FontSize = $"{font.Size}pt";
        paragraph.Style.FontWeight = "bold";
        paragraph.Style.FontStyle = "italic";

        // Optional: Render to PNG for visual verification
        using (var renderer = new ImageRenderer())
        {
            renderer.Render(document, "output.png");
        }

        // Save HTML for manual inspection
        document.Save("styled.html");

        Console.WriteLine("Styled document generated: styled.html and output.png");
    }
}
```

**Erwartete Ausgabe**

- `styled.html` zeigt einen Absatz mit Arial 12 pt, fett und kursiv.
- `output.png` enthält ein Bild desselben formatierten Absatzes.

## Fazit

Sie wissen jetzt, wie Sie **Schriftartenstile** in C# mit dem Aspose.HTML **c#‑Schriftkonstruktor** kombinieren können. Durch **Festlegen der Schriftfamilie**, **Festlegen der Schriftgröße in C#** und das Übergeben einer bitweisen ODER‑Verknüpfung von `WebFontStyle`‑Flags können Sie **fetten kursiven Text** (oder jede andere Kombination) mit minimalem Code erzeugen. Wenden Sie dasselbe Muster auf andere Elemente an, speichern Sie Schriften für die Performance zwischen und erweitern Sie den Ansatz bei Bedarf um Unterstreichung oder Durchstreichung.

Bereit, mehr zu entdecken? Versuchen Sie:

- Verwendung von `WebFontStyle.Underline`, um **Schriftunterstreichung festzulegen**.
- Laden benutzerdefinierter Web‑Schriften mit `@font-face` und deren Anwendung über denselben Konstruktor.
- Rendern von PDFs anstelle von Bildern, indem Sie `ImageRenderer` durch `PdfRenderer` ersetzen.

Viel Spaß beim Programmieren und genießen Sie die Flexibilität, Text programmgesteuert in C# zu formatieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [HTML‑Dokument in C# erstellen – Fettschrift‑Kursiv‑Text mit benutzerdefinierter Schrift](/html/english/net/html-document-manipulation/create-html-document-c-bold-italic-text-with-custom-font/)
- [HTML‑Dokument in C# erstellen – Rendern zu PNG mit fetter kursiver Schrift](/html/english/net/rendering-html-documents/create-html-document-c-render-to-png-with-bold-italic-font/)
- [HTML als PDF in C# speichern – Vollständiger Leitfaden mit Schriftarten](/html/indonesian/net/html-extensions-and-conversions/save-html-as-pdf-in-c-complete-guide-with-fonts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}