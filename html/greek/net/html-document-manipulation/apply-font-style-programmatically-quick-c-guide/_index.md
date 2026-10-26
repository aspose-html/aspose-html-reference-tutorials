---
category: general
date: 2026-04-23
description: Εφαρμόστε το στυλ γραμματοσειράς προγραμματιστικά και μάθετε πώς να αφαιρέσετε
  την υπογράμμιση από το κείμενο, να αλλάξετε το στυλ κειμένου και να ορίσετε έντονο
  κείμενο προγραμματιστικά σε ένα σύντομο οδηγό.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: el
og_description: Εφαρμόστε το στυλ γραμματοσειράς προγραμματιστικά και ανακαλύψτε πώς
  να αφαιρέσετε την υπογράμμιση από το κείμενο, να αλλάξετε το στυλ κειμένου και να
  ορίσετε έντονο κείμενο προγραμματιστικά σε ένα σύντομο, πρακτικό οδηγό.
og_title: Εφαρμογή Στυλ Γραμματοσειράς Προγραμματιστικά – Γρήγορος Οδηγός C#
tags:
- csharp
- ui
- text-formatting
- programming
title: Εφαρμογή Στυλ Γραμματοσειράς Προγραμματιστικά – Σύντομος Οδηγός C#
url: /el/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή Στυλ Γραμματοσειράς Προγραμματιστικά – Γρήγορος Οδηγός C#

Έχετε ποτέ χρειαστεί να **εφαρμόσετε στυλ γραμματοσειράς** σε ένα στοιχείο UI αλλά δεν ήξερτε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν πειραματίζονται για πρώτη φορά με δυναμική μορφοποίηση κειμένου. Τα καλά νέα; Σε λίγα μόνο λεπτά θα ξέρετε ακριβώς πώς να αλλάξετε την εμφάνιση μιας ετικέτας, να αφαιρέσετε την υπογράμμιση από το κείμενο και να ορίσετε έντονο κείμενο προγραμματιστικά χωρίς να ψάχνετε σε ατελείωτη τεκμηρίωση.

Σε αυτό το **μαθήμα μορφοποίησης κειμένου** θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα, θα εξηγήσουμε το «γιατί» πίσω από κάθε γραμμή και θα προσθέσουμε πρακτικές συμβουλές που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο WinForms ή WPF. Χωρίς περιττές πληροφορίες, μόνο ό,τι χρειάζεται για να ολοκληρωθεί η εργασία.

---

## Τι Θα Μάθετε

- Πώς να **εφαρμόσετε στυλ γραμματοσειράς** χρησιμοποιώντας μια μικρή βοηθητική κλάση.  
- Τα ακριβή βήματα για **αφαίρεση υπογράμμισης από το κείμενο** διατηρώντας τα άλλα στυλ ανέπαφα.  
- Τρόποι για **αλλαγή στυλ κειμένου** (έντονο, πλάγιο, υπογράμμιση) εν κινήσει.  
- Ένα πλήρες, έτοιμο για αντιγραφή απόσπασμα που **ορίζει έντονο κείμενο προγραμματιστικά**.  
- Κοινές παγίδες και διαχείριση ειδικών περιπτώσεων ώστε να μην εκπλαγείτε αργότερα.

**Προαπαιτούμενα:** .NET 6+ (ή οποιοδήποτε πρόσφατο .NET Framework), βασικές γνώσεις C# και ένα IDE της επιλογής σας (Visual Studio, Rider ή VS Code). Αυτό είναι όλο—δεν απαιτούνται επιπλέον πακέτα NuGet.

## Βήμα 1 – Εφαρμογή Στυλ Γραμματοσειράς στο Στοιχείο Σας

Ο πυρήνας κάθε λειτουργίας **εφαρμογής στυλ γραμματοσειράς** είναι ένα enum `FontStyle` συνδυασμένο με ένα αντικείμενο `Font`. Για να διατηρήσουμε τον κώδικα καθαρό, θα τυλίξουμε τη λογική του enum μέσα σε μια μικρή κλάση `WebFontStyle`. Αυτή η κλάση αντικατοπτρίζει τις ιδιότητες που είδατε στο αρχικό απόσπασμα (`Bold`, `Italic`, `Underline`) και δημιουργεί μια τιμή `FontStyle` που μπορείτε να περάσετε στο `Font`.

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**Γιατί αυτό είναι σημαντικό:**  
Απομονώνοντας τη λογική δημιουργίας σημαιών, αποφεύγετε τη διάσπαση των bitwise `|` λειτουργιών σε όλο τον κώδικα UI. Είναι πιο εύκολο στην ανάγνωση, πιο εύκολο στη δοκιμή, και—το πιο σημαντικό—κάνει την πρόθεση **εφαρμογής στυλ γραμματοσειράς** απόλυτα σαφή.

## Βήμα 2 – Αφαίρεση Υπογράμμισης από το Κείμενο (και Διατήρηση των Άλλων Στυλ Ανεπηρέαστα)

Ας υποθέσουμε ότι κληρονομείτε μια ετικέτα που είναι ήδη υπογραμμισμένη, αλλά το σχέδιο απαιτεί απλό έντονο κείμενο. Δεν θέλετε να χάσετε την έντονη γραφή ενώ αφαιρείτε την υπογράμμιση. Εδώ η κλάση `WebFontStyle` δείχνει την αξία της.

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**Κύριο σημείο:** Ορίζοντας `Underline = false` ρητά λέτε στο βοηθό να *εξαιρέσει* τη σημαία υπογράμμισης. Αν παραλείψετε τη γραμμή εντελώς, η προηγούμενη υπογράμμιση θα παραμείνει, κάτι που είναι κοινή πηγή σφαλμάτων όταν οι προγραμματιστές αλλάζουν μόνο την ιδιότητα `Bold`.

