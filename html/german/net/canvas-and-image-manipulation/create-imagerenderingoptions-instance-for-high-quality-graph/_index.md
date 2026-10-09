---
category: general
date: 2026-10-09
description: Erstellen Sie eine ImageRenderingOptions‑Instanz, um Antialiasing zu
  aktivieren und die Grafikrendering‑Qualität in .NET‑Anwendungen zu verbessern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: de
lastmod: 2026-10-09
og_description: Erstellen Sie eine ImageRenderingOptions‑Instanz, um Antialiasing
  zu aktivieren und ein glatteres Grafik‑Rendering in .NET zu erreichen. Folgen Sie
  der Schritt‑für‑Schritt‑Anleitung.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Erstelle eine ImageRenderingOptions‑Instanz – steigere die Grafikqualität
  in .NET
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
title: Erstelle eine ImageRenderingOptions‑Instanz für die hochwertige Grafikdarstellung
url: /de/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen einer ImageRenderingOptions‑Instanz für hochqualitative Grafikdarstellung

Wenn Sie **eine ImageRenderingOptions‑Instanz erstellen** müssen, um glattere Grafiken zu erzeugen, zeigt Ihnen dieser Leitfaden genau, wie das geht. Durch die Konfiguration von Antialiasing entfernen Sie gezackte Kanten und erhalten professionelle Ausgaben ohne zusätzliche Bibliotheken.

Sie lernen, wie man `ImageRenderingOptions` instanziiert, Antialiasing aktiviert und die Optionen an eine Rendering‑Engine wie Aspose.Slides oder System.Drawing anhängt. Das Tutorial geht davon aus, dass Sie mit grundlegender C#‑Syntax vertraut sind und eine .NET‑Entwicklungsumgebung bereitsteht.

## Voraussetzungen

- .NET 6.0 oder höher (die API ist in .NET Standard 2.0+ verfügbar)
- Ein Verweis auf die Assembly, die `ImageRenderingOptions` enthält (z. B. `Aspose.Slides.NET`)
- Eine IDE wie Visual Studio 2022 oder VS Code mit der C#‑Erweiterung
- Grundlegendes Verständnis von Grafik‑Rendering‑Pipelines

## Schritt 1: ImageRenderingOptions‑Instanz erstellen

Der erste Schritt besteht darin, ein neues `ImageRenderingOptions`‑Objekt zu erstellen. Dieses Objekt dient als Container für alle rendering‑bezogenen Flags.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Durch das Erstellen der Instanz erhalten Sie die volle Kontrolle darüber, wie Vektorgrafiken gerastert werden. Sie können später bestimmte Funktionen wie Antialiasing, Text‑Rendering‑Modus oder Bildkompression aktivieren oder deaktivieren.

## Schritt 2: Antialiasing aktivieren, um das Grafik‑Rendering zu verbessern

Antialiasing glättet den Übergang zwischen Pixel­farben und reduziert den Treppeneffekt bei diagonalen oder gekrümmten Linien. Die ältere Eigenschaft `SmoothingMode` ist veraltet; `UseAntialiasing` ist der moderne, empfohlene Ansatz.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Durch das Setzen von `UseAntialiasing` auf `true` wird die Rendering‑Engine angewiesen, während der Rasterung einen hochqualitativen Filter anzuwenden. Dieses Flag wirkt sowohl bei Vektorformen als auch bei Text und sorgt für eine konsistente visuelle Treue über die Folie hinweg.

### Warum nicht SmoothingMode verwenden?

`SmoothingMode` gehört zu `System.Drawing.Graphics` und wirkt nur auf GDI+-Zeichnungen. Wenn Sie Folien oder PDFs über Aspose.Slides rendern, ist `ImageRenderingOptions.UseAntialiasing` das einzige Flag, das die Bibliothek berücksichtigt. Die Verwendung der neueren Eigenschaft garantiert Zukunftskompatibilität und eliminiert unerwartetes Verhalten auf Nicht‑Windows‑Plattformen.

## Schritt 3: Die Optionen auf einen Rendering‑Vorgang anwenden

Nachdem die `ImageRenderingOptions`‑Instanz konfiguriert ist, übergeben Sie sie an die Methode, die das eigentliche Rendering durchführt. Unten finden Sie ein vollständiges, ausführbares Beispiel, das eine Präsentation lädt, die erste Folie als PNG rendert und das Bild mit aktiviertem Antialiasing speichert.

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

