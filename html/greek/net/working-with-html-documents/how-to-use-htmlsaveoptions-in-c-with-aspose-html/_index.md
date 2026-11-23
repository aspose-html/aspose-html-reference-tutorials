---
category: general
date: 2026-09-10
description: Μάθετε πώς να χρησιμοποιείτε το HtmlSaveOptions σε C# για να ελέγχετε
  τα στυλ των web‑font και να αποθηκεύετε αρχεία HTML με το Aspose.HTML. Περιλαμβάνεται
  πλήρες παράδειγμα κώδικα και πρακτικές συμβουλές.
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
language: el
lastmod: 2026-09-10
og_description: Πώς να χρησιμοποιήσετε το HtmlSaveOptions σε C# για να ενεργοποιήσετε
  τα έντονα και πλάγια στυλ web‑font κατά την αποθήκευση HTML με το Aspose.HTML. Ακολουθήστε
  το πλήρες παράδειγμα και τις συμβουλές βέλτιστων πρακτικών.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Πώς να χρησιμοποιήσετε το HtmlSaveOptions σε C# με το Aspose.HTML – βήμα‑βήμα
  οδηγός
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
title: Πώς να χρησιμοποιήσετε το HtmlSaveOptions σε C# με το Aspose.HTML
url: /el/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το HtmlSaveOptions σε C# με το Aspose.HTML

Εάν χρειάζεται να ελέγξετε πώς το Aspose.HTML αποθηκεύει ένα έγγραφο HTML, **η εκμάθηση της χρήσης του HtmlSaveOptions είναι ουσιώδης**. Αυτό το tutorial σας δείχνει βήμα‑βήμα πώς να χρησιμοποιήσετε το HtmlSaveOptions για να ενεργοποιήσετε τις έντονες και πλάγιες μορφές web‑font κατά την αποθήκευση ενός εγγράφου.

Η βιβλιοθήκη Aspose HTML παρέχει ένα πλούσιο API για φόρτωση, επεξεργασία και εξαγωγή περιεχομένου HTML. Στο τέλος αυτού του οδηγού θα μπορείτε να:

* Φορτώσετε ένα υπάρχον αρχείο HTML σε ένα `HTMLDocument`.
* Διαμορφώσετε το `HtmlSaveOptions` ώστε να εφαρμόζει συγκεκριμένες σημαίες `WebFontStyle`.
* Αποθηκεύσετε το τροποποιημένο έγγραφο σε νέα θέση ή σε ροή.
* Επεκτείνετε τη λύση για άλλες μορφές γραμματοσειρών, προσαρμοσμένο CSS και διαχείριση σφαλμάτων.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη.
* Ένα έγκυρο license για **Aspose.HTML for .NET** (η δωρεάν δοκιμαστική έκδοση λειτουργεί για αυτό το παράδειγμα).
* Visual Studio 2022 (ή οποιοδήποτε IDE C#) για τη μεταγλώττιση και εκτέλεση του κώδικα.

Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από το `Aspose.HTML`.

## Step 1: Set up the project and import namespaces

Δημιουργήστε ένα νέο έργο **Console App** και προσθέστε το πακέτο NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Στη συνέχεια, στην κορυφή του `Program.cs`, εισάγετε τους απαιτούμενους χώρους ονομάτων:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Αυτοί οι χώροι ονομάτων εκθέτουν τους τύπους `HTMLDocument`, `HtmlSaveOptions` και `WebFontStyle` που θα χρησιμοποιήσετε σε όλο το tutorial.

## Step 2: Load the source HTML document

Η πρώτη ενέργεια είναι η ανάγνωση του HTML που θέλετε να επεξεργαστείτε. Αντικαταστήστε το `"YOUR_DIRECTORY/input.html"` με την πραγματική διαδρομή του αρχείου σας.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` αναλύει το markup, δημιουργεί ένα δέντρο DOM και το ετοιμάζει για επεξεργασία. Εάν το αρχείο δεν υπάρχει, θα ριχθεί εξαίρεση, επομένως ίσως θελήσετε να τυλίξετε αυτή την κλήση σε μπλοκ try‑catch για κώδικα παραγωγής.

## Step 3: Create and configure HtmlSaveOptions

`HtmlSaveOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς τη διαδικασία αποθήκευσης. Για να ενεργοποιήσετε τις έντονες και πλάγιες μορφές web‑font, συνδυάστε τις αντίστοιχες σημαίες `WebFontStyle` χρησιμοποιώντας τον τελεστή bitwise OR (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Γιατί να διαμορφώσετε το WebFontStyle;

Κατά την εξαγωγή ενός εγγράφου HTML, το Aspose.HTML μπορεί να ενσωματώσει web fonts που ταιριάζουν με το αρχικό στυλ. Ορίζοντας το `WebFontStyle`, λέτε στον εξαγωγέα ποιες παραλλαγές γραμματοσειράς να συμπεριλάβει. Αυτό μειώνει το τελικό μέγεθος του αρχείου όταν χρειάζεστε μόνο συγκεκριμένα στυλ και εγγυάται ότι η παραγόμενη έξοδος ταιριάζει με την πηγή.

#### Συνηθισμένες παραλλαγές

| Επιθυμητό στυλ | Αντίστοιχη σημαία `WebFontStyle` |
|---------------|-----------------------------------|
| Κανονικό (regular) | `WebFontStyle.Regular` |
| Έντονο | `WebFontStyle.Bold` |
| Πλάγιο | `WebFontStyle.Italic` |
| Έντονο + Πλάγιο | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Όλες οι παραλλαγές | `WebFontStyle.All` |

Μπορείτε να συνδυάσετε οποιονδήποτε συνδυασμό ταιριάζει στο σενάριό σας.

## Step 4: Save the document with the configured options

Τώρα γράψτε το έγγραφο σε νέο αρχείο. Η μέθοδος `Save` δέχεται τη διαδρομή προορισμού και το αντικείμενο `HtmlSaveOptions` που προετοιμάσατε.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Εάν χρειάζεται να γράψετε σε μνήμη (π.χ., για αποστολή του αρχείου μέσω HTTP), χρησιμοποιήστε την υπερφόρτωση που δέχεται αντικείμενο `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Step 5: Verify the result

Ανοίξτε το `output.html` σε έναν περιηγητή ή ελέγξτε το αρχείο με έναν επεξεργαστή κειμένου. Θα πρέπει να δείτε ότι το τμήμα `<style>` περιέχει τώρα κανόνες `@font-face` για τις έντονες και πλάγιες παραλλαγές οποιωνδήποτε web fonts που αναφέρονται στο αρχικό έγγραφο.

**Αναμενόμενο απόσπασμα εξόδου:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Εάν το αρχικό HTML αναφερόταν σε οικογένεια γραμματοσειράς που είχε μόνο κανονικό βάρος, το Aspose.HTML θα συμπεριλάβει μόνο αυτό το αρχείο, σεβόμενος τη ρύθμιση `WebFontStyle`.

## Advanced: Using HtmlSaveOptions with additional features

### 5.1 Έλεγχος ενσωμάτωσης CSS

Μπορείτε να αποφασίσετε αν θα ενσωματώσετε το CSS ενσωματωμένα, θα διατηρήσετε εξωτερικούς συνδέσμους ή θα ενσωματώσετε τα πάντα:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Saving to a specific encoding

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Handling large documents

Για πολύ μεγάλα αρχεία HTML, σκεφτείτε τη ροή εξόδου για αποφυγή υψηλής κατανάλωσης μνήμης:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Error handling best practice

Τυλίξτε ολόκληρη τη ροή εργασίας σε μπλοκ try‑catch και καταγράψτε τις λεπτομέρειες της εξαίρεσης. Αυτό διασφαλίζει ότι τυχόν σφάλματα I/O ή ανάλυσης θα πιαστούν:

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

## Pro tip: Reuse HtmlSaveOptions across multiple saves

Εάν χρειάζεται να αποθηκεύσετε πολλά έγγραφα με την ίδια διαμόρφωση στυλ γραμματοσειράς, δημιουργήστε ένα μόνο αντικείμενο `HtmlSaveOptions` και επαναχρησιμοποιήστε το. Αυτό μειώνει το κόστος κατανομής αντικειμένων και εγγυάται συνεπή έξοδο.

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

## Complete runnable example

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενσωματώνει όλα τα βήματα που συζητήθηκαν. Αντιγράψτε το στο `Program.cs` και εκτελέστε το αφού προσαρμόσετε τις διαδρομές αρχείων.

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

### Αναμενόμενη έξοδος κονσόλας

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Ανοίξτε το παραγόμενο `output.html` για να επιβεβαιώσετε ότι οι έντονες και πλάγιες μορφές web‑font είναι παρούσες.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε το HtmlSaveOptions** για να ελέγξετε την ενσωμάτωση web‑font, τη διαχείριση CSS και την κωδικοποίηση κατά την αποθήκευση HTML με τη βιβλιοθήκη Aspose HTML σε C#. Διαμορφώνοντας τις σημαίες `WebFontStyle` μπορείτε να προσαρμόσετε την έξοδο ώστε να περιλαμβάνει μόνο τις παραλλαγές γραμματοσειράς που χρειάζεστε, βελτιώνοντας την απόδοση και μειώνοντας το μέγεθος του αρχείου.

Από εδώ μπορείτε να εξερευνήσετε άλλες ιδιότητες του `HtmlSaveOptions` όπως `ImageSavingMode`, `JavaScriptSavingMode`, ή να συνδυάσετε πολλαπλές επιλογές για σύνθετες διαδρομές μετατροπής. Πειραματιστείτε με αποθήκευση σε ροές για web APIs ή ενσωματώστε τη ροή εργασίας σε ένα μεγαλύτερο σύστημα δημιουργίας εγγράφων.

---

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε HTML με το Aspose.Html – Πλήρης οδηγός C#](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Πώς να χρησιμοποιήσετε το Aspose για απόδοση HTML σε PNG σε C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Πώς να χρησιμοποιήσετε το Aspose για απόδοση HTML σε PNG – Οδηγός βήμα‑βήμα](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}