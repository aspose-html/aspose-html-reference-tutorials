---
category: general
date: 2026-08-19
description: Αποθήκευση HTML ως ZIP σε C# χρησιμοποιώντας το Aspose.HTML και έναν
  προσαρμοσμένο διαχειριστή πόρων. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για την ενσωμάτωση
  πόρων και τη δημιουργία ενός φορητού αρχείου.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save HTML as ZIP
- custom resource handler
- Aspose.HTML C#
- HTML archive generation
- resource streaming C#
language: el
lastmod: 2026-08-19
og_description: Αποθηκεύστε HTML ως ZIP σε C# χρησιμοποιώντας το Aspose.HTML και έναν
  προσαρμοσμένο διαχειριστή πόρων. Αυτό το σεμινάριο δείχνει τον πλήρη κώδικα, εξηγεί
  γιατί κάθε βήμα είναι σημαντικό και καλύπτει κοινά προβλήματα.
og_image_alt: Screenshot of C# code that saves an HTML document as a ZIP archive
og_title: Αποθήκευση HTML ως ZIP με προσαρμοσμένο διαχειριστή πόρων σε C# – πλήρης
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  headline: Save HTML as ZIP with a custom resource handler in C#
  type: TechArticle
- description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  name: Save HTML as ZIP with a custom resource handler in C#
  steps:
  - name: Saving to a specific folder inside the ZIP
    text: 'If you want all resources to reside under a subfolder (e.g., `assets/`),
      modify the handler to prepend the folder name to each file name:'
  - name: Streaming directly to a network location
    text: 'When the ZIP must be sent over HTTP without touching the local file system,
      use a `MemoryStream` for the final archive:'
  - name: Handling large resources
    text: 'Large images or videos can exhaust memory if you keep everything in `MemoryStream`.
      Switch to a file‑based stream inside the handler:'
  - name: Preserving original URLs
    text: 'Aspose.HTML rewrites the `src`/`href` attributes to point to the new locations
      inside the ZIP. If you need to keep the original URLs for later processing,
      capture them before saving:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- ZIP archive
- resource handling
title: Αποθήκευση HTML ως ZIP με προσαρμοσμένο διαχειριστή πόρων σε C#
url: /el/net/advanced-features/save-html-as-zip-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση HTML ως ZIP με προσαρμοσμένο διαχειριστή πόρων σε C#

Εάν χρειάζεται να **αποθηκεύσετε HTML ως ZIP** ελέγχοντας πώς αποθηκεύονται οι συνδεδεμένοι πόροι, αυτός ο οδηγός παρέχει μια πλήρη λύση. Θα μάθετε πώς να δημιουργήσετε έναν προσαρμοσμένο διαχειριστή πόρων, να ρυθμίσετε τις επιλογές αποθήκευσης Aspose.HTML και να δημιουργήσετε ένα φορητό αρχείο ZIP που περιέχει το αρχείο HTML και τα περιουσιακά του στοιχεία.

Η σωστή ενσωμάτωση των πόρων είναι σημαντική όταν θέλετε να διανείμετε μια αυτόνομη ιστοσελίδα, να αρχειοθετήσετε μια αναφορά για συμμόρφωση ή να αποθηκεύσετε ένα στιγμιότυπο για χρήση εκτός σύνδεσης. Τα παρακάτω βήματα λειτουργούν με Aspose.HTML 23.10 ή νεότερη έκδοση και απαιτούν μόνο περιβάλλον ανάπτυξης .NET.

## Τι θα δημιουργήσετε

Στο τέλος αυτού του tutorial θα έχετε:

* Μια κλάση C# που υλοποιεί το `ResourceHandler` και επιστρέφει ένα stream για κάθε πόρο.
* Κώδικα που φορτώνει ένα υπάρχον αρχείο HTML από το δίσκο.
* Ρύθμιση του `HTMLSaveOptions` ώστε να χρησιμοποιεί τον προσαρμοσμένο διαχειριστή.
* Κλήση στο `HTMLDocument.Save` που παράγει το `output.zip`, ένα αρχείο ZIP που περιέχει το έγγραφο HTML και όλους τους αναφερόμενους πόρους.

