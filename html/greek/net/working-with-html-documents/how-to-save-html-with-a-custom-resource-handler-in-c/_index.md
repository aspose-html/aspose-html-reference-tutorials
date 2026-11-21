---
category: general
date: 2026-11-20
description: Μάθετε πώς να αποθηκεύετε HTML χρησιμοποιώντας έναν προσαρμοσμένο ResourceHandler
  σε C# και επίσης να αποθηκεύετε HTML σε αρχεία zip με σύντομο, έτοιμο για παραγωγή
  κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: el
lastmod: 2026-11-20
og_description: Πώς να αποθηκεύσετε HTML χρησιμοποιώντας έναν προσαρμοσμένο ResourceHandler
  σε C# και προαιρετικά να αποθηκεύσετε HTML σε αρχεία zip — πλήρης, εκτελέσιμη οδηγία
  για προγραμματιστές .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Πώς να αποθηκεύσετε HTML με έναν προσαρμοσμένο διαχειριστή πόρων σε C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Πώς να αποθηκεύσετε HTML με έναν προσαρμοσμένο διαχειριστή πόρων σε C#
url: /el/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε HTML με έναν προσαρμοσμένο διαχειριστή πόρων σε C#

Αν χρειάζεστε να γνωρίζετε **πώς να αποθηκεύσετε HTML** από μια συμβολοσειρά στη μνήμη ή ένα αναλυμένο έγγραφο, αυτός ο οδηγός παρουσιάζει μια πλήρη λύση. Η χρήση ενός προσαρμοσμένου `ResourceHandler` σας επιτρέπει να ελέγχετε τη ροή προορισμού, πράγμα που σημαίνει ότι μπορείτε να **αποθηκεύσετε HTML σε zip** αρχεία χωρίς να γράψετε προσωρινά αρχεία.

Θα δείτε γιατί ένα `ResourceHandler` προτιμάται έναντι της παλαιότερης προσέγγισης `IOutputStorage`, πώς να το ρυθμίσετε και πώς να το επεκτείνετε για συμπίεση zip. Στο τέλος αυτού του σεμιναρίου μπορείτε να ενσωματώσετε τον κώδικα σε οποιοδήποτε έργο .NET 6+ και να το προσαρμόσετε στις δικές σας απαιτήσεις αποθήκευσης.

## Τι θα δημιουργήσετε

* Ένας ελάχιστος `ResourceHandler` που επιστρέφει ένα `MemoryStream`.
* Ένα `HtmlDocument` που δημιουργείται με **HtmlAgilityPack**.
* Μία κλήση στο `doc.Save` που γράφει το HTML στη ροή που παρέχεται από το διαχειριστή.
* Ένα προαιρετικό wrapper που συμπιέζει το παραγόμενο HTML σε αρχείο zip.

Προαπαιτούμενα:

* .NET 6 SDK ή νεότερο.
* Πακέτο NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Βασική εξοικείωση με ροές C#.

## Βήμα 1: Δημιουργήστε έναν προσαρμοσμένο διαχειριστή πόρων (πρωτεύων τρόπος για **πώς να αποθηκεύσετε html**)

Η βασική κλάση `ResourceHandler` (διαθέσιμη από την έκδοση 24.2 του viewer SDK) ορίζει μία μοναδική αφηρημένη μέθοδο, `HandleResource`. Η υλοποίηση αυτής της μεθόδου σας δίνει πλήρη έλεγχο στο πού γράφεται το HTML.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Γιατί είναι σημαντικό:** Επιστρέφοντας ένα `MemoryStream`, αποφεύγετε την I/O του δίσκου, μειώνετε την καθυστέρηση και διατηρείτε τον κώδικα ντετερμινιστικό για μονάδες δοκιμών. Ο διαχειριστής καλείται αυτόματα από τη μέθοδο `Save`, οπότε δεν χρειάζεται ποτέ να περάσετε ρητά μια ροή.

## Βήμα 2: Φορτώστε ή δημιουργήστε το έγγραφο HTML

`HtmlAgilityPack` παρέχει μια βολική κλάση `HtmlDocument` που μπορεί να αναλύσει μια συμβολοσειρά, ένα αρχείο ή μια ροή. Για αυτό το παράδειγμα φορτώνουμε ένα απλό κυριολεκτικό, αλλά ο ίδιος κώδικας λειτουργεί με οποιαδήποτε πηγή HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Γιατί είναι σημαντικό:** Η διατήρηση του εγγράφου στη μνήμη ευθυγραμμίζεται με την προσέγγιση βασισμένη σε ροές του προσαρμοσμένου διαχειριστή. Επίσης σας επιτρέπει να χειριστείτε το DOM πριν από την αποθήκευση, όπως η εισαγωγή σεναρίων ή η διόρθωση κακοσχηματισμένων ετικετών.

## Βήμα 3: Αποθηκεύστε το έγγραφο χρησιμοποιώντας τον προσαρμοσμένο διαχειριστή

