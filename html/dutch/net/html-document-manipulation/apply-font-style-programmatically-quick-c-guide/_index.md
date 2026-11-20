---
category: general
date: 2026-04-23
description: Pas lettertype stijl programmatically toe en leer hoe je onderstreping
  van tekst verwijdert, de tekststijl wijzigt en vetgedrukte tekst programmatically
  instelt in een beknopte tutorial.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: nl
og_description: Pas lettertype stijl programmeerbaar toe en ontdek hoe je onderstreping
  uit tekst verwijdert, tekststijl wijzigt en vetgedrukte tekst instelt in een korte,
  praktische tutorial.
og_title: Lettertype stijl via code toepassen – Snelle C#‑gids
tags:
- csharp
- ui
- text-formatting
- programming
title: Lettertype stijl programmatically toepassen – Snelle C#-gids
url: /nl/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lettertype‑stijl programmatically toepassen – Snelle C#‑gids

Heb je ooit **lettertype‑stijl** moeten toepassen op een UI‑element, maar wist je niet waar te beginnen? Je bent niet de enige—de meeste ontwikkelaars lopen tegen dit probleem aan wanneer ze voor het eerst met dynamische tekstopmaak spelen. Het goede nieuws? Over een paar minuten weet je precies hoe je het uiterlijk van een label wijzigt, onderstreping van tekst verwijdert en vetgedrukte tekst programmatically instelt zonder eindeloos door documentatie te zoeken.

In deze **tekst‑opmaak‑tutorial** lopen we een volledig, uitvoerbaar voorbeeld door, leggen we het “waarom” achter elke regel uit, en strooien we praktische tips die je kunt copy‑pasten in elk WinForms‑ of WPF‑project. Geen poespas, alleen de zaken die het werk doen.

---

## Wat je gaat leren

- Hoe je **lettertype‑stijl** toepast met een kleine helper‑klasse.  
- De precieze stappen om **onderstreping van tekst** te **verwijderen** terwijl andere stijlen behouden blijven.  
- Manieren om **tekststijl** (vet, cursief, onderstrepen) on‑the‑fly te wijzigen.  
- Een volledige, copy‑ready snippet die **vetgedrukte tekst programmatically** instelt.  
- Veelvoorkomende valkuilen en edge‑case‑afhandeling zodat je later niet voor verrassingen komt te staan.

**Prerequisites:** .NET 6+ (of een recente .NET Framework), basiskennis van C#, en een IDE naar keuze (Visual Studio, Rider, of VS Code). Dat is alles—geen extra NuGet‑pakketten nodig.

---

## Stap 1 – Lettertype‑stijl toepassen op je controle

De kern van elke **apply font style**‑operatie is een `FontStyle`‑enum gecombineerd met een `Font`‑object. Om de code overzichtelijk te houden, wikkelen we de enum‑logica in een kleine `WebFontStyle`‑klasse. Deze klasse spiegelt de eigenschappen die je in het oorspronkelijke fragment zag (`Bold`, `Italic`, `Underline`) en bouwt een `FontStyle`‑waarde die je aan `Font` kunt doorgeven.

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

**Waarom dit belangrijk is:**  
Door de flag‑bouwlogica te isoleren, vermijd je dat je bitwise `|`‑operaties door je UI‑code verspreidt. Het is makkelijker leesbaar, makkelijker te testen, en—het belangrijkste—maakt de **apply font style**‑intentie glashelder.

---

## Stap 2 – Onderstreping van tekst verwijderen (en andere stijlen behouden)

Stel, je hebt een label geërfd dat al onderstreept is, maar het ontwerp vraagt om gewone vetgedrukte tekst. Je wilt de vetgedruktheid niet verliezen terwijl je de onderstreping verwijdert. Hier komt de `WebFontStyle`‑klasse van pas.

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

**Kernpunt:** Het expliciet instellen van `Underline = false` vertelt de helper om de onderstrepings‑flag *uit te sluiten*. Als je die regel weglaten, blijft de eerdere onderstreping bestaan, wat een veelvoorkomende bron van bugs is wanneer ontwikkelaars alleen de `Bold`‑eigenschap toggelen.

---

## Stap 3 – Tekststijl wijzigen: Vet, Cursief en meer

Je vraagt je misschien af: “Wat als ik ook cursief moet toggelen?” Hetzelfde object werkt voor elke combinatie. Hieronder vind je een snel overzicht dat je kunt raadplegen tijdens het coderen.

| Gewenste stijl | `Bold` | `Italic` | `Underline` |
|----------------|--------|----------|-------------|
| **Alleen vet** | true   | false    | false       |
| *Alleen cursief* | false  | true     | false       |
| **Vet + Cursief** | true   | true     | false       |
| **Vet + Onderstrepen** | true   | false    | true        |

Stel simpelweg de eigenschappen in die je nodig hebt en roep `ToFont` aan. De helper doet het zware werk voor je, zodat jij je kunt concentreren op de UI‑logica.

---

## Volledig voorbeeld – Vetgedrukte tekst programmatically instellen

Hieronder staat een **volledig, uitvoerbaar WinForms**‑voorbeeld dat alles laat zien wat we hebben behandeld. Plak het in een nieuw console‑style WinForms‑project en druk op **F5**.

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

### Verwacht resultaat

Wanneer je het programma uitvoert, verschijnt er een venster met de tekst **“Hello, world!”** weergegeven **vet**, **niet cursief**, en **zonder onderstreping**. Die visuele bevestiging laat zien dat de **apply font style**‑logica perfect heeft gewerkt.

---

## Pro‑tips & Edge Cases

- **Dynamische updates:** Als je de stijl moet wijzigen nadat het formulier is weergegeven (bijv. als reactie op een checkbox), maak dan gewoon een nieuwe `WebFontStyle`‑instantie of wijzig de eigenschappen en wijs `lbl.Font` opnieuw toe. De UI werkt direct bij.
- **High‑DPI‑overwegingen:** Wanneer je een `Font`‑object vervangt, schaalt Windows dit automatisch op basis van de huidige DPI. Geen extra code nodig tenzij je handmatig schaalbeheer doet.
- **WPF‑equivalent:** In WPF bind je `FontWeight`, `FontStyle` en `TextDecorations` in plaats van een `Font`‑object te verwisselen. Hetzelfde logische scheidingsprincipe geldt—houd stijl‑logica buiten de view‑laag.
- **Voorkomen van geheugenlekken:** Het opnieuw toewijzen van `Label.Font` maakt een nieuw `Font`‑object aan. Dispose het oude object als je vaak stijlen verwisselt: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Conclusie

Je weet nu hoe je **lettertype‑stijl** toepast op elk .NET‑control, **onderstreping van tekst** verwijdert, en **tekststijl** on‑the‑fly wijzigt—en dat alles terwijl je code schoon en herbruikbaar blijft. De kleine `WebFontStyle`‑helper zet een handvol booleaanse vlaggen om in een solide, testbaar component, en het volledige voorbeeld bewijst dat je **vetgedrukte tekst programmatically** kunt instellen in slechts een paar regels.

Wat nu? Probeer deze aanpak te combineren met door de gebruiker gedreven instellingen, of experimenteer met andere `FontStyle`‑flags zoals `Strikeout`. Je kunt zelfs een klein UI‑paneel exposen waarmee niet‑technische gebruikers vet, cursief of onderstrepen kunnen kiezen tijdens runtime—zonder opnieuw te compileren.

Als je deze **tekst‑opmaak‑tutorial** nuttig vond, laat dan een reactie achter of deel je eigen variaties. Happy coding, en moge je UI er altijd precies uitzien zoals jij het wilt! 

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}