---
category: general
date: 2026-10-05
description: Μετατρέψτε HTML σε PDF με το Aspose.HTML προσθέτοντας έντονη και πλάγια
  στυλ γραμματοσειράς. Μάθετε πώς να αποθηκεύετε HTML ως PDF και να προσαρμόζετε τις
  επιλογές απόδοσης.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- save html as pdf
- add font style pdf
- set bold italic font
- aspose html pdf conversion
language: el
lastmod: 2026-10-05
og_description: Μετατρέψτε HTML σε PDF με το Aspose.HTML, προσθέτοντας έντονη και
  πλάγια γραμματοσειρά. Αυτός ο οδηγός δείχνει πώς να αποθηκεύσετε HTML ως PDF, να
  διαμορφώσετε το antialiasing και να εξασφαλίσετε καθαρή απόδοση κειμένου.
og_image_alt: Screenshot of PDF generated from HTML using Aspose.HTML with bold‑italic
  font
og_title: Μετατροπή HTML σε PDF με έντονη‑πλάγια γραμματοσειρά χρησιμοποιώντας το
  Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Convert HTML to PDF with Aspose.HTML while adding bold and italic font
    styles. Learn how to save HTML as PDF and customize rendering options.
  headline: Convert HTML to PDF with bold‑italic font using Aspose.HTML
  type: TechArticle
- description: Convert HTML to PDF with Aspose.HTML while adding bold and italic font
    styles. Learn how to save HTML as PDF and customize rendering options.
  name: Convert HTML to PDF with bold‑italic font using Aspose.HTML
  steps:
  - name: Enable antialiasing for smoother images
    text: Antialiasing reduces jagged edges on raster graphics. Setting `UseAntialiasing`
      replaces the older `SmoothingMode` property and yields a cleaner visual result.
  - name: Enable text hinting for clearer rendering
    text: Text hinting aligns glyphs to pixel boundaries, which makes small fonts
      easier to read. The `UseHinting` flag supersedes the older `TextRenderingHint`.
  - name: Define bold and italic font style (set bold italic font)
    text: Aspose.HTML represents font styles with the `WebFontStyle` flags. By combining
      `Bold` and `Italic`, you instruct the renderer to apply both styles to any matching
      text.
  - name: Combine options and **save HTML as PDF**
    text: Now that image, text, and font options are configured, you can invoke `Document.Save`
      with the `HtmlSaveOptions` instance. The output file will be a PDF that reflects
      all of the rendering tweaks.
  - name: Full, runnable example
    text: Putting all of the pieces together gives you a self‑contained program you
      can copy, paste, and run.
  type: HowTo
tags:
- Aspose.HTML
- C#
- PDF generation
- HTML-to-PDF
title: Μετατροπή HTML σε PDF με έντονη‑πλάγια γραμματοσειρά χρησιμοποιώντας το Aspose.HTML
url: /el/net/html-extensions-and-conversions/convert-html-to-pdf-with-bold-italic-font-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF με γραμματοσειρά έντονη‑πλάγια χρησιμοποιώντας το Aspose.HTML

Αν χρειάζεστε **μετατροπή HTML σε PDF** και θέλετε το αποτέλεσμα να διατηρεί το έντονο και πλάγιο κείμενο, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.HTML. Θα μάθετε πώς να *αποθηκεύσετε HTML ως PDF* ενώ διαμορφώνετε τις επιλογές απόδοσης για ομαλές εικόνες και καθαρό κείμενο.

Το tutorial καλύπτει τα πάντα, από τη φόρτωση του πηγαίου αρχείου HTML μέχρι τον ορισμό ενός **στυλ γραμματοσειράς έντονη‑πλάγια**, ώστε να μπορείτε να παράγετε επαγγελματικά PDFs χωρίς επιπλέον επεξεργασία. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο η βιβλιοθήκη Aspose.HTML for .NET.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
* Ένα έγκυρο license του Aspose.HTML for .NET ή ένα προσωρινό κλειδί αξιολόγησης  
* Ένα αρχείο HTML (`input.html`) που θέλετε να μετατρέψετε  

Η προετοιμασία αυτών διασφαλίζει ότι ο κώδικας θα εκτελεστεί χωρίς ελλείψεις εξαρτήσεων.

## Μετατροπή HTML σε PDF με προσαρμοσμένες επιλογές απόδοσης

