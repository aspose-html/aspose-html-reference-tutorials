---
category: general
date: 2025-12-29
description: Πώς να συμπιέσετε HTML σε C# γρήγορα χρησιμοποιώντας το Aspose.HTML –
  αποθηκεύστε το HTML σε zip με έναν προσαρμοσμένο ZipResourceHandler. Μάθετε βήμα‑βήμα.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: el
og_description: Πώς να συμπιέσετε HTML σε C# γρήγορα χρησιμοποιώντας το Aspose.HTML.
  Ακολουθήστε αυτόν τον οδηγό για να αποθηκεύσετε HTML σε zip και να δημιουργήσετε
  ένα αρχείο zip με προσαρμοσμένη διαχείριση πόρων.
og_title: Πώς να συμπιέσετε HTML σε Zip με C# – Αποθήκευση HTML σε Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Πώς να συμπιέσετε HTML σε Zip με C# – Αποθήκευση HTML σε Zip
url: /el/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Συμπιέσετε HTML σε Zip με C# – Αποθήκευση HTML σε Zip

Η συμπίεση HTML σε Zip με C# είναι μια συχνή ανάγκη όταν θέλετε να συσκευάσετε ιστοσελίδες για χρήση εκτός σύνδεσης. Είτε δημιουργείτε ένα μόνο αρχείο με τις εικόνες του είτε εξάγετε ολόκληρο τον ιστότοπο, η **αποθήκευση HTML σε zip** κρατά όλα οργανωμένα και φορητά. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που όχι μόνο συμπιέζει το HTML markup αλλά και ρέει κάθε αναφερόμενο πόρο κατευθείαν στο αρχείο.

Θα μάθετε πώς να:

* Δημιουργείτε ένα zip αρχείο προγραμματιστικά με το .NET `System.IO.Compression`.
* Ενσωματώνετε έναν προσαρμοσμένο `ResourceHandler` στο Aspose.HTML ώστε οι πόροι να ρέουν απευθείας στο zip.
* Διαχειρίζεστε ειδικές περιπτώσεις όπως υπάρχοντα zip αρχεία και μεγάλα δυαδικά στοιχεία.

Δεν απαιτούνται εξωτερικά εργαλεία—μόνο C#, Aspose.HTML και λίγες γραμμές κώδικα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* **.NET 6+** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6.2 και νεότερες εκδόσεις).
* **Aspose.HTML for .NET** – μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την ιστοσελίδα της Aspose ή να χρησιμοποιήσετε μια αδειοδοτημένη έκδοση.
* Ένα περιβάλλον ανάπτυξης (Visual Studio, VS Code, Rider—ό,τι προτιμάτε).

Αυτό είναι όλο. Δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από το `System.IO.Compression` (συμπεριλαμβάνεται στο .NET) και το `Aspose.HTML`.

## Βήμα 1: Ρύθμιση του Project και των Imports

Δημιουργήστε ένα νέο console project (ή ενσωματώστε τον κώδικα σε ένα υπάρχον). Προσθέστε τις απαιτούμενες οδηγίες `using` στην αρχή του αρχείου σας:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Συμβουλή:** Αν χρησιμοποιείτε Visual Studio, το IDE θα προτείνει την προσθήκη του απαραίτητου πακέτου NuGet για το `Aspose.Html`. Αποδεχτείτε το και είστε έτοιμοι να ξεκινήσετε.

## Βήμα 2: Υλοποίηση ενός Προσαρμοσμένου ZipResourceHandler

