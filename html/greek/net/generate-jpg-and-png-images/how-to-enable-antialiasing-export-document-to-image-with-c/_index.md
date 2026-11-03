---
category: general
date: 2026-04-06
description: Μάθετε πώς να ενεργοποιήσετε το antialiasing, να ορίσετε το πλάτος και
  το ύψος της εικόνας και να αποθηκεύσετε το έγγραφο ως PNG σε C# – ένας γρήγορος
  οδηγός για την εξαγωγή εγγράφου σε εικόνα.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: el
og_description: Πώς να ενεργοποιήσετε την εξομάλυνση όταν εξάγετε ένα έγγραφο σε εικόνα.
  Αυτός ο οδηγός σας δείχνει πώς να ορίσετε το πλάτος της εικόνας, το ύψος της εικόνας
  και να αποθηκεύσετε το έγγραφο ως PNG.
og_title: Πώς να ενεργοποιήσετε την εξομάλυνση – Εξαγωγή εγγράφου σε εικόνα
tags:
- C#
- ImageRendering
- Antialiasing
title: Πώς να ενεργοποιήσετε την εξομάλυνση – Εξαγωγή εγγράφου σε εικόνα με C#
url: /el/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε το Antialiasing – Εξαγωγή εγγράφου σε εικόνα σε C#

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε το antialiasing** ενώ μετατρέπετε ένα έγγραφο σε εικόνα; Ίσως δοκιμάσατε μια γρήγορη κλήση `Save` και το αποτέλεσμα φαινόταν σκαλισμένο, ειδικά στις διαγώνιες γραμμές. Τα καλά νέα είναι ότι δεν χρειάζεστε κάποιον μάγο των γραφικών—απλώς μερικές γραμμές C# και τις σωστές επιλογές.

Σε αυτό το tutorial θα περάσουμε από τον ορισμό του πλάτους της εικόνας, του ύψους της εικόνας και, τελικά, **αποθήκευση εγγράφου ως PNG** ώστε να μπορείτε να **εξάγετε το έγγραφο σε εικόνα** με λείες άκρες. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση snippet που παράγει ένα καθαρό PNG 800 × 600 με ενεργοποιημένο antialiasing.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)  
- Αναφορά σε βιβλιοθήκη rendering που υποστηρίζει `ImageRenderingOptions` (π.χ., Aspose.Words, Syncfusion ή οποιοδήποτε API που εκθέτει παρόμοιες ιδιότητες)  
- Βασική κατανόηση της σύνταξης C#  

Καμία βαριά εγκατάσταση—απλώς προσθέστε το πακέτο NuGet και είστε έτοιμοι.

## Βήμα 1: Εγκατάσταση της βιβλιοθήκης Rendering

Πρώτα, προσθέστε το πακέτο στο project σας. Αν χρησιμοποιείτε Aspose.Words, τρέξτε:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Κρατήστε την έκδοση της βιβλιοθήκης ενημερωμένη· η τελευταία έκδοση (από Απρίλιο 2026) προσθέτει βελτιώσεις απόδοσης για antialiasing.

## Βήμα 2: Δημιουργία του αντικειμένου Document

Φορτώστε ή δημιουργήστε το έγγραφο που θέλετε να αποδώσετε. Ακολουθεί ένα ελάχιστο παράδειγμα που δημιουργεί ένα μονοσέλιδο έγγραφο με μια απλή παράγραφο:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Η κλάση `Document` είναι το σημείο εισόδου· όλα όσα αποδίδετε προέρχονται από αυτήν. Σε πραγματικά έργα πιθανότατα θα φορτώσετε ένα υπάρχον .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Βήμα 3: Ορισμός επιλογών Rendering (Πλάτος, Ύψος, Antialiasing)

Τώρα απαντάμε στην κεντρική ερώτηση: **πώς να ενεργοποιήσετε το antialiasing**. Το αντικείμενο `ImageRenderingOptions` σας επιτρέπει να ενεργοποιήσετε την εξομάλυνση και να ελέγξετε τις διαστάσεις.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Παρατηρήστε τα σχόλια: αναφέρουν ρητά **set image width**, **set image height** και **UseAntialiasing**—τα τρία κουμπιά που μετράνε περισσότερο όταν θέλετε ένα επεξεργασμένο PNG.

### Γιατί είναι σημαντικό το Antialiasing

Χωρίς antialiasing, οι διαγώνιες γραμμές και οι καμπύλες εμφανίζονται «σκαλοπατιές» επειδή ο renderer αντιμετωπίζει κάθε pixel ως ενεργό ή ανενεργό. Η ενεργοποίησή του αναμειγνύει τα pixel των άκρων, δημιουργώντας μια οπτική απαλότητα που μιμείται αυτό που βλέπετε σε έναν επεξεργαστή φωτογραφιών. Η ανταλλαγή είναι μια μικρή αύξηση του χρόνου επεξεργασίας, αλλά για τις περισσότερες εξαγωγές UI είναι αμελητέα.

