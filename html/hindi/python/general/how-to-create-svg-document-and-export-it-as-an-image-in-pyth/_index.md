---
category: general
date: 2026-10-02
description: Python में SVG दस्तावेज़ बनाना, SVG को फ़ाइल में सहेजना, और एक छोटा,
  पूर्ण स्क्रिप्ट के साथ SVG छवि निर्यात करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: hi
lastmod: 2026-10-02
og_description: Python में SVG दस्तावेज़ बनाएं और इस व्यावहारिक ट्यूटोरियल के साथ
  SVG छवि निर्यात करें। स्क्रिप्ट का पालन करें, SVG को फ़ाइल में सहेजें, और वेक्टर
  ग्राफ़िक को तुरंत पुनः उपयोग करें।
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Python में SVG दस्तावेज़ बनाएं – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Python में SVG दस्तावेज़ कैसे बनाएं और इसे छवि के रूप में निर्यात करें
url: /hi/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में SVG दस्तावेज़ बनाना और उसे इमेज के रूप में एक्सपोर्ट करना

यदि आपको प्रोग्रामेटिक रूप से **SVG दस्तावेज़ बनाना** है, तो यह ट्यूटोरियल आपको Python के साथ इसे कैसे करना है, दिखाता है। आप एक पूर्ण स्क्रिप्ट देखेंगे जो एक साधारण सर्कल बनाता है, SVG को फ़ाइल में सहेजता है, और एक एक्सपोर्टेबल SVG इमेज उत्पन्न करता है जिसे आप कहीं भी एम्बेड कर सकते हैं।

कोड से स्केलेबल वेक्टर ग्राफ़िक्स जेनरेट करने से GUI एडिटर में मैन्युअल रूप से शैप ड्रॉ करने की मेहनत बचती है। इस गाइड के अंत तक आप SVG निर्माण को डेटा‑विज़ुअलाइज़ेशन पाइपलाइन, ऑटोमेटेड रिपोर्ट जेनरेटर, या किसी भी प्रोजेक्ट में इंटीग्रेट कर सकते हैं जिसे स्पष्ट, रिज़ॉल्यूशन‑इंडिपेंडेंट ग्राफ़िक्स चाहिए।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Python 3.8 या नया संस्करण स्थापित हो
- `svgwrite` लाइब्रेरी (इंस्टॉल करने के लिए `pip install svgwrite` चलाएँ)
- वह डायरेक्टरी जहाँ SVG सहेजा जाएगा, उसमें लिखने की अनुमति

इन आवश्यकताओं से उदाहरण हल्का और अधिकांश वातावरण के साथ संगत रहता है।

## चरण 1: SVG लाइब्रेरी इंस्टॉल और इम्पोर्ट करें

पहला कदम है थर्ड‑पार्टी लाइब्रेरी जोड़ना जो SVG निर्माण के लिए सुविधाजनक API प्रदान करती है।

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` SVG फ़ाइल की XML संरचना को एब्स्ट्रैक्ट करता है, जिससे आप कच्चे मार्कअप की बजाय ज्योमेट्री पर ध्यान केंद्रित कर सकते हैं।

## चरण 2: SVG दस्तावेज़ ऑब्जेक्ट बनाएं

अब आप `svgwrite.Drawing` को इंस्टैंशिएट करके **SVG दस्तावेज़ बनाना** शुरू कर सकते हैं। यह ऑब्जेक्ट रूट `<svg>` एलिमेंट का प्रतिनिधित्व करता है और सभी बाद के शैप्स को रखता है।

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` आर्ग्यूमेंट रेंडर किए गए पिक्सेल आयाम निर्धारित करता है, जबकि `viewBox` एक कोऑर्डिनेट सिस्टम स्थापित करता है जो बाद में आप परिभाषित करेंगे वाली ज्योमेट्री से मेल खाता है।

## चरण 3: सर्कल एलिमेंट जोड़ें

एक सर्कल उसके केंद्र (`cx`, `cy`) और त्रिज्या (`r`) द्वारा परिभाषित होता है। इन एट्रिब्यूट्स को अटैच करने के लिए `circle` हेल्पर का उपयोग करें।

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

सर्कल 100 × 100 कैनवास के मध्य में स्थित है, प्रत्येक पक्ष पर 10‑पिक्सेल मार्जिन छोड़ते हुए। अपने डिज़ाइन भाषा के अनुसार `fill` और `stroke` को समायोजित करें।

## चरण 4: SVG को फ़ाइल में सहेजें

