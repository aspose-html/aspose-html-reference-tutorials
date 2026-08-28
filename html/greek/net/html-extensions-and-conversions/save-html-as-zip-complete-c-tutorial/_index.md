---
category: general
date: 2025-12-30
description: Αποθηκεύστε το HTML ως ZIP γρήγορα χρησιμοποιώντας έναν προσαρμοσμένο
  διαχειριστή πόρων. Μάθετε πώς να μετατρέψετε μια ιστοσελίδα σε ZIP και να εξάγετε
  εικόνες και CSS σε λίγα βήματα.
draft: false
keywords:
- save html as zip
- custom resource handler
- convert webpage to zip
- extract images css
language: el
og_description: Αποθηκεύστε το HTML ως ZIP με έναν προσαρμοσμένο διαχειριστή πόρων.
  Ακολουθήστε αυτόν τον οδηγό για να μετατρέψετε τη σελίδα σε ZIP και να εξάγετε εικόνες
  και CSS χωρίς κόπο.
og_title: Αποθήκευση HTML ως ZIP – Πλήρες Μάθημα C#
tags:
- Aspose.HTML
- C#
- File Compression
title: Αποθήκευση HTML ως ZIP – Πλήρης Οδηγός C#
url: /el/net/html-extensions-and-conversions/save-html-as-zip-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση HTML ως ZIP – Πλήρη Εκμάθηση C#

Έχετε αναρωτηθεί ποτέ πώς να **αποθηκεύσετε HTML ως ZIP** χωρίς να χρησιμοποιήσετε εξωτερικά εργαλεία; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να αρχειοθετήσουν μια πλήρη ιστοσελίδα—συμπεριλαμβανομένων εικόνων, CSS και script—ώστε να την διανείμουν, να την αποθηκεύσουν ή να την αναλύσουν αργότερα. Τα καλά νέα; Με το Aspose.HTML μπορείτε να το κάνετε προγραμματιστικά, και το μυστικό κρύβεται σε έναν **προσαρμοσμένο διαχειριστή πόρων** που γράφει κάθε ληφθέν στοιχείο κατευθείαν σε μια καταχώρηση ZIP.

Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεστε: από τη ρύθμιση του έργου μέχρι τη δημιουργία του διαχειριστή, τη μετατροπή μιας ιστοσελίδας σε ZIP και, τέλος, την εξαγωγή εικόνων και CSS αν τα χρειαστείτε ξεχωριστά. Χωρίς εξωτερικά script, χωρίς χειροκίνητο copy‑paste—απλός κώδικας C# που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε έναν **προσαρμοσμένο διαχειριστή πόρων** που παρεμβάλλεται σε κάθε αίτημα πόρου.
- Τα ακριβή βήματα για **μετατροπή ιστοσελίδας σε ZIP** χρησιμοποιώντας τη μέθοδο `HTMLDocument.Save` του Aspose.HTML.
- Τρόπους **εξαγωγής εικόνων CSS** από το παραγόμενο αρχείο για περαιτέρω επεξεργασία.
- Συνηθισμένα προβλήματα (όπως διπλά ονόματα αρχείων) και συμβουλές για να διατηρείτε το ZIP σας οργανωμένο.

**Προαπαιτούμενα** – Θα πρέπει να έχετε:

- .NET 6+ (ή .NET Framework 4.7.2+) εγκατεστημένο.
- Μια πρόσφατη έκδοση του πακέτου NuGet Aspose.HTML for .NET.
- Βασική εξοικείωση με ροές C# και το namespace `System.IO.Compression`.

Έτοιμοι; Ας ξεκινήσουμε.

![Διάγραμμα που δείχνει τη ροή αποθήκευσης HTML ως ZIP, από URL σε αρχείο ZIP](save-html-as-zip-diagram.png "διαδικασία αποθήκευσης html ως zip")

## Αποθήκευση HTML ως ZIP – Επισκόπηση

Σε υψηλό επίπεδο η διαδικασία μοιάζει με αυτή:

1. **Αρχικοποίηση** ενός `FileStream` που δείχνει στο αρχείο εξόδου `.zip`.
2. **Δημιουργία** ενός `ZipResourceHandler` (ο προσαρμοσμένος μας διαχειριστής) και παροχή του ρεύματος.
3. **Φόρτωση** της στοχευμένης ιστοσελίδας με `HTMLDocument`.
4. **Αποθήκευση** του εγγράφου, αφήνοντας τον διαχειριστή να γράψει κάθε πόρο στο αρχείο.

Επειδή ο διαχειριστής επιστρέφει ένα ρεύμα εγγραφής για κάθε πόρο, το Aspose.HTML κάνει το βαρέως δουλειά—κατεβάζει εικόνες, CSS, JavaScript και τα ενσωματώνει ακριβώς εκεί που ανήκουν μέσα στο ZIP.