**Erklärung der wichtigsten Zeilen**

- `new Presentation("sample.pptx")` lädt die Quelldatei.  
- `GetThumbnail(2f, 2f, imgOptions)` erstellt ein Bitmap der Folie mit dem Doppelten der Standard‑DPI und wendet dabei die von Ihnen konfigurierten Rendering‑Optionen an.  
- Das resultierende PNG (`slide1_antialiased.png`) zeigt glatte Kurven und Text dank `UseAntialiasing = true`.

### Erwartete Ausgabe

Öffnen Sie `slide1_antialiased.png` in einem beliebigen Bildbetrachter. Im Vergleich zu einem Rendering ohne Antialiasing werden Sie Folgendes bemerken:

- Abgerundete Ecken von Formen erscheinen ohne gezackte Schritte.  
- Textränder sind scharf, aber gleichzeitig weich, wodurch pixelige Artefakte eliminiert werden.  
- Die gesamte visuelle Qualität entspricht dem, was Sie in der ursprünglichen PowerPoint‑Ansicht sehen würden.

## Schritt 4: Optionale Anpassungen für fortgeschrittenes Grafik‑Rendering

Während Antialiasing das am häufigsten genutzte Flag ist, bietet `ImageRenderingOptions` zusätzliche Steuerungen:

| Eigenschaft | Zweck | Typischer Wert |
|-------------|-------|----------------|
| `UseHighQualityRendering` | Aktiviert Sub‑Pixel‑Rendering für Text | `true` |
| `PixelFormat` | Bestimmt die Farbtiefe des Ausgabebitmaps | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Legt das Zielformat des Bildes fest (PNG, JPEG usw.) | `Export.SaveFormat.Png` |

Sie können diese Einstellungen verketten:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Pro‑Tipp:** Beim Erzeugen von großformatigen PDFs oder hochauflösenden PNGs sollten Sie `UseAntialiasing` aktiviert lassen, aber die Speichernutzung im Auge behalten. Antialiasing erhöht den Verarbeitungsaufwand, was auf schwächeren Rechnern auffallen kann.

## Häufige Fallstricke und wie man sie vermeidet

1. **Vergessen, die Optionen zu übergeben** – Rendering‑Methoden, die `ImageRenderingOptions` akzeptieren, ignorieren Antialiasing, wenn Sie die Überladung ohne den Options‑Parameter aufrufen. Verwenden Sie stets die drei‑Parameter‑Version von `GetThumbnail` oder die entsprechende Methode.  
2. **Mischen von SmoothingMode mit ImageRenderingOptions** – Das Setzen von `Graphics.SmoothingMode` hat keinen Einfluss auf das Rendering von Aspose.Slides. Verlassen Sie sich ausschließlich auf `UseAntialiasing`.  
3. **Verwendung einer veralteten Bibliotheksversion** – `ImageRenderingOptions` wurde in Aspose.Slides 20.5 eingeführt. Stellen Sie sicher, dass Ihr NuGet‑Paket aktuell ist; andernfalls könnte die Klasse fehlen oder die Eigenschaft `UseAntialiasing` nicht besitzen.

## Fazit

Sie wissen jetzt, wie man **eine ImageRenderingOptions‑Instanz erstellt**, Antialiasing aktiviert und die Optionen in einen Rendering‑Workflow integriert. Dieser Ansatz garantiert ein glatteres Grafik‑Rendering, ersetzt die veraltete `SmoothingMode`‑Einstellung und funktioniert konsistent über .NET‑Plattformen hinweg.

Ab hier können Sie weitere Rendering‑Flags erkunden, mit unterschiedlichen DPI‑Skalen experimentieren oder die Technik mit dem PDF‑Export für druckfähige Assets kombinieren. Das Beherrschen von `ImageRenderingOptions` ist ein Grundpfeiler der hochpräzisen .NET‑Grafikprogrammierung.

---

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [PNG aus HTML erstellen – Vollständiger C# Rendering‑Leitfaden](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Bild aus HTML in C# erstellen – Vollständiger Schritt‑für‑Schritt‑Leitfaden](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Canvas‑Text erstellen – Vollständiger Leitfaden zum Rendern von Text auf Bildern](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}