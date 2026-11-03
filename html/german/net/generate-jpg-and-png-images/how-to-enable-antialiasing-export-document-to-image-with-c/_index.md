---
category: general
date: 2026-04-06
description: Erfahren Sie, wie Sie Antialiasing aktivieren, Bildbreite und -höhe festlegen
  und das Dokument in C# als PNG speichern – ein kurzer Leitfaden zum Exportieren
  von Dokumenten als Bild.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: de
og_description: Wie man Antialiasing aktiviert, wenn man ein Dokument als Bild exportiert.
  Dieser Leitfaden zeigt, wie man die Bildbreite festlegt, die Bildhöhe einstellt
  und das Dokument als PNG speichert.
og_title: Wie man Kantenglättung aktiviert – Dokument als Bild exportieren
tags:
- C#
- ImageRendering
- Antialiasing
title: Wie man Antialiasing aktiviert – Dokument in Bild exportieren mit C#
url: /de/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Antialiasing aktiviert – Dokument in Bild exportieren in C#

Haben Sie sich schon einmal gefragt, **wie man Antialiasing** aktiviert, während man ein Dokument in ein Bild umwandelt? Vielleicht haben Sie einen schnellen `Save`‑Aufruf ausprobiert und das Ergebnis sah gezackt aus, besonders bei diagonalen Linien. Die gute Nachricht: Sie benötigen keinen Grafikzauberer – nur ein paar Zeilen C# und die richtigen Optionen.

In diesem Tutorial gehen wir Schritt für Schritt durch das Festlegen der Bildbreite, das Festlegen der Bildhöhe und schließlich das **Speichern des Dokuments als PNG**, sodass Sie **ein Dokument in ein Bild exportieren** können, mit glatten Kanten. Am Ende haben Sie ein sofort einsatzbereites Snippet, das ein scharfes 800 × 600 PNG mit aktiviertem Antialiasing erzeugt.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)  
- Ein Verweis auf eine Rendering‑Bibliothek, die `ImageRenderingOptions` unterstützt (z. B. Aspose.Words, Syncfusion oder jede API, die ähnliche Eigenschaften bereitstellt)  
- Grundlegendes Verständnis der C#‑Syntax  

Keine aufwändige Einrichtung – einfach das NuGet‑Paket hinzufügen und loslegen.

## Schritt 1: Rendering‑Bibliothek installieren

Zuerst das Paket in Ihr Projekt einbinden. Wenn Sie Aspose.Words verwenden, führen Sie aus:

```bash
dotnet add package Aspose.Words
```

> **Pro‑Tipp:** Halten Sie die Bibliotheksversion aktuell; das neueste Release (Stand April 2026) enthält Performance‑Optimierungen für Antialiasing.

## Schritt 2: Dokument‑Objekt erstellen

Laden oder erstellen Sie das Dokument, das Sie rendern möchten. Hier ein minimales Beispiel, das ein einseitiges Dokument mit einem einfachen Absatz erzeugt:

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

Die Klasse `Document` ist der Einstiegspunkt; alles, was Sie rendern, stammt daraus. In realen Projekten würden Sie wahrscheinlich ein vorhandenes .docx laden:

```csharp
// Document doc = new Document("input.docx");
```

## Schritt 3: Rendering‑Optionen festlegen (Breite, Höhe, Antialiasing)

Jetzt beantworten wir die Kernfrage: **wie man Antialiasing aktiviert**. Das Objekt `ImageRenderingOptions` ermöglicht das Umschalten der Glättung und die Steuerung der Abmessungen.

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

Beachten Sie die Kommentare: Sie erwähnen ausdrücklich **set image width**, **set image height** und **UseAntialiasing** – die drei wichtigsten Stellschrauben, wenn Sie ein hochwertiges PNG wollen.

### Warum Antialiasing wichtig ist

Ohne Antialiasing erscheinen diagonale Linien und Kurven treppenartig, weil der Renderer jedes Pixel nur als an oder aus betrachtet. Durch das Aktivieren werden Randpixel gemischt, was eine visuelle Weichzeichnung erzeugt, die dem Ergebnis eines Bildeditors ähnelt. Der Nachteil ist ein minimaler Anstieg der Verarbeitungszeit, der für die meisten UI‑bezogenen Exporte jedoch vernachlässigbar ist.

