---
category: general
date: 2026-08-03
description: Μετατρέψτε HTML σε PDF σε C# με πλήρη έλεγχο απόδοσης. Μάθετε πώς να
  ορίζετε το στυλ γραμματοσειράς προγραμματιστικά, να ενεργοποιείτε την εξομάλυνση
  και να βελτιώνετε την καθαρότητα του κειμένου.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- set font style programmatically
language: el
lastmod: 2026-08-03
og_description: Μετατρέψτε HTML σε PDF σε C# με λεπτομερείς επιλογές. Αυτός ο οδηγός
  δείχνει πώς να ορίσετε το στυλ γραμματοσειράς προγραμματιστικά, να ενεργοποιήσετε
  την εξομάλυνση και να παράγετε PDF υψηλής ποιότητας.
og_image_alt: Diagram showing conversion of HTML to PDF using C# with font style settings
og_title: Μετατροπή HTML σε PDF σε C# – πλήρης έλεγχος απόδοσης
schemas:
- author: Aspose
  dateModified: '2026-08-03'
  description: Convert HTML to PDF in C# with full rendering control. Learn how to
    set font style programmatically, enable antialiasing, and improve text clarity.
  headline: Convert HTML to PDF in C# – set font style programmatically
  type: TechArticle
tags:
- C#
- PDF conversion
- HTML rendering
title: Μετατροπή HTML σε PDF σε C# – ορισμός στυλ γραμματοσειράς προγραμματιστικά
url: /el/net/html-extensions-and-conversions/convert-html-to-pdf-in-c-set-font-style-programmatically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF σε C# – ορισμός στυλ γραμματοσειράς προγραμματιστικά

Αν χρειάζεστε **μετατροπή HTML σε PDF** σε μια εφαρμογή .NET, αυτό το tutorial σας οδηγεί βήμα‑βήμα σε μια πλήρη, έτοιμη για παραγωγή λύση. Θα δείτε πώς να **ορίσετε το στυλ γραμματοσειράς προγραμματιστικά**, να βελτιώσετε την απόδοση των εικόνων και να ενεργοποιήσετε το hinting κειμένου—όλα χωρίς να αφήσετε τον κώδικα C#.

Η μετατροπή ιστοσελίδων σε PDF είναι συχνή απαίτηση για αναφορές, τιμολόγηση και αρχειοθέτηση. Αυτός ο οδηγός καλύπτει τα πάντα, από τη ρύθμιση του έργου μέχρι ένα πλήρες, εκτελέσιμο παράδειγμα. Στο τέλος του άρθρου θα μπορείτε να δημιουργείτε PDF που διατηρούν τη διάταξη, την τυπογραφία και την οπτική πιστότητα.

## Τι θα μάθετε

* Πώς να προσθέσετε το απαιτούμενο πακέτο NuGet και να εισάγετε namespaces.  
* Πώς να διαμορφώσετε το `HtmlConversionOptions` για έλεγχο της απόδοσης.  
* Πώς να **ορίσετε το στυλ γραμματοσειράς προγραμματιστικά** χρησιμοποιώντας τις σημαίες `WebFontStyle`.  
* Πώς να ενεργοποιήσετε το antialiasing για εικόνες και το hinting για κείμενο.  
* Πώς να καλέσετε την κλάση `Converter` για να παραγάγετε το τελικό αρχείο PDF.  

Το tutorial υποθέτει ότι έχετε εγκατεστημένο το Visual Studio 2022 (ή νεότερο) και το .NET 6 ή νεότερο. Δεν απαιτείται πρόσθετο εργαλείο.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|---|---|
| .NET 6 SDK ή νεότερο | Παρέχει το runtime για το έργο C#. |
| Visual Studio 2022 (ή οποιοδήποτε IDE) | Διευκολύνει τη δημιουργία και την αποσφαλμάτωση του έργου. |
| Πρόσβαση στο Internet για αποκατάσταση πακέτων NuGet | Απαιτείται για λήψη της βιβλιοθήκης μετατροπής. |
| Ένα απλό αρχείο HTML (`input.html`) | Λειτουργεί ως το πηγαίο έγγραφο για τη μετατροπή. |

> **Pro tip:** Κρατήστε το αρχείο HTML στον ίδιο φάκελο με το έργο για να αποφύγετε προβλήματα σχετιζόμενα με διαδρομές.

