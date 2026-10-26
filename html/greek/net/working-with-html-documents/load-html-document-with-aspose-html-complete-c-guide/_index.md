---
category: general
date: 2026-03-25
description: Φορτώστε έγγραφο HTML χρησιμοποιώντας το Aspose.HTML και ενσωματώστε
  τις γραμματοσειρές στο HTML, προσαρμοσμένο χειριστή πόρων, επαναφορά της ροής μνήμης
  και τις επιλογές αποθήκευσης Aspose HTML. Οδηγός βήμα‑βήμα.
draft: false
keywords:
- load html document
- embed fonts html
- custom resource handler
- rewind memory stream
- aspose html save
language: el
og_description: Φορτώστε έγγραφο HTML χρησιμοποιώντας το Aspose.HTML, ενσωματώστε
  γραμματοσειρές HTML και χρησιμοποιήστε έναν προσαρμοσμένο διαχειριστή πόρων. Μάθετε
  πώς να επαναφέρετε τη ροή μνήμης και να αποθηκεύσετε με το Aspose.HTML.
og_title: Φόρτωση εγγράφου HTML με το Aspose.HTML – Πλήρης οδηγός C#
tags:
- Aspose.HTML
- C#
- HTML processing
title: Φόρτωση εγγράφου HTML με το Aspose.HTML – Πλήρης οδηγός C#
url: /el/net/working-with-html-documents/load-html-document-with-aspose-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση εγγράφου HTML με Aspose.HTML – Πλήρης οδηγός C#

Έχετε ποτέ χρειαστεί να **φορτώσετε έγγραφο HTML** σε μια εφαρμογή .NET αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε κάθε πόρο—CSS, εικόνες, ακόμη και ενσωματωμένες γραμματοσειρές—ακριβώς εκεί που τα χρειάζεστε; Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση ενός εγγράφου HTML, τη χρήση ενός **custom resource handler**, την ενσωμάτωση γραμματοσειρών, την επαναφορά ενός memory stream, και τελικά την κλήση του **aspose html save** ώστε η έξοδος να είναι έτοιμη για περαιτέρω χρήση.

Θα καλύψουμε τα πάντα, από τον αρχικό κατασκευαστή `HTMLDocument` μέχρι την τελική κλήση `File.WriteAllBytes`, καθώς και μερικές πρακτικές συμβουλές που θα εκτιμήσετε όταν αντιμετωπίσετε ειδικές περιπτώσεις. Δεν απαιτούνται εξωτερικές αναφορές· απλώς αντιγράψτε‑και‑επικολλήστε τον κώδικα και είστε έτοιμοι.

## Τι θα χρειαστείτε

- **Aspose.HTML for .NET** (v23.12 ή νεότερη). Το πακέτο NuGet είναι `Aspose.Html`.
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή VS Code με την επέκταση C#).
- Ένα δείγμα αρχείου HTML (`sample.html`) τοποθετημένο κάπου που μπορείτε να αναφερθείτε με απόλυτη ή σχετική διαδρομή.
- Βασική εξοικείωση με streams και σύνταξη C#.

Αν τα έχετε ήδη, υπέροχα—ας προχωρήσουμε κατευθείαν.

## Βήμα 1: Φόρτωση εγγράφου HTML (Κύρια ενέργεια)

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `HTMLDocument`, υποδεικνύοντας το αρχείο προέλευσης. Αυτή η ενέργεια **φορτώνει το έγγραφο HTML** στο in‑memory μοντέλο του Aspose, αναλύοντας το markup και προετοιμάζοντας τυχόν συνδεδεμένους πόρους.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;

// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του εγγράφου με αυτόν τον τρόπο επιτρέπει στο Aspose να επιλύει αυτόματα σχετικές URL, κάτι που είναι απαραίτητο όταν αργότερα ενσωματώνετε γραμματοσειρές ή άλλα περιουσιακά στοιχεία.

## Βήμα 2: Δημιουργία προσαρμοσμένου Resource Handler

Το Aspose.HTML καλεί ένα `ResourceHandler` κάθε φορά που χρειάζεται να γράψει έναν πόρο (HTML, CSS, εικόνες, γραμματοσειρές). Παρέχοντας το δικό μας handler αποκτούμε πλήρη έλεγχο του πού πηγαίνουν αυτά τα bytes. Σε αυτό το παράδειγμα κατευθύνουμε τα πάντα σε ένα ενιαίο `MemoryStream`, αλλά θα μπορούσατε να διαφοροποιήσετε ανάλογα με το `resource.Type`.

```csharp
// Define a custom resource handler that writes everything to one memory stream
class MemoryHandler : ResourceHandler
{
    // Expose the stream so we can read it later
    public MemoryStream Output { get; } = new MemoryStream();

    // This method is invoked for each resource Aspose.HTML wants to save
    public override Stream HandleResource(Resource resource)
    {
        // For demonstration we write all resources (HTML, CSS, images, fonts) to the same stream.
        // In production you might inspect resource.Type and route accordingly.
        return Output;
    }
}

// Instantiate the handler
MemoryHandler handler = new MemoryHandler();
```

