---
category: general
date: 2025-12-29
description: Δημιουργήστε έγγραφο HTML σε C# και μάθετε πώς να ορίσετε την οικογένεια
  γραμματοσειράς, το μέγεθος γραμματοσειράς, στη συνέχεια αποθηκεύστε το HTML ως PDF
  ή μετατρέψτε το HTML σε PDF χρησιμοποιώντας το Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: el
og_description: Δημιουργήστε έγγραφο HTML σε C# και δείτε αμέσως πώς να ορίσετε την
  οικογένεια γραμματοσειράς, το μέγεθος γραμματοσειράς, στη συνέχεια αποθηκεύστε το
  HTML ως PDF ή μετατρέψτε το HTML σε PDF με το Aspose.HTML.
og_title: Δημιουργία εγγράφου HTML – Στυλιζαρισμένο κείμενο & εξαγωγή PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Δημιουργία εγγράφου HTML με μορφοποιημένο κείμενο και εξαγωγή σε PDF – Πλήρης
  οδηγός
url: /el/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου HTML με μορφοποιημένο κείμενο και εξαγωγή σε PDF

Κάποτε χρειάστηκε να **δημιουργήσετε έγγραφο HTML** εν κινήσει και να το μετατρέψετε σε PDF χωρίς να αφήσετε τον κώδικα C#; Ίσως δημιουργείτε μια μηχανή αναφορών, έναν γεννήτρια τιμολογίων ή απλώς μια γρήγορη προεπισκόπηση για χρήστες. Τα καλά νέα είναι ότι μπορείτε να το κάνετε σε λίγες γραμμές χρησιμοποιώντας το Aspose.HTML, και θα έχετε πλήρη έλεγχο πάνω στην οικογένεια γραμματοσειράς, το μέγεθος γραμματοσειράς και ακόμη και το έντονο‑πλάγιο στυλ.

Σε αυτό το tutorial θα περάσουμε από τη διαδικασία από την αρχική δημιουργία ενός εγγράφου HTML στη μνήμη μέχρι την αποθήκευση του ως αρχείο PDF. Στο τέλος θα ξέρετε ακριβώς πώς να **ορίσετε οικογένεια γραμματοσειράς**, **ορίσετε μέγεθος γραμματοσειράς**, και **αποθηκεύσετε HTML ως PDF** (δηλαδή **μετατρέψετε HTML σε PDF**) με ένα καθαρό, έτοιμο για παραγωγή παράδειγμα κώδικα.

## Τι θα χρειαστείτε

- .NET 6+ (το API λειτουργεί τόσο με .NET Core όσο και με .NET Framework)  
- Πακέτο NuGet Aspose.HTML for .NET (`Aspose.Html`) – εγκαταστήστε το με `dotnet add package Aspose.Html`  
- Ένας φάκελος στο δίσκο όπου μπορεί να γραφτεί το παραγόμενο PDF  

Καμία επιπλέον πρότυπη HTML, κανένας εξωτερικός μετατροπέας, μόνο καθαρός C#.

![Δημιουργία εγγράφου HTML εικονογράφηση](/images/create-html-document.png){alt="παράδειγμα δημιουργίας εγγράφου HTML"}

## Βήμα 1: Δημιουργία του εγγράφου HTML

Πρώτα, χρειαζόμαστε ένα κενό αντικείμενο HTMLDocument. Σκεφτείτε το ως ένα φρέσκο καμβά όπου θα ζωγραφίσετε αργότερα την μορφοποιημένη παράγραφο.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Γιατί είναι σημαντικό:** Το `HTMLDocument` σας παρέχει μια δομή τύπου DOM που μπορείτε να χειριστείτε προγραμματιστικά. Δεν χρειάζεται να αγγίξετε ακατέργαστες συμβολοσειρές ή I/O αρχείων μέχρι το πολύ τέλος.

## Βήμα 2: Προσθήκη παραγράφου και ορισμός οικογένειας γραμματοσειράς & μεγέθους

Τώρα θα δημιουργήσουμε ένα στοιχείο `<p>`, θα εισάγουμε κείμενο και θα ορίσουμε ρητά την οικογένεια γραμματοσειράς και το μέγεθος. Εδώ μπροστά βγαίνουν οι λέξεις-κλειδιά **set font family** και **set font size**.

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

**Συμβουλή:** Αν χρειάζεστε εναλλακτική γραμματοσειρά ασφαλή για το web, μπορείτε να δώσετε μια λίστα χωρισμένη με κόμμα όπως `"Arial, Helvetica, sans-serif"`· το πρόγραμμα περιήγησης (ή το Aspose) θα επιλέξει την πρώτη διαθέσιμη γραμματοσειρά.

