---
category: general
date: 2026-09-10
description: Erfahren Sie, wie Sie HtmlSaveOptions in C# verwenden, um Web‑Font‑Stile
  zu steuern und HTML‑Dateien mit Aspose.HTML zu speichern. Vollständiges Codebeispiel
  und praktische Tipps inklusive.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: de
lastmod: 2026-09-10
og_description: Wie man HtmlSaveOptions in C# verwendet, um fette und kursive Web‑Font‑Stile
  beim Speichern von HTML mit Aspose.HTML zu aktivieren. Folgen Sie dem vollständigen
  Beispiel und den Best‑Practice‑Tipps.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Wie man HtmlSaveOptions in C# mit Aspose.HTML verwendet – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Wie man HtmlSaveOptions in C# mit Aspose.HTML verwendet
url: /de/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HtmlSaveOptions in C# mit Aspose.HTML verwendet

Wenn Sie steuern müssen, wie Aspose.HTML ein HTML‑Dokument speichert, **ist das Erlernen der Verwendung von HtmlSaveOptions unerlässlich**. Dieses Tutorial zeigt Ihnen Schritt für Schritt, wie Sie HtmlSaveOptions verwenden, um fette und kursive Web‑Font‑Stile beim Speichern eines Dokuments zu aktivieren.

Die Aspose‑HTML‑Bibliothek bietet eine umfangreiche API zum Laden, Manipulieren und Exportieren von HTML‑Inhalten. Am Ende dieses Leitfadens können Sie:

* Eine vorhandene HTML‑Datei in ein `HTMLDocument` laden.
* `HtmlSaveOptions` konfigurieren, um bestimmte `WebFontStyle`‑Flags anzuwenden.
* Das modifizierte Dokument an einem neuen Ort oder in einen Stream speichern.
* Die Lösung für andere Schriftstile, benutzerdefiniertes CSS und Fehlerbehandlung erweitern.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* .NET 6.0 oder höher installiert.
* Eine gültige Lizenz für **Aspose.HTML for .NET** (die kostenlose Testversion funktioniert für dieses Beispiel).
* Visual Studio 2022 (oder jede C#‑IDE), um den Code zu kompilieren und auszuführen.

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.HTML` hinaus erforderlich.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie ein neues **Console‑App**‑Projekt und fügen Sie das Aspose.HTML‑NuGet‑Paket hinzu:

```bash
dotnet add package Aspose.HTML
```

Fügen Sie dann am Anfang von `Program.cs` die erforderlichen Namespaces ein:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Diese Namespaces stellen die Typen `HTMLDocument`, `HtmlSaveOptions` und `WebFontStyle` bereit, die Sie im gesamten Tutorial verwenden werden.

## Schritt 2: Quell‑HTML‑Dokument laden

Der erste Schritt besteht darin, das zu verarbeitende HTML zu lesen. Ersetzen Sie `"YOUR_DIRECTORY/input.html"` durch den tatsächlichen Pfad zu Ihrer Datei.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` analysiert das Markup, erstellt einen DOM‑Baum und macht ihn zur Manipulation bereit. Wenn die Datei nicht existiert, wird eine Ausnahme ausgelöst, daher sollten Sie diesen Aufruf in Produktionscode in einen try‑catch‑Block einbetten.

## Schritt 3: HtmlSaveOptions erstellen und konfigurieren

`HtmlSaveOptions` ermöglicht es Ihnen, den Speicherprozess fein abzustimmen. Um fette und kursive Web‑Font‑Stile zu aktivieren, kombinieren Sie die entsprechenden `WebFontStyle`‑Flags mit dem bitweisen ODER‑Operator (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Warum WebFontStyle konfigurieren?

Wenn Sie ein HTML‑Dokument exportieren, kann Aspose.HTML Web‑Fonts einbetten, die dem ursprünglichen Styling entsprechen. Durch das Setzen von `WebFontStyle` teilen Sie dem Exporter mit, welche Schriftvarianten eingebunden werden sollen. Dies reduziert die endgültige Dateigröße, wenn Sie nur bestimmte Stile benötigen, und stellt sicher, dass die gerenderte Ausgabe dem Original entspricht.

#### Häufige Varianten

| Gewünschter Stil | Entsprechendes `WebFontStyle`‑Flag |
|------------------|------------------------------------|
| Normal (regular) | `WebFontStyle.Regular` |
| Fett | `WebFontStyle.Bold` |
| Kursiv | `WebFontStyle.Italic` |
| Fett + Kursiv | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Alle Varianten | `WebFontStyle.All` |

Sie können jede Kombination verwenden, die zu Ihrem Szenario passt.

## Schritt 4: Dokument mit den konfigurierten Optionen speichern

Schreiben Sie nun das Dokument in eine neue Datei. Die Methode `Save` akzeptiert den Zielpfad und die vorbereitete `HtmlSaveOptions`‑Instanz.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Falls Sie in einen Memory‑Stream schreiben müssen (z. B. um die Datei über HTTP zu senden), verwenden Sie die Überladung, die ein `Stream`‑Objekt akzeptiert:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Schritt 5: Ergebnis überprüfen

Öffnen Sie `output.html` in einem Browser oder prüfen Sie die Datei mit einem Texteditor. Sie sollten sehen, dass der `<style>`‑Block nun `@font-face`‑Regeln für sowohl fette als auch kursive Varianten aller im Originaldokument referenzierten Web‑Fonts enthält.

**Erwarteter Ausgabeschnipsel:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Wenn das ursprüngliche HTML eine Schriftfamilie referenzierte, die nur ein reguläres Gewicht hatte, wird Aspose.HTML nur diese Datei einbinden und dabei die `WebFontStyle`‑Konfiguration berücksichtigen.

## Fortgeschritten: HtmlSaveOptions mit zusätzlichen Funktionen verwenden

### 5.1 Steuerung der CSS‑Einbettung

Sie können entscheiden, ob CSS inline eingebettet, externe Links beibehalten oder alles eingebettet werden soll:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Speichern mit einer bestimmten Kodierung

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Umgang mit großen Dokumenten

Bei sehr großen HTML‑Dateien sollten Sie das Ausgabestreaming in Betracht ziehen, um einen hohen Speicherverbrauch zu vermeiden:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Best Practices für Fehlerbehandlung

Umwickeln Sie den gesamten Workflow mit einem try‑catch‑Block und protokollieren Sie die Ausnahmedetails. So wird sichergestellt, dass alle I/O‑ oder Parsing‑Fehler erfasst werden:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Profi‑Tipp: HtmlSaveOptions für mehrere Saves wiederverwenden

Wenn Sie mehrere Dokumente mit derselben Schriftstil‑Konfiguration speichern müssen, erstellen Sie eine einzelne `HtmlSaveOptions`‑Instanz und verwenden Sie sie erneut. Dies reduziert den Overhead bei der Objektallokation und garantiert konsistente Ausgaben.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Vollständiges ausführbares Beispiel

Unten finden Sie das vollständige Programm, das alle besprochenen Schritte integriert. Kopieren Sie es in `Program.cs` und führen Sie es nach Anpassung der Dateipfade aus.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Erwartete Konsolenausgabe

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Öffnen Sie das erzeugte `output.html`, um zu bestätigen, dass fette und kursive Web‑Font‑Stile vorhanden sind.

## Fazit

Sie wissen jetzt **wie man HtmlSaveOptions verwendet**, um das Einbetten von Web‑Fonts, die CSS‑Verarbeitung und die Kodierung beim Speichern von HTML mit der Aspose‑HTML‑Bibliothek in C# zu steuern. Durch das Konfigurieren der `WebFontStyle`‑Flags können Sie die Ausgabe so anpassen, dass nur die benötigten Schriftvarianten eingebunden werden, was die Leistung verbessert und die Dateigröße reduziert.

Ab hier können Sie weitere Eigenschaften von `HtmlSaveOptions` wie `ImageSavingMode`, `JavaScriptSavingMode` erkunden oder mehrere Optionen für komplexe Konvertierungspipelines kombinieren. Experimentieren Sie mit dem Speichern in Streams für Web‑APIs oder integrieren Sie den Workflow in ein größeres Dokument‑Generierungssystem.

---

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML mit Aspose.Html speichert – Vollständiger C#‑Leitfaden](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Wie man Aspose verwendet, um HTML in PNG in C# zu rendern](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Wie man Aspose verwendet, um HTML in PNG zu rendern – Schritt‑für‑Schritt‑Leitfaden](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}