## Βήμα 1: Εγκατάσταση της βιβλιοθήκης μετατροπής

Το δείγμα κώδικα χρησιμοποιεί τη βιβλιοθήκη **GroupDocs.Conversion for .NET**, η οποία προσφέρει `HtmlConversionOptions` και μια κλάση `Converter`. Εγκαταστήστε την μέσω του NuGet Package Manager:

```bash
dotnet add package GroupDocs.Conversion
```

Το πακέτο προσθέτει τους απαραίτητους τύπους στο έργο σας και φέρνει όλες τις εξαρτήσεις.

## Βήμα 2: Δημιουργία έργου κονσόλας C#

Ανοίξτε μια γραμμή εντολών και εκτελέστε:

```bash
dotnet new console -n HtmlToPdfDemo
cd HtmlToPdfDemo
```

Αυτό δημιουργεί μια ελάχιστη εφαρμογή κονσόλας με όνομα `HtmlToPdfDemo`. Ανοίξτε το παραγόμενο αρχείο `Program.cs`; θα αντικαταστήσετε το περιεχόμενό του με το πλήρες παράδειγμα αργότερα.

## Βήμα 3: Διαμόρφωση επιλογών μετατροπής – ορισμός στυλ γραμματοσειράς προγραμματιστικά

Η κλάση `HtmlConversionOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς πώς η μηχανή HTML αποδίδει τη σελίδα. Για **ορισμό στυλ γραμματοσειράς προγραμματιστικά**, συνδυάστε τις τιμές της απαρίθμησης `WebFontStyle` χρησιμοποιώντας bitwise OR:

```csharp
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Load;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options;
using GroupDocs.Conversion.Options.Pdf;

// Step 3: Build conversion options with custom font style
var conversionOptions = new HtmlConversionOptions();

// Choose bold and italic simultaneously
conversionOptions.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

// Enable antialiasing for smoother images
conversionOptions.ImageRenderingOptions.UseAntialiasing = true;

// Turn on hinting for clearer glyph rendering
conversionOptions.TextOptions.UseHinting = true;
```

**Γιατί είναι σημαντικό:**  
* `WebFontStyle.Bold | WebFontStyle.Italic` λέει στον renderer να εφαρμόσει και τα δύο στυλ σε οποιοδήποτε κείμενο χρησιμοποιεί την προεπιλεγμένη γραμματοσειρά.  
* Το antialiasing μειώνει τις γωνιές σκαλισμού σε raster εικόνες, ειδικά κατά την κλιμάκωση.  
* Το hinting ευθυγραμμίζει τα περιγράμματα των glyphs σε πλέγματα pixel, βελτιώνοντας την αναγνωσιμότητα σε οθόνες χαμηλής ανάλυσης και στο παραγόμενο PDF.

## Βήμα 4: Εκτέλεση της μετατροπής

Με τις επιλογές έτοιμες, καλέστε την κλάση `Converter`. Η μέθοδος `Convert` δέχεται τρία ορίσματα: τη διαδρομή του πηγαίου αρχείου HTML, τη διαδρομή του προορισμού PDF και το αντικείμενο επιλογών.

```csharp
// Step 4: Convert the HTML file to PDF using the configured options
string inputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "input.html");
string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "output.pdf");

// Create the converter and execute the conversion
new Converter().Convert(inputPath, outputPath, conversionOptions);
```

Η μέθοδος εκτελείται συγχρονισμένα και ρίχνει εξαίρεση εάν το πηγαίο αρχείο δεν μπορεί να διαβαστεί ή η διαδρομή εξόδου είναι άκυρη. Τυλίξτε την κλήση σε block try‑catch για κώδικα παραγωγής.

## Βήμα 5: Επαλήθευση του αποτελέσματος

Αφού ολοκληρωθεί το πρόγραμμα, ανοίξτε το `output.pdf` με οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε:

* Κείμενο αποδοθέν σε **bold and italic** (ακόμη και αν το αρχικό HTML δεν καθόριζε αυτά τα στυλ).  
* Οι εικόνες να εμφανίζονται πιο ομαλές χάρη στο antialiasing.  
* Η καθαρότητα του κειμένου να έχει βελτιωθεί με το hinting, ειδικά για μικρά μεγέθη γραμματοσειράς.

Εάν το PDF δεν αντανακλά τα αναμενόμενα στυλ, ελέγξτε ξανά ότι το αρχείο HTML αναφέρει μια web‑safe γραμματοσειρά ή περιλαμβάνει έναν κανόνα `@font-face` που μπορεί να φορτώσει ο μετατροπέας.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που ενσωματώνει όλα τα προηγούμενα βήματα. Αντιγράψτε τον κώδικα στο `Program.cs`, τοποθετήστε ένα αρχείο `input.html` δίπλα του και τρέξτε `dotnet run`.

```csharp
// Program.cs
using System;
using System.IO;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

