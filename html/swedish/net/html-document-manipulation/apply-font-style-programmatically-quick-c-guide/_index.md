---
category: general
date: 2026-04-23
description: Applicera teckensnittsstil programatiskt och lär dig hur du tar bort
  understrykning från text, ändrar textstil och sätter fet text programatiskt i en
  kortfattad handledning.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: sv
og_description: Applicera teckensnittsstil programatiskt och upptäck hur du tar bort
  understrykning från text, ändrar textstil och sätter fet text programatiskt i en
  kort, praktisk handledning.
og_title: Applicera teckensnittsstil programatiskt – Snabb C#‑guide
tags:
- csharp
- ui
- text-formatting
- programming
title: Applicera teckensnittsstil programatiskt – Snabb C#-guide
url: /sv/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicera teckensnittsstil programatiskt – Snabb C#‑guide

Har du någonsin behövt **apply font style** på ett UI‑element men varit osäker på var du ska börja? Du är inte ensam – de flesta utvecklare stöter på detta problem när de först börjar leka med dynamisk textformatering. Den goda nyheten? På bara några minuter vet du exakt hur du ändrar en etikettens utseende, tar bort understrykning från text och sätter fet text programatiskt utan att leta igenom oändliga dokument.

I den här **text formatting tutorial** går vi igenom ett komplett, körbart exempel, förklarar “varför” bakom varje rad och strör in praktiska tips som du kan copy‑paste in i vilket WinForms‑ eller WPF‑projekt som helst. Ingen fluff, bara det som får jobbet gjort.

---

## Vad du kommer att lära dig

- Hur du **apply font style** med en liten hjälparklass.  
- De exakta stegen för att **remove underline from text** samtidigt som du behåller andra stilar intakta.  
- Sätt att **change text style** (bold, italic, underline) i farten.  
- Ett komplett, kopieringsklart kodsnutt som **sets bold text programmatically**.  
- Vanliga fallgropar och hantering av edge‑cases så att du inte blir överraskad senare.

**Förutsättningar:** .NET 6+ (eller någon recent .NET Framework), grundläggande C#‑kunskaper och en IDE du föredrar (Visual Studio, Rider eller VS Code). Det är allt – inga extra NuGet‑paket behövs.

## Steg 1 – Applicera teckensnittsstil på din kontroll

Kärnan i varje **apply font style**‑operation är en `FontStyle`‑enum kombinerad med ett `Font`‑objekt. För att hålla koden snygg omsluter vi enum‑logiken i en liten `WebFontStyle`‑klass. Denna klass speglar egenskaperna du såg i det ursprungliga kodsnutten (`Bold`, `Italic`, `Underline`) och bygger ett `FontStyle`‑värde som du kan skicka till `Font`.

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

**Varför detta är viktigt:**  
Genom att isolera flagg‑bygglogiken undviker du att sprida bitvisa `|`‑operationer över hela din UI‑kod. Det blir lättare att läsa, lättare att testa och – viktigast av allt – gör avsikten **apply font style** kristallklar.

## Steg 2 – Ta bort understrykning från text (och behåll andra stilar intakta)

Anta att du har ärvt en etikett som redan är understruken, men designen kräver ren fet text. Du vill inte förlora fetstil när du tar bort understrykningen. Här kommer `WebFontStyle`‑klassen till sin rätt.

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

**Viktigt:** Genom att sätta `Underline = false` explicit talar du om för hjälpen att *exkludera* understrykning‑flaggan. Om du utelämnar raden helt skulle den tidigare understrykningen bestå, vilket är en vanlig felkälla när utvecklare bara växlar `Bold`‑egenskapen.

## Steg 3 – Ändra textstil: Fet, Kursiv och mer

Du kanske undrar, “Vad händer om jag också behöver växla kursiv?” Samma objekt fungerar för alla kombinationer. Nedan är en snabb matris du kan referera till medan du kodar.

| Önskad stil | `Bold` | `Italic` | `Underline` |
|-------------|--------|----------|-------------|
| **Endast fet** | true   | false    | false       |
| *Endast kursiv* | false  | true     | false       |
| **Fet + Kursiv** | true   | true     | false       |
| **Fet + Understreck** | true   | false    | true        |

Ställ bara in de egenskaper du behöver och anropa `ToFont`. Hjälpen gör det tunga lyftet åt dig, så att du kan fokusera på UI‑logiken.

## Fullt exempel – Sätt fet text programatiskt

Nedan är ett **komplett, körbart WinForms**‑exempel som demonstrerar allt vi gått igenom. Klistra in det i ett nytt konsol‑stil WinForms‑projekt och tryck **F5**.

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

### Förväntat resultat

När du kör programmet visas ett fönster med texten **“Hello, world!”** renderad **fet**, **inte kursiv**, och **utan någon understrykning**. Den visuella bekräftelsen visar att **apply font style**‑logiken fungerade perfekt.

## Pro‑tips & edge‑cases

- **Dynamiska uppdateringar:** Om du behöver ändra stilen efter att formuläret visats (t.ex. som svar på en kryssruta), skapa bara om `WebFontStyle`‑instansen eller ändra dess egenskaper och återtilldela `lbl.Font`. UI‑et uppdateras omedelbart.
- **High‑DPI‑överväganden:** När du ersätter ett `Font`‑objekt skalar Windows det automatiskt baserat på aktuell DPI. Ingen extra kod behövs såvida du inte hanterar skalning manuellt.
- **WPF‑motsvarighet:** I WPF skulle du binda `FontWeight`, `FontStyle` och `TextDecorations` istället för att byta ett `Font`‑objekt. Samma logiska separation gäller – håll stil‑logiken utanför visningslagret.
- **Undvika minnesläckor:** Att återtilldela `Label.Font` skapar ett nytt `Font`‑objekt. Disposera det gamla om du byter stilar ofta: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

## Slutsats

Du vet nu hur du **apply font style** på vilken .NET‑kontroll som helst, **remove underline from text**, och **change text style** i farten – allt medan du håller din kod ren och återanvändbar. Den lilla `WebFontStyle`‑hjälpen förvandlar ett fåtal boolska flaggor till en solid, testbar komponent, och det fullständiga exemplet visar att du kan **set bold text programmatically** på bara några rader.

Vad blir nästa steg? Prova att kombinera detta tillvägagångssätt med användarstyrda inställningar, eller experimentera med andra `FontStyle`‑flaggor som `Strikeout`. Du kan till och med exponera en liten UI‑panel som låter icke‑tekniska användare välja fet, kursiv eller understrykning vid körning – ingen omkompilering krävs.

Om du fann denna **text formatting tutorial** hjälpsam, tveka inte att lämna en kommentar eller dela dina egna varianter. Lycklig kodning, och må ditt UI alltid se exakt ut som du tänkt!

---

![Skärmdump som visar hur man applicerar teckensnittsstil på en etikett i C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}