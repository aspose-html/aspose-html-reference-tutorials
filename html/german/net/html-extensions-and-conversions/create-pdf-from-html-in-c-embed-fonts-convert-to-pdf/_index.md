---
category: general
date: 2026-03-29
description: Erstellen Sie PDF aus HTML mit Aspose.HTML in C#. Erfahren Sie, wie Sie
  Schriftarten einbetten, HTML in PDF konvertieren und HTML in wenigen Schritten als
  PDF speichern.
draft: false
keywords:
- create pdf from html
- how to embed font
- convert html to pdf
- save html as pdf
- how to create pdf
language: de
og_description: PDF aus HTML mit Aspose.HTML erstellen. Dieser Leitfaden zeigt, wie
  man Schriftarten einbettet, HTML in PDF konvertiert und HTML schnell als PDF speichert.
og_title: PDF aus HTML in C# erstellen – Schriftarten einbetten & in PDF konvertieren
tags:
- Aspose.HTML
- C#
- PDF generation
title: PDF aus HTML in C# erstellen – Schriftarten einbetten & in PDF konvertieren
url: /de/net/html-extensions-and-conversions/create-pdf-from-html-in-c-embed-fonts-convert-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF aus HTML in C# erstellen – Schriftarten einbetten & in PDF konvertieren

Haben Sie jemals **PDF aus HTML erstellen** müssen, waren sich aber nicht sicher, wie Sie Ihre benutzerdefinierten Schriftarten scharf halten? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn sie Web‑Inhalte in ein druckbares Format überführen. Die gute Nachricht: Aspose.HTML macht es mühelos: Sie können eine Web‑Font einbetten, HTML in PDF konvertieren und sogar **HTML als PDF speichern** mit nur wenigen Zeilen C#.

In diesem Tutorial führen wir Sie durch alles, was Sie benötigen: Einrichten eines HTML‑Dokuments, **wie man Schriftarten einbettet**, Konvertieren des Markups in ein PDF und schließlich das Speichern des Ergebnisses. Am Ende haben Sie ein vollständiges, ausführbares Beispiel, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- .NET 6.0 oder höher (die API funktioniert auch mit .NET Core und .NET Framework)  
- Aspose.HTML für .NET (Sie können das kostenlose Test‑NuGet‑Paket holen: `Aspose.HTML`)  
- Eine benutzerdefinierte Schriftdatei (z. B. `OpenSans.woff2`) neben Ihrer ausführbaren Datei platzieren  
- Eine bevorzugte IDE – Visual Studio, Rider oder sogar VS Code reicht aus  

Keine zusätzliche Konfiguration, keine externen Dienste. Nur ein paar NuGet‑Referenzen und Sie sind startklar.

---

## Schritt 1: PDF aus HTML erstellen – HTMLDocument initialisieren

Zuerst benötigen Sie ein `HTMLDocument`‑Objekt, das die Seite repräsentiert, die Sie in ein PDF umwandeln möchten. Betrachten Sie es als eine virtuelle Browser‑Leinwand, in die Sie Styles, Skripte oder rohes HTML einfügen können.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Dom;

