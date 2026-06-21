---
category: general
date: 2026-04-23
description: फ़ॉन्ट शैली को प्रोग्रामेटिकली लागू करें और संक्षिप्त ट्यूटोरियल में
  टेक्स्ट से अंडरलाइन हटाना, टेक्स्ट शैली बदलना, और प्रोग्रामेटिकली बोल्ड टेक्स्ट
  सेट करना सीखें।
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: hi
og_description: फ़ॉन्ट शैली को प्रोग्रामेटिकली लागू करें और जानें कि टेक्स्ट से अंडरलाइन
  कैसे हटाएँ, टेक्स्ट शैली बदलें, और प्रोग्रामेटिकली बोल्ड टेक्स्ट कैसे सेट करें,
  एक संक्षिप्त, व्यावहारिक ट्यूटोरियल में।
og_title: फ़ॉन्ट शैली को प्रोग्रामेटिक रूप से लागू करें – त्वरित C# गाइड
tags:
- csharp
- ui
- text-formatting
- programming
title: फ़ॉन्ट शैली को प्रोग्रामेटिकली लागू करें – त्वरित C# गाइड
url: /hi/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# प्रोग्रामेटिकली फ़ॉन्ट स्टाइल लागू करें – त्वरित C# गाइड

क्या आपको कभी **फ़ॉन्ट स्टाइल लागू** करने की ज़रूरत पड़ी लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स को पहली बार डायनामिक टेक्स्ट फ़ॉर्मेटिंग करते समय यही समस्या आती है। अच्छी खबर? कुछ ही मिनटों में आप जान जाएंगे कि लेबल की उपस्थिति कैसे बदलें, टेक्स्ट से अंडरलाइन कैसे हटाएँ, और बॉल्ड टेक्स्ट प्रोग्रामेटिकली कैसे सेट करें बिना अनगिनत डॉक्यूमेंट्स के बीच खोजे।

इस **टेक्स्ट फ़ॉर्मेटिंग ट्यूटोरियल** में हम एक पूर्ण, चलने योग्य उदाहरण पर चलते हैं, प्रत्येक लाइन के “क्यों” को समझाते हैं, और व्यावहारिक टिप्स देते हैं जिन्हें आप किसी भी WinForms या WPF प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। कोई फ़ज़ नहीं, सिर्फ वही चीज़ें जो काम करती हैं।

---

## आप क्या सीखेंगे

- एक छोटे हेल्पर क्लास का उपयोग करके **फ़ॉन्ट स्टाइल लागू** करना।  
- **टेक्स्ट से अंडरलाइन हटाने** के सटीक कदम, जबकि अन्य स्टाइल्स बरकरार रहें।  
- रन‑टाइम पर **टेक्स्ट स्टाइल बदलने** (बोल्ड, इटैलिक, अंडरलाइन) के तरीके।  
- एक पूर्ण, कॉपी‑रेडी स्निपेट जो **प्रोग्रामेटिकली बॉल्ड टेक्स्ट सेट** करता है।  
- सामान्य पिटफ़ॉल्स और एज‑केस हैंडलिंग ताकि बाद में आश्चर्य न हो।

**पूर्वापेक्षाएँ:** .NET 6+ (या कोई भी हालिया .NET Framework), बुनियादी C# ज्ञान, और आपका पसंदीदा IDE (Visual Studio, Rider, या VS Code)। बस इतना ही—कोई अतिरिक्त NuGet पैकेज नहीं चाहिए।

---

## चरण 1 – अपने कंट्रोल पर फ़ॉन्ट स्टाइल लागू करें

किसी भी **फ़ॉन्ट स्टाइल लागू** ऑपरेशन का मूल `FontStyle` एनेम और `Font` ऑब्जेक्ट का संयोजन है। कोड को साफ़ रखने के लिए हम एनेम लॉजिक को एक छोटे `WebFontStyle` क्लास में रैप करेंगे। यह क्लास उन प्रॉपर्टीज़ को दर्शाता है जो आपने मूल स्निपेट में देखी थीं (`Bold`, `Italic`, `Underline`) और एक `FontStyle` वैल्यू बनाता है जिसे आप `Font` को पास कर सकते हैं।

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

**यह क्यों महत्वपूर्ण है:**  
फ़्लैग‑बिल्डिंग लॉजिक को अलग करके, आप बिटवाइज़ `|` ऑपरेशन्स को अपने UI कोड में बिखरने से बचते हैं। पढ़ने में आसान, टेस्ट करने में आसान, और—सबसे महत्वपूर्ण—**फ़ॉन्ट स्टाइल लागू** इरादा स्पष्ट बनाता है।

---

## चरण 2 – टेक्स्ट से अंडरलाइन हटाएँ (और अन्य स्टाइल्स बरकरार रखें)

मान लीजिए आपके पास एक लेबल है जो पहले से अंडरलाइन है, लेकिन डिज़ाइन में साधारण बॉल्ड टेक्स्ट चाहिए। आप बॉल्डनेस खोए बिना अंडरलाइन हटाना चाहते हैं। यहाँ `WebFontStyle` क्लास काम आती है।

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

**मुख्य बिंदु:** `Underline = false` सेट करने से हेल्पर को *अंडरलाइन फ़्लैग को बाहर* करने को स्पष्ट रूप से बताया जाता है। यदि आप यह लाइन पूरी तरह छोड़ दें तो पिछली अंडरलाइन बनी रहेगी, जो अक्सर तब बग बन जाता है जब डेवलपर्स केवल `Bold` प्रॉपर्टी टॉगल करते हैं।

