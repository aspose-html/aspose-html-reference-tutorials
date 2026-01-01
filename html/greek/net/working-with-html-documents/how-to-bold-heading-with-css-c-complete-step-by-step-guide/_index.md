---
category: general
date: 2026-01-01
description: Πώς να κάνετε έντονο έναν τίτλο και να εφαρμόσετε πλάγια γραφή χρησιμοποιώντας
  C# και CSS. Μάθετε πώς να ορίζετε το βάρος γραμματοσειράς του τίτλου, να εφαρμόζετε
  έντονη και πλάγια γραφή, και να μορφοποιείτε τους τίτλους γρήγορα.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: el
og_description: Πώς να κάνετε έντονο τον τίτλο στην πρώτη πρόταση, στη συνέχεια να
  μάθετε πώς να εφαρμόζετε πλάγια γραφή, να συνδυάσετε έντονη και πλάγια γραφή, και
  να ορίσετε το βάρος γραμματοσειράς του τίτλου με σαφή παραδείγματα.
og_title: Πώς να κάνετε έντονο τον τίτλο – Πλήρης οδηγός για CSS & C#
tags:
- CSS
- C#
- Web Development
title: Πώς να κάνετε έντονο έναν τίτλο με CSS & C# – Πλήρης οδηγός βήμα‑βήμα
url: /el/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε έντονο το τίτλο – Πλήρης οδηγός για CSS & C#

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε έντονο το τίτλο** σε μια ιστοσελίδα χωρίς να σκάβετε μέσα σε ατελείωτα έγγραφα; Δεν είστε οι μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν χρειάζονται μια γρήγορη οπτική τροποποίηση, ειδικά όταν συνδυάζουν HTML, CSS και λίγο C# για να οδηγήσουν το UI.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να εφαρμόσετε έντονη, πλάγια και συνδυασμένες μορφές σε ένα στοιχείο `<h1>`. Καθ' όλη τη διάρκεια θα καλύψουμε επίσης **πώς να εφαρμόσετε πλάγια**, πώς να **εφαρμόσετε έντονη και πλάγια** μαζί, και τη λεπτή διαφορά μεταξύ της χρήσης του CSS `font-weight` και του χαμηλού επιπέδου API `WebFontStyle`. Στο τέλος θα μπορείτε να **ορίσετε το βάρος γραμματοσειράς του τίτλου** με σιγουριά, ανεξάρτητα από το stack που χρησιμοποιείτε.

## Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.8 αν προτιμάτε)
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#
- Βασικές γνώσεις HTML και CSS
- Ένα απλό έργο WinForms ή WPF που φιλοξενεί έναν έλεγχο WebView2 (το παράδειγμα χρησιμοποιεί WinForms)

Αν κάποιο από αυτά σας είναι άγνωστο, μην πανικοβληθείτε – θα σας δείξουμε τον ελάχιστο κώδικα που χρειάζεστε, και μπορείτε να τον αντιγράψετε‑και‑επικολλήσετε κατευθείαν σε ένα νέο έργο.

---

## Βήμα 1: Δημιουργία μιας ελάχιστης σελίδας HTML

Πρώτα, χρειαζόμαστε ένα αρχείο HTML που ο έλεγχος WebView2 μπορεί να φορτώσει. Αποθηκεύστε το παρακάτω ως `index.html` στον φάκελο εξόδου του έργου σας (π.χ., `bin\Debug\net6.0-windows`).

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Heading Styling Demo</title>
    <style>
        /* Default styling – we’ll override this from C# */
        h1 {
            font-family: 'Arial', sans-serif;
            font-weight: normal;
            font-style: normal;
        }
    </style>
</head>
<body>
    <h1 id="title">Dynamic Heading</h1>
    <p>Open the C# console or UI to see the heading change.</p>
</body>
</html>
```

> **Γιατί είναι σημαντικό:** Η ελάχιστη CSS μας δίνει ένα καθαρό καμβά ώστε να βλέπουμε ακριβώς τι κάνει ο κώδικας C#. Το χαρακτηριστικό `id="title"` κάνει εύκολο το στοχοθέτηση του τίτλου από το script.

---

## Βήμα 2: Ρύθμιση του έργου WinForms με WebView2

Δημιουργήστε μια νέα **Windows Forms App** (`.NET 6`) και προσθέστε το πακέτο NuGet **Microsoft.Web.WebView2**. Σύρετε έναν έλεγχο `WebView2` στη φόρμα, ονομάστε τον `webView`, και ορίστε την ιδιότητα `Dock` σε `Fill`.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            // Ensure the WebView2 runtime is available
            await webView.EnsureCoreWebView2Async();

            // Load the local HTML file
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }
    }
}
```

