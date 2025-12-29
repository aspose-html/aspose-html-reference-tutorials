---
category: general
date: 2025-12-29
description: Erstellen Sie ein HTML‑Dokument in C# und lernen Sie, wie Sie die Schriftfamilie
  und die Schriftgröße festlegen, dann das HTML als PDF speichern oder HTML in PDF
  konvertieren mit Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: de
og_description: Erstellen Sie ein HTML‑Dokument in C# und sehen Sie sofort, wie Sie
  die Schriftfamilie festlegen, die Schriftgröße einstellen und das HTML dann als
  PDF speichern oder HTML in PDF konvertieren mit Aspose.HTML.
og_title: HTML‑Dokument erstellen – formatierter Text & PDF‑Export
tags:
- aspnet
- csharp
- pdf-generation
title: HTML-Dokument mit formatiertem Text erstellen und als PDF exportieren – Vollständige
  Anleitung
url: /de/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-Dokument mit formatiertem Text erstellen und als PDF exportieren

Haben Sie schon einmal **HTML-Dokument** on the fly erstellen und in ein PDF umwandeln müssen, ohne Ihren C#‑Code zu verlassen? Vielleicht bauen Sie eine Reporting‑Engine, einen Rechnungsgenerator oder einfach eine Schnellvorschau für Benutzer. Die gute Nachricht: Mit ein paar Zeilen und Aspose.HTML können Sie das erledigen und haben die volle Kontrolle über Schriftfamilie, Schriftgröße und sogar fette‑kursiv‑Formatierung.

In diesem Tutorial führen wir Sie durch den gesamten Prozess – vom Erzeugen eines HTML-Dokuments im Speicher bis zum Speichern als PDF‑Datei. Am Ende wissen Sie genau, wie Sie **Schriftfamilie festlegen**, **Schriftgröße festlegen** und **HTML als PDF speichern** (auch bekannt als **HTML in PDF konvertieren**) mit einem sauberen, produktionsbereiten Code‑Beispiel.

## Was Sie benötigen

- .NET 6+ (die API funktioniert sowohl mit .NET Core als auch mit .NET Framework)  
- Aspose.HTML für .NET NuGet‑Paket (`Aspose.Html`) – Installation via `dotnet add package Aspose.Html`  
- Ein Ordner auf dem Datenträger, in den das erzeugte PDF geschrieben werden kann  

Keine zusätzlichen HTML-Templates, keine externen Konverter, nur reines C#.

![Illustration zur Erstellung eines HTML-Dokuments](/images/create-html-document.png){alt="Beispiel für die Erstellung eines HTML-Dokuments"}

## Schritt 1: HTML-Dokument erstellen

Zuerst benötigen wir ein leeres HTML‑Dokument‑Objekt. Stellen Sie sich das wie eine leere Leinwand vor, auf der Sie später Ihren formatierten Absatz malen.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Warum das wichtig ist:** `HTMLDocument` liefert Ihnen eine DOM‑ähnliche Struktur, die Sie programmgesteuert manipulieren können. Sie müssen bis zum Schluss nicht mehr mit rohen Zeichenketten oder Datei‑I/O arbeiten.

## Schritt 2: Absatz hinzufügen und Schriftfamilie & Schriftgröße festlegen

Jetzt erstellen wir ein `<p>`‑Element, fügen Text ein und definieren ausdrücklich die Schriftfamilie und -größe. Hier kommen die Schlüsselwörter **set font family** und **set font size** zum Einsatz.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro‑Tipp:** Wenn Sie ein Web‑sicheres Fallback benötigen, können Sie eine kommagetrennte Liste wie `"Arial, Helvetica, sans-serif"` angeben; der Browser (oder Aspose) wählt die zuerst verfügbare Schrift aus.

## Schritt 3: Fette und kursive Formatierung mit WebFontStyle‑Flags anwenden