## Βήμα 4: Αποθήκευση εγγράφου ως PNG (Export Document to Image)

Με τις επιλογές έτοιμες, τελικά **αποθηκεύουμε το έγγραφο ως PNG**. Η μέθοδος `Save` δέχεται τη διαδρομή του αρχείου και τις επιλογές που μόλις διαμορφώσαμε.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Αυτό είναι—το έγγραφό σας είναι τώρα ένα PNG 800 × 600 με ενεργό antialiasing. Αν ανοίξετε το `output.png` θα δείτε καθαρό κείμενο, λείες γραμμές και χωρίς σκαλισμένα artefacts.

### Επαλήθευση του αποτελέσματος

Μπορείτε γρήγορα να ελέγξετε το αρχείο σε οποιονδήποτε προβολέα εικόνων. Αναζητήστε:

- Σωστές διαστάσεις (800 × 600)  
- Καμία ορατή σκαλοπατιδική άκρη στο κείμενο ή σε οποιοδήποτε σχήμα  
- Διαφανές φόντο αν το έγγραφό σας δεν περιείχε χρώμα φόντου (οι περισσότερες βιβλιοθήκες προεπιλογή είναι λευκό)

Αν η εικόνα φαίνεται σκαλισμένη, ελέγξτε ξανά ότι `UseAntialiasing = true` δεν παρακάμπτεται αλλού.

## Βήμα 5: Edge Cases & Variations

### Αλλαγή του μορφότυπου εξόδου

Θέλετε JPEG αντί για PNG; Απλώς αλλάξτε την επέκταση του αρχείου και προαιρετικά ρυθμίστε τη συμπίεση:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Εξαγωγή πολλαπλών σελίδων

Όταν το πηγαίο έγγραφο έχει πολλές σελίδες, ο renderer δημιουργεί ξεχωριστά αρχεία εικόνας ανά σελίδα εξ ορισμού. Μπορείτε να κάνετε βρόχο στις σελίδες:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Αποθήκευση σε Stream (π.χ., HTTP response)

Αν δημιουργείτε ένα web API, ίσως θέλετε να επιστρέψετε το PNG απευθείας:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑αντιγραφή πρόγραμμα που ενσωματώνει κάθε βήμα που συζητήθηκε:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει το `output.png` στο φάκελο του εκτελέσιμου. Ανοίξτε το και θα δείτε ένα λείο, 800 × 600 PNG—ακριβώς αυτό που θέλαμε να πετύχουμε.

## Συχνές Ερωτήσεις & Επίλυση Προβλημάτων

- **Τι γίνεται αν η εικόνα φαίνεται θολή;**  
  Η θολότητα μπορεί να συμβεί όταν μεγεθύνετε μια μικρή πηγή σελίδας. Κρατήστε το μέγεθος της πηγής σελίδας κοντά στις διαστάσεις στόχου, ή αυξήστε το DPI μέσω `imageOptions.Resolution` (π.χ., `Resolution = 300`).

- **Λειτουργεί αυτό σε .NET Framework;**  
  Ναι. Το ίδιο API υπάρχει στο κλασικό framework· απλώς αναφέρετε το αντίστοιχο DLL.

- **Μπορώ να ελέγξω το χρώμα φόντου;**  
  Απόλυτα. Ορίστε `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` πριν την αποθήκευση.

- **Είναι το antialiasing επιταχυνόμενο από υλικό;**  
  Οι περισσότερες βιβλιοθήκες εκτελούν λογισμικό antialiasing. Αν χρειάζεστε επιτάχυνση GPU, ψάξτε για engine rendering που το υποστηρίζει ρητά.

## Συμπέρασμα

Καλύψαμε **πώς να ενεργοποιήσετε το antialiasing** όταν **εξάγετε το έγγραφο σε εικόνα**, περάσαμε από **set image width** και **set image height**, και σας δείξαμε τα ακριβή βήματα για **save document as PNG**. Το παραπάνω snippet είναι έτοιμο για παραγωγή, και μπορείτε τώρα να το προσαρμόσετε σε JPEG, PDF πολλαπλών σελίδων, ή ακόμη και να ρέξετε την εικόνα απευθείας σε έναν client.

Στη συνέχεια, μπορείτε να εξερευνήσετε την προσθήκη υδατογραφιών, τη ρύθμιση DPI για εκτύπωση υψηλής ποιότητας, ή την ενσωμάτωση αυτής της λογικής σε ένα endpoint ASP.NET Core. Οι ίδιες αρχές ισχύουν—απλώς αντικαταστήστε τη διαδρομή αρχείου με ένα stream απόκρισης.

Καλή προγραμματιστική δουλειά και απολαύστε τις καθαρές, antialiased εικόνες!

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}