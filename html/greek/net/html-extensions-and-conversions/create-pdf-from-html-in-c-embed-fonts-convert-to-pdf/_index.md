---
category: general
date: 2026-03-29
description: Δημιουργήστε PDF από HTML με το Aspose.HTML σε C#. Μάθετε πώς να ενσωματώσετε
  γραμματοσειρά, να μετατρέψετε HTML σε PDF και να αποθηκεύσετε HTML ως PDF σε λίγα
  βήματα.
draft: false
keywords:
- create pdf from html
- how to embed font
- convert html to pdf
- save html as pdf
- how to create pdf
language: el
og_description: Δημιουργήστε PDF από HTML με το Aspose.HTML. Αυτός ο οδηγός δείχνει
  πώς να ενσωματώσετε γραμματοσειρά, να μετατρέψετε HTML σε PDF και να αποθηκεύσετε
  HTML ως PDF γρήγορα.
og_title: Δημιουργία PDF από HTML σε C# – Ενσωμάτωση γραμματοσειρών & Μετατροπή σε
  PDF
tags:
- Aspose.HTML
- C#
- PDF generation
title: Δημιουργία PDF από HTML σε C# – Ενσωμάτωση γραμματοσειρών & Μετατροπή σε PDF
url: /el/net/html-extensions-and-conversions/create-pdf-from-html-in-c-embed-fonts-convert-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF από HTML σε C# – Ενσωμάτωση Γραμματοσειρών & Μετατροπή σε PDF

Ποτέ δεν χρειάστηκε να **δημιουργήσετε PDF από HTML** χωρίς να ξέρετε πώς να διατηρήσετε τις προσαρμοσμένες γραμματοσειρές σας καθαρά; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν μετατρέπουν περιεχόμενο ιστού σε εκτυπώσιμη μορφή. Τα καλά νέα είναι ότι το Aspose.HTML το κάνει εύκολο: μπορείτε να ενσωματώσετε μια web‑font, να μετατρέψετε HTML σε PDF και ακόμη **να αποθηκεύσετε HTML ως PDF** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεστε: δημιουργία ενός εγγράφου HTML, εκμάθηση **πώς να ενσωματώσετε γραμματοσειρά**, μετατροπή του markup σε PDF και τέλος αποθήκευση του αποτελέσματος. Στο τέλος θα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (το API λειτουργεί επίσης με .NET Core και .NET Framework)  
- Aspose.HTML for .NET (μπορείτε να κατεβάσετε το δωρεάν trial πακέτο NuGet: `Aspose.HTML`)  
- Ένα αρχείο προσαρμοσμένης γραμματοσειράς (π.χ., `OpenSans.woff2`) τοποθετημένο δίπλα στο εκτελέσιμο σας  
- Ένα αγαπημένο IDE—Visual Studio, Rider ή ακόμη και VS Code αρκεί  

Καμία επιπλέον ρύθμιση, καμία εξωτερική υπηρεσία. Μόνο λίγες αναφορές NuGet και είστε έτοιμοι.

---

## Βήμα 1: Δημιουργία PDF από HTML – Αρχικοποίηση του HTMLDocument

Πρώτα απ' όλα: χρειάζεστε ένα αντικείμενο `HTMLDocument` που αντιπροσωπεύει τη σελίδα που θέλετε να μετατρέψετε σε PDF. Σκεφτείτε το ως έναν εικονικό καμβά περιηγητή όπου μπορείτε να ενσωματώσετε στυλ, scripts ή ακατέργαστο HTML.

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

> **Γιατί είναι σημαντικό:** Η κλάση `HTMLDocument` αναλύει το markup ακριβώς όπως θα έκανε ένας περιηγητής, διασφαλίζοντας ότι η διάταξη, το CSS και οι γραμματοσειρές γίνονται σεβαστές πριν η μηχανή PDF πάρει το χειρισμό.

---

## Βήμα 2: Πώς να Ενσωματώσετε Γραμματοσειρά – Προσθήκη ενός `<style>` Block με @font-face