Aspose.HTML stellt ein praktisches Enum `WebFontStyle` bereit, mit dem Sie Stile über ein bitweises OR kombinieren können. Lassen Sie uns den Text sowohl fett **als auch** kursiv formatieren.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Was im Hintergrund passiert:** Die Eigenschaft `FontStyle` wird in die CSS‑Deklarationen `font-weight` und `font-style` übersetzt. Durch das OR‑Verknüpfen der Flags vermeiden wir das Schreiben von zwei separaten CSS‑Zeilen.

## Schritt 4: HTML in PDF konvertieren (HTML als PDF speichern)

Der letzte Schritt ist die eigentliche Konvertierung. Mit einem einzigen Aufruf von `Save` rendert Aspose.HTML das DOM und schreibt eine PDF‑Datei auf die Festplatte. Damit werden sowohl die Anforderungen **save html as pdf** als auch **convert html to pdf** erfüllt.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Erwartetes Ergebnis:** Öffnen Sie `styled.pdf` und Sie sehen einen einzelnen Absatz mit dem Text „Bold & Italic text“ in 18‑px Arial, fett und kursiv dargestellt. Die PDF‑Abmessungen entsprechen einer Standard‑A4‑Seite, und der Text ist auswählbar – dank Vektor‑Rendering.

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie das komplette, sofort ausführbare Programm:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Ausführen des Codes

1. Installieren Sie das Aspose.HTML NuGet‑Paket:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Ersetzen Sie `C:\Temp\styled.pdf` durch einen Ordner, für den Sie Schreibrechte haben.  
3. Bauen und ausführen: `dotnet run`.  

Sie sollten die Konsolenausgabe sehen, die den Dateipfad bestätigt, und das PDF wird den formatierten Absatz enthalten.

## Häufige Fragen & Sonderfälle

- **Was, wenn ich eine benutzerdefinierte Web‑Schrift benötige?**  
  Laden Sie die Schrift mit `HTMLFontFaceRule` oder referenzieren Sie eine entfernte `@font-face`‑CSS‑Datei, bevor Sie den Absatz erstellen.

- **Kann ich vor der Konvertierung Bilder hinzufügen?**  
  Absolut. Verwenden Sie `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` und setzen Sie `img.Source` auf einen lokalen Pfad oder ein Data‑URI.

- **Wie sieht es mit mehrseitigen PDFs aus?**  
  Fügen Sie weitere Elemente (Tabellen, Divs usw.) hinzu und Aspose.HTML paginiert automatisch, sobald der Inhalt die Seitenhöhe überschreitet.

- **Gibt es eine Möglichkeit, PDF‑Metadaten zu steuern?**  
  Übergeben Sie eine Instanz von `PdfSaveOptions` und setzen Sie Eigenschaften wie `Author`, `Title` oder `PdfAConformanceLevel`.

## Zusammenfassung

Wir haben behandelt, wie man in C# **HTML‑Dokument** erstellt, **Schriftfamilie** festlegt, **Schriftgröße** festlegt, fette‑kursive Stile anwendet und schließlich **HTML als PDF speichert** – also effektiv **HTML in PDF konvertiert** mit Aspose.HTML. Der Code‑Abschnitt ist kurz genug, um in jedes .NET‑Projekt eingefügt zu werden, und gleichzeitig umfassend genug, um als solide Grundlage für komplexere Reporting‑Szenarien zu dienen.

## Nächste Schritte

- Experimentieren Sie mit CSS‑Klassen für wiederverwendbare Stile.  
- Kombinieren Sie mehrere Absätze, Tabellen und Bilder, um umfangreichere PDFs zu erstellen.  
- Untersuchen Sie die PDF/A‑Konformität, falls Sie archivierungsfähige Dokumente benötigen.  

Passen Sie Schrift, Größe oder Farben nach Belieben an – es gibt keine Grenze dafür, was Sie programmatisch erzeugen können. Viel Spaß beim Coden, und möge Ihr PDF stets genau so rendern, wie Sie es sich vorstellen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}