---
title: Μετατροπή EPUB σε XPS σε .NET με Aspose.HTML
linktitle: Μετατροπή EPUB σε XPS στο .NET
second_title: Aspose.HTML .NET API χειρισμού HTML
description: Μάθετε πώς να μετατρέπετε το EPUB σε XPS στο .NET χρησιμοποιώντας το Aspose.HTML για .NET. Ακολουθήστε τον οδηγό βήμα προς βήμα για εύκολες μετατροπές.
type: docs
weight: 13
url: /el/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Αναζητάτε έναν απρόσκοπτο τρόπο μετατροπής αρχείων EPUB σε μορφή XPS στις εφαρμογές σας .NET; Το Aspose.HTML για .NET παρέχει μια ισχυρή λύση για να το πετύχετε αυτό χωρίς κόπο. Σε αυτόν τον οδηγό βήμα προς βήμα, θα σας καθοδηγήσουμε στη διαδικασία μετατροπής του EPUB σε XPS χρησιμοποιώντας το Aspose.HTML. Ας αρχίσουμε!

## Προαπαιτούμενα

Πριν ξεκινήσετε τη διαδικασία μετατροπής EPUB σε XPS, θα πρέπει να βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

### 1. Aspose.HTML για .NET Library

 Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη Aspose.HTML για .NET στο έργο σας. Εάν δεν το έχετε κάνει, μπορείτε να το αποκτήσετε από το[Σελίδα λήψης Aspose.HTML για .NET](https://releases.aspose.com/html/net/).

### 2. Εισαγάγετε το αρχείο EPUB

Θα χρειαστείτε ένα αρχείο EPUB που θέλετε να μετατρέψετε σε XPS. Βεβαιωθείτε ότι έχετε διαθέσιμο αρχείο EPUB για μετατροπή.

### 3. .NET Αναπτυξιακό Περιβάλλον

Αυτός ο οδηγός προϋποθέτει ότι έχετε ρυθμίσει ένα λειτουργικό περιβάλλον ανάπτυξης .NET στον υπολογιστή σας.

## Εισαγωγή χώρου ονομάτων

Για να ξεκινήσετε, θα πρέπει να εισαγάγετε τον απαραίτητο χώρο ονομάτων για το Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Μετατροπή EPUB σε XPS

Ας αναλύσουμε τη διαδικασία μετατροπής ενός αρχείου EPUB σε μορφή XPS σε πολλά βήματα.

### Βήμα 1.1: Ανοίξτε το Αρχείο EPUB

Αρχικά, ανοίξτε το υπάρχον αρχείο EPUB για ανάγνωση χρησιμοποιώντας ένα FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Συνεχίστε με τη διαδικασία μετατροπής
}
```

### Βήμα 1.2: Δημιουργία XpsSaveOptions

Δημιουργήστε μια παρουσία του XpsSaveOptions. Αυτό το βήμα είναι κρίσιμο για τη διαμόρφωση της εξόδου XPS:

```csharp
var options = new XpsSaveOptions();
```

### Βήμα 1.3: Μετατροπή EPUB σε XPS

Τώρα, ας καλέσουμε τη μέθοδο ConvertEPUB για να μετατρέψουμε το EPUB σε XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Καθορίστε προσαρμοσμένες επιλογές XPS

Μπορείτε να προσαρμόσετε περαιτέρω την έξοδο XPS καθορίζοντας προσαρμοσμένες επιλογές όπως το μέγεθος σελίδας και το χρώμα φόντου.

### Βήμα 2.1: Προσαρμοσμένο μέγεθος σελίδας και χρώμα φόντου

Δημιουργήστε μια παρουσία του XpsSaveOptions με προσαρμοσμένο μέγεθος σελίδας και χρώμα φόντου:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Βήμα 2.2: Μετατρέψτε το EPUB σε XPS με προσαρμοσμένες επιλογές

Τώρα, καλέστε τη μέθοδο ConvertEPUB για να μετατρέψετε το EPUB σε XPS με τις προσαρμοσμένες επιλογές:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Χρησιμοποιήστε τον πάροχο προσαρμοσμένης ροής

Σε αυτό το βήμα, θα μετατρέψουμε το EPUB σε XPS χρησιμοποιώντας έναν πάροχο προσαρμοσμένης ροής, επιτρέποντάς σας να χειριστείτε τα δεδομένα που προκύπτουν.

### Βήμα 3.1: Δημιουργήστε ένα MemoryStreamProvider

Δημιουργήστε μια παρουσία του MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Συνεχίστε με τη διαδικασία μετατροπής
}
```