class FontStyleDemo
{
    static void Main()
    {
        // 1️⃣ Create a fresh HTMLDocument – this is the starting point for conversion
        var htmlDocument = new HTMLDocument();
```

> **Warum das wichtig ist:** Die `HTMLDocument`‑Klasse analysiert das Markup exakt wie ein Browser, sodass Layout, CSS und Schriftarten respektiert werden, bevor die PDF‑Engine übernimmt.

---

## Schritt 2: Wie man Schriftarten einbettet – Einen `<style>`‑Block mit @font-face hinzufügen

Das Einbetten einer benutzerdefinierten Schriftart ist ein zweistufiger Vorgang: Die Schrift mit `@font-face` deklarieren und dann auf die gewünschten Elemente anwenden. Unten erstellen wir das Style‑Element dynamisch und holen die Schriftdatei aus demselben Ordner wie die ausführbare Datei.

```csharp
        // 2️⃣ Build a <style> element that defines the custom web font and applies it
        var styleElement = htmlDocument.CreateElement("style");
        styleElement.InnerHTML = @"
            @font-face {
                font-family: 'OpenSans';
                src: url('OpenSans.woff2') format('woff2');
                font-weight: normal;
                font-style: normal;
            }
            body {
                font-family: 'OpenSans';
                font-weight: " + ((int)WebFontStyle.Bold) + @";
                font-style: " + ((int)WebFontStyle.Italic) + @";
            }";

        // Insert the style into the <head> so the browser engine sees it
        htmlDocument.Head.AppendChild(styleElement);
```

> **Pro‑Tipp:** Wenn Sie mehrere Gewichte oder Stile benötigen, fügen Sie zusätzliche `@font-face`‑Regeln mit `font-weight: 700` oder `font-style: italic` hinzu. Aspose.HTML berücksichtigt jede Variation beim Rendern.

---

## Schritt 3: Inhalt hinzufügen – Body mit HTML füllen

Jetzt, wo die Schrift bereit ist, fügen Sie etwas HTML in den Dokument‑Body ein. Alles, was Sie hier schreiben, wird mit der eingebetteten Schrift gerendert.

```csharp
        // 3️⃣ Add some content that will use the defined font style
        htmlDocument.Body.InnerHTML = "<p>Styled text using WebFontStyle.</p>";
```

> **Was, wenn Sie komplexeres Markup benötigen?** Sie können eine externe HTML‑Datei über `new HTMLDocument("file.html")` laden oder einen vollständigen DOM‑Baum programmgesteuert aufbauen – Aspose.HTML verarbeitet Tabellen, Bilder und sogar SVGs.

---

## Schritt 4: HTML in PDF konvertieren und HTML als PDF speichern

An diesem Punkt haben Sie ein vollständig gestyltes HTML‑Dokument im Speicher. Die nächste Zeile weist Aspose.HTML an, es direkt in eine PDF‑Datei zu rendern. Das ist das Kernstück von **convert html to pdf**.

```csharp
        // 4️⃣ Choose an output path and save the document as PDF
        string outputPath = "styled.pdf"; // change to your desired folder
        htmlDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

> **Warum `Save` funktioniert:** Im Hintergrund rastert Aspose.HTML das DOM auf eine PDF‑Leinwand, bewahrt Vektortext (so bleibt die Schrift auswählbar) und die Layout‑Treue. Es ist keine Zwischenschritt‑Bildkonvertierung nötig, was die Dateigröße gering hält.

---

## Schritt 5: Ergebnis überprüfen – PDF öffnen und Schrift prüfen

Nachdem Sie das Programm ausgeführt haben, suchen Sie `styled.pdf` und öffnen es in einem beliebigen PDF‑Viewer. Sie sollten den Absatz in *OpenSans* mit fetter und kursiver Formatierung sehen. Wenn der Text als Ersatzschrift erscheint, überprüfen Sie Folgendes:

1. `OpenSans.woff2` befindet sich im selben Ordner wie die ausführbare Datei.  
2. Der Dateiname stimmt exakt überein (Groß‑/Kleinschreibung auf Linux beachten).  
3. Die `src`‑URL in `@font-face` verwendet den korrekten relativen Pfad.

---

## Häufige Fallstricke beim **How to Create PDF** aus HTML

| Problem | Warum es passiert | Schnelle Lösung |
|-------|----------------|-----------|
| Schrift wird nicht angezeigt | Pfad‑Tippfehler oder fehlende Datei | Verwenden Sie einen absoluten Pfad (`Path.Combine(Directory.GetCurrentDirectory(), "OpenSans.woff2")`) |
| Text erscheint als Bild | `WebFontStyle`‑Enum falsch verwendet | Stellen Sie sicher, dass Sie wie gezeigt zu `int` casten, oder setzen Sie CSS `font-weight: bold;` direkt |
| PDF leer | Kein Inhalt in `Body.InnerHTML` | Überprüfen Sie, ob die HTML‑Zeichenkette nicht leer oder fehlerhaft ist |
| Große Dateigröße | Eingebettete hochauflösende Bilder | Bilder komprimieren oder das `Image`‑Element mit `srcset` verwenden |

---

## Bonus: HTML als PDF speichern mit benutzerdefinierter Seitengröße

Wenn Sie ein bestimmtes Seitenlayout benötigen – zum Beispiel A4 Hochformat – können Sie beim Aufruf von `Save` `PdfSaveOptions` übergeben. Dies zeigt eine weitere Möglichkeit, **save html as pdf** mit feiner Steuerung zu nutzen.

```csharp
using Aspose.Html.Rendering.Pdf;

// ...

        // 4️⃣ (Alternative) Save with custom page dimensions
        var pdfOptions = new PdfSaveOptions
        {
            PageSetup = new PageSetup
            {
                Width = 595,   // A4 width in points
                Height = 842   // A4 height in points
            }
        };
        htmlDocument.Save("styled-a4.pdf", pdfOptions);
```

> **Hinweis für Randfälle:** Wenn Sie die Seitengröße angeben, wird Aspose.HTML den Inhalt neu fließen lassen, um zu passen, was Zeilenumbrüche beeinflussen kann. Testen Sie mit Ihrem tatsächlichen HTML, um sicherzustellen, dass das Layout akzeptabel bleibt.

---

## Vollständiges funktionierendes Beispiel (zum Kopieren‑Einfügen bereit)

Unten finden Sie das gesamte Programm, bereit zum Kompilieren. Legen Sie einfach Ihre `OpenSans.woff2`‑Datei neben das `.csproj`, installieren das Aspose.HTML‑NuGet‑Paket und klicken **Run**.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Dom;
using Aspose.Html.Rendering.Pdf; // Needed for PdfSaveOptions (optional)

class FontStyleDemo
{
    static void Main()
    {
        // Step 1 – Initialize the HTML document
        var htmlDocument = new HTMLDocument();

        // Step 2 – Embed the custom font via @font-face
        var styleElement = htmlDocument.CreateElement("style");
        styleElement.InnerHTML = @"
            @font-face {
                font-family: 'OpenSans';
                src: url('OpenSans.woff2') format('woff2');
                font-weight: normal;
                font-style: normal;
            }
            body {
                font-family: 'OpenSans';
                font-weight: " + ((int)WebFontStyle.Bold) + @";
                font-style: " + ((int)WebFontStyle.Italic) + @";
            }";
        htmlDocument.Head.AppendChild(styleElement);

        // Step 3 – Add HTML content that uses the font
        htmlDocument.Body.InnerHTML = "<p>Styled text using WebFontStyle.</p>";

        // Step 4 – Convert HTML to PDF (basic save)
        string outputPath = "styled.pdf";
        htmlDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");

        // Optional: Save with custom page size (demonstrates save html as pdf)
        var pdfOptions = new PdfSaveOptions
        {
            PageSetup = new PageSetup { Width = 595, Height = 842 } // A4
        };
        htmlDocument.Save("styled-a4.pdf", pdfOptions);
        Console.WriteLine("PDF with custom page size saved as styled-a4.pdf");
    }
}
```

**Erwartete Ausgabe:** Zwei PDF‑Dateien (`styled.pdf` und `styled-a4.pdf`) erscheinen im Ausführungsordner. Beide zeigen den Absatz in OpenSans, fett und kursiv, exakt wie im CSS definiert.

---

## Fazit

Wir haben Ihnen gerade **how to create PDF from HTML** mit Aspose.HTML gezeigt, **how to embed font** behandelt, einen sauberen **convert html to pdf**‑Workflow demonstriert und sogar ein fortgeschrittenes **save html as pdf**‑Szenario mit benutzerdefinierten Seitengrößen erkundet. Die Kernidee ist einfach: ein `HTMLDocument` erstellen, eine `@font-face`‑Regel einfügen, Ihr Markup hinzufügen und Aspose die schwere Arbeit erledigen lassen.

Was kommt als Nächstes? Versuchen Sie, die Schrift zu wechseln, Bilder hinzuzufügen oder mehrseitige Berichte zu erzeugen. Sie können auch mit CSS‑Media‑Queries experimentieren, um unterschiedliche Layouts für Bildschirm und Druck zu erzeugen. Die Bibliothek ist flexibel genug für Rechnungen, Zertifikate oder sogar E‑Books – alles ohne C# zu verlassen.

Wenn Sie auf Probleme stoßen, überprüfen Sie den Schriftpfad erneut und stellen Sie sicher, dass Ihre NuGet‑Paketversion zur .NET‑Runtime passt, die Sie anvisieren. Viel Spaß beim Coden und beim Umwandeln von HTML in schöne PDFs!  

<img src="assets/create-pdf-from-html-diagram.png" alt="Beispiel für PDF aus HTML mit eingebetteter Schrift">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}