Το Aspose.HTML καλεί έναν `ResourceHandler` όποτε χρειάζεται να γράψει έναν πόρο (όπως εικόνα, αρχείο CSS ή script). Υπερφορτώνοντας τη μέθοδο `HandleResource`, μπορούμε να αποφασίσουμε ακριβώς πού θα καταλήξει κάθε πόρος. Ο παρακάτω handler δημιουργεί μια καταχώρηση zip που αντικατοπτρίζει τη λογική διαδρομή του πόρου και επιστρέφει ένα ρεύμα εγγραφής που δείχνει κατευθείαν σε αυτήν την καταχώρηση.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Γιατί είναι σημαντικό:**  
Αντί να γράφουμε τους πόρους σε έναν προσωρινό φάκελο και μετά να συμπιέζουμε το φάκελο, αυτός ο handler ρέει τα δεδομένα άμεσα, μειώνοντας τις ενέργειες I/O στο δίσκο και τη χρήση μνήμης. Επίσης, εγγυάται ότι η εσωτερική ιεραρχία φακέλων του zip ταιριάζει με τις σχετικές διαδρομές του HTML, κάτι που απαιτούν οι browsers όταν αποσυμπιέζετε και ανοίγετε τη σελίδα.

## Βήμα 3: Προετοιμασία του Zip Αρχείου

Τώρα θα ανοίξουμε (ή θα δημιουργήσουμε) το αρχείο zip προορισμού. Η σημαία `FileMode.Create` αντικαθιστά τυχόν υπάρχον αρχείο—ιδανική για επαναλαμβανόμενες κατασκευές. Αν προτιμάτε να διατηρήσετε ένα υπάρχον αρχείο, αλλάξτε σε `FileMode.OpenOrCreate` και διαχειριστείτε τις διπλές καταχωρήσεις ανάλογα.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Περίπτωση:** Αν η διαδικασία τερματιστεί πριν το μπλοκ `using` απελευθερώσει το αρχείο, μπορεί να μείνει ένα κατεστραμμένο zip. Η εκτέλεση του κώδικα μέσα σε `try/catch` και η διαγραφή του μερικώς δημιουργημένου αρχείου σε περίπτωση αποτυχίας αποτελεί απλό μέτρο ασφαλείας.

## Βήμα 4: Δημιουργία του HTML Εγγράφου με Ενσωματωμένο Πόρο

Για επίδειξη, θα δημιουργήσουμε μια μικρή σελίδα HTML που αναφέρεται σε μια εικόνα με όνομα `image.png`. Σε πραγματικό σενάριο θα φορτώνετε το HTML από αρχείο ή από μια συμβολοσειρά που προέρχεται από βάση δεδομένων.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Αν έχετε πραγματικά αρχεία εικόνας στο δίσκο, μπορείτε να τα προσθέσετε στο zip χειροκίνητα πριν αποθηκεύσετε το HTML, ή να αφήσετε το Aspose.HTML να τα ανακτήσει μέσω του handler (π.χ., από URL). Ο handler που γράψαμε λειτουργεί τόσο για τοπικές διαδρομές όσο και για απομακρυσμένα URLs.

## Βήμα 5: Ρύθμιση των Επιλογών Αποθήκευσης για Χρήση του ZipResourceHandler

Τώρα λέμε στο Aspose.HTML να χρησιμοποιήσει τον προσαρμοσμένο μας handler όταν γράφει πόρους. Η κλάση `HTMLSaveOptions` επιτρέπει επίσης να ορίσετε το όνομα του αρχείου εξόδου μέσα στο zip (προεπιλογή είναι `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Βήμα 6: Αποθήκευση του Εγγράφου – Όλα Ρέουν στο Zip

Τέλος, καλέστε τη μέθοδο `Save`. Το Aspose.HTML αναλύει το markup, εντοπίζει το `<img>` tag, καλεί το `HandleResource` για το `image.png`, και γράφει τόσο το HTML αρχείο όσο και την εικόνα στο ίδιο αρχείο zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Όταν τα μπλοκ `using` ολοκληρωθούν, το `ZipArchive` τελειοποιεί το αρχείο, καθιστώντας το έτοιμο για διανομή.

### Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα ενωμένο. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs` και τρέξτε—δεν χρειάζονται περαιτέρω τροποποιήσεις.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση, το `output.zip` περιέχει δύο καταχωρήσεις:

```
index.html
image.png
```

Αν αποσυμπιέσετε το αρχείο και ανοίξετε το `index.html` σε έναν browser, η εικόνα θα εμφανιστεί σωστά επειδή η σχετική διαδρομή διατηρείται.

## Συχνές Ερωτήσεις

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}