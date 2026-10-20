---
category: general
date: 2026-03-29
description: Μάθετε πώς να χρησιμοποιείτε το ZipArchive σε C# για να μετατρέψετε HTML
  σε ZIP, να αποθηκεύσετε HTML σε ZIP και να συμπιέσετε εικόνες HTML — όλα σε ένα
  σαφές σεμινάριο.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: el
og_description: Ανακαλύψτε πώς να χρησιμοποιήσετε το ZipArchive σε C# για να μετατρέψετε
  HTML σε ZIP, να αποθηκεύσετε HTML σε ZIP και να συμπιέσετε εικόνες HTML με ένα πλήρες,
  εκτελέσιμο παράδειγμα.
og_title: Πώς να χρησιμοποιήσετε το ZipArchive – Αποθήκευση HTML και πόρων σε αρχείο
  ZIP
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Πώς να χρησιμοποιήσετε το ZipArchive – Αποθήκευση HTML και πόρων σε αρχείο
  ZIP
url: /el/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το ZipArchive – Αποθήκευση HTML και Πόρων σε Αρχείο ZIP

Έχετε αναρωτηθεί **πώς να χρησιμοποιήσετε το ZipArchive** για να συσκευάσετε μια σελίδα HTML μαζί με τις εικόνες, το CSS και άλλα περιουσιακά στοιχεία της; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να παραδώσουν ένα αυτόνομο πακέτο HTML, ειδικά όταν η σελίδα αναφέρεται σε εξωτερικούς πόρους. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.HTML μπορείτε **να μετατρέψετε HTML σε ZIP**, **να αποθηκεύσετε HTML σε ZIP**, και ακόμη **να συμπιέσετε εικόνες HTML** χωρίς να φύγετε από το IDE σας.

Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός απλού `HTMLDocument` μέχρι τη διαχείριση κάθε συνδεδεμένου πόρου μέσω ενός προσαρμοσμένου `ResourceHandler`. Στο τέλος θα έχετε ένα έτοιμο αρχείο ZIP που μπορείτε να τοποθετήσετε σε οποιονδήποτε web server ή ως συνημμένο email. Χωρίς εξωτερικά scripts, χωρίς χειροκίνητη αντιγραφή—απλώς .NET.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6+** (ή .NET Framework 4.6+). Τα API που χρησιμοποιούνται είναι μέρος του `System.IO.Compression`.
- **Aspose.HTML for .NET** εγκατεστημένο (πακέτο NuGet `Aspose.Html`).
- Βασική κατανόηση της σύνταξης C#.
- Ένα IDE όπως το Visual Studio ή το VS Code.

Αυτό είναι όλο. Χωρίς επιπλέον εργαλεία, χωρίς τρίτες εφαρμογές zip. Έτοιμοι; Ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Project και Προσθήκη Εξαρτήσεων

Δημιουργήστε ένα νέο console project:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Το πακέτο `Aspose.Html` μας παρέχει την κλάση `HTMLDocument` και τη βασική κλάση `ResourceHandler` που θα επεκτείνουμε αργότερα. Ο ενσωματωμένος χώρος ονομάτων `System.IO.Compression` παρέχει τις κλάσεις `ZipArchive` και `ZipArchiveEntry`.

> **Pro tip:** Αν στοχεύετε σε .NET 6, μπορείτε να χρησιμοποιήσετε top‑level statements για να κρατήσετε τη μέθοδο `Main` πιο καθαρή. Ο κώδικας παρακάτω χρησιμοποιεί κλασική κλάση `Program` για σαφήνεια.

## Βήμα 2: Δημιουργία Προσαρμοσμένου Resource Handler

Όταν το Aspose.HTML αποθηκεύει ένα έγγραφο, ζητά από ένα `ResourceHandler` ένα `Stream` για κάθε εξωτερικό αρχείο (εικόνες, CSS, γραμματοσειρές κ.λπ.). Με την υπερισχύση του `HandleResource` μπορούμε να διοχετεύσουμε κάθε πόρο κατευθείαν σε μια καταχώρηση zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Γιατί είναι σημαντικό:** Αντί να γράφουμε πρώτα τους πόρους στο δίσκο και μετά να τους συμπιέζουμε, ο handler τα ρέει απευθείας, μειώνοντας το I/O και εξασφαλίζοντας ότι το zip παραμένει συγχρονισμένο με το περιεχόμενο του HTML.

## Βήμα 3: Δημιουργία του HTML Εγγράφου

Για επίδειξη, θα ενσωματώσουμε ένα μικρό απόσπασμα HTML που αναφέρει μια εξωτερική εικόνα με όνομα `logo.png`. Σε πραγματικό project μπορεί να φορτώνετε HTML από αρχείο ή βάση δεδομένων.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Αν χρειάζεστε **συμπίεση εικόνων HTML**, απλώς βεβαιωθείτε ότι το αρχείο εικόνας βρίσκεται δίπλα στο εκτελέσιμο (ή ενσωματωμένο ως πόρος). Ο `ZipResourceHandler` θα προσθέσει αυτόματα την εικόνα στο αρχείο.

## Βήμα 4: Άνοιγμα (ή Δημιουργία) του Αρχείου ZIP και Αποθήκευση