Το πρώτο βήμα είναι η φόρτωση του εγγράφου HTML και η δημιουργία μιας παρουσίας `HtmlSaveOptions` που θα περιέχει όλες τις προτιμήσεις απόδοσης. Αυτό το αντικείμενο λέει στο Aspose.HTML πώς να αντιμετωπίζει εικόνες, κείμενο και γραμματοσειρές κατά τη **aspose html pdf conversion**.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Text;

// Load the HTML document you want to convert
var document = new Document("YOUR_DIRECTORY/input.html");

// Create a container for all save options
var saveOptions = new HtmlSaveOptions();
```

### Ενεργοποίηση antialiasing για ομαλότερες εικόνες

Το antialiasing μειώνει τις γωνίες σκακιού στα raster γραφικά. Ο ορισμός του `UseAntialiasing` αντικαθιστά την παλαιότερη ιδιότητα `SmoothingMode` και προσφέρει πιο καθαρό οπτικό αποτέλεσμα.

```csharp
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true   // smoother image rendering
};

saveOptions.ImageRenderingOptions = imageOptions;
```

### Ενεργοποίηση text hinting για πιο καθαρή απόδοση

Το text hinting ευθυγραμμίζει τα glyphs στα όρια των pixel, κάτι που κάνει τις μικρές γραμματοσειρές πιο ευανάγνωστες. Η σημαία `UseHinting` αντικαθιστά το παλαιότερο `TextRenderingHint`.

```csharp
var textOptions = new TextOptions
{
    UseHinting = true   // clearer text rendering
};

saveOptions.TextOptions = textOptions;
```

### Ορισμός στυλ γραμματοσειράς έντονη‑πλάγια (set bold italic font)

Το Aspose.HTML αντιπροσωπεύει τα στυλ γραμματοσειράς με τις σημαίες `WebFontStyle`. Συνδυάζοντας τα `Bold` και `Italic`, υποδεικνύετε στον renderer να εφαρμόσει και τα δύο στυλ σε οποιοδήποτε κείμενο ταιριάζει.

```csharp
var fontStyle = new WebFontStyle
{
    Style = WebFontStyle.Bold | WebFontStyle.Italic   // set bold italic font
};