## Προαπαιτήσεις

* .NET 6.0 SDK ή νεότερο (το παράδειγμα λειτουργεί επίσης σε .NET Framework 4.7.2).
* Visual Studio 2022 ή οποιοδήποτε IDE που υποστηρίζει έργα C#.
* Πακέτο NuGet Aspose.HTML for .NET (`Aspose.Html`).
* Ένα αρχείο HTML (`example.html`) με τουλάχιστον έναν εξωτερικό πόρο (εικόνα, CSS, script) ώστε να δείτε τον διαχειριστή σε δράση.

## Βήμα 1: Δημιουργία προσαρμοσμένου διαχειριστή πόρων

Ο **προσαρμοσμένος διαχειριστής πόρων** καθορίζει πού γράφεται κάθε εξωτερικό στοιχείο. Η υλοποίηση του `ResourceHandler` σας δίνει πλήρη έλεγχο του stream εξόδου.

```csharp
using Aspose.Html;
using System.IO;

/// <summary>
/// Provides a stream for each resource referenced by the HTML document.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    /// <summary>
    /// Returns a writable stream for the given resource.
    /// </summary>
    /// <param name="resource">Metadata about the resource being saved.</param>
    /// <returns>A stream that Aspose.HTML will write the resource to.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // Create a memory stream for the resource.
        // In production you might write to a file on disk, a cloud blob, or a database.
        return new MemoryStream();
    }
}
```

**Γιατί είναι σημαντικό:**  
Η `HandleResource` καλείται για κάθε εξωτερικό αρχείο (εικόνες, φύλλα στυλ, scripts). Επιστρέφοντας ένα νέο `MemoryStream` επιτρέπετε στο Aspose.HTML να συλλέξει τα δεδομένα στη μνήμη, τα οποία η διαδικασία αποθήκευσης θα συμπιέσει αργότερα σε αρχείο ZIP. Εάν χρειάζεστε τους πόρους στο δίσκο, αντικαταστήστε το `new MemoryStream()` με `File.Create(Path.Combine(outputFolder, resource.FileName))`.

## Βήμα 2: Φόρτωση του εγγράφου HTML

Φορτώστε το αρχείο πηγής χρησιμοποιώντας το `HTMLDocument`. Ο κατασκευαστής δέχεται διαδρομή αρχείου, URL ή stream.

```csharp
using Aspose.Html;

// Adjust the path to point to your HTML file.
string htmlPath = Path.Combine("YOUR_DIRECTORY", "example.html");

// Load the document into memory.
HTMLDocument doc = new HTMLDocument(htmlPath);
```

**Γιατί είναι σημαντικό:**  
Η φόρτωση του εγγράφου πρώτα διασφαλίζει ότι το Aspose.HTML αναλύει το DOM και εντοπίζει όλους τους συνδεδεμένους πόρους. Η βιβλιοθήκη στη συνέχεια περνά κάθε εντοπισμένο πόρο στον διαχειριστή που ορίσατε στο προηγούμενο βήμα.

## Βήμα 3: Ρύθμιση επιλογών αποθήκευσης με τον προσαρμοσμένο διαχειριστή

Το `HTMLSaveOptions` σας επιτρέπει να ορίσετε τη μορφή εξόδου και τον διαχειριστή πόρων.

```csharp
using Aspose.Html.Saving;

// Create default save options.
HTMLSaveOptions saveOptions = new HTMLSaveOptions();

// Attach the custom resource handler.
saveOptions.ResourceHandler = new MyResourceHandler();
```

