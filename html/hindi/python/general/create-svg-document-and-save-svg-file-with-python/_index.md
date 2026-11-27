---
category: general
date: 2026-11-27
description: Python का उपयोग करके SVG दस्तावेज़ बनाएं और SVG फ़ाइल सहेजें। वेक्टर
  को SVG के रूप में निर्यात करना सीखें और जल्दी से एक SVG छवि उत्पन्न करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: hi
lastmod: 2026-11-27
og_description: Python के साथ SVG दस्तावेज़ बनाएं और SVG फ़ाइल सहेजें। यह गाइड आपको
  दिखाता है कि कैसे वेक्टर को SVG के रूप में निर्यात करें और कुछ ही मिनटों में SVG
  छवि बनाएं।
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Python का उपयोग करके SVG दस्तावेज़ बनाएं और SVG फ़ाइल सहेजें
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Python के साथ SVG दस्तावेज़ बनाएं और SVG फ़ाइल सहेजें
url: /hi/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python के साथ SVG दस्तावेज़ बनाएं और SVG फ़ाइल सहेजें

यदि आपको शून्य से **SVG दस्तावेज़ बनाना** है, तो यह गाइड आपको पूरी प्रक्रिया से गुजराएगा। आप देखेंगे कि कैसे **SVG फ़ाइल सहेजें** डिस्क पर, वेक्टर को SVG के रूप में निर्यात करें, और कुछ ही कोड लाइनों में तैयार‑उपयोगी SVG छवि प्राप्त करें।

प्रोग्रामेटिक रूप से स्केलेबल ग्राफ़िक्स जेनरेट करना रिपोर्ट, UI आइकन, या किसी भी स्थिति में उपयोगी है जहाँ आप रिज़ॉल्यूशन‑इंडिपेंडेंट छवियां चाहते हैं। इस ट्यूटोरियल के अंत तक आप “**how to create SVG**?” का उत्तर दे पाएँगे सरल आकारों के लिए और इस पैटर्न को जटिल वेक्टर आर्टवर्क तक विस्तारित कर सकेंगे।

## आपको क्या चाहिए

- Python 3.8 या नया  
- `svgwrite` पैकेज (`pip` के माध्यम से स्थापित किया जा सकता है)  
- आउटपुट फ़ाइल के लिए लिखने योग्य डायरेक्टरी  

कोई बाहरी ग्राफ़िक्स एडिटर आवश्यक नहीं है; सब कुछ कमांड लाइन से चलता है।

## चरण 1: `svgwrite` लाइब्रेरी स्थापित करें

`svgwrite` साफ़, Pythonic API प्रदान करता है SVG मार्कअप बनाने के लिए। इसे एक बार स्थापित करें:

```bash
pip install svgwrite
```

> **Pro tip:** निर्भरताओं को अलग रखने के लिए एक वर्चुअल एनवायरनमेंट (`python -m venv .venv`) का उपयोग करें।

## चरण 2: SVG दस्तावेज़ बनाएं

अब हम वास्तव में **SVG दस्तावेज़ बनाते** हैं। `Drawing` क्लास रूट `<svg>` तत्व को दर्शाती है और नेमस्पेस को स्वचालित रूप से संभालती है।

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

`Drawing` इंस्टेंस सभी आगे के SVG ऑपरेशनों के लिए प्रवेश बिंदु है। `size` निर्दिष्ट करके हम कैनवास के आयाम सेट करते हैं, जो ब्राउज़र द्वारा छवि रेंडर करने को प्रभावित करता है।

## चरण 3: लाल वृत्त तत्व जोड़ें

आकार जोड़ना सरल है। `circle` मेथड एक `<circle>` तत्व बनाता है; फिर हम इसे रूट से जोड़ते हैं।

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

हमने वृत्त क्यों चुना: वृत्त वेक्टर प्रिमिटिव्स होते हैं जो गुणवत्ता में कोई कमी के बिना स्केलेबिलिटी दर्शाते हैं, जिससे आउटपुट **export vector as SVG** वर्कफ़्लो का परीक्षण करने के लिए आदर्श बनता है।

## चरण 4: SVG फ़ाइल सहेजें