// Apply the style to the document's default font settings
document.DefaultFont = new FontSettings
{
    FontStyle = fontStyle
};
```

> **Pro tip:** Αν το HTML σας ήδη χρησιμοποιεί ετικέτες `<b>` ή `<i>`, ο renderer σέβεται αυτόματα αυτές τις ετικέτες. Η ρητή προσέγγιση με `WebFontStyle` είναι χρήσιμη όταν θέλετε να επιβάλετε ένα στυλ σε ολόκληρο το έγγραφο.

### Συνδυασμός επιλογών και **αποθήκευση HTML ως PDF**

Τώρα που οι επιλογές εικόνας, κειμένου και γραμματοσειράς είναι διαμορφωμένες, μπορείτε να καλέσετε το `Document.Save` με την παρουσία `HtmlSaveOptions`. Το αρχείο εξόδου θα είναι ένα PDF που αντικατοπτρίζει όλες τις ρυθμίσεις απόδοσης.

```csharp
// Save the document as a PDF using the configured options
document.Save("YOUR_DIRECTORY/output.pdf", saveOptions);
```

### Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια παίρνετε ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να εκτελέσετε.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Text;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML document you want to convert
        var document = new Document("YOUR_DIRECTORY/input.html");

        // 2️⃣ Configure image rendering (antialiasing)
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true
        };

        // 3️⃣ Configure text rendering (hinting)
        var textOptions = new TextOptions
        {
            UseHinting = true
        };

        // 4️⃣ Define bold‑italic font style
        var fontStyle = new WebFontStyle
        {
            Style = WebFontStyle.Bold | WebFontStyle.Italic
        };
        document.DefaultFont = new FontSettings
        {
            FontStyle = fontStyle
        };

        // 5️⃣ Bundle all options into HtmlSaveOptions
        var saveOptions = new HtmlSaveOptions
        {
            ImageRenderingOptions = imageOptions,
            TextOptions = textOptions
        };

        // 6️⃣ Save the HTML as a PDF
        document.Save("YOUR_DIRECTORY/output.pdf", saveOptions);
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο με όνομα `output.pdf` στο φάκελο `YOUR_DIRECTORY`. Ανοίξτε το σε οποιονδήποτε προβολέα PDF και θα δείτε το αρχικό περιεχόμενο HTML αποδομένο με ομαλές εικόνες και **έντονη‑πλάγια** γραμματοσειρά όπου απαιτείται.

## Συχνές ερωτήσεις και αντιμετώπιση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το HTML μου χρησιμοποιεί προσαρμοσμένη web γραμματοσειρά;* | Προσθέστε το αρχείο γραμματοσειράς στον ίδιο φάκελο με το HTML και αναφερθείτε σε αυτό με `@font-face` σε ένα μπλοκ `<style>`. Το Aspose.HTML θα ενσωματώσει αυτόματα τη γραμματοσειρά κατά τη μετατροπή. |
| *Θα προκαλέσουν μεγάλα αρχεία HTML προβλήματα μνήμης;* | Για πολύ μεγάλα έγγραφα, σκεφτείτε τη μετατροπή σελίδα‑με‑σελίδα χρησιμοποιώντας το `Document.Pages` και αποθηκεύοντας κάθε τμήμα ξεχωριστά, έπειτα συγχωνεύστε τα PDFs με μια βιβλιοθήκη ειδική για PDF. |
| *Πώς αλλάζω το μέγεθος σελίδας του PDF;* | Ορίστε `saveOptions.PageSetup.PaperSize = PaperSize.A4;` πριν καλέσετε το `Save`. |
| *Μπορώ να κρυπτογραφήσω το παραγόμενο PDF;* | Ναι. Χρησιμοποιήστε `PdfSaveOptions` (αντί για `HtmlSaveOptions`) και ορίστε τις ιδιότητες `Encryption`. Αυτό το tutorial εστιάζει στο `HtmlSaveOptions` για απλότητα. |
| *Τι κάνω αν το αποτέλεσμα φαίνεται θολό;* | Βεβαιωθείτε ότι το `UseAntialiasing` είναι `true` και αυξήστε το DPI της εικόνας μέσω `imageOptions.Dpi = 300;`. Μεγαλύτερο DPI προσφέρει πιο οξείς raster εικόνες, αλλά αυξάνει το μέγεθος του αρχείου. |

## Συμβουλές για χρήση σε παραγωγή

* **Καταχωρίστε το license νωρίς:** Εγγράψτε το license του Aspose.HTML πριν δημιουργήσετε το αντικείμενο `Document` για να αποφύγετε μηνύματα υδατογραφήματος.  
  ```csharp
  var license = new Aspose.Html.License();
  license.SetLicense("Aspose.HTML.lic");
  ```
* **Διαχείριση διαδρομών:** Χρησιμοποιήστε `Path.Combine` για ασφαλή κατασκευή διαδρομών αρχείων σε Windows, Linux και macOS.  
* **Καταγραφή:** Τυλίξτε τη μετατροπή σε μπλοκ `try / catch` και καταγράψτε το `HtmlConversionException` για εντοπισμό σφαλμάτων.  
* **Απόδοση:** Επαναχρησιμοποιήστε μια ενιαία παρουσία `HtmlSaveOptions` αν μετατρέπετε πολλά αρχεία σε batch· η δημιουργία νέας παρουσίας ανά αρχείο προσθέτει επιπλέον φόρτο.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή λύση για **μετατροπή HTML σε PDF** ενώ προσθέτετε χαρακτηριστικά στυλ γραμματοσειράς PDF όπως **set bold italic font**. Το παράδειγμα δείχνει όλη τη ροή **aspose html pdf conversion**: φόρτωση HTML, ρύθμιση antialiasing και hinting, ορισμός στυλ έντονη‑πλάγια, και τελικά **save html as pdf**.

Από εδώ μπορείτε να εξερευνήσετε πρόσθετες προσαρμογές—όπως ενσωμάτωση προσαρμοσμένων γραμματοσειρών, αλλαγή περιθωρίων σελίδας ή προσθήκη υδατογραφήματος. Πειραματιστείτε με τις διάφορες επιλογές απόδοσης που προσφέρει το Aspose.HTML για να βελτιστοποιήσετε τα PDFs σας σε οποιοδήποτε σενάριο. Καλή κωδικοποίηση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Μετατροπή HTML σε PDF σε Java – Πλήρης Οδηγός με Ενσωμάτωση Γραμματοσειρών](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-complete-guide-with-font-embeddi/)
- [Μετατροπή HTML σε PDF σε Java – Ορισμός Μεγέθους Σελίδας PDF, Ανάλυσης και Αποθήκευση HTML](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-pdf-page-size-resolution-and/)
- [Πώς να χρησιμοποιήσετε το Aspose – Batch Μετατροπή HTML σε PDF σε Java](/html/english/java/conversion-html-to-other-formats/how-to-use-aspose-batch-convert-html-to-pdf-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}