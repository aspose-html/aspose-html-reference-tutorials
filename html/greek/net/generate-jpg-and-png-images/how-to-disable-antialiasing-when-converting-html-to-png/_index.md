---
category: general
date: 2026-03-25
description: Μάθετε πώς να απενεργοποιήσετε την εξομάλυνση (antialiasing) κατά τη
  μετατροπή HTML σε PNG, εξασφαλίζοντας απόδοση pixel‑perfect. Περιλαμβάνει βήματα
  για τη δημιουργία εικόνας από HTML, την αποθήκευση HTML ως PNG και τη δημιουργία
  PNG από HTML.
draft: false
keywords:
- how to disable antialiasing
- convert html to png
- render html as image
- save html as png
- create png from html
language: el
og_description: Ανακαλύψτε τη βήμα‑βήμα μέθοδο για την απενεργοποίηση του antialiasing
  κατά τη μετατροπή HTML σε PNG, εξασφαλίζοντας τέλεια εικόνα pixel‑perfect κάθε φορά.
og_title: Πώς να απενεργοποιήσετε την εξομάλυνση κατά τη μετατροπή HTML σε PNG
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Πώς να απενεργοποιήσετε την εξομάλυνση κατά τη μετατροπή HTML σε PNG
url: /el/net/generate-jpg-and-png-images/how-to-disable-antialiasing-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Απενεργοποιήσετε το Antialiasing Κατά τη Μετατροπή HTML σε PNG

Έχετε αναρωτηθεί ποτέ **πώς να απενεργοποιήσετε το antialiasing** ώστε η μετατροπή HTML‑σε‑PNG να φαίνεται ακριβώς όπως η πηγαία σήμανση; Ίσως δημιουργείτε έναν γεννήτρια μικρογραφιών για UI στοιχεία και οι θολές άκρες καταστρέφουν την οπτική πιστότητα. Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να **μετατρέψουν HTML σε PNG** για στιγμιότυπα οθόνης pixel‑perfect.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη διαδικασία **απόδοσης HTML ως εικόνα**, θα ρυθμίσουμε τη γραμμή απόδοσης ώστε να απενεργοποιήσουμε το antialiasing, και τελικά θα **αποθηκεύσουμε HTML ως PNG** χρησιμοποιώντας το Aspose.HTML for .NET. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που δημιουργεί ένα καθαρό PNG από οποιοδήποτε αρχείο HTML, και θα καταλάβετε γιατί η απενεργοποίηση του antialiasing είναι σημαντική για ορισμένα σενάρια ευαίσθητα στο σχεδιασμό.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- **Aspose.HTML for .NET** πακέτο NuGet (`Aspose.HTML`).  
- Ένα απλό αρχείο `input.html` που θέλετε να rasterize.  
- Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider, ή ακόμη και VS Code με την επέκταση C#.

Δεν απαιτούνται επιπλέον εγγενείς βιβλιοθήκες ή εξωτερικά εργαλεία· το Aspose.HTML διαχειρίζεται τα πάντα στο παρασκήνιο.

## Βήμα 1: Εγκατάσταση Aspose.HTML