## Βήμα 1: Ρύθμιση του Έργου

Πρώτα, δημιουργήστε μια νέα εφαρμογή console (ή ενσωματώστε τον κώδικα σε υπάρχουσα υπηρεσία). Στη συνέχεια προσθέστε το πακέτο NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Βεβαιωθείτε ότι έχετε επίσης αναφορά στο `System.IO.Compression`—είναι μέρος της βασικής βιβλιοθήκης κλάσεων, οπότε δεν απαιτείται επιπλέον πακέτο.

## Βήμα 2: Δημιουργία Προσαρμοσμένου Διαχειριστή Πόρων

Ο **προσαρμοσμένος διαχειριστής πόρων** είναι η καρδιά της λύσης. Λαμβάνει ένα αντικείμενο `ResourceInfo` για κάθε ζητούμενο στοιχείο και επιστρέφει ένα `Stream` όπου το Aspose.HTML θα γράψει τα δεδομένα. Θα αντιστοιχίσουμε τη διαδρομή URL σε όνομα καταχώρησης ZIP, διατηρώντας την αρχική δομή φακέλων.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;
using System.IO.Compression;

/// <summary>
/// Writes every fetched resource directly into a ZIP entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    /// <summary>
    /// Opens a ZIP archive in "Create" mode. The archive stays open
    /// until the handler is disposed.
    /// </summary>
    /// <param name="zipStream">The underlying stream for the ZIP file.</param>
    public ZipResourceHandler(Stream zipStream)
    {
        // leaveOpen:true lets us close the handler without closing the file stream.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    /// <summary>
    /// Called for each resource (image, CSS, script, etc.).
    /// </summary>
    /// <param name="resourceInfo">Info about the requested resource.</param>
    /// <returns>A writable stream that points to a new ZIP entry.</returns>
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Trim leading '/' to avoid creating an empty top‑level folder.
        var entryName = resourceInfo.Url.PathAndQuery.TrimStart('/');
        // Ensure a valid entry name; duplicate names are overwritten.
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        // Return the stream that Aspose.HTML will write into.
        return entry.Open();
    }

    protected override void Dispose(bool disposing)
    {
        if (disposing)
        {
            _zipArchive?.Dispose();
        }
        base.Dispose(disposing);
    }
}
```

**Γιατί είναι σημαντικό:** Επιστρέφοντας ένα νέο ρεύμα `ZipArchiveEntry` για κάθε πόρο, αποφεύγουμε προσωρινά αρχεία και κρατάμε τη χρήση μνήμης χαμηλή. Ο διαχειριστής μας δίνει επίσης πλήρη έλεγχο πάνω στην ονομασία—χρήσιμο όταν αργότερα θέλετε να **εξάγετε εικόνες CSS** από το αρχείο.

## Βήμα 3: Προετοιμασία Ρεύματος Εξόδου ZIP

Τώρα ανοίγουμε ένα `FileStream` που δείχνει στο τελικό αρχείο ZIP. Το ρεύμα αυτό περνάει στον διαχειριστή που μόλις δημιουργήσαμε.

```csharp
// Adjust the path to wherever you want the ZIP to land.
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Using statement ensures the stream is closed even if an exception occurs.
using var zipFileStream = new FileStream(zipPath, FileMode.Create, FileAccess.Write);
```

> **Συμβουλή:** Αν χρειάζεστε το ZIP ως απόκριση HTTP, αντικαταστήστε το `FileStream` με ένα `MemoryStream` και γράψτε το byte array στο σώμα της απόκρισης.

## Βήμα 4: Φόρτωση και Μετατροπή της Ιστοσελίδας

Με τον διαχειριστή έτοιμο, μπορούμε να φορτώσουμε οποιοδήποτε δημόσιο URL. Το Aspose.HTML λύνει αυτόματα τις σχετικές συνδέσεις, κατεβάζει τα στοιχεία και καλεί τον διαχειριστή μας για καθένα.

```csharp
// Step 4: Instantiate the handler with the ZIP stream.
var zipHandler = new ZipResourceHandler(zipFileStream);

// Step 5: Load the target HTML page.
var url = "https://example.com"; // Change to the page you want to archive.
var htmlDoc = new HTMLDocument(url);

// Step 6: Save the document – the handler writes everything into the ZIP.
htmlDoc.Save(zipHandler, new SaveOptions(SaveFormat.Html));

// Dispose the handler to flush the ZIP archive.
zipHandler.Dispose();