> **Συμβουλή:** Αν χρειάζεστε ενσωμάτωση γραμματοσειρών, ορίστε `HTMLSaveOptions.EmbedFonts = true` (δείτε το Βήμα 4). Ο handler θα λάβει τα αρχεία γραμματοσειρών ως ξεχωριστούς πόρους, τα οποία μπορείτε να αποθηκεύσετε όπου θέλετε.

## Βήμα 3: Προετοιμασία επιλογών αποθήκευσης (συμπεριλαμβανομένης της ενσωμάτωσης γραμματοσειρών HTML)

Το Aspose παρέχει `HTMLSaveOptions` για να προσαρμόσετε την έξοδο. Η πιο συνηθισμένη προσαρμογή για το σενάριό μας είναι το `EmbedFonts`, το οποίο αναγκάζει τη βιβλιοθήκη να ενσωματώνει οποιεσδήποτε αναφερόμενες γραμματοσειρές απευθείας στο παραγόμενο HTML χρησιμοποιώντας base‑64 data URIs.

```csharp
HTMLSaveOptions saveOptions = new HTMLSaveOptions()
{
    // Embedding fonts makes the output self‑contained – perfect for email or offline use.
    EmbedFonts = true,

    // You can also control whether resources are saved as separate files or inline.
    // For this tutorial we keep everything in the memory stream via the handler.
    Resources = SaveResourcesMode.External
};
```

> **Γιατί να ενεργοποιήσετε το EmbedFonts;** Χωρίς αυτό, ένας πελάτης που δεν έχει εγκατεστημένη τη γραμματοσειρά θα επιστρέψει σε μια γενική γραμματοσειρά, διαταράσσοντας το σχεδιασμό σας. Η ενσωμάτωση εγγυάται οπτική πιστότητα.

## Βήμα 4: Αποθήκευση του εγγράφου χρησιμοποιώντας το προσαρμοσμένο Handler

Τώρα ζητάμε από το Aspose να αποδώσει το έγγραφο και να περάσει το `MemoryHandler` μαζί με τις επιλογές που μόλις διαμορφώσαμε. Εδώ συμβαίνει η πραγματική λειτουργία **aspose html save**.

```csharp
// Save the document; the handler receives every resource.
document.Save(handler, saveOptions);
```

Σε αυτό το σημείο, το stream `handler.Output` περιέχει το πλήρως αποδοθέν HTML συν τυχόν ενσωματωμένα περιουσιακά στοιχεία. Αν εξετάσετε το stream, θα δείτε ένα ενιαίο, ενωμένο μπλοκ bytes.

## Βήμα 5: Επαναφορά του Memory Stream και αποθήκευση στο δίσκο

Πριν μπορέσουμε να διαβάσουμε από ένα `MemoryStream`, πρέπει να επαναφέρουμε τη θέση του στην αρχή. Αυτό είναι το κλασικό βήμα **rewind memory stream**—διαφορετικά θα λάβετε ένα κενό αρχείο ή μια περικομμένη έξοδο.

```csharp
// Rewind the stream to the beginning so we can read from it.
handler.Output.Position = 0;

// Write the generated HTML to a file on disk.
File.WriteAllBytes("YOUR_DIRECTORY/generated.html", handler.Output.ToArray());
```

> **Τι θα δείτε:** Το `generated.html` περιέχει τώρα το αρχικό markup, όλα τα CSS, τις εικόνες και τις γραμματοσειρές ενσωματωμένες ως data URIs. Ανοίξτε το σε έναν περιηγητή και η σελίδα θα φαίνεται ακριβώς όπως το αρχικό `sample.html`, ακόμη και αν μετακινήσετε το αρχείο σε άλλο υπολογιστή.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα κομμάτια μαζί, έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας. Μπορείτε να το αντιγράψετε σε ένα νέο αρχείο `.cs` και να το εκτελέσετε.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;

namespace AsposeHtmlDemo
{
    // Custom handler that writes every resource into a single MemoryStream
    class MemoryHandler : ResourceHandler
    {
        public MemoryStream Output { get; } = new MemoryStream();

