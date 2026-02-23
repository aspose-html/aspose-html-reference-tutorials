---
category: general
date: 2026-02-22
description: Ο προσαρμοσμένος διαχειριστής πόρων σάς επιτρέπει να καταγράψετε την
  έξοδο HTML. Μάθετε πώς να φορτώσετε ένα έγγραφο HTML, να χρησιμοποιήσετε τη λειτουργία
  αποθήκευσης του Aspose HTML και να αποθηκεύσετε το HTML σε ροή με ένα απλό παράδειγμα
  C#.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: el
og_description: Μάθετε πώς ένας προσαρμοσμένος διαχειριστής πόρων καταγράφει την έξοδο
  HTML, φορτώνει το έγγραφο HTML και αποθηκεύει το HTML σε ροή χρησιμοποιώντας το
  Aspose HTML σε C#.
og_title: Προσαρμοσμένος Διαχειριστής Πόρων στο Aspose HTML – Οδηγός αποθήκευσης σε
  ροή
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Προσαρμοσμένος Διαχειριστής Πόρων στο Aspose HTML – Οδηγός Αποθήκευσης σε Ροή
url: /el/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

under "What You’ll Need" etc.

Make sure to keep URLs unchanged. There are no URLs besides maybe none.

There are markdown links? Not in this content.

There are images? None.

Thus translation straightforward.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμοσμένος Διαχειριστής Πόρων – Καταγραφή Εξόδου HTML με Aspose HTML

Έχετε χρειαστεί ποτέ έναν **custom resource handler** για να παρεμβείτε σε κάθε αρχείο που γράφει το Aspose HTML κατά τη διάρκεια μιας μετατροπής; Ίσως θέλετε να μεταφέρετε HTML, εικόνες ή CSS απευθείας στη μνήμη αντί για το δίσκο. Αυτό είναι ένα πολύ συνηθισμένο σενάριο όταν χτίζετε μια web‑service που πρέπει να παραμείνει stateless ή όταν απλώς θέλετε να **save HTML to stream** για επεξεργασία αργότερα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα που δείχνει πώς να **load HTML document**, να συνδέσετε έναν **custom resource handler**, και να χρησιμοποιήσετε το **Aspose HTML save** για να καταγράψετε κάθε κομμάτι εξόδου σε ένα `MemoryStream`. Στο τέλος θα καταλάβετε όχι μόνο το “τι” αλλά και το “γιατί” πίσω από κάθε γραμμή, και θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

> **Γιατί να το κάνετε;**  
> Η καταγραφή της εξόδου HTML στη μνήμη σας επιτρέπει να αποφύγετε το I/O του συστήματος αρχείων, μειώνει την καθυστέρηση σε cloud functions, και σας δίνει πλήρη έλεγχο πάνω στην ονομασία, τη συμπίεση ή ακόμη και σε μετασχηματισμούς κατά την πτήση.

---

## Τι Θα Χρειαστείτε