Καλώντας το `doc.Save` με μια παρουσία του `MyHandler` ενεργοποιείται η μέθοδος `HandleResource`. Το HTML γράφεται απευθείας στη ροή που επιστρέψατε.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Μετά την ολοκλήρωση του `Save`, το `MemoryStream` μέσα στο `MyHandler` περιέχει το σειριοποιημένο HTML. Μπορείτε να το ανακτήσετε ως εξής:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Αποτέλεσμα:** Η κονσόλα εκτυπώνει το ακριβές HTML που περάσατε στο `LoadHtml`. Αυτό αποδεικνύει ότι τώρα καταλαβαίνετε **πώς να αποθηκεύσετε HTML** με έναν προσαρμοσμένο διαχειριστή.

## Βήμα 4: Επεκτείνοντας τον διαχειριστή για **αποθήκευση HTML σε zip**

Αν θέλετε να αρχειοθετήσετε το HTML, τροποποιήστε το `MyHandler` ώστε να γράφει σε ένα `ZipArchiveEntry`. Ο χώρος ονομάτων .NET `System.IO.Compression` το καθιστά απλό.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Τώρα χρησιμοποιήστε το νέο διαχειριστή:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Γιατί λειτουργεί:** Η μέθοδος `HandleResource` δημιουργεί μια καταχώρηση zip με όνομα `document.html`. Όταν το `doc.Save` γράφει στη ροή που επιστράφηκε, τα δεδομένα συμπιέζονται αυτόματα. Επειδή το zip δημιουργείται στη μνήμη, μπορείτε να το επιστρέψετε από ένα web API, να το επισυνάψετε σε email ή να το αποθηκεύσετε σε βάση δεδομένων χωρίς να αγγίξετε το σύστημα αρχείων.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

### Τι γίνεται αν χρειάζομαι πολλά αρχεία HTML στο ίδιο zip;

Δημιουργήστε μια νέα καταχώρηση για κάθε κλήση στο `HandleResource`. Το όρισμα `resourceName` συνήθως περιέχει το όνομα αρχείου, οπότε μπορείτε να το χρησιμοποιήσετε απευθείας:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Πώς να διαχειριστείτε μεγάλα έγγραφα χωρίς να εξαντλήσετε τη μνήμη;

Αντικαταστήστε το `MemoryStream` με ένα `FileStream` που δείχνει σε ένα προσωρινό αρχείο. Ο διαχειριστής τότε επιστρέφει τη ροή αρχείου, και μπορείτε αργότερα να διαγράψετε το αρχείο μετά τη δημιουργία του zip.

### Λειτουργεί αυτή η προσέγγιση με .NET Core σε Linux;

Ναι. Όλα τα API που χρησιμοποιούνται (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) είναι διασταυρούμενα. Βεβαιωθείτε ότι το πλαίσιο-στόχος είναι τουλάχιστον .NET 6 για τη βέλτιστη συμβατότητα.

### Μπορώ να κρυπτογραφήσω το αρχείο zip;

`ZipArchive` υποστηρίζει κρυπτογράφηση με κωδικό πρόσβασης μόνο μέσω βιβλιοθηκών τρίτων (π.χ., `SharpZipLib`). Αν απαιτείται κρυπτογράφηση, τυλίξτε τα bytes εξόδου με μια βιβλιοθήκη που παρέχει κρυπτογράφηση AES πριν τα στείλετε στον πελάτη.

## Συμβουλές επαγγελματιών

* **Επαναχρησιμοποίηση του διαχειριστή** όταν επεξεργάζεστε πολλά έγγραφα σε παρτίδα· η δημιουργία νέου `ZipArchive` για κάθε αρχείο προσθέτει περιττό κόστος.
* **Ορίστε `LeaveOpen: true`** στον κατασκευαστή του `ZipArchive` αν χρειάζεται να διαβάσετε τα bytes του zip ενώ το αρχείο είναι ακόμα ανοιχτό.
* **Επικυρώστε το HTML** πριν την αποθήκευση καλώντας `doc.OptionCheckSyntax = true;` – αυτό εντοπίζει κακοσχηματισμένες ετικέτες νωρίς.
* **Καταγράψτε το μέγεθος** του παραγόμενου zip· ένα ασυνήθιστα μεγάλο αποτέλεσμα συχνά υποδεικνύει διπλότυπους πόρους ή έλλειψη συμπίεσης.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει ένα μοναδικό αρχείο που μπορείτε να επικολλήσετε σε ένα κονσόλα έργο (`dotnet new console`) και να εκτελέσετε. Δείχνει τόσο την αποθήκευση απλού HTML όσο και τη συμπίεση zip.



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε HTML σε C# με προσαρμοσμένο διαχειριστή πόρων](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Πώς να χρησιμοποιήσετε το ZipArchive – Αποθήκευση HTML και πόρων σε αρχείο ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [αποθήκευση html ως zip με προσαρμοσμένο διαχειριστή πόρων – οδηγός βήμα‑βήμα](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}