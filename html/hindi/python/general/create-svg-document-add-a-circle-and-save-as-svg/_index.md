---
category: general
date: 2026-07-31
description: SVG दस्तावेज़ बनाना, उसमें एक वृत्त जोड़ना और शीघ्रता से SVG फ़ाइल सहेजना
  सीखें। कुछ ही पायथन कोड लाइनों से ग्राफ़िक को SVG के रूप में निर्यात करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: hi
lastmod: 2026-07-31
og_description: SVG दस्तावेज़ बनाएं, एक वृत्त जोड़ें, और सेकंडों में SVG फ़ाइल सहेजें।
  यह गाइड आपको स्पष्ट, चलाने योग्य कोड के साथ ग्राफ़िक को SVG के रूप में निर्यात करना
  दिखाता है।
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVG दस्तावेज़ बनाएं – एक वृत्त जोड़ें और SVG के रूप में सहेजें
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG दस्तावेज़ बनाएं – एक वृत्त जोड़ें और SVG के रूप में सहेजें
url: /hi/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG दस्तावेज़ बनाएं – एक सर्कल जोड़ें और SVG के रूप में सहेजें

क्या आपको कभी कोड से **create SVG document** बनाने की ज़रूरत पड़ी लेकिन शुरू कहाँ से करें, यह नहीं पता चला? आप अकेले नहीं हैं; कई डेवलपर्स को वेक्टर ग्राफ़िक्स के साथ पहली बार प्रयोग करते समय यही समस्या आती है। इस ट्यूटोरियल में हम एक छोटा, स्व-समाहित उदाहरण लेकर दिखाएंगे कि कैसे **add circle to SVG** किया जाए, फिर **save SVG file** करके आप **export graphic as SVG** को वेब या डिज़ाइन टूल्स में उपयोग कर सकें।

हम इसे हल्का रखेंगे: कुछ ही पंक्तियों का Python कोड, एक लोकप्रिय SVG हेल्पर लाइब्रेरी, और थोड़ी सी व्याख्या। अंत तक आपके पास एक तैयार‑उपयोग `circle.svg` फ़ाइल आपके फ़ोल्डर में होगी, और आप समझेंगे कि प्रत्येक कदम क्यों महत्वपूर्ण है—कोई अस्पष्ट “see docs” शॉर्टकट नहीं।

## आपको क्या चाहिए

- Python 3.8+ (कोई भी हालिया संस्करण काम करेगा)
- `svgwrite` पैकेज – इसे `pip install svgwrite` से इंस्टॉल करें
- एक टेक्स्ट एडिटर या IDE (VS Code, PyCharm, या यहाँ तक कि Notepad भी चलेगा)
- उस डायरेक्टरी में लिखने की अनुमति जहाँ आप फ़ाइल सहेजना चाहते हैं

बस इतना ही। कोई भारी निर्भरताएँ नहीं, कोई बाहरी सेवाएँ नहीं।

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Why this matters:** `Drawing` क्लास आपके लिए सभी XML बायलरप्लेट को संभालता है—नेमस्पेस, हेडर, और रूट `<svg>` एलिमेंट। फ़ाइलनाम पहले से निर्दिष्ट करके हम पहले से जानते हैं कि फ़ाइल कहाँ जाएगी, जिससे बाद के **save svg file** चरण को सरल बनाता है।

### प्रो टिप
यदि आप लूप में कई फ़ाइलें जनरेट करने की योजना बना रहे हैं, तो प्रत्येक `Drawing` को एक अनूठा नाम दें या `io.BytesIO` का उपयोग करके सब कुछ मेमोरी में रखें जब तक आप लिखने के लिए तैयार न हों।

## चरण 1: SVG दस्तावेज़ सेट अप करें

SVG दस्तावेज़ बनाना उतना ही सरल है जितना कि `svgwrite` से `Drawing` ऑब्जेक्ट को इंस्टैंशिएट करना। इस ऑब्जेक्ट को आप एक खाली कैनवास के रूप में सोच सकते हैं जहाँ हर आकार रहता है।

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Why we use `center` and `radius` variables:** हार्ड‑कोडेड नंबर कोड को पढ़ने और रखरखाव में कठिन बनाते हैं। मानों को नाम देकर हम इरादा स्पष्ट करते हैं—यह सर्कल 200 × 200 कैनवास के बिल्कुल मध्य में स्थित है और इतना बड़ा है कि दिखाई दे।

## चरण 2: SVG में एक सर्कल जोड़ें

अब जब दस्तावेज़ मौजूद है, चलिए **add circle to SVG** करते हैं। `add()` मेथड किसी भी शेप ऑब्जेक्ट को स्वीकार करता है; एक `Circle` केंद्र में एक साधारण लाल बिंदु के लिए बिल्कुल सही है।

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