Console.WriteLine($"✅ Webpage saved as ZIP at: {zipPath}");
```

**Τι συμβαίνει στο παρασκήνιο;**  
- Το `HTMLDocument` αναλύει το HTML, εντοπίζει ετικέτες `<img>`, `<link rel="stylesheet">` και `<script>`.  
- Για κάθε πόρο, καλεί το `ZipResourceHandler.HandleResource`.  
- Ο διαχειριστής δημιουργεί μια αντίστοιχη καταχώρηση (`images/logo.png`, `css/site.css`, κλπ.) και μεταφέρει τα ληφθέντα bytes κατευθείαν στο αρχείο ZIP.

## Βήμα 5: Επαλήθευση Περιεχομένων ZIP

Ανοίξτε το παραγόμενο `output.zip` με οποιονδήποτε διαχειριστή αρχείων. Θα πρέπει να δείτε μια ιεραρχία φακέλων που αντικατοπτρίζει την αρχική ιστοσελίδα:

```
/index.html
/images/logo.png
/css/site.css
/js/app.js
...
```

Αν χρειάζεστε να **εξάγετε εικόνες CSS** για περαιτέρω ανάλυση, μπορείτε απλώς να απαριθμήσετε τις καταχωρήσεις:

```csharp
using (var zip = ZipFile.OpenRead(zipPath))
{
    foreach (var entry in zip.Entries)
    {
        if (entry.FullName.EndsWith(".png") || entry.FullName.EndsWith(".jpg"))
        {
            Console.WriteLine($"Image: {entry.FullName}");
        }
        else if (entry.FullName.EndsWith(".css"))
        {
            Console.WriteLine($"CSS: {entry.FullName}");
        }
    }
}
```

Αυτό το απόσπασμα κώδικα εκτυπώνει κάθε εικόνα και αρχείο CSS που αποθήκευσε ο διαχειριστής—χρήσιμο για αυτοματοποιημένες γραμμές εργασίας που χρειάζονται έλεγχο CSS ή δημιουργία μικρογραφιών.

## Συνηθισμένα Προβλήματα και Συμβουλές

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Διπλά ονόματα αρχείων (π.χ. δύο `logo.png` σε διαφορετικούς φακέλους) | Η `CreateEntry` αντικαθιστά την προηγούμενη καταχώρηση με το ίδιο όνομα. | Διατηρήστε το πλήρες σχετικό μονοπάτι (`resourceInfo.Url.PathAndQuery`) όπως κάνουμε, ή προσθέστε ένα μοναδικό GUID. |
| Μεγάλες ιστοσελίδες προκαλούν υψηλή χρήση μνήμης | Το Aspose.HTML μπορεί να κάνει buffer πόρων πριν τη ροή. | Χρησιμοποιήστε `CompressionLevel.Optimal` και απελευθερώστε άμεσα τον διαχειριστή. |
| Λείπουν πόροι λόγω αυθεντικοποίησης | Η βιβλιοθήκη δεν μπορεί να κατεβάσει στοιχεία πίσω από login. | Παρέχετε προσαρμοσμένο `HttpClient` με διαπιστευτήρια μέσω των υπερφορτώσεων του κατασκευαστή `HTMLDocument`. |
| Το αρχείο ZIP παραμένει κλειδωμένο μετά την εκτέλεση | Δεν κλήθηκε το `zipHandler.Dispose()`. | Τυλίξτε τον διαχειριστή σε `using` block ή καλέστε `Dispose` χειροκίνητα όπως φαίνεται. |

## Συμπέρασμα

Τώρα έχετε μια πλήρως λειτουργική μέθοδο για **αποθήκευση HTML ως ZIP** χρησιμοποιώντας έναν **προσαρμοσμένο διαχειριστή πόρων**. Η προσέγγιση σας επιτρέπει να **μετατρέψετε ιστοσελίδα σε ZIP** σε μία μόνο διαδρομή, ενώ αυτόματα **εξάγετε εικόνες CSS** για οποιαδήποτε επόμενη εργασία. Είτε δημιουργείτε μια υπηρεσία αρχειοθέτησης web, ένα εργαλείο backup στατικών site, είτε απλώς χρειάζεστε έναν εύκολο τρόπο να συσκευάσετε μια σελίδα για offline προβολή, αυτό το μοτίβο κλιμακώνεται άψογα και παραμένει εντός του οικοσυστήματος .NET.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε το `FileStream` με `MemoryStream` για να επιστρέψετε το ZIP απευθείας από ένα endpoint API ASP.NET Core. Ή πειραματιστείτε με επεξεργασία των εξαγόμενων CSS—ίσως τρέξτε έναν minifier πριν αποθηκεύσετε το αρχείο. Οι δυνατότητες είναι πρακτικά απεριόριστες, και η βασική ιδέα παραμένει η ίδια: αφήστε το Aspose.HTML να κάνει το κατέβασμα, και ο διαχειριστής σας να γράφει.

Αν αντιμετωπίσετε προβλήματα, ελέγξτε την έξοδο της κονσόλας για προειδοποιήσεις και θυμηθείτε τις παραπάνω συμβουλές. Καλή αρχειοθέτηση! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}