Τώρα ενώνουμε όλα. Ανοίγουμε ένα `FileStream` για το αρχείο εξόδου, δημιουργούμε ένα `ZipArchive` σε λειτουργία *Update*, και περνάμε τον προσαρμοσμένο handler στη μέθοδο `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Όταν τα μπλοκ `using` ολοκληρωθούν, το zip κλείνει αυτόματα. Το παραγόμενο `output.zip` περιέχει:

- `index.html` (το σειριοποιημένο HTML έγγραφο)
- `logo.png` (η εικόνα που αναφέρεται στο HTML)

Μπορείτε να ελέγξετε τα περιεχόμενα ανοίγοντας το zip σε οποιονδήποτε εξερευνητή αρχείων.

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Προαιρετικό)

Πάντα είναι καλή ιδέα να ελέγξετε ότι το zip λειτουργεί σωστά. Εδώ είναι ένα σύντομο απόσπασμα που μπορείτε να τρέξετε μετά τον προηγούμενο κώδικα για να απαριθμήσετε τις καταχωρήσεις:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Θα πρέπει να δείτε κάτι σαν:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Ανοίξτε το `index.html` από το φάκελο εξαγωγής και θα δείτε την εικόνα να εμφανίζεται σωστά—απόδειξη ότι η **αποθήκευση HTML σε ZIP** λειτούργησε όπως αναμενόταν.

## Συνηθισμένες Παραλλαγές & Edge Cases

### 1. Χρήση Διαφορετικού Ονόματος Καταχώρησης για το Αρχείο HTML

Από προεπιλογή το Aspose γράφει το HTML στο `index.html`. Αν χρειάζεστε προσαρμοσμένο όνομα, μπορείτε να ορίσετε `htmlDocument.FileName` πριν την αποθήκευση:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Προσθήκη Επιπλέον Αρχείων Χειροκίνητα

Μερικές φορές θέλετε να συμπεριλάβετε επιπλέον αρχεία (π.χ. README). Μπορείτε να τα προσθέσετε απευθείας στο `ZipArchive` πριν καλέσετε `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Αποτελεσματική Διαχείριση Μεγάλων Εικόνων

Αν το HTML σας αναφέρει πολύ μεγάλες εικόνες, σκεφτείτε να τις μειώσετε σε μέγεθος εκ των προτέρων για να κρατήσετε το μέγεθος του zip λογικό. Το πακέτο `System.Drawing.Common` μπορεί να βοηθήσει:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Στη συνέχεια, δείξτε στο `<img src='logo_resized.png'>` του HTML.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Συγκεντώνεται και εκτελείται αμέσως, εφόσον έχετε εγκαταστήσει το πακέτο NuGet Aspose.HTML.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει μήνυμα επιτυχίας, και το `output.zip` εμφανίζεται στον φάκελο του project περιέχοντας `index.html` και `logo.png`.

## Συχνές Ερωτήσεις

- **Λειτουργεί αυτό σε .NET Core;**  
  Ναι. Το `System.IO.Compression.ZipArchive` είναι μέρος του .NET Standard, οπότε ο ίδιος κώδικας τρέχει σε .NET 5, .NET 6 και .NET 7.

- **Τι γίνεται αν χρειαστώ **συμπίεση εικόνων HTML** πιο εντατικά;**  
  Μπορείτε να προεπεξεργαστείτε τις εικόνες (αλλαγή μεγέθους, μετατροπή σε WebP κ.λπ.) πριν τις προσθέσετε στο zip. Ο handler απλώς ρέει τα δεδομένα που λαμβάνει.

- **Μπορώ να κρυπτογραφήσω το zip;**  
  Το `ZipArchive` υποστηρίζει κρυπτογράφηση AES μόνο μέσω τρίτων βιβλιοθηκών (π.χ. `SharpZipLib`). Αν χρειάζεστε κρυπτογράφηση, δημιουργήστε το zip με αυτή τη βιβλιοθήκη και μετά δώστε το stream στο Aspose ως προσαρμοσμένο `ResourceHandler`.

- **Υπάρχει τρόπος να ορίσω τον ριζικό φάκελο μέσα στο zip;**  
  Ναι—προσθέστε ένα όνομα φακέλου στο `resourceName` μέσα στο `HandleResource`, π.χ. `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Συμπέρασμα

Τώρα ξέρετε **πώς να χρησιμοποιήσετε το ZipArchive** σε C# για **να μετατρέψετε HTML σε ZIP**, **να αποθηκεύσετε HTML σε ZIP**, και **να συμπιέσετε εικόνες HTML** σε μια ενιαία, καθαρή ροή εργασίας. Επεκτείνοντας το `ResourceHandler` αποφύγαμε τα προσωρινά αρχεία και διατηρήσαμε τη διαδικασία αποδοτική στη μνήμη. Το μοτίβο κλιμακώνεται εύκολα: απλώς τοποθετήστε το παραγόμενο zip σε web server, στείλτε το με email ή αποθηκεύστε το σε cloud storage.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- **Δημιουργία αρχείων ZIP προγραμματιστικά** για ολόκληρους φακέλους ιστοτόπων (`create zip archive c#`).
- **Προσθήκη μετατροπών PDF ή DOCX** πριν το zip για πιο πλούσια πακέτα τεκμηρίωσης.
- **Ενσωμάτωση με ASP.NET Core** για άμεση ροή του zip στον πελάτη μέσω `FileStreamResult`.

Έχετε περισσότερες ερωτήσεις για το zip HTML, τη διαχείριση γραμματοσειρών ή τη βελτιστοποίηση μεγέθους εικόνας; Αφήστε σχόλιο ή στείλτε μου μήνυμα στο Stack Overflow. Καλό coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}