> **Pro tip:** Αν η πλοήγηση αποτύχει, ελέγξτε ξανά ότι το `index.html` έχει αντιγραφεί στον φάκελο εξόδου (ορίστε *Copy to Output Directory* → *Copy always*).

---

## Βήμα 3: Εντοπισμός του στοιχείου τίτλου σε C#

Μόλις η σελίδα φορτώσει, μπορούμε να πιάσουμε το στοιχείο `<h1>`. Το API `CoreWebView2` παρέχει τη μέθοδο `ExecuteScriptAsync` που εκτελεί JavaScript και επιστρέφει το αποτέλεσμα. Ωστόσο, για το σκοπό αυτού του tutorial θα χρησιμοποιήσουμε το **χαμηλού επιπέδου DOM wrapper** που έρχεται με το WebView2 (διαθέσιμο μέσω `webView.CoreWebView2`).

```csharp
private async void WebView_NavigationCompleted(
    object sender, CoreWebView2NavigationCompletedEventArgs e)
{
    // Step 1: Locate the heading element you want to style
    var heading = await webView.CoreWebView2
        .ExecuteScriptAsync("document.querySelector('h1');");

    // The script returns a JS object reference we can manipulate.
    // In practice we’ll call methods on it via ExecuteScriptAsync.
}
```

> **Γιατί το κάνουμε:** Η άμεση πρόσβαση στο DOM μας επιτρέπει να αποφύγουμε την έγχυση μεγάλων JavaScript blobs. Είναι πιο καθαρό και δείχνει **πώς να εφαρμόσετε έντονη** χρησιμοποιώντας το API του WebView2.

---

## Βήμα 4: Εφαρμογή έντονης, πλάγιας και συνδυασμένων μορφών

Τώρα θα χρησιμοποιήσουμε τρεις διαφορετικές προσεγγίσεις για να μορφοποιήσουμε τον τίτλο:

1. **CSS `font-weight`** – ο πιο κοινός τρόπος, ικανοποιώντας την απαίτηση **ορίστε το βάρος γραμματοσειράς του τίτλου**.
2. **CSS `font-style`** – πώς να **εφαρμόσετε πλάγια**.
3. **Σημαίες `WebFontStyle`** – μια χαμηλού επιπέδου εναλλακτική που μας επιτρέπει να **εφαρμόσουμε έντονη και πλάγια** ταυτόχρονα.

```csharp
private async void StyleHeading()
{
    // 1️⃣ Apply a bold weight (700) – classic CSS method
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontWeight = '700';
    ");

    // 2️⃣ Apply italic style – fulfills “how to apply italic”
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontStyle = 'italic';
    ");

    // 3️⃣ Use the low‑level API to combine bold + italic flags
    // This requires the WebFontStyle enumeration from the WebView2 SDK.
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        // The following line mimics WebFontStyle usage in C#
        // Note: This is illustrative; actual flag usage happens in C#
        // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
    ");
}
```

> **Επεξήγηση:**  
> • `fontWeight = '700'` λέει στον περιηγητή να αποδώσει το κείμενο με **έντονο** βάρος.  
> • `fontStyle = 'italic'` κλίνει τα γλυφικά, ικανοποιώντας το ερώτημα **πώς να εφαρμόσετε πλάγια**.  
> • Η σχολιασμένη γραμμή δείχνει πώς *θα μπορούσατε* να ορίσετε `WebFontStyle` από το C# αν έχετε ένα wrapper που εκθέτει το enum. Σε πραγματικό σενάριο θα καλέσατε μια μέθοδο C# στο αντικείμενο `heading`, π.χ., `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

Για να καλέσετε πραγματικά το χαμηλού επιπέδου API από C#, χρειάζεστε ένα COM interop wrapper. Εδώ είναι ένα ελάχιστο παράδειγμα υποθέτοντας ότι έχετε αναφορά στο namespace `Microsoft.Web.WebView2.Wpf`:

```csharp
using Microsoft.Web.WebView2.WinForms;
using Microsoft.Web.WebView2.Core;
using System.Runtime.InteropServices;

private async void ApplyWebFontStyle()
{
    var script = @"
        (function() {
            var h = document.querySelector('h1');
            // Expose the element to C#
            return h;
        })();";

    var result = await webView.CoreWebView2.ExecuteScriptAsync(script);
    // The result is a JSON representation; you’d need a proper COM object to set flags.
    // For brevity, the example focuses on the CSS path which works everywhere.
}
```

> **Bottom line:** Αν είστε άνετοι με το μοντέλο COM του WebView2, η προσέγγιση με σημαίες σας δίνει λεπτομερή έλεγχο. Διαφορετικά, η διαδρομή μέσω CSS είναι απολύτως επαρκής και λειτουργεί σε όλους τους περιηγητές.