        public override Stream HandleResource(Resource resource)
        {
            // All resources (HTML, CSS, images, fonts) go to the same stream.
            // You could branch on resource.Type here if needed.
            return Output;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source HTML document
            HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");

            // 2️⃣ Create the custom resource handler
            MemoryHandler handler = new MemoryHandler();

            // 3️⃣ Configure save options – embed fonts for a self‑contained file
            HTMLSaveOptions saveOptions = new HTMLSaveOptions()
            {
                EmbedFonts = true,
                Resources = SaveResourcesMode.External
            };

            // 4️⃣ Save the document using the handler (this triggers aspose html save)
            document.Save(handler, saveOptions);

            // 5️⃣ Rewind the memory stream and write the result to disk
            handler.Output.Position = 0; // rewind memory stream
            File.WriteAllBytes("YOUR_DIRECTORY/generated.html", handler.Output.ToArray());

            Console.WriteLine("HTML document loaded, processed, and saved successfully!");
        }
    }
}
```

### Αναμενόμενη έξοδος

- **`generated.html`** – ένα ενιαίο αρχείο HTML με όλα τα CSS, τις εικόνες και τις γραμματοσειρές ενσωματωμένα.
- Δεν δημιουργούνται επιπλέον φάκελοι ή αρχεία επειδή όλα κατευθύνθηκαν μέσω του `MemoryHandler`.

Ανοίξτε το αρχείο σε Chrome, Edge ή Firefox· θα πρέπει να δείτε την ίδια διάταξη με το αρχικό `sample.html`. Αν εξετάσετε την πηγή, ψάξτε για αλφαριθμητικά `data:font/ttf;base64,...`—αυτά είναι τα ενσωματωμένα δεδομένα γραμματοσειράς.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Τι κάνω αν χρειάζομαι ξεχωριστά αρχεία για εικόνες;

Μπορείτε να τροποποιήσετε το `HandleResource` ώστε να ελέγχει το `resource.Type`. Για εικόνες (`ResourceType.Image`) επιστρέψτε ένα `FileStream` που δείχνει σε έναν αφιερωμένο φάκελο, ενώ συνεχίζετε να επιστρέφετε το ίδιο `MemoryStream` για HTML και CSS. Αυτό κρατά το HTML ελαφρύ αλλά σας επιτρέπει να διαχειρίζεστε τα περιουσιακά στοιχεία ξεχωριστά.

### Πώς να διαχειριστώ μεγάλα έγγραφα χωρίς να εξαντλήσω τη μνήμη;

Ένα ενιαίο `MemoryStream` λειτουργεί καλά για μέτρια αρχεία (< 10 MB). Για μεγαλύτερα φορτία, σκεφτείτε τη ροή απευθείας σε `FileStream` ή τη χρήση του `SaveResourcesMode.Zip` του Aspose για να συσσωρεύσετε τα πάντα σε ένα αρχείο zip.

### Λειτουργεί το `EmbedFonts = true` με όλες τις μορφές γραμματοσειρών;

Το Aspose.HTML υποστηρίζει TrueType (`.ttf`) και OpenType (`.otf`). Μορφές web‑font όπως `.woff` επίσης υποστηρίζονται, αλλά πρέπει να αναφέρονται στο CSS με έναν σωστό κανόνα `@font-face`. Η βιβλιοθήκη θα τις ενσωματώσει αυτόματα όταν ενεργοποιηθεί η επιλογή.

### Μπορώ να στοχεύσω .NET Core;

Απολύτως. Ο ίδιος κώδικας εκτελείται σε .NET 5, .NET 6 ή .NET 7. Απλώς βεβαιωθείτε ότι αναφέρετε τη σωστή έκδοση του πακέτου Aspose.HTML που ταιριάζει με το πλαίσιο-στόχο σας.

## Συνοπτική επισκόπηση

Σας δείξαμε πώς να **φορτώσετε έγγραφο html** χρησιμοποιώντας το Aspose.HTML, να διαμορφώσετε έναν **custom resource handler**, να ενεργοποιήσετε το **embed fonts html**, να **rewind memory stream** σωστά, και τελικά να εκτελέσετε ένα **aspose html save** που παράγει ένα πλήρως αυτόνομο αρχείο HTML. Το πρότυπο είναι αρκετά ευέλικτο για προχωρημένα σενάρια—είτε χρειάζεστε να χωρίσετε πόρους, να τα συμπιέσετε σε zip ή να τα ρέξετε απευθείας σε δικτυακή τοποθεσία.

## Τι ακολουθεί;

- **Εξερευνήστε το `HTMLRenderingOptions`** για να ελέγξετε DPI, μέγεθος σελίδας ή rasterization αν χρειάζεστε PDFs.
- **Συνδυάστε με το Aspose.PDF** για να μετατρέψετε το παραγόμενο HTML σε PDF σε μια ενιαία διαδικασία.
- **Εφαρμόστε ένα επίπεδο caching** για συχνά προσπελαζόμενους πόρους, μειώνοντας το I/O σε επόμενες αποθηκεύσεις.

Μη διστάσετε να πειραματιστείτε, να σπάσετε πράγματα, και μετά να επιστρέψετε σε αυτόν τον οδηγό για μια γρήγορη επανάληψη. Καλή προγραμματιστική, και εύχομαι το HTML σας πάντα να αποδίδει ακριβώς όπως το θέλετε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}