- **.NET 6** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Πακέτο NuGet **Aspose.HTML for .NET** (`Aspose.Html`).  
- Ένα απλό αρχείο HTML (`input.html`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.  
- Οποιοδήποτε IDE προτιμάτε — Visual Studio, Rider, ή VS Code με επεκτάσεις C#.

Δεν απαιτείται επιπλέον ρύθμιση· το API κάνει όλη τη βαριά δουλειά.

---

## Βήμα 1 – Δημιουργία Προσαρμοσμένου Διαχειριστή Πόρων

Η καρδιά αυτής της τεχνικής είναι η κληρονομιά από την κλάση `Aspose.Html.Rendering.ResourceHandler`. Με την υπερισχύση του `HandleResource` αποφασίζετε **πού** θα κατευθύνεται κάθε ροή πόρου. Στην περίπτωσή μας επιστρέφουμε ένα νέο `MemoryStream` για κάθε αίτηση, πράγμα που σημαίνει ότι κάθε CSS, εικόνα ή υπο‑HTML τμήμα ζει μόνο στη RAM.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Συμβουλή:** Αν χρειάζεται να παρακολουθείτε τις ροές (π.χ. για να τις γράψετε αργότερα σε αρχείο ZIP), αποθηκεύστε τις σε ένα `Dictionary<string, MemoryStream>` με κλειδί το `resourceInfo.Uri`.

---

## Βήμα 2 – Φόρτωση του Εγγράφου HTML

Πριν μπορέσετε να αποθηκεύσετε οτιδήποτε, πρέπει να **load HTML document** σε μια παρουσία `HTMLDocument`. Το Aspose HTML μπορεί να διαβάσει από διαδρομή αρχείου, URL ή ακόμη και από συμβολοσειρά. Εδώ χρησιμοποιούμε τοπικό αρχείο για απλότητα.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

Αν το HTML σας αναφέρεται σε εξωτερικούς πόρους (εικόνες, γραμματοσειρές κ.λπ.), βεβαιωθείτε ότι το base URI είναι σωστό· διαφορετικά ο διαχειριστής δεν θα μπορεί να τους εντοπίσει.

---

## Βήμα 3 – Δημιουργία του Προσαρμοσμένου Διαχειριστή

Τώρα δημιουργούμε μια παρουσία του διαχειριστή που ορίσαμε νωρίτερα. Τίποτα περίπλοκο — απλώς ένα `new`. Αυτό το αντικείμενο θα περάσει στη μέθοδο `Save` στο επόμενο βήμα.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

Επειδή ο διαχειριστής ζει μόνο στη μνήμη, δεν χρειάζεται να ανησυχείτε για δικαιώματα αρχείων ή καθαρισμό στο δίσκο.

---

## Βήμα 4 – Αποθήκευση του Εγγράφου με Aspose HTML Save

Η λειτουργία **Aspose HTML save** δέχεται ένα `ResourceHandler`. Καθώς η μηχανή διασχίζει το DOM και επιλύει κάθε συνδεδεμένο πόρο, καλεί το `HandleResource`. Η υλοποίησή μας επιστρέφει ένα `MemoryStream`, έτσι κάθε κομμάτι καταλήγει στη RAM.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

Σε αυτό το σημείο η μετατροπή ολοκληρώνεται, αλλά οι ροές παραμένουν στη μνήμη. Μπορείτε τώρα να τις διαβάσετε, να τις γράψετε σε βάση δεδομένων ή να τις επιστρέψετε σε απόκριση API.

---

## Βήμα 5 – Ανάκτηση και Επαλήθευση των Καταγεγραμμένων Ροών

Επειδή επιστρέψαμε ένα νέο `MemoryStream` κάθε φορά, χρειαζόμαστε τρόπο να κρατήσουμε αναφορές. Παρακάτω υπάρχει μια γρήγορη επέκταση του προηγούμενου διαχειριστή που αποθηκεύει κάθε ροή σε λεξικό ώστε να μπορείτε να τις εξετάσετε μετά την αποθήκευση.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

Η εκτέλεση αυτού του κώδικα θα εκτυπώσει το τελικό HTML που παρήγαγε το Aspose, επιβεβαιώνοντας ότι η **capture html output** λειτουργεί όπως αναμένεται.

---

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

### 1. Τι γίνεται αν το έγγραφο είναι τεράστιο;

Η κατανάλωση μνήμης μπορεί να αυξηθεί γρήγορα. Για μεγάλα PDFs ή HTML με πολλές εικόνες υψηλής ανάλυσης, σκεφτείτε να κάνετε streaming απευθείας σε `FileStream` ή σε **buffered network stream** αντί για `MemoryStream`. Ο διαχειριστής μπορεί να αποφασίσει βάσει του `resourceInfo.MimeType`.

### 2. Πρέπει να απελευθερώσω τις ροές;

Ναι. Αφού ολοκληρώσετε την επεξεργασία, καλέστε `Dispose()` σε κάθε `MemoryStream` (ή αφήστε ένα `using` block να το κάνει). Στο παράδειγμα παρακολούθησης θα μπορούσαμε να προσθέσουμε:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Μπορώ να μετονομάσω τους πόρους πριν την αποθήκευση;

Απολύτως. Μέσα στο `HandleResource` έχετε πρόσβαση στο `resourceInfo.Uri`. Μπορείτε να το ξαναγράψετε, να προσθέσετε πρόθεμα ή ακόμη και να παραλείψετε ορισμένα αρχεία επιστρέφοντας `null`.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Είναι αυτή η προσέγγιση thread‑safe;

Μια ενιαία παρουσία διαχειριστή **δεν** πρέπει να μοιράζεται μεταξύ ταυτόχρονων κλήσεων `Save`. Δημιουργήστε νέο διαχειριστή ανά μετατροπή, ή προστατέψτε το εσωτερικό λεξικό με κλείδωμα (lock) αν πρέπει να το επαναχρησιμοποιήσετε.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα που μπορείτε να επικολλήσετε σε μια εφαρμογή console. Δείχνει τα πάντα — από τη φόρτωση του αρχείου HTML μέχρι την εκτύπωση της καταγεγραμμένης εξόδου.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει το πλήρως αποδομημένο HTML (συμπεριλαμβανομένου τυχόν inline CSS που μπορεί να έχει δημιουργήσει το Aspose) ακολουθούμενο από επιβεβαίωση ότι όλες οι ροές έχουν απελευθερωθεί.

---

## Συμπέρασμα

Μόλις μάθατε πώς να υλοποιήσετε έναν **custom resource handler** στο Aspose HTML, να **load an HTML document**, και να **save HTML to stream** ενώ **capture the HTML output** για περαιτέρω επεξεργασία. Το μοτίβο είναι ελαφρύ, ευαίσθητο στο νήμα, και πλήρως επεκτάσιμο — μπορείτε να αντικαταστήσετε το `MemoryStream` με αρχείο, socket δικτύου ή API αποθήκευσης cloud με λίγες γραμμές κώδικα.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **Αποθήκευση σε αρχείο ZIP** (ιδανικό για ομαδοποίηση HTML, CSS και εικόνων).  
- **Εφαρμογή μετασχηματισμών** (π.χ. ελαχιστοποίηση CSS κατά τη διάρκεια).  
- **Streaming απευθείας σε HTTP response** σε ASP.NET Core για άμεση λήψη.

Δοκιμάστε τα και θα δείτε πόσο ισχυρός μπορεί να είναι ένας προσαρμοσμένος **custom resource handler** σε πραγματικά σενάρια. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}