**Γιατί είναι σημαντικό:**  
Χωρίς την ανάθεση του `ResourceHandler`, το Aspose.HTML γράφει τους πόρους σε έναν προσωρινό φάκελο στο δίσκο, τον οποίο δεν μπορείτε να ελέγξετε. Συνδέοντας το `MyResourceHandler`, καθορίζετε ακριβώς πώς θα αποθηκευτεί κάθε πόρος πριν δημιουργηθεί το αρχείο ZIP.

## Βήμα 4: Αποθήκευση του εγγράφου ως αρχείο ZIP

Τέλος, καλέστε το `HTMLDocument.Save` με `SaveFormat.Zip`. Η μέθοδος συμπιέζει το αρχείο HTML και όλα τα streams που παρείχε ο διαχειριστής.

```csharp
// Define the output ZIP path.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Save the document as a ZIP archive.
doc.Save(zipPath, SaveFormat.Zip, saveOptions);
```

Με την ολοκλήρωση της κλήσης, το `output.zip` περιέχει:

* `example.html` – το αρχικό αρχείο HTML με ενημερωμένους συνδέσμους πόρων.
* Όλα τα εξωτερικά στοιχεία (εικόνες, CSS, JS) αποθηκευμένα ως ξεχωριστές καταχωρήσεις, καθεμία δημιουργημένη από τον προσαρμοσμένο διαχειριστή.

## Επαλήθευση του αποτελέσματος

Ανοίξτε το παραγόμενο ZIP με οποιονδήποτε προβολέα αρχείων. Θα πρέπει να δείτε μια δομή φακέλων παρόμοια με:

```
output.zip
│─ example.html
│─ images/
│   └─ logo.png
│─ styles/
│   └─ main.css
│─ scripts/
│   └─ app.js
```

Ανοίξτε το `example.html` από το εξαγόμενο φάκελο σε έναν φυλλομετρητή· η σελίδα πρέπει να αποδίδει ακριβώς όπως το αρχικό αρχείο, επιβεβαιώνοντας ότι οι πόροι ενσωματώθηκαν σωστά.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Αποθήκευση σε συγκεκριμένο φάκελο μέσα στο ZIP

Εάν θέλετε όλοι οι πόροι να βρίσκονται κάτω από υποφάκελο (π.χ., `assets/`), τροποποιήστε τον διαχειριστή ώστε να προσθέτει το όνομα του φακέλου στο όνομα κάθε αρχείου:

```csharp
public override Stream HandleResource(Resource resource)
{
    string folder = "assets";
    string entryName = Path.Combine(folder, resource.FileName);
    // Aspose.HTML uses the entry name when packing the ZIP.
    resource.FileName = entryName;
    return new MemoryStream();
}
```

### Απευθείας ροή σε τοποθεσία δικτύου

Όταν το ZIP πρέπει να σταλεί μέσω HTTP χωρίς να αγγίξει το τοπικό σύστημα αρχείων, χρησιμοποιήστε ένα `MemoryStream` για το τελικό αρχείο:

```csharp
using (var zipStream = new MemoryStream())
{
    doc.Save(zipStream, SaveFormat.Zip, saveOptions);
    zipStream.Position = 0; // Reset for reading.
    // Send zipStream to a web API, store in Azure Blob, etc.
}
```

### Διαχείριση μεγάλων πόρων

Μεγάλες εικόνες ή βίντεο μπορούν να εξαντλήσουν τη μνήμη εάν όλα παραμένουν σε `MemoryStream`. Μεταβείτε σε ροή βασισμένη σε αρχείο μέσα στον διαχειριστή:

```csharp
public override Stream HandleResource(Resource resource)
{
    string tempPath = Path.GetTempFileName();
    return new FileStream(tempPath, FileMode.Create, FileAccess.Write);
}
```

Μετά το `doc.Save`, μπορείτε να διαγράψετε τα προσωρινά αρχεία.

### Διατήρηση των αρχικών URL