अंत में, मार्कअप को डिस्क पर लिखें। यह चरण **save SVG file** आवश्यकता को पूरा करता है और एक फ़ाइल बनाता है जिसे आप किसी भी ब्राउज़र या वेक्टर एडिटर में खोल सकते हैं।

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

जब आप स्क्रिप्ट चलाएंगे, तो आपको कंसोल संदेश दिखाई देगा जो उत्पन्न फ़ाइल के स्थान की पुष्टि करता है।

### अपेक्षित आउटपुट

परिणामी `circle.svg` में शामिल है:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

फ़ाइल को ब्राउज़र में खोलने पर एक स्पष्ट लाल वृत्त दिखता है, और क्योंकि यह वेक्टर‑आधारित है, आप पिक्सेलेशन के बिना अनंत तक ज़ूम कर सकते हैं।

## चरण 5: सामान्य विविधताएँ और किनारे के मामले

### अधिक जटिल वेक्टर निर्यात करना

यदि आपको मल्टी‑शेप चित्रण के लिए **export vector as SVG** करने की आवश्यकता है, तो बस `dwg.add()` पैटर्न को अन्य प्रिमिटिव्स (`rect`, `line`, `path`, आदि) के साथ दोहराएँ। उदाहरण के लिए:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Unicode और टेक्स्ट को संभालना

SVG पूर्ण Unicode समर्थन के साथ टेक्स्ट तत्वों का समर्थन करता है। बहुभाषी लेबल एम्बेड करने के लिए `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` का उपयोग करें।

### अलग स्थान पर सहेजना

जब **save SVG image** को उपयोगकर्ता‑निर्दिष्ट फ़ोल्डर में सहेजते हैं, तो अनुमति त्रुटियों से बचने के लिए पथ को मान्य करें:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### आउटपुट को मिनिफ़ाई करना

प्रोडक्शन पाइपलाइन के लिए, आप छोटा फ़ाइल आकार चाहते हो सकते हैं। `dwg.tostring()` में `pretty=False` पास करें और परिणाम को मैन्युअली लिखें:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## वैकल्पिक लाइब्रेरीज़ के साथ SVG कैसे बनाएं (वैकल्पिक)

जबकि `svgwrite` हल्का और शुद्ध‑Python है, अन्य इकोसिस्टम मौजूद हैं:

- **cairosvg** – PNG, PDF, या HTML को SVG में परिवर्तित करता है।  
- **lxml** – XML APIs का उपयोग करके SVG मार्कअप को मैन्युअली बनाने देता है।  

लाइब्रेरी चुनना आपके प्रोजेक्ट की जटिलता और मौजूदा निर्भरताओं पर निर्भर करता है।

## निष्कर्ष

अब आप जानते हैं कि Python का उपयोग करके **SVG दस्तावेज़ बनाएं**, वेक्टर आकार जोड़ें, और **SVG फ़ाइल सहेजें**। संपूर्ण समाधान **export vector as SVG**, **SVG image** जेनरेट करने के चरण दिखाता है, और सामान्य प्रश्न **how to create SVG** का प्रोग्रामेटिक उत्तर देता है।

अब आप कर सकते हैं:

- लूप्स के साथ स्क्रिप्ट का विस्तार करके चार्ट या आइकन स्वचालित रूप से जेनरेट करें।  
- SVG आउटपुट को वेब एप्लिकेशन या ईमेल टेम्पलेट्स में एकीकृत करें।  
- `svgwrite` के साथ `<animate>` तत्व जोड़कर एनीमेशन का अन्वेषण करें।

विभिन्न आकारों, रंगों और ग्रेडिएंट्स के साथ प्रयोग करें ताकि अपने Python प्रोजेक्ट्स में स्केलेबल वेक्टर ग्राफ़िक्स की शक्ति को पूरी तरह उपयोग कर सकें। कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [SVG दस्तावेज़ बनाएं – एक वृत्त जोड़ें और SVG के रूप में सहेजें](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Python में SVG दस्तावेज़ बनाएं – SVG को PNG में बदलने का गाइड](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Python में SVG फ़ाइल लोड करें – निर्यात, एम्बेड और कन्वर्ट का पूर्ण गाइड](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}