## Βήμα 3 – Αλλαγή Στυλ Κειμένου: Έντονο, Πλάγιο και Περισσότερα

Μπορεί να αναρωτιέστε, «Τι γίνεται αν χρειαστεί να εναλλάξω και το πλάγιο;» Το ίδιο αντικείμενο λειτουργεί για οποιονδήποτε συνδυασμό. Παρακάτω υπάρχει ένας γρήγορος πίνακας που μπορείτε να χρησιμοποιήσετε ως αναφορά κατά τον προγραμματισμό.

| Επιθυμητό Στυλ | `Bold` | `Italic` | `Underline` |
|---------------|--------|----------|-------------|
| **Μόνο Έντονο** | true   | false    | false       |
| *Μόνο Πλάγιο* | false  | true     | false       |
| **Έντονο + Πλάγιο** | true   | true     | false       |
| **Έντονο + Underline** | true   | false    | true        |

Απλώς ορίστε τις ιδιότητες που χρειάζεστε και καλέστε το `ToFont`. Ο βοηθός κάνει το σκληρό έργο για εσάς, ώστε να μπορείτε να εστιάσετε στη λογική του UI.

## Πλήρες Παράδειγμα – Ορισμός Έντονου Κειμένου Προγραμματιστικά

Παρακάτω υπάρχει ένα **πλήρες, εκτελέσιμο παράδειγμα WinForms** που δείχνει όλα όσα καλύψαμε. Επικολλήστε το σε ένα νέο έργο WinForms τύπου console και πατήστε **F5**.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, εμφανίζεται ένα παράθυρο με το κείμενο **«Hello, world!»** εμφανιζόμενο **έντονα**, **μη πλάγια**, και **χωρίς καμία υπογράμμιση**. Αυτή η οπτική επιβεβαίωση σας δείχνει ότι η λογική **εφαρμογής στυλ γραμματοσειράς** λειτούργησε άψογα.

## Επαγγελματικές Συμβουλές & Ειδικές Περιπτώσεις

- **Δυναμικές ενημερώσεις:** Αν χρειαστεί να αλλάξετε το στυλ μετά την εμφάνιση της φόρμας (π.χ., ως απάντηση σε ένα checkbox), απλώς δημιουργήστε ξανά το στιγμιότυπο `WebFontStyle` ή τροποποιήστε τις ιδιότητές του και εκχωρήστε ξανά το `lbl.Font`. Το UI ενημερώνεται άμεσα.
- **Σκέψεις για High‑DPI:** Όταν αντικαθιστάτε ένα αντικείμενο `Font`, τα Windows το κλιμακώνουν αυτόματα βάσει του τρέχοντος DPI. Δεν απαιτείται επιπλέον κώδικας εκτός αν διαχειρίζεστε χειροκίνητα την κλιμάκωση.
- **Ισοδύναμο WPF:** Στο WPF θα δεσμεύετε `FontWeight`, `FontStyle` και `TextDecorations` αντί να ανταλλάσσετε ένα αντικείμενο `Font`. Η ίδια λογική διαχωρισμού ισχύει—κρατήστε τη λογική στυλ εκτός του επιπέδου προβολής.
- **Αποφυγή διαρροών μνήμης:** Η επαναανάθεση του `Label.Font` δημιουργεί ένα νέο αντικείμενο `Font`. Αποδεσμεύστε το παλιό αν αλλάζετε στυλ συχνά: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

## Συμπέρασμα

Τώρα ξέρετε πώς να **εφαρμόσετε στυλ γραμματοσειράς** σε οποιοδήποτε στοιχείο .NET, **να αφαιρέσετε την υπογράμμιση από το κείμενο**, και **να αλλάξετε το στυλ κειμένου** εν κινήσει—όλα ενώ διατηρείτε τον κώδικά σας καθαρό και επαναχρησιμοποιήσιμο. Ο μικρός βοηθός `WebFontStyle` μετατρέπει μια σειρά boolean flags σε ένα σταθερό, δοκιμαστικό στοιχείο, και το πλήρες παράδειγμα αποδεικνύει ότι μπορείτε να **ορίσετε έντονο κείμενο προγραμματιστικά** σε λίγες μόνο γραμμές.

Τι ακολουθεί; Δοκιμάστε να συνδυάσετε αυτή την προσέγγιση με ρυθμίσεις που ελέγχονται από τον χρήστη, ή πειραματιστείτε με άλλες σημαίες `FontStyle` όπως `Strikeout`. Μπορείτε ακόμη να εκθέσετε ένα μικρό πάνελ UI που επιτρέπει σε μη‑τεχνικούς χρήστες να επιλέγουν έντονο, πλάγιο ή υπογράμμιση σε χρόνο εκτέλεσης—χωρίς ανάγκη επαναμεταγλώττισης.

Αν βρήκατε αυτό το **μαθήμα μορφοποίησης κειμένου** χρήσιμο, μη διστάσετε να αφήσετε ένα σχόλιο ή να μοιραστείτε τις δικές σας παραλλαγές. Καλή προγραμματιστική, και εύχομαι το UI σας να φαίνεται πάντα ακριβώς όπως το θέλετε!

![Στιγμιότυπο οθόνης που δείχνει πώς να εφαρμόσετε στυλ γραμματοσειράς σε μια ετικέτα σε C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}