Το Aspose.HTML ξαναγράφει τα χαρακτηριστικά `src`/`href` ώστε να δείχνουν στις νέες θέσεις μέσα στο ZIP. Εάν χρειάζεται να διατηρήσετε τα αρχικά URL για μεταγενέστερη επεξεργασία, καταγράψτε τα πριν από την αποθήκευση:

```csharp
foreach (var img in doc.Images)
{
    Console.WriteLine($"Original src: {img.Source}");
}
```

## Pro tips

* **Επαναχρησιμοποίηση του διαχειριστή** – Δημιουργήστε μία μόνο παρουσία του `MyResourceHandler` και επαναχρησιμοποιήστε την σε πολλαπλές αποθηκεύσεις για να αποφύγετε επαναλαμβανόμενες εκχωρήσεις.
* **Επικύρωση πόρων** – Μέσα στη `HandleResource`, μπορείτε να εξετάσετε το `resource.MimeType` ή το `resource.FileName` για να φιλτράρετε ανεπιθύμητα αρχεία (π.χ., να παραλείψετε scripts ανάλυσης).
* **Ορισμός επιπέδου συμπίεσης** – Το `HTMLSaveOptions` εκθέτει την ιδιότητα `CompressionLevel` (0–9). Υψηλότερες τιμές παράγουν μικρότερα ZIP με κόστος μεγαλύτερης χρήσης CPU.

## Πλήρες, εκτελέσιμο παράδειγμα

Ακολουθεί το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε ένα νέο έργο κονσόλας (`dotnet new console`). Δείχνει κάθε βήμα, από τη φόρτωση του αρχείου HTML έως την παραγωγή του `output.zip`.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Return a memory stream for each resource.
        // Replace with FileStream if you need disk persistence.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Define paths.
        string baseDir = Path.Combine(Environment.CurrentDirectory, "YOUR_DIRECTORY");
        string htmlPath = Path.Combine(baseDir, "example.html");
        string zipPath = Path.Combine(baseDir, "output.zip");

        // 2️⃣ Load the HTML document.
        HTMLDocument doc = new HTMLDocument(htmlPath);

        // 3️⃣ Configure save options with the custom handler.
        HTMLSaveOptions saveOptions = new HTMLSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save as a ZIP archive.
        doc.Save(zipPath, SaveFormat.Zip, saveOptions);

        Console.WriteLine($"HTML saved as ZIP at: {zipPath}");
    }
}
```

**Αναμενόμενη έξοδος**

```
HTML saved as ZIP at: C:\path\to\YOUR_DIRECTORY\output.zip
```

Εξαγάγετε το ZIP για να επαληθεύσετε τη δομή που περιγράφηκε παραπάνω.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε HTML ως ZIP** χρησιμοποιώντας το Aspose.HTML για .NET, αξιοποιώντας έναν **προσαρμοσμένο διαχειριστή πόρων** για να ελέγξετε πού θα γραφτεί κάθε στοιχείο. Αυτή η προσέγγιση σας δίνει πλήρη ευελιξία στην αποθήκευση πόρων, επιτρέπει επεξεργασία εντός μνήμης και ενσωματώνεται εύκολα σε ροές εργασίας στο cloud ή on‑premises.

Από εδώ μπορείτε:

* Να επεκτείνετε τον διαχειριστή ώστε να γράφει πόρους στο Azure Blob Storage (δευτερεύον κλειδί: custom resource handler).
* Να συνδυάσετε το ZIP με ψηφιακή υπογραφή για ασφαλή παράδοση εγγράφων.
* Να χρησιμοποιήσετε το `HTMLSaveOptions` για τη δημιουργία άλλων μορφών (π.χ., MHTML) ενώ συνεχίζετε να διαχειρίζεστε προγραμματιστικά τους πόρους.

Πειραματιστείτε με διαφορετικούς τύπους ροών, επίπεδα συμπίεσης και δομές φακέλων ώστε να ταιριάζουν στις απαιτήσεις του έργου σας. Καλός κώδικας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}