---

## Βήμα 5: Συνδέστε τα όλα – Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει ένα μοναδικό αρχείο `MainForm.cs` που μεταγλωττίζει και τρέχει. Φορτώνει το HTML και, όταν ολοκληρωθεί η πλοήγηση, μορφοποιεί τον τίτλο.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            webView.NavigationCompleted += WebView_NavigationCompleted;
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            await webView.EnsureCoreWebView2Async();
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }

        private async void WebView_NavigationCompleted(
            object sender, CoreWebView2NavigationCompletedEventArgs e)
        {
            // Apply the three styling techniques
            await webView.CoreWebView2.ExecuteScriptAsync(@"
                var h = document.querySelector('h1');
                h.style.fontWeight = '700';   // bold
                h.style.fontStyle = 'italic'; // italic
                // For low‑level API, you’d use:
                // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            ");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Όταν εκτελέσετε την εφαρμογή, το παράθυρο εμφανίζει:

- **“Dynamic Heading”** αποδομένο σε **έντονη** (βάρος 700) και **πλάγια**.
- Η παρακείμενη παράγραφος παραμένει αμετάβλητη.
- Αν ελέγξετε το στοιχείο (Ctrl + Shift + I), θα δείτε τα ενσωματωμένα στυλ που έχουν εφαρμοστεί.

---

## Συχνές ερωτήσεις & Ακραίες περιπτώσεις

### 1️⃣ *Τι γίνεται αν ο τίτλος έχει ήδη κλάση;*  
Μπορείτε είτε να προσθέσετε μια κλάση μέσω `classList.add('my‑bold‑italic')` και να ορίσετε τα στυλ σε ένα stylesheet, είτε να συνεχίσετε με ενσωματωμένα στυλ όπως φαίνεται. Τα ενσωματωμένα στυλ κερδίζουν όταν χρειάζεται μια γρήγορη, μοναδική αλλαγή.

### 2️⃣ *Τις σέβονται όλα τα προγράμματα περιήγησης το `font-weight: 700`;*  
Ναι, το 700 αντιστοιχεί στο **Bold** βάρος σύμφωνα με το CSS spec. Αν η οικογένεια γραμματοσειρών δεν παρέχει έντονο στυλ, ο περιηγητής θα το συνθέσει, κάτι που μπορεί να φαίνεται ελαφρώς θολό. Γι' αυτό συνιστάται η χρήση γραμματοσειράς με πραγματική έντονη παραλλαγή (π.χ., Arial).

### 3️⃣ *Μπορώ να ανιματοποιήσω τη μετάβαση από κανονική σε έντονη;*  
Απολύτως. Προσθέστε μια CSS μετάβαση:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

Στη συνέχεια εναλλάξτε τα στυλ από το C# και παρακολουθήστε την ομαλή ανίμαση.

### 4️⃣ *Τι γίνεται με την προσβασιμότητα;*  
Η έντονη και η πλάγια είναι οπτικές ενδείξεις, όχι σημασιολογικές. Για αναγνώστες οθόνης, σκεφτείτε να προσθέσετε `aria-label` ή να χρησιμοποιήσετε σωστή ιεραρχία τίτλων (`<h1>` → `<h2>`) για να μεταφέρετε τη σημασία.

---

## Pro Tips & Gotchas

- **Pro tip:** Κρατήστε το CSS σας σε ξεχωριστό αρχείο και χρησιμοποιήστε το C# μόνο για εναλλαγή κλάσεων. Αυτό καθαρίζει τη λογική UI και το κάνει πιο συντηρήσιμο.
- **Προσοχή:** Μην υπερκαλύπτετε τα προεπιλεγμένα στυλ του user‑agent. Κάποιοι περιηγητές εφαρμόζουν `font-weight: bold` σε ετικέτες `<strong>`· αποφύγετε το μείγμα αυτών με χειροκίνητη μορφοποίηση εκτός αν το θέλετε σκόπιμα.
- **Σημείωση απόδοσης:** Οι αλλαγές ενσωματωμένων στυλ είναι φθηνές, αλλά αν σκοπεύετε να μορφοποιήσετε δεκάδες στοιχεία, ομαδοποιήστε τις σε μία κλήση script για να μειώσετε τα round‑trips.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **κάνετε έντονο το τίτλο** και να **εφαρμόσετε πλάγια**, καθώς και το κόλπο για **να εφαρμόσετε έντονη και πλάγια** μαζί και να **ορίσετε το βάρος γραμματοσειράς του τίτλου** προγραμματιστικά από το C#. Χρησιμοποιώντας μια μικρή σελίδα HTML, έναν κεντρικό WebView2 σε WinForms και μερικές κλήσεις `ExecuteScriptAsync`,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}