ग्राफ़िक तैयार होने के बाद, आप `save` मेथड का उपयोग करके **SVG को फ़ाइल में सहेजें** सकते हैं। यह एक वैध XML लिखता है जिसे ब्राउज़र और वेक्टर एडिटर समझते हैं।

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

फ़ाइल `circle.svg` अब वर्तमान कार्यशील डायरेक्टरी में मौजूद है। आप इसे वेब ब्राउज़र, Inkscape, या किसी भी टूल में खोल सकते हैं जो SVG फ़ॉर्मेट को सपोर्ट करता है।

## चरण 5: एक्सपोर्टेड SVG इमेज की जाँच करें

सहेजी गई फ़ाइल को ब्राउज़र में खोलें और आउटपुट की पुष्टि करें। आपको निर्दिष्ट रंगों के साथ केंद्रित सर्कल दिखना चाहिए। कच्चा XML इस प्रकार दिखता है:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

क्योंकि SVG वेक्टर‑आधारित है, आप इमेज को गुणवत्ता खोए बिना स्केल कर सकते हैं, जो रिस्पॉन्सिव वेब डिज़ाइन्स या हाई‑रेज़ॉल्यूशन प्रिंट के लिए आदर्श है।

## प्रो टिप: SVG को PNG या JPEG में एक्सपोर्ट करें

यदि आपको रास्टर संस्करण चाहिए, तो SVG फ़ाइल को **CairoSVG** जैसे कन्वर्ज़न टूल के साथ मिलाएँ:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

यह चरण **SVG इमेज को एक्सपोर्ट** करके बिटमैप फ़ॉर्मेट में बदलता है, जो तब उपयोगी होता है जब डाउनस्ट्रीम सिस्टम सीधे SVG रेंडर नहीं कर पाते।

## सामान्य वैरिएशन्स और एज केस

| वैरिएशन | कैसे संभालें |
|-----------|---------------|
| कई शैप्स | प्रत्येक नए एलिमेंट (rect, line, path) के लिए `dwg.add()` कॉल करें। |
| डायनामिक डाइमेंशन्स | `Drawing` बनाने से पहले डेटा से `size` और `viewBox` की गणना करें। |
| टेक्स्ट लेबल्स | `dwg.text("Label", insert=("10", "20"))` का उपयोग करें और `font_size` तथा `fill` से स्टाइल करें। |
| दस्तावेज़ का पुनः उपयोग | `Drawing` ऑब्जेक्ट को मेमोरी में रखें और जब भी अपडेटेड फ़ाइल चाहिए, `save()` कॉल करें। |
| बड़ी फ़ाइलें | आउटपुट को `dwg.tostring()` से स्ट्रीम करें और मेमोरी स्पाइक से बचने के लिए मैन्युअली फ़ाइल ऑब्जेक्ट में लिखें। |

इन परिदृश्यों को संभालने से आपका **SVG जेनरेट करने का** स्क्रिप्ट साधारण आइकन्स से लेकर जटिल डायग्राम तक स्केल हो जाता है।

## पूर्ण स्क्रिप्ट पुनरावलोकन

नीचे वह पूर्ण, चलाने योग्य उदाहरण है जिसमें सभी चरण और वैकल्पिक कन्वर्ज़न शामिल हैं:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

इस स्क्रिप्ट को चलाने पर `circle.svg` और, यदि `cairosvg` स्थापित है, तो `circle.png` बनेंगे। दोनों फ़ाइलें वेब पेज, रिपोर्ट, या आगे की प्रोसेसिंग के लिए तैयार हैं।

## निष्कर्ष

अब आप जानते हैं कि Python में **SVG दस्तावेज़ बनाना**, **SVG को फ़ाइल में सहेजना**, और **SVG इमेज को एक्सपोर्ट करना** कैसे है। उदाहरण ने आवश्यक API कॉल्स को कवर किया, प्रत्येक चरण के महत्व को समझाया, और अधिक जटिल ग्राफ़िक्स के लिए विस्तार प्रदान किए। 

आगे, अतिरिक्त **SVG Python ट्यूटोरियल** विषयों जैसे पाथ ड्रॉइंग, ग्रेडिएंट्स लागू करना, और एनीमेशन पर खोज करें। इन तकनीकों को इंटीग्रेट करने से आप अपने Python एप्लिकेशन से डायनामिक, डेटा‑ड्रिवेन वेक्टर ग्राफ़िक्स सीधे जेनरेट कर पाएँगे। Happy coding!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}