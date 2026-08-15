---
category: general
date: 2026-03-14
description: Αποδώστε HTML σε εικόνα γρήγορα χρησιμοποιώντας το Aspose.HTML. Μάθετε
  πώς να μετατρέψετε μια ιστοσελίδα σε PNG, να ορίσετε το στυλ γραμματοσειράς και
  να αποθηκεύσετε την αποδοθείσα εικόνα με λίγες μόνο γραμμές κώδικα C#.
draft: false
keywords:
- render html to image
- convert webpage to png
- convert html to png
- set font style
- save rendered image
language: el
og_description: Απόδοση HTML σε εικόνα με το Aspose.HTML. Αυτό το σεμινάριο δείχνει
  πώς να μετατρέψετε μια ιστοσελίδα σε PNG, να ορίσετε το στυλ γραμματοσειράς και
  να αποθηκεύσετε την αποδοθείσα εικόνα σε C#.
og_title: Απόδοση HTML σε Εικόνα σε C# – Γρήγορος και Εύκολος Οδηγός
tags:
- C#
- Aspose.HTML
- Image Rendering
title: Απόδοση HTML σε εικόνα με C# – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/rendering-html-documents/render-html-to-image-in-c-complete-step-by-step-guide/
---

, tables, etc.

Let's craft translation.

Be careful with Greek characters and punctuation.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόδοση HTML σε Εικόνα – Πλήρης Οδηγός C#

Κάποτε χρειάστηκε να **render HTML to image** αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξεις; Δεν είσαι ο μόνος. Σε πολλές περιπτώσεις web‑automation ή αναφοράς καταλήγεις με μια ζωντανή σελίδα που θέλεις να αρχειοθετήσεις ως PNG, JPEG ή ακόμα και BMP. Τα καλά νέα είναι ότι το Aspose.HTML κάνει αυτό παιχνιδάκι, επιτρέποντάς σου να **convert webpage to PNG** με λίγες μόνο γραμμές κώδικα.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία: από την εγκατάσταση του πακέτου Aspose.HTML, τη φόρτωση μιας απομακρυσμένης URL, τη ρύθμιση των επιλογών απόδοσης (συμπεριλαμβανομένου του πώς να **set font style**), και τέλος **save rendered image** στο δίσκο. Στο τέλος θα έχεις μια έτοιμη για εκτέλεση εφαρμογή console που παράγει ένα καθαρό στιγμιότυπο οποιασδήποτε ιστοσελίδας.

## Τι Θα Χρειαστείτε

| Prerequisite | Reason |
|--------------|--------|
| .NET 6.0 SDK ή νεότερο | Το Aspose.HTML στοχεύει στο .NET Standard 2.0+, οπότε το .NET 6 σας δίνει το πιο σύγχρονο runtime. |
| Visual Studio 2022 (ή VS Code) | Ένα άνετο IDE επιταχύνει το debugging. |
| Aspose.HTML for .NET NuGet package | Αυτός είναι ο κινητήρας που κάνει τη βαριά δουλειά. |
| Έγκυρη άδεια Aspose.HTML (προαιρετικό) | Χωρίς άδεια θα εμφανίζεται υδατογράφημα στην έξοδο εικόνας. |

Μπορείτε να αποκτήσετε το πακέτο μέσω του CLI:

```bash
dotnet add package Aspose.HTML
```

Αν προτιμάτε το GUI, απλώς αναζητήστε “Aspose.HTML” στον NuGet Package Manager.

---

## Βήμα 1: Φορτώστε τη Σελίδα που Θέλετε να Rasterize

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δώσετε στο Aspose.HTML ένα έγγραφο προέλευσης. Μπορεί να είναι τοπικό αρχείο, μια συμβολοσειρά ή μια απομακρυσμένη URL. Στις περισσότερες πραγματικές περιπτώσεις θα δουλεύετε με μια ζωντανή ιστοσελίδα, οπότε ας **convert webpage to PNG** δείχνοντας στο `https://example.com`.

```csharp
using Aspose.Html;

// ...

// Create an HtmlDocument from a remote URL
HtmlDocument htmlDoc = new HtmlDocument("https://example.com");

// Optional: verify that the document loaded successfully
if (htmlDoc.IsEmpty)
{
    Console.WriteLine("Failed to load the page. Check the URL or your network.");
    return;
}
```

> **Why this matters:** Η φόρτωση της σελίδας ως `HtmlDocument` σας δίνει πλήρη πρόσβαση στο DOM, πράγμα που σημαίνει ότι μπορείτε να ενσωματώσετε CSS, να τροποποιήσετε τη διάταξη ή ακόμη και να εκτελέσετε JavaScript πριν το rasterizing.