Το πρώτο που χρειάζεστε είναι η βιβλιοθήκη Aspose.HTML. Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.HTML
```

Ή, αν προτιμάτε το UI του NuGet, αναζητήστε **Aspose.HTML** και κάντε κλικ στο *Install*. Αυτό το πακέτο περιλαμβάνει μια ισχυρή μηχανή απόδοσης που μπορεί να εξάγει PNG, JPEG, BMP και άλλα.

> **Pro tip:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (από τον Μάρτιο 2026 είναι η 23.12) για να επωφεληθείτε από διορθώσεις σφαλμάτων που αφορούν την απόδοση εικόνας και τον έλεγχο antialiasing.

## Βήμα 2: Φόρτωση του HTML Εγγράφου

Μόλις το πακέτο είναι στη θέση του, μπορείτε να φορτώσετε το HTML που θέλετε να μετατρέψετε. Η κλάση `HTMLDocument` αφαιρεί το DOM και σας επιτρέπει να το τροποποιήσετε πριν από την απόδοση, αν χρειάζεται.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Path to your source HTML file
string inputPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Create a new HTMLDocument instance
HTMLDocument htmlDoc = new HTMLDocument(inputPath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του εγγράφου πρώτα σας δίνει την ευκαιρία να ενσωματώσετε CSS ή να διορθώσετε σχετικές URL πριν το βήμα rasterization. Επίσης απομονώνει την απόδοση από το σύστημα αρχείων, κάνοντας τον κώδικα πιο εύκολο στη δοκιμή.

## Βήμα 3: Διαμόρφωση ImageSaveOptions και Απενεργοποίηση Antialiasing

Αυτή είναι η ουσία του tutorial: η απενεργοποίηση του antialiasing. Το Aspose.HTML εκθέτει το `ImageRenderingOptions` όπου μπορείτε να αλλάξετε το `UseAntialiasing`. Ορίζοντάς το σε `false` αναγκάζει τη μηχανή να αποδώσει κάθε pixel ακριβώς όπως ορίζεται από τα διανυσματικά σχήματα, παράγοντας ένα **pixel‑perfect PNG**.

```csharp
// Create ImageSaveOptions for PNG output
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach rendering options
    ImageRenderingOptions = new ImageRenderingOptions
    {
        // Disable antialiasing for a crisp raster image
        UseAntialiasing = false
    }
};
```

### Τι Κάνει Πραγματικά το Antialiasing

Το antialiasing εξομαλύνει τις άκρες των σχημάτων αναμειγνύοντας τα χρώματα των γειτονικών pixel. Ενώ αυτό φαίνεται εξαιρετικό για φωτογραφίες ή πολύπλογα γραφικά, μπορεί να θολώσει τα αιχμηρά UI στοιχεία (π.χ. εικονίδια ή κείμενο σε μικρά μεγέθη). Η απενεργοποίησή του εξασφαλίζει ότι κάθε γραμμή παραμένει ακονισμένη—ακριβώς αυτό που χρειάζεστε όταν **δημιουργείτε PNG από HTML** για δοκιμές UI ή τεκμηρίωση.

## Βήμα 4: Απόδοση και Αποθήκευση του PNG

Τώρα που οι επιλογές είναι ρυθμισμένες, καλέστε `Save` στο `HTMLDocument`. Η μέθοδος δέχεται τη διαδρομή εξόδου και το προηγουμένως διαμορφωμένο `ImageSaveOptions`.

```csharp
// Destination path for the PNG file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");

// Render the HTML and write the PNG file
htmlDoc.Save(outputPath, saveOptions);
```

Η εκτέλεση του παραπάνω κώδικα θα δημιουργήσει το `output.png` ακριβώς δίπλα στο εκτελέσιμο σας. Ανοίξτε το σε οποιονδήποτε προβολέα εικόνας—θα δείτε μια καθαρή, χωρίς antialiasing απόδοση του `input.html`.

### Αναμενόμενο Αποτέλεσμα

| Πριν (Antialiasing Ενεργό) | Μετά (Antialiasing Απενεργοποιημένο) |
|----------------------------|--------------------------------------|
| ![Απόδοση με antialiasing](antialiased.png "παράδειγμα απενεργοποίησης antialiasing με θολές άκρες") | ![Απόδοση pixel‑perfect](pixelperfect.png "παράδειγμα απενεργοποίησης antialiasing με αιχμηρές άκρες") |

*Η αριστερή εικόνα δείχνει την προεπιλεγμένη απόδοση με antialiasing, ενώ η δεξιά παρουσιάζει το καθαρό αποτέλεσμα μετά την απενεργοποίηση του antialiasing.*

> **Σημείωση:** Τα screenshots παραπάνω είναι placeholders· αντικαταστήστε τα με τα δικά σας αρχεία όταν δημοσιεύετε.

## Βήμα 5: Επαλήθευση της Εξόδου Προγραμματιστικά (Προαιρετικό)

Αν χρειάζεται να διασφαλίσετε ότι το PNG πληροί ορισμένα κριτήρια (π.χ. ακριβείς διαστάσεις ή βάθος χρώματος), μπορείτε να το ελέγξετε χρησιμοποιώντας `System.Drawing` ή `SixLabors.ImageSharp`. Εδώ είναι ένας γρήγορος έλεγχος με `ImageSharp`:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;

using (Image<Rgba32> img = Image.Load<Rgba32>(outputPath))
{
    Console.WriteLine($"Width: {img.Width}px, Height: {img.Height}px");
    // Verify that the image has no blended pixels (simple heuristic)
    // You could compare a few pixel values against expected RGBA values.
}
```

Αυτό το επιπλέον βήμα είναι χρήσιμο όταν αυτοματοποιείτε τη δημιουργία PNG σε CI pipeline και πρέπει να εγγυηθείτε τη συνέπεια.

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

### Τι γίνεται αν το HTML μου χρησιμοποιεί εξωτερικούς πόρους;

Αν το HTML αναφέρεται σε CSS, γραμματοσειρές ή εικόνες μέσω σχετικών URL, βεβαιωθείτε ότι η βάση URL του `HTMLDocument` δείχνει στο φάκελο που περιέχει αυτά τα assets:

```csharp
HTMLDocument htmlDoc = new HTMLDocument(inputPath, new Uri("file:///" + Path.GetDirectoryName(inputPath) + "/"));
```

### Μπορώ να αλλάξω το DPI ή το Μέγεθος της Εικόνας;

Απόλυτα. Το `ImageRenderingOptions` σας επιτρέπει επίσης να ορίσετε `Resolution` (dots per inch) και `Width`/`Height`:

```csharp
saveOptions.ImageRenderingOptions.Resolution = 300; // High‑resolution PNG
saveOptions.ImageRenderingOptions.Width = 800;      // Desired pixel width
saveOptions.ImageRenderingOptions.Height = 600;     // Desired pixel height
```

Απλώς θυμηθείτε ότι η αύξηση του DPI χωρίς κλιμάκωση του viewport μπορεί να παράγει μεγαλύτερο αρχείο με το ίδιο οπτικό μέγεθος.

### Επηρεάζει η Απενεργοποίηση του Antialiasing την Αναγνωσιμότητα του Κειμένου;

Για τις περισσότερες σύγχρονες γραμματοσειρές, η απενεργοποίηση του antialiasing μπορεί να κάνει το μικρό κείμενο να φαίνεται σκαλιστό. Αν χρειάζεστε καθαρό κείμενο **και** ομαλές άκρες, σκεφτείτε να αποδώσετε σε υψηλότερη ανάλυση και μετά να κάνετε downscale με αλγόριθμο υψηλής ποιότητας. Αυτό το κόλπο διατηρεί την αναγνωσιμότητα ενώ σας δίνει έλεγχο πάνω στο τελικό pixel grid.

### Είναι Αυτή η Προσέγγιση Πλατφόρμα‑Ανεξάρτητη;

Ναι. Το Aspose.HTML είναι καθαρό .NET και τρέχει σε Windows, Linux και macOS. Η μόνη πλατφόρμα‑συγκεκριμένη λεπτομέρεια είναι η διαθεσιμότητα των συστημικών γραμματοσειρών· ίσως χρειαστεί να ενσωματώσετε προσαρμοσμένες γραμματοσειρές στο HTML ή να τις εγκαταστήσετε στο μηχάνημα-στόχο.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Περιλαμβάνει όλες τις απαραίτητες δηλώσεις `using`, διαχείριση σφαλμάτων και σχόλια.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // -------------------------------------------------
                // 1️⃣ Define input and output paths
                // -------------------------------------------------
                string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
                string outputPng = Path.Combine(Environment.CurrentDirectory, "output.png");

                // -------------------------------------------------
                // 2️⃣ Load the HTML document
                // -------------------------------------------------
                // BaseUri ensures relative resources resolve correctly
                var htmlDoc = new HTMLDocument(inputHtml, new Uri("file:///" + Path.GetDirectoryName(inputHtml) + "/"));

                // -------------------------------------------------
                // 3️⃣ Configure rendering options – disable antialiasing
                // -------------------------------------------------
                var saveOptions = new ImageSaveOptions(SaveFormat.Png)
                {
                    ImageRenderingOptions = new ImageRenderingOptions
                    {
                        UseAntialiasing = false,   // 👈 The key line for pixel‑perfect output
                        // Optional: set resolution or size here
                    }
                };

                // -------------------------------------------------
                // 4️⃣ Render and save the PNG
                // -------------------------------------------------
                htmlDoc.Save(outputPng, saveOptions);
                Console.WriteLine($"✅ PNG created at: {outputPng}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Τρέξτε το πρόγραμμα, και θα δείτε το **output.png** να εμφανίζεται δίπλα στο εκτελέσιμο. Ανοίξτε το—χωρίς θολές άκρες, μόνο μια καθαρή raster copy του HTML σας.

## Συμπέρασμα

Καλύψαμε **πώς να απενεργοποιήσετε το antialiasing** όταν **μετατρέπετε HTML σε PNG**, περάσαμε από κάθε βήμα διαμόρφωσης, και παρέχουμε ένα πλήρες, εκτελέσιμο παράδειγμα που **αποδίδει HTML ως εικόνα**, **αποθηκεύει HTML ως PNG**, και σας επιτρέπει να **δημιουργήσετε PNG από HTML** με pixel‑perfect πιστότητα.  

Αν θέλετε να προχωρήσετε παραπέρα, δοκιμάστε διαφορετικές μορφές εικόνας (JPEG, BMP), εξερευνήστε τεχνικές κλιμάκωσης vector‑to‑raster, ή ενσωματώστε αυτό το snippet σε μια web υπηρεσία που δημιουργεί μικρογραφίες on‑the‑fly. Οι ίδιες αρχές ισχύουν είτε χτίζετε έναν γεννήτρια τεκμηρίωσης, ένα εργαλείο visual regression testing, είτε έναν δυναμικό εξαγωγέα γραφημάτων.

Έχετε περισσότερες ερωτήσεις σχετικά με ιδιαιτερότητες απόδοσης ή δυνατότητες του Aspose.HTML; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}