### Βήμα 3.2: Μετατρέψτε το EPUB σε XPS με τον πάροχο ροής

Μετατρέψτε το EPUB σε XPS χρησιμοποιώντας το MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Βήμα 3.3: Πρόσβαση και αποθήκευση αποτελεσμάτων

Ανακτήστε τη ροή μνήμης που περιέχει τα δεδομένα που έχουν μετατραπεί και αποθηκεύστε την σε ένα αρχείο εξόδου:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Πηγαίος κώδικας κατηγορίας MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Λίστα αντικειμένων MemoryStream που δημιουργήθηκαν κατά την απόδοση του εγγράφου
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Αυτή η μέθοδος καλείται όταν απαιτείται η μόνη ροή εξόδου, για παράδειγμα για μορφές XPS, PDF ή TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Αυτή η μέθοδος καλείται όταν απαιτείται η δημιουργία πολλαπλών ροών εξόδου. Για παράδειγμα, κατά την απόδοση του HTML στη λίστα των αρχείων εικόνας (JPG, PNG, κ.λπ.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Εδώ μπορείτε να απελευθερώσετε τη ροή γεμάτη δεδομένα και, για παράδειγμα, να την ξεπλύνετε στον σκληρό δίσκο
            }
            public void Dispose()
            {
                // Αποδέσμευση πόρων
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Συγχαρητήρια! Μετατρέψατε επιτυχώς ένα αρχείο EPUB σε μορφή XPS χρησιμοποιώντας το Aspose.HTML για .NET.

## συμπέρασμα

Σε αυτό το ολοκληρωμένο σεμινάριο, εξερευνήσαμε πώς να αξιοποιήσουμε το Aspose.HTML για .NET για να μετατρέψουμε αρχεία EPUB σε μορφή XPS με διάφορες επιλογές προσαρμογής. Είτε είστε έμπειρος προγραμματιστής είτε μόλις ξεκινάτε, το Aspose.HTML απλοποιεί τη διαδικασία, επιτρέποντάς σας να χειρίζεστε εύκολα τις μετατροπές EPUB σε XPS.

 Έχετε ερωτήσεις ή αντιμετωπίσατε προβλήματα; Ελέγξτε το[Aspose.HTML Τεκμηρίωση](https://reference.aspose.com/html/net/) για περισσότερες πληροφορίες ή ζητήστε βοήθεια από το[Φόρουμ κοινότητας Aspose.HTML](https://forum.aspose.com/).

## Συχνές Ερωτήσεις

### Τι είναι το Aspose.HTML για .NET;
Το Aspose.HTML για .NET είναι μια ισχυρή βιβλιοθήκη που επιτρέπει στους προγραμματιστές να εργάζονται με έγγραφα HTML, EPUB και XPS σε εφαρμογές .NET.

### Πού μπορώ να κατεβάσω το Aspose.HTML για .NET;
 Μπορείτε να κάνετε λήψη του Aspose.HTML για .NET από το[σελίδα λήψης](https://releases.aspose.com/html/net/).

### Υπάρχει διαθέσιμη δωρεάν δοκιμή για το Aspose.HTML για .NET;
 Ναι, μπορείτε να λάβετε δωρεάν δοκιμή από[εδώ](https://releases.aspose.com/).

### Πώς μπορώ να αποκτήσω μια προσωρινή άδεια χρήσης για το Aspose.HTML για .NET;
 Για να λάβετε προσωρινή άδεια, επισκεφτείτε το[σελίδα προσωρινής άδειας](https://purchase.aspose.com/temporary-license/).

### Πού μπορώ να βρω περισσότερα σεμινάρια και τεκμηρίωση για το Aspose.HTML για .NET;
 Εξερευνήστε ένα ευρύ φάσμα εκπαιδευτικών προγραμμάτων και λεπτομερούς τεκμηρίωσης για το[Aspose.HTML Τεκμηρίωση](https://reference.aspose.com/html/net/) σελίδα.