> **Why we use `center` और `radius` variables:** हार्ड‑कोडेड नंबर कोड को पढ़ने और रखरखाव में कठिन बनाते हैं। मानों को नाम देकर हम इरादा स्पष्ट करते हैं—यह सर्कल 200 × 200 कैनवास के बिल्कुल मध्य में स्थित है और इतना बड़ा है कि दिखाई दे।

### किनारा मामला – पारदर्शी पृष्ठभूमि
यदि आपको पारदर्शी पृष्ठभूमि चाहिए (SVG का डिफ़ॉल्ट), तो आप रूट पर `fill` सेट करना छोड़ सकते हैं। सफ़ेद पृष्ठभूमि के लिए, जोड़ें:

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

सर्कल जोड़ने से पहले इसे रखें ताकि आयत नीचे की परत में रहे।

## चरण 3: SVG फ़ाइल सहेजें

शेप के साथ, अंतिम कदम **save SVG file** है। `save()` मेथड XML को डिस्क पर लिखता है, और क्योंकि हमने पहले ही `Drawing` को फ़ाइलनाम दिया है, एक ही कॉल काम कर देती है।

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

> **What happens under the hood?** `svgwrite` एलिमेंट ट्री को स्ट्रिंग में सीरियलाइज़ करता है, XML घोषणा जोड़ता है, और UTF‑8 एन्कोडिंग का उपयोग करके लिखता है। यदि लक्ष्य डायरेक्टरी मौजूद नहीं है, तो Python `FileNotFoundError` उठाएगा; सुनिश्चित करें कि पथ वैध है या `os.makedirs()` से बनाएं।

### बोनस: प्रोग्रामेटिकली ग्राफ़िक को SVG के रूप में एक्सपोर्ट करें
यदि आपको SVG सामग्री स्ट्रिंग के रूप में चाहिए—उदाहरण के लिए, इसे HTML ईमेल में एम्बेड करने के लिए—तो आप `save()` के बजाय `dwg.tostring()` कॉल कर सकते हैं:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ रखते हुए, यहाँ एक पूर्ण, चलाने‑के‑लिए‑तैयार स्क्रिप्ट है:

{{CODE_BLOCK_6}}

**Expected output:** स्क्रिप्ट चलाने के बाद, आपको उसी फ़ोल्डर में एक `circle.svg` फ़ाइल दिखेगी। इसे ब्राउज़र या किसी भी वेक्टर एडिटर में खोलने पर एक सफ़ेद वर्ग के केंद्र में लाल सर्कल दिखेगा—बिल्कुल वही जो हमने प्रोग्राम किया था।

## सामान्य प्रश्न और सावधानियाँ

- **What if I want a different shape?** `dwg.circle` को `dwg.rect`, `dwg.ellipse`, या यहाँ तक कि एक कस्टम `<path>` स्ट्रिंग से बदलें। API सभी शेप्स में सुसंगत है।
- **Can I embed the SVG directly in HTML?** बिल्कुल। आपने जो फ़ाइल अभी बनाई है उसे `<img src="circle.svg" alt="Red circle">` से रेफ़रेंस किया जा सकता है या `<svg>` टैग्स के साथ इनलाइन किया जा सकता है।
- **Why not write raw XML?** आप कर सकते हैं, लेकिन `svgwrite` जैसी लाइब्रेरीज़ नेमस्पेस की अजीबियों को संभालती हैं और कोड को बहुत अधिक मेंटेनेबल बनाती हैं—विशेषकर जब आप ग्रेडिएंट्स या एनीमेशन जोड़ना शुरू करते हैं।

## निष्कर्ष

अब आप जानते हैं कि कैसे **create SVG document**, **add circle to SVG**, और **save SVG file** किया जाता है ताकि आप **export graphic as SVG** केवल कुछ ही Python लाइनों से कर सकें। यह पैटर्न स्केलेबल है: सर्कल को किसी भी वेक्टर शेप से बदलें, डेटा पर लूप करके चार्ट बनाएं, या डिज़ाइन सिस्टम के लिए एसेट्स को बैच‑प्रोसेस करें।

अगले कदम? टेक्स्ट लेबल जोड़ने, ग्रेडिएंट्स के साथ प्रयोग करने, या एक ही स्क्रिप्ट में आइकनों की पूरी गैलरी जेनरेट करने की कोशिश करें। यदि आप अधिक उन्नत फीचर्स के बारे में जिज्ञासु हैं, तो `svgwrite` डॉक्यूमेंटेशन में ग्रुप्स (`<g>`), ट्रांसफ़ॉर्म्स, और एनीमेशन सपोर्ट देखें।

हैप्पी कोडिंग, और आपके वेक्टर हमेशा क्रिस्प रहें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं ताकि आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}