## Βήμα 3: Εφαρμογή έντονου και πλάγιου στυλ με σημαίες WebFontStyle

Το Aspose.HTML εκθέτει ένα χρήσιμο enum `WebFontStyle` που σας επιτρέπει να συνδυάσετε στυλ με bitwise OR. Ας κάνουμε το κείμενο ταυτόχρονα έντονο **και** πλάγιο.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Τι συμβαίνει στο παρασκήνιο;** Η ιδιότητα `FontStyle` μεταφράζεται σε δηλώσεις CSS `font-weight` και `font-style`. Με το OR των σημαιών αποφεύγουμε την ανάγκη για δύο ξεχωριστές γραμμές CSS.

## Βήμα 4: Μετατροπή του HTML σε PDF (Αποθήκευση HTML ως PDF)

Το τελευταίο βήμα είναι η πραγματική μετατροπή. Με μία κλήση στο `Save`, το Aspose.HTML αποδίδει το DOM και γράφει ένα αρχείο PDF στο δίσκο. Αυτό καλύπτει τόσο τις απαιτήσεις **save html as pdf** όσο και **convert html to pdf**.

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

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `styled.pdf` και θα δείτε μια μοναδική παράγραφο με το κείμενο “Bold & Italic text” σε 18‑px Arial, εμφανιζόμενο έντονα και πλάγια. Οι διαστάσεις του PDF ταιριάζουν με μια τυπική σελίδα A4, και το κείμενο είναι επιλέξιμο—ευχαριστώντας το διανυσματικό rendering.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

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

### Εκτέλεση του κώδικα

1. Εγκαταστήστε το πακέτο NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Αντικαταστήστε το `C:\Temp\styled.pdf` με έναν φάκελο στον οποίο έχετε δικαίωμα εγγραφής.  
3. Κατασκευάστε και τρέξτε: `dotnet run`.  

Θα πρέπει να δείτε το μήνυμα στην κονσόλα που επιβεβαιώνει τη θέση του αρχείου, και το PDF θα περιέχει τη μορφοποιημένη παράγραφο.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν χρειαστώ προσαρμοσμένη γραμματοσειρά web;**  
  Φορτώστε τη γραμματοσειρά με `HTMLFontFaceRule` ή αναφέρετε ένα απομακρυσμένο αρχείο CSS `@font-face` πριν δημιουργήσετε την παράγραφο.

- **Μπορώ να προσθέσω εικόνες πριν τη μετατροπή;**  
  Απόλυτα. Χρησιμοποιήστε `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` και ορίστε `img.Source` σε τοπική διαδρομή ή data URI.

- **Τι γίνεται με PDF πολλαπλών σελίδων;**  
  Προσθέστε περισσότερα στοιχεία (πίνακες, div κ.λπ.) και το Aspose.HTML θα σελιδοποιήσει αυτόματα όταν το περιεχόμενο υπερβεί το ύψος της σελίδας.

- **Υπάρχει τρόπος να ελέγξω τα μεταδεδομένα του PDF;**  
  Περάστε μια παρουσία `PdfSaveOptions` και ορίστε ιδιότητες όπως `Author`, `Title` ή `PdfAConformanceLevel`.

## Περίληψη

Καλύψαμε πώς να **δημιουργήσετε έγγραφο HTML** σε C#, **ορίσετε οικογένεια γραμματοσειράς**, **ορίσετε μέγεθος γραμματοσειράς**, να εφαρμόσετε στυλ έντονο‑πλάγιο, και τελικά **αποθηκεύσετε HTML ως PDF**—δηλαδή **να μετατρέψετε HTML σε PDF** με το Aspose.HTML. Το απόσπασμα κώδικα είναι αρκετά μικρό για να το ενσωματώσετε σε οποιοδήποτε έργο .NET, αλλά και αρκετά πλήρες για να λειτουργήσει ως σταθερό θεμέλιο για πιο σύνθετα σενάρια αναφοράς.

## Επόμενα Βήματα

- Πειραματιστείτε με κλάσεις CSS για επαναχρησιμοποιήσιμη μορφοποίηση.  
- Συνδυάστε πολλαπλές παραγράφους, πίνακες και εικόνες για πιο πλούσια PDFs.  
- Εξερευνήστε τη συμμόρφωση PDF/A αν χρειάζεστε έγγραφα αρχείου υψηλής ποιότητας.  

Νιώστε ελεύθεροι να τροποποιήσετε τη γραμματοσειρά, το μέγεθος ή τα χρώματα—δεν υπάρχει όριο σε ό,τι μπορείτε να δημιουργήσετε προγραμματιστικά. Καλό κώδικα, και τα PDFs σας να αποδίδουν πάντα ακριβώς όπως το φαντάζεστε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}