## Schritt 4: Dokument als PNG speichern (Dokument in Bild exportieren)

Mit den vorbereiteten Optionen können wir nun **das Dokument als PNG speichern**. Die `Save`‑Methode erhält den Dateipfad und die zuvor konfigurierten Optionen.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Das war’s – Ihr Dokument ist jetzt ein 800 × 600 PNG mit angewendetem Antialiasing. Öffnen Sie `output.png` und Sie sehen klaren Text, glatte Linien und keine gezackten Artefakte.

### Ergebnis überprüfen

Sie können die Datei schnell in einem Bildbetrachter prüfen. Achten Sie auf:

- Korrekte Abmessungen (800 × 600)  
- Keine sichtbaren Treppeneffekte an Text oder Formen  
- Einen transparenten Hintergrund, falls Ihr Dokument keine Hintergrundfarbe enthält (die meisten Bibliotheken verwenden standardmäßig Weiß)

Falls das Bild gezackt aussieht, prüfen Sie, ob `UseAntialiasing = true` nicht an anderer Stelle überschrieben wird.

## Schritt 5: Sonderfälle & Varianten

### Ausgabeformat ändern

Möchten Sie JPEG statt PNG? Ändern Sie einfach die Dateierweiterung und passen Sie optional die Kompression an:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Mehrere Seiten exportieren

Wenn das Quell‑Dokument mehrere Seiten hat, erzeugt der Renderer standardmäßig separate Bilddateien pro Seite. Sie können über die Seiten iterieren:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### In einen Stream speichern (z. B. HTTP‑Antwort)

Wenn Sie eine Web‑API bauen, möchten Sie das PNG vielleicht direkt zurückgeben:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Vollständiges Beispiel

Unten finden Sie das komplette, copy‑paste‑bereite Programm, das alle besprochenen Schritte integriert:

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

Wenn Sie dieses Programm ausführen, entsteht `output.png` im Ordner der ausführbaren Datei. Öffnen Sie es, und Sie sehen ein glattes 800 × 600 PNG – genau das, was wir erreichen wollten.

## Häufige Fragen & Fehlersuche

- **Was tun, wenn das Bild unscharf aussieht?**  
  Unscharfheit kann auftreten, wenn Sie eine kleine Quellseite hochskalieren. Halten Sie die Quellseitengröße nahe an den Zielabmessungen oder erhöhen Sie die DPI über `imageOptions.Resolution` (z. B. `Resolution = 300`).

- **Funktioniert das auch unter .NET Framework?**  
  Ja. Die gleiche API ist im klassischen Framework vorhanden; Sie müssen nur die passende DLL referenzieren.

- **Kann ich die Hintergrundfarbe steuern?**  
  Absolut. Setzen Sie `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` vor dem Speichern.

- **Wird Antialiasing hardwarebeschleunigt?**  
  Die meisten Bibliotheken führen Software‑Antialiasing aus. Wenn Sie GPU‑Beschleunigung benötigen, suchen Sie nach einer Rendering‑Engine, die dies explizit unterstützt.

## Fazit

Wir haben **wie man Antialiasing aktiviert** beim **Export eines Dokuments in ein Bild** behandelt, das **Festlegen der Bildbreite** und **Bildhöhe** durchgegangen und Ihnen die genauen Schritte gezeigt, um **ein Dokument als PNG zu speichern**. Das obige Snippet ist produktionsreif, und Sie können es jetzt leicht auf JPEG, mehrseitige PDFs oder das direkte Streamen des Bildes zu einem Client anpassen.

Als Nächstes könnten Sie Wasserzeichen hinzufügen, die DPI für druckfähige Ausgaben anpassen oder diese Logik in einen ASP.NET Core‑Endpunkt integrieren. Die gleichen Prinzipien gelten – nur den Dateipfad durch einen Response‑Stream ersetzen.

Viel Spaß beim Coden und genießen Sie die scharfen, antialiased Bilder!

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}