---

## Βήμα 2: Ρυθμίστε τις Επιλογές Απόδοσης Εικόνας

Τώρα που το HTML είναι στη μνήμη, πρέπει να πείτε στον renderer πώς θέλετε να φαίνεται η τελική εικόνα. Εδώ μπορείτε να **set font style**, να ενεργοποιήσετε antialiasing ή να ρυθμίσετε το DPI. Παρακάτω υπάρχει μια σταθερή προεπιλεγμένη διαμόρφωση που ισορροπεί ποιότητα και ταχύτητα.

```csharp
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// ...

ImageRenderingOptions renderingOptions = new ImageRenderingOptions
{
    // Smoother curves and text – especially important for vector graphics
    UseAntialiasing = true,

    // Improves glyph clarity on Linux and low‑resolution displays
    TextOptions = { UseHinting = true },

    // Demonstrates how to set a combined font style (bold + italic)
    FontStyle = WebFontStyle.Bold | WebFontStyle.Italic,

    // Optional: increase DPI for a higher‑resolution PNG (default is 96)
    // DpiX = 150,
    // DpiY = 150,
};
```

> **Pro tip:** Αν χρειάζεστε μόνο κανονικό βάρος, αφαιρέστε τις σημαίες `WebFontStyle`. Για τίτλους μπορεί να θέλετε μόνο το `WebFontStyle.Bold`, ενώ για λεζάντες το `WebFontStyle.Italic`.

---

## Βήμα 3: Απόδοση Σελίδας και **Save Rendered Image** ως PNG

Με το έγγραφο και τις επιλογές έτοιμες, το τελευταίο βήμα είναι να δημιουργήσετε ένα `ImageRenderer` και να γράψετε το αρχείο εξόδου. Το μπλοκ `using` εξασφαλίζει ότι οι πόροι απελευθερώνονται άμεσα.

```csharp
using (var imageRenderer = new ImageRenderer(htmlDoc, renderingOptions))
{
    // Path where the PNG will be saved – adjust as needed
    string outputPath = Path.Combine(
        Environment.CurrentDirectory,
        "page.png");

    imageRenderer.Save(outputPath);
    Console.WriteLine($"✅ Image saved to: {outputPath}");
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε ένα αρχείο `page.png` στον φάκελο του έργου σας, το οποίο περιέχει ένα πιστό στιγμιότυπο του *example.com*. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων και θα παρατηρήσετε το έντονο‑πλάγιο στυλ που ζητήσαμε νωρίτερα.

### Αναμενόμενο Αποτέλεσμα

```
✅ Image saved to: C:\Projects\RenderHtml\bin\Debug\net6.0\page.png
```

Το PNG θα έχει περίπου 800 × 600 px (ανάλογα με τις αρχικές διαστάσεις της σελίδας) με ομαλές άκρες χάρη στο antialiasing.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια ελάχιστη εφαρμογή console που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Συγκεντρώνεται και τρέχει αμέσως.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the target web page
        HtmlDocument htmlDoc = new HtmlDocument("https://example.com");
        if (htmlDoc.IsEmpty)
        {
            Console.WriteLine("Unable to load the URL. Exiting.");
            return;
        }

        // 2️⃣ Set up rendering options (including font style)
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            TextOptions = { UseHinting = true },
            FontStyle = WebFontStyle.Bold | WebFontStyle.Italic
        };

        // 3️⃣ Render and **save rendered image** as PNG
        using (var imageRenderer = new ImageRenderer(htmlDoc, renderingOptions))
        {
            string outputPath = Path.Combine(
                Environment.CurrentDirectory,
                "page.png");
            imageRenderer.Save(outputPath);
            Console.WriteLine($"✅ Image saved to: {outputPath}");
        }
    }
}
```

Τρέξτε το με:

```bash
dotnet run
```

…και θα έχετε ένα φρέσκο PNG έτοιμο για αρχειοθέτηση, αποστολή email ή ενσωμάτωση σε αναφορά.

---

## Παραλλαγές & Ακραίες Περιπτώσεις

### 1. Μετατροπή σε JPEG Αντί για PNG

Αν το downstream σύστημα σας προτιμά JPEG (μικρότερο μέγεθος αρχείου, απώλεια συμπίεσης), απλώς αλλάξτε την επέκταση αρχείου στο `Save`. Το Aspose.HTML ανιχνεύει αυτόματα τη μορφή από τη διαδρομή.

```csharp
imageRenderer.Save("page.jpg");   // JPEG output
```

Μπορείτε επίσης να ρυθμίσετε την ποιότητα συμπίεσης μέσω `JpegRenderingOptions`.

### 2. Αλλαγή Διαστάσεων Εικόνας

Μερικές φορές χρειάζεστε μια μικρογραφία αντί για πλήρες στιγμιότυπο. Ορίστε το `ImageSize` στις επιλογές:

```csharp
renderingOptions.ImageSize = new Size(400, 300); // width × height in pixels
```

### 3. Διαχείριση Σελίδων με Προστασία Αυθεντικοποίησης

Αν η στοχευμένη URL απαιτεί βασική αυθεντικοποίηση, παρέχετε τα διαπιστευτήρια μέσω `HttpWebRequest` πριν δημιουργήσετε το `HtmlDocument`. Εναλλακτικά, κατεβάστε το HTML μόνοι σας (χρησιμοποιώντας `HttpClient`) και δώστε το ως συμβολοσειρά:

```csharp
string html = await new HttpClient().GetStringAsync("https://secure.example.com");
HtmlDocument doc = new HtmlDocument(html);
```

### 4. Χρήση Προσαρμοσμένης Γραμματοσειράς

Το Aspose.HTML μπορεί να ενσωματώσει τοπικές γραμματοσειρές. Καταχωρίστε το φάκελο γραμματοσειρών πριν φορτώσετε το έγγραφο:

```csharp
HtmlLoadOptions loadOptions = new HtmlLoadOptions();
loadOptions.Fonts.AddFolder(@"C:\MyFonts");
HtmlDocument htmlDoc = new HtmlDocument("https://example.com", loadOptions);
```

Τώρα οποιεσδήποτε δηλώσεις `font-family` στη σελίδα θα αντιστοιχούν στα προσαρμοσμένα αρχεία σας.

### 5. Απόδοση Πολλών Σελίδων σε Βρόχο

Αν χρειάζεστε batch‑processing λίστας URL:

```csharp
string[] urls = { "https://example.com", "https://contoso.com" };
int i = 1;
foreach (var url in urls)
{
    HtmlDocument doc = new HtmlDocument(url);
    using var renderer = new ImageRenderer(doc, renderingOptions);
    renderer.Save($"page_{i++}.png");
}
```

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Blank PNG file | `HtmlDocument.IsEmpty` true (page failed to load) | Επαληθεύστε τη URL, ελέγξτε το proxy δικτύου, βεβαιωθείτε ότι είναι ενεργοποιημένο το TLS 1.2. |
| Garbled text on Linux | Font hinting disabled | Ορίστε `renderingOptions.TextOptions.UseHinting = true;`. |
| Watermark on output | No license provided | Καταχωρίστε προσωρινή ή πλήρη άδεια μέσω `License license = new License(); license.SetLicense("Aspose.Total.lic");`. |
| Low‑resolution image | Default DPI 96 is insufficient for print | Αυξήστε τα `renderingOptions.DpiX` και `DpiY` στα 150‑300. |

---

## 🎉 Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για **render HTML to image** με το Aspose.HTML σε C#. Από τη φόρτωση απομακρυσμένης σελίδας, τη ρύθμιση antialiasing και **set font style**, μέχρι το τελικό **save rendered image** ως PNG, όλη η ροή εργασίας χωράει σε λίγα συνοπτικά βήματα.  

Τώρα μπορείτε να **convert webpage to PNG** άμεσα, να ενσωματώσετε στιγμιότυπα σε αναφορές ή να δημιουργήσετε μικρογραφίες για κατάλογο—χωρίς ανάγκη αυτοματοποίησης προγράμματος περιήγησης.

### Τι Ακολουθεί;

- Πειραματιστείτε με **convert html to png** για διαφορετικά μεγέθη οθόνης (mobile vs desktop).  
- Δοκιμάστε εξαγωγή σε PDF χρησιμοποιώντας `PdfRenderer` αν χρειάζεστε εκτυπώσιμο έγγραφο.  
- Εξερευνήστε τα API χειρισμού DOM του Aspose.HTML για να ενσωματώσετε υδατογραφήματα ή προσαρμοσμένο CSS πριν την απόδοση.

Έχετε ερωτήσεις σχετικά με ακραίες περιπτώσεις, άδειες ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

---

![Screenshot of a rendered page showing the result of render html to image](/images/render-html-to-image-example.png "render html to image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}