---

## चरण 3 – टेक्स्ट स्टाइल बदलें: बॉल्ड, इटैलिक, और अधिक

आप सोच सकते हैं, “अगर मुझे इटैलिक भी टॉगल करना हो तो?” वही ऑब्जेक्ट किसी भी संयोजन के लिए काम करता है। नीचे एक त्वरित मैट्रिक्स है जिसे आप कोडिंग के दौरान रेफ़रेंस कर सकते हैं।

| इच्छित स्टाइल | `Bold` | `Italic` | `Underline` |
|---------------|--------|----------|-------------|
| **केवल बॉल्ड** | true   | false    | false       |
| *केवल इटैलिक* | false  | true     | false       |
| **बॉल्ड + इटैलिक** | true   | true     | false       |
| **बॉल्ड + अंडरलाइन** | true   | false    | true        |

सिर्फ वह प्रॉपर्टीज़ सेट करें जिनकी आपको ज़रूरत है और `ToFont` को कॉल करें। हेल्पर आपके लिए भारी काम कर लेगा, ताकि आप UI लॉजिक पर ध्यान दे सकें।

---

## पूर्ण उदाहरण – प्रोग्रामेटिकली बॉल्ड टेक्स्ट सेट करें

नीचे एक **पूर्ण, चलने योग्य WinForms** उदाहरण है जो हमने अब तक कवर किया है। इसे एक नए कंसोल‑स्टाइल WinForms प्रोजेक्ट में पेस्ट करें और **F5** दबाएँ।

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

### अपेक्षित परिणाम

जब आप प्रोग्राम चलाएँगे, एक विंडो खुलेगी जिसमें टेक्स्ट **“Hello, world!”** **बॉल्ड**, **इटैलिक नहीं**, और **बिना किसी अंडरलाइन** के दिखेगा। यह विज़ुअल कन्फर्मेशन बताता है कि **फ़ॉन्ट स्टाइल लागू** लॉजिक पूरी तरह काम कर रहा है।

---

## प्रो टिप्स एवं एज केस

- **डायनामिक अपडेट:** यदि आपको फॉर्म दिखाने के बाद स्टाइल बदलनी हो (जैसे चेकबॉक्स के जवाब में), बस `WebFontStyle` इंस्टेंस को फिर से बनाएँ या उसकी प्रॉपर्टीज़ बदलें और `lbl.Font` को पुनः असाइन करें। UI तुरंत अपडेट हो जाएगा।  
- **हाई‑DPI विचार:** जब आप `Font` ऑब्जेक्ट बदलते हैं, विंडोज़ स्वचालित रूप से वर्तमान DPI के आधार पर स्केल करता है। अतिरिक्त कोड की ज़रूरत नहीं जब तक आप मैन्युअली स्केलिंग नहीं संभाल रहे हों।  
- **WPF समकक्ष:** WPF में आप `FontWeight`, `FontStyle`, और `TextDecorations` को बाइंड करेंगे, न कि `Font` ऑब्जेक्ट को स्वैप करेंगे। वही लॉजिकल विभाजन लागू होता है—स्टाइल लॉजिक को व्यू लेयर से बाहर रखें।  
- **मेमोरी लीक्स से बचें:** `Label.Font` को पुनः असाइन करने से नया `Font` ऑब्जेक्ट बनता है। यदि आप बार‑बार स्टाइल बदल रहे हैं तो पुराने को डिस्पोज़ करें: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## निष्कर्ष

अब आप किसी भी .NET कंट्रोल पर **फ़ॉन्ट स्टाइल लागू**, **टेक्स्ट से अंडरलाइन हटाने**, और **रन‑टाइम पर टेक्स्ट स्टाइल बदलने** के तरीके जानते हैं—और वह भी कोड को साफ़ और पुन: उपयोग योग्य रखते हुए। छोटा `WebFontStyle` हेल्पर कुछ बूलियन फ़्लैग्स को एक ठोस, टेस्टेबल कंपोनेंट में बदल देता है, और पूर्ण उदाहरण सिद्ध करता है कि आप केवल कुछ लाइनों में **प्रोग्रामेटिकली बॉल्ड टेक्स्ट सेट** कर सकते हैं।

अब क्या? इस एप्रोच को यूज़र‑ड्रिवन सेटिंग्स के साथ मिलाएँ, या अन्य `FontStyle` फ़्लैग्स जैसे `Strikeout` के साथ प्रयोग करें। आप एक छोटा UI पैनल भी बना सकते हैं जो नॉन‑टेक्निकल यूज़र्स को रन‑टाइम पर बॉल्ड, इटैलिक, या अंडरलाइन चुनने की अनुमति देता है—बिना री‑कम्पाइल के।

यदि आपको यह **टेक्स्ट फ़ॉर्मेटिंग ट्यूटोरियल** उपयोगी लगा, तो टिप्पणी छोड़ें या अपनी खुद की वैरिएशन शेयर करें। कोडिंग का आनंद लें, और आपका UI हमेशा वही दिखे जैसा आप चाहते हैं!

---

![फ़ॉन्ट स्टाइल को लेबल पर लागू करने का स्क्रीनशॉट C# में](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}