Η ενσωμάτωση μιας προσαρμοσμένης γραμματοσειράς είναι μια διαδικασία δύο βημάτων: δηλώνετε τη γραμματοσειρά με `@font-face`, έπειτα την εφαρμόζετε στα στοιχεία που σας ενδιαφέρουν. Παρακάτω δημιουργούμε το στοιχείο style δυναμικά, αντλώντας το αρχείο γραμματοσειράς από τον ίδιο φάκελο με το εκτελέσιμο.

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

> **Pro tip:** Αν χρειάζεστε πολλαπλά βάρη ή στυλ, προσθέστε επιπλέον κανόνες `@font-face` με `font-weight: 700` ή `font-style: italic`. Το Aspose.HTML θα σεβαστεί κάθε παραλλαγή κατά το rendering.

---

## Βήμα 3: Προσθήκη Περιεχομένου – Συμπλήρωση του Body με HTML

Τώρα που η γραμματοσειρά είναι έτοιμη, προσθέστε λίγο HTML στο σώμα του εγγράφου. Οτιδήποτε γράψετε εδώ θα αποδοθεί χρησιμοποιώντας την ενσωματωμένη γραμματοσειρά.

```csharp
        // 3️⃣ Add some content that will use the defined font style
        htmlDocument.Body.InnerHTML = "<p>Styled text using WebFontStyle.</p>";
```

> **Τι γίνεται αν χρειάζεστε πιο σύνθετο markup;** Μπορείτε να φορτώσετε ένα εξωτερικό αρχείο HTML μέσω `new HTMLDocument("file.html")` ή να δημιουργήσετε ένα πλήρες DOM δέντρο προγραμματιστικά—το Aspose.HTML διαχειρίζεται πίνακες, εικόνες και ακόμη SVG.

---

## Βήμα 4: Μετατροπή HTML σε PDF και Αποθήκευση HTML ως PDF

Σε αυτό το σημείο έχετε ένα πλήρως μορφοποιημένο έγγραφο HTML στη μνήμη. Η επόμενη γραμμή λέει στο Aspose.HTML να το αποδώσει κατευθείαν σε αρχείο PDF. Αυτό είναι το βασικό στοιχείο του **convert html to pdf**.

```csharp
        // 4️⃣ Choose an output path and save the document as PDF
        string outputPath = "styled.pdf"; // change to your desired folder
        htmlDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

> **Γιατί λειτουργεί το `Save`:** Στο παρασκήνιο, το Aspose.HTML rasterizes το DOM σε έναν καμβά PDF, διατηρώντας το κείμενο ως vector (οπότε η γραμματοσειρά παραμένει επιλέξιμη) και τη πιστότητα της διάταξης. Δεν απαιτείται ενδιάμεση μετατροπή σε εικόνα, κάτι που κρατά το μέγεθος του αρχείου χαμηλό.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος – Άνοιγμα του PDF και Έλεγχος της Γραμματοσειράς

Αφού τρέξετε το πρόγραμμα, εντοπίστε το `styled.pdf` και ανοίξτε το σε οποιονδήποτε PDF viewer. Θα πρέπει να δείτε την παράγραφο αποδομένη σε *OpenSans* με έντονη και πλάγια μορφοποίηση. Αν το κείμενο εμφανίζεται με fallback γραμματοσειρά, ελέγξτε:

1. Το `OpenSans.woff2` βρίσκεται στον ίδιο φάκελο με το εκτελέσιμο.  
2. Το όνομα του αρχείου ταιριάζει ακριβώς (case‑sensitive σε Linux).  
3. Η URL `src` στο `@font-face` χρησιμοποιεί τη σωστή σχετική διαδρομή.

---

## Συνηθισμένα Προβλήματα όταν **How to Create PDF** from HTML

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| Η γραμματοσειρά δεν εμφανίζεται | Λάθος διαδρομή ή λείπει το αρχείο | Χρησιμοποιήστε απόλυτη διαδρομή (`Path.Combine(Directory.GetCurrentDirectory(), "OpenSans.woff2")`) |
| Το κείμενο εμφανίζεται ως εικόνα | Λάθος χρήση του enum `WebFontStyle` | Βεβαιωθείτε ότι κάνετε cast σε `int` όπως φαίνεται, ή ορίστε απευθείας `font-weight: bold;` στο CSS |
| Το PDF είναι κενό | Δεν υπάρχει περιεχόμενο στο `Body.InnerHTML` | Επαληθεύστε ότι η HTML συμβολοσειρά δεν είναι κενή ή κατεστραμμένη |
| Μεγάλο μέγεθος αρχείου | Ενσωματωμένες εικόνες υψηλής ανάλυσης | Συμπιέστε τις εικόνες ή χρησιμοποιήστε στοιχείο `Image` με `srcset` |

---

## Bonus: Αποθήκευση HTML ως PDF με Προσαρμοσμένο Μέγεθος Σελίδας

Αν χρειάζεστε συγκεκριμένη διάταξη—π.χ. A4 portrait—μπορείτε να περάσετε `PdfSaveOptions` κατά την κλήση του `Save`. Αυτό δείχνει έναν ακόμη τρόπο **save html as pdf** με λεπτομερή έλεγχο.

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

> **Σημείωση για ειδικές περιπτώσεις:** Όταν ορίζετε μέγεθος σελίδας, το Aspose.HTML θα επαναδιαρθρώσει το περιεχόμενο ώστε να χωράει, κάτι που μπορεί να επηρεάσει τις αλλαγές γραμμής. Δοκιμάστε με το πραγματικό σας HTML για να βεβαιωθείτε ότι η διάταξη παραμένει αποδεκτή.

---

## Πλήρες Παράδειγμα Εργασίας (Ready‑to‑Copy)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Απλώς τοποθετήστε το αρχείο `OpenSans.woff2` δίπλα στο `.csproj`, εγκαταστήστε το πακέτο NuGet Aspose.HTML, και πατήστε **Run**.

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

**Αναμενόμενο αποτέλεσμα:** Δύο αρχεία PDF (`styled.pdf` και `styled-a4.pdf`) εμφανίζονται στον φάκελο εκτέλεσης. Και τα δύο εμφανίζουν την παράγραφο σε OpenSans, έντονη και πλάγια, ακριβώς όπως ορίζεται στο CSS.

---

## Συμπέρασμα

Σας δείξαμε πώς να **δημιουργήσετε PDF από HTML** χρησιμοποιώντας το Aspose.HTML, καλύψαμε **πώς να ενσωματώσετε γραμματοσειρά**, παρουσιάσαμε μια καθαρή ροή **convert html to pdf**, και εξετάσαμε ένα προχωρημένο σενάριο **save html as pdf** με προσαρμοσμένες διαστάσεις σελίδας. Η βασική ιδέα είναι απλή: δημιουργήστε ένα `HTMLDocument`, ενσωματώστε έναν κανόνα `@font-face`, προσθέστε το markup σας, και αφήστε το Aspose να κάνει το δύσκολο.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε τη γραμματοσειρά, να προσθέσετε εικόνες ή να δημιουργήσετε αναφορές πολλαπλών σελίδων. Μπορείτε επίσης να πειραματιστείτε με CSS media queries για διαφορετικές διατάξεις για οθόνη vs. εκτύπωση. Η βιβλιοθήκη είναι αρκετά ευέλικτη για τιμολόγια, πιστοποιητικά ή ακόμη και e‑books—όλα χωρίς να αφήσετε τη C#.

Αν αντιμετωπίσετε προβλήματα, ελέγξτε ξανά τη διαδρομή της γραμματοσειράς και βεβαιωθείτε ότι η έκδοση του πακέτου NuGet ταιριάζει με το .NET runtime που στοχεύετε. Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή HTML σε όμορφα PDFs!  

<img src="assets/create-pdf-from-html-diagram.png" alt="Παράδειγμα δημιουργίας PDF από HTML με ενσωματωμένη γραμματοσειρά">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}