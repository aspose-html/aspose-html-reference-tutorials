---
category: general
date: 2026-04-23
description: Applica lo stile del carattere programmaticamente e scopri come rimuovere
  la sottolineatura dal testo, modificare lo stile del testo e impostare il testo
  in grassetto programmaticamente in un tutorial conciso.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: it
og_description: Applica lo stile del carattere programmaticamente e scopri come rimuovere
  la sottolineatura dal testo, cambiare lo stile del testo e impostare il testo in
  grassetto programmaticamente in un breve tutorial pratico.
og_title: Applica lo stile del font programmaticamente – Guida rapida C#
tags:
- csharp
- ui
- text-formatting
- programming
title: Applicare lo stile del carattere programmaticamente – Guida rapida C#
url: /it/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applica lo stile del font programmaticamente – Guida rapida C#

Ti è mai capitato di dover **applicare lo stile del font** a un elemento UI ma non sapevi da dove cominciare? Non sei l'unico—la maggior parte degli sviluppatori incappa in questo ostacolo quando si avvicina per la prima volta alla formattazione dinamica del testo. La buona notizia? In pochi minuti saprai esattamente come modificare l'aspetto di un'etichetta, rimuovere la sottolineatura dal testo e impostare il testo in grassetto programmaticamente senza dover cercare tra infinite documentazioni.

In questo **tutorial di formattazione del testo** ti guideremo attraverso un esempio completo e eseguibile, spiegheremo il “perché” dietro ogni riga e inseriremo consigli pratici che potrai copiare‑incollare in qualsiasi progetto WinForms o WPF. Niente fronzoli, solo ciò che serve a portare a termine il lavoro.

---

## Cosa Imparerai

- Come **applicare lo stile del font** usando una piccola classe helper.  
- I passaggi precisi per **rimuovere la sottolineatura dal testo** mantenendo intatti gli altri stili.  
- Modi per **cambiare lo stile del testo** (grassetto, corsivo, sottolineato) al volo.  
- Uno snippet completo, pronto per il copia‑incolla, che **imposta il testo in grassetto programmaticamente**.  
- Trappole comuni e gestione dei casi limite così non sarai sorpreso in seguito.

**Prerequisiti:** .NET 6+ (o qualsiasi versione recente del .NET Framework), conoscenza base di C# e un IDE a tua scelta (Visual Studio, Rider o VS Code). Tutto qui—non sono necessari pacchetti NuGet aggiuntivi.

---

## Passo 1 – Applica lo Stile del Font al Tuo Controllo

Il nucleo di qualsiasi operazione di **applicare lo stile del font** è un enum `FontStyle` combinato con un oggetto `Font`. Per mantenere il codice ordinato avvolgeremo la logica dell'enum all'interno di una piccola classe `WebFontStyle`. Questa classe rispecchia le proprietà viste nello snippet originale (`Bold`, `Italic`, `Underline`) e costruisce un valore `FontStyle` che puoi passare a `Font`.

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

**Perché è importante:**  
Isolando la logica di costruzione dei flag, eviti di spargere operazioni bitwise `|` in tutto il codice UI. È più leggibile, più facile da testare e—soprattutto—rende l'intento di **applicare lo stile del font** cristallino.

---

## Passo 2 – Rimuovi la Sottolineatura dal Testo (e Mantieni Intatti gli Altri Stili)

Supponi di aver ereditato un'etichetta già sottolineata, ma il design richiede un semplice testo in grassetto. Non vuoi perdere il grassetto mentre rimuovi la sottolineatura. È qui che la classe `WebFontStyle` brilla.

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

**Punto chiave:** Impostare `Underline = false` indica esplicitamente all'helper di *escludere* il flag della sottolineatura. Se ometti la riga del tutto, la sottolineatura precedente persisterà, il che è una fonte comune di bug quando gli sviluppatori attivano solo la proprietà `Bold`.

---

## Passo 3 – Cambia lo Stile del Testo: Grassetto, Corsivo e Altro

Potresti chiederti, “E se avessi bisogno di attivare anche il corsivo?” Lo stesso oggetto funziona per qualsiasi combinazione. Di seguito trovi una rapida matrice di riferimento durante la codifica.

| Stile desiderato | `Bold` | `Italic` | `Underline` |
|------------------|--------|----------|-------------|
| **Solo grassetto** | true   | false    | false       |
| *Solo corsivo* | false  | true     | false       |
| **Grassetto + Corsivo** | true   | true     | false       |
| **Grassetto + Sottolineato** | true   | false    | true        |

Imposta semplicemente le proprietà di cui hai bisogno e chiama `ToFont`. L'helper fa il lavoro pesante per te, così puoi concentrarti sulla logica UI.

---

## Esempio Completo – Imposta il Testo in Grassetto Programmaticamente

Di seguito trovi un esempio **completo e eseguibile WinForms** che dimostra tutto ciò che abbiamo trattato. Incollalo in un nuovo progetto WinForms in stile console e premi **F5**.

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

### Risultato Atteso

Quando esegui il programma, appare una finestra con il testo **“Hello, world!”** visualizzato **in grassetto**, **non in corsivo**, e **senza alcuna sottolineatura**. Questa conferma visiva ti indica che la logica di **applicare lo stile del font** ha funzionato perfettamente.

---

## Consigli Pro & Casi Limite

- **Aggiornamenti dinamici:** Se devi cambiare lo stile dopo che il form è stato mostrato (ad esempio in risposta a una checkbox), ricrea l'istanza `WebFontStyle` o modifica le sue proprietà e riassegna `lbl.Font`. L'interfaccia si aggiorna istantaneamente.
- **Considerazioni High‑DPI:** Quando sostituisci un oggetto `Font`, Windows lo scala automaticamente in base al DPI corrente. Nessun codice aggiuntivo necessario a meno che tu non gestisca manualmente lo scaling.
- **Equivalente WPF:** In WPF collegheresti `FontWeight`, `FontStyle` e `TextDecorations` invece di scambiare un oggetto `Font`. La stessa separazione logica si applica—mantieni la logica di stile fuori dal layer di visualizzazione.
- **Evitare perdite di memoria:** Riassegnare `Label.Font` crea un nuovo oggetto `Font`. Disporre quello vecchio se scambi gli stili frequentemente: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Conclusione

Ora sai come **applicare lo stile del font** a qualsiasi controllo .NET, **rimuovere la sottolineatura dal testo** e **cambiare lo stile del testo** al volo—tutto mantenendo il tuo codice pulito e riutilizzabile. Il piccolo helper `WebFontStyle` trasforma una manciata di flag booleani in un componente solido e testabile, e l'esempio completo dimostra che puoi **impostare il testo in grassetto programmaticamente** in poche righe.

Cosa fare dopo? Prova a combinare questo approccio con impostazioni guidate dall'utente, o sperimenta altri flag `FontStyle` come `Strikeout`. Potresti anche esporre un piccolo pannello UI che permette agli utenti non tecnici di scegliere grassetto, corsivo o sottolineatura a runtime—senza necessità di ricompilare.

Se hai trovato utile questo **tutorial di formattazione del testo**, sentiti libero di lasciare un commento o condividere le tue varianti. Buona programmazione, e che la tua UI abbia sempre l'aspetto esattamente come lo desideri! 

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}