namespace HtmlToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths for source HTML and target PDF
            string inputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "input.html");
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "output.pdf");

            // Ensure the input file exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Input file not found: {inputPath}");
                return;
            }

            // Configure conversion options
            var conversionOptions = new HtmlConversionOptions
            {
                // Combine bold and italic styles programmatically
                FontStyle = WebFontStyle.Bold | WebFontStyle.Italic,

                // Improve image rendering quality
                ImageRenderingOptions = { UseAntialiasing = true },

                // Enhance text clarity
                TextOptions = { UseHinting = true }
            };

            try
            {
                // Perform the conversion
                new Converter().Convert(inputPath, outputPath, conversionOptions);
                Console.WriteLine($"Conversion succeeded. PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Conversion failed: {ex.Message}");
            }
        }
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Conversion succeeded. PDF saved to: C:\Path\To\Your\App\output.pdf
```

Ανοίξτε το παραγόμενο PDF για να επιβεβαιώσετε τα εφαρμοσμένα στυλ.

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Προτεινόμενη προσέγγιση |
|---|---|
| **External CSS or fonts** | Τοποθετήστε τα αρχεία CSS και τους πόρους γραμματοσειρών στον ίδιο φάκελο με το `input.html` ή αναφερθείτε σε απόλυτες URL που είναι προσβάσιμες από το μηχάνημα που εκτελεί τη μετατροπή. |
| **Large HTML documents** | Αυξήστε το προεπιλεγμένο όριο μνήμης προσαρμόζοντας το `ConversionConfig` εάν αντιμετωπίσετε `OutOfMemoryException`. |
| **Dynamic content (JavaScript)** | Η βιβλιοθήκη δεν εκτελεί JavaScript. Προ‑αποδώστε τα δυναμικά τμήματα στο server‑side ή χρησιμοποιήστε έναν headless browser για να δημιουργήσετε ένα στατικό στιγμιότυπο HTML πριν τη μετατροπή. |
| **Unicode characters not displaying** | Βεβαιωθείτε ότι το HTML δηλώνει `<meta charset="UTF-8">` και ότι οι πηγαίες γραμματοσειρές περιέχουν τα απαιτούμενα glyphs. |
| **Incorrect page size** | Ορίστε `conversionOptions.PageSize = PageSize.A4` (ή άλλη τιμή enum) για να εξασφαλίσετε συνεπείς διαστάσεις. |

## Συμβουλές απόδοσης

* Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Converter` όταν μετατρέπετε πολλά αρχεία· μειώνει το κόστος εκκίνησης.  
* Απενεργοποιήστε περιττές λειτουργίες απόδοσης (π.χ., `EnableHyperlinks`) εάν δεν τις χρειάζεστε, κάτι που επιταχύνει την επεξεργασία.  
* Γράψτε το PDF σε ροή μνήμης (memory stream) όταν χρειάζεται να το στείλετε απευθείας μέσω HTTP αντί να το αποθηκεύσετε σε δίσκο.

## Επόμενα βήματα

Τώρα που μπορείτε να **μετατρέψετε HTML σε PDF** με προσαρμοσμένες ρυθμίσεις γραμματοσειράς, εξερευνήστε τα παρακάτω σχετικά θέματα:

* **Set page margins programmatically** – προσαρμόστε το `conversionOptions.Margin` για έλεγχο του λευκού χώρου.  
* **Add watermarks** – χρησιμοποιήστε το `PdfConversionOptions` για επικάλυψη κειμένου ή εικόνων.  
* **Batch conversion** – επαναλάβετε τη διαδικασία για μια συλλογή αρχείων HTML και επαναχρησιμοποιήστε το ίδιο αντικείμενο επιλογών.

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Convert SVG to PDF in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}