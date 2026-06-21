---
category: general
date: 2026-03-05
description: كيفية استعلام HTML في Java لقراءة ملف HTML واستخراج الصور. تعلم قراءة
  ملف HTML في Java، الحصول على عناوين URL للصور في Java، والتكرار على NodeList في
  Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: ar
og_description: كيفية استعلام HTML في جافا واسترجاع عناوين URL للصور. يوضح هذا الدليل
  كيفية قراءة ملف HTML في جافا، وتحديد موقع الصور، والتكرار عبر NodeList في جافا.
og_title: كيفية استعلام HTML في جافا – استخراج عناوين URL للصور
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: كيفية استعلام HTML في جافا – استخراج روابط الصور
url: /ar/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استعلام HTML في جافا – استخراج عناوين صور

هل تساءلت يومًا **كيف تستعلم عن HTML** في جافا لاستخراج كل صورة في صفحة؟ لست وحدك—المطورون يحتاجون باستمرار إلى قراءة ملفات HTML، استخراج الصور، ثم القيام بشيء مفيد مع عناوين URL. في هذا الدرس سنستعرض مثالًا عمليًا يوضح بالضبط **كيفية استعلام HTML**، قراءة ملف HTML بأسلوب جافا، والحصول على عناوين الصور بطريقة جافا.

سنستخدم Aspose.HTML لجافا، لكن المفاهيم—XPath، محددات CSS، والتكرار على `NodeList`—تنطبق على أي مكتبة DOM. بنهاية هذا الدليل ستكون مرتاحًا مع **كيفية استخراج الصور**، وتعرف **كيفية التكرار على NodeList جافا**، وستحصل على مقطع شفرة جاهز يمكنك إدراجه في مشروعك.

![مثال على استعلام HTML في جافا](https://example.com/placeholder.png "مثال على استعلام HTML في جافا")

---

## ما ستتعلمه

- تحميل مستند HTML من القرص (read HTML file Java)
- تحديد وسوم `<img>` باستخدام كل من XPath ومحددات CSS (how to extract images)
- التكرار عبر `NodeList` الناتج (iterate over NodeList Java)
- طباعة سمة `src` لكل صورة (get image URLs Java)

بدون خدمات خارجية، بدون أدوات بناء معقدة—فقط جافا صافية واعتماد Maven واحد.

---

## المتطلبات المسبقة

- جافا 8 أو أحدث مثبتة
- Maven أو Gradle لإدارة الاعتمادات
- إلمام أساسي بهيكلية HTML
- اختياري لكن مفيد: ملف HTML بسيط (`sample.html`) يحتوي على بعض عناصر `<figure><img …></figure>`

إذا كان لديك هذه المتطلبات، يمكننا البدء فورًا.

---

## الخطوة 1: قراءة ملف HTML جافا – تحميل المستند

أولًا وأهم شيء: نحتاج إلى جلب HTML إلى الذاكرة. فئة `HTMLDocument` في Aspose.HTML تقوم بالعمل الشاق. فكر فيها كفتح كتاب لتتمكن من الانتقال إلى أي صفحة.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**لماذا هذا مهم:** تحميل الملف يمنحك شجرة DOM يمكنك الاستعلام عنها. إذا كان المسار خاطئًا، ستحصل على `FileNotFoundException`، لذا تحقق من الموقع قبل التشغيل.

---

## الخطوة 2: تحديد الصور باستخدام XPath – كيفية استخراج الصور

XPath لغة استعلام قوية تتيح لك تحديد العقد بدقة بالليزر. هنا نطلب كل `<img>` داخل `<figure>` يحتوي أيضًا على سمة `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**لماذا XPath؟** إنها مختصرة وتعمل حتى عندما يكون HTML فوضويًا. التعبير `//figure/img[@alt]` يترجم إلى: “أي `<img>` تحت `<figure>` يحمل سمة `alt`.” إذا احتجت لتصفية حسب سمات أخرى، فقط عدل الأقواس.

---

## الخطوة 3: تحديد الصور باستخدام محدد CSS – طريقة بديلة لاستخراج الصور

أحيانًا تفضل صيغة CSS لأنها تعكس ما تكتبه في أوراق الأنماط. `querySelectorAll` يقبل نفس المحدد الذي تستخدمه في المتصفح.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**لماذا كلاهما؟** عرض كلا الطريقتين يوضح لك أنه يمكنك اختيار الأداة التي ترتاح لها أكثر. عمليًا ستلتزم بإحدى الطريقتين، لكن وجود المثالين يجعل الدرس أكثر اكتمالًا.

---

## الخطوة 4: التكرار على NodeList جافا – الحصول على عناوين الصور جافا

الآن بعد أن لدينا مجموعة، نحتاج إلى المرور عليها. هنا يأتي دور **iterate over NodeList Java**. سنستخرج سمة `src` لكل صورة ونطبعها.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**لماذا حلقة `for` التقليدية؟** فئة Aspose `NodeList` لا تنفذ `Iterable`، لذا لا يمكن استخدام صيغة `for‑each` الموسعة. استخدام حلقة بالمؤشر هو الطريقة الموثوقة لـ **iterate over NodeList Java**.

---

## النتيجة المتوقعة

تشغيل البرنامج ضد HTML تجريبي مثل:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

سيفتح لك ما يشبه:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

إذا كان ملفك يحتوي على المزيد من وسوم `<img>` التي تستوفي الشروط، ستزداد الأرقام وفقًا لذلك.

---

## الأخطاء الشائعة والنصائح الاحترافية

- **مشكلات مسار الملف:** استخدم مسارًا مطلقًا أو ضع `sample.html` نسبةً إلى دليل عمل مشروعك.  
- **غياب سمة `alt`:** استعلامات XPath/CSS لدينا تصفي بـ `[@alt]`. إذا أردت *كل* الصور، احذف فلتر السمة (`//figure/img` أو `figure img`).  
- **الأداء:** للمستندات الضخمة، فكر في محللات تدفقية، لكن لمعظم مهام استخراج الويب تكون طريقة DOM كافية.  
- **مشكلات الترميز:** Aspose.HTML يحترم مجموعة الأحرف المعلن عنها في HTML. إذا ظهرت رموز غير مفهومة، تأكد من حفظ الملف كـ UTF‑8.  

---

## توسيع المثال

الآن بعد أن يمكنك **الحصول على عناوين الصور جافا**، قد ترغب في:

1. **تحميل الصور** باستخدام `java.net.URL` و `Files.copy`.  
2. **تخزين العناوين في قاعدة بيانات** للمعالجة لاحقًا.  
3. **تصفية حسب امتداد الملف** (`src.endsWith(".png")`).  

جميع هذه التوسعات بسيطة ويمكن تنفيذها داخل الحلقة المعروضة في الخطوة 4.

---

## الخاتمة

في هذا الدليل غطينا **كيفية استعلام HTML** في جافا من البداية إلى النهاية: تحميل الملف، تحديد الصور بكل من XPath ومحددات CSS، و**التكرار على NodeList جافا** لطباعة سمة `src` لكل صورة. الآن لديك أساس قوي لـ **كيفية استخراج الصور**، وتعرف بالضبط **كيفية قراءة ملف HTML جافا** باستخدام Aspose.HTML.

لا تتردد في تعديل الشفرة لتناسب احتياجاتك الخاصة—سواء كان ذلك باستخراج سمات أخرى، التعامل مع وسوم `<a>`، أو تمرير العناوين إلى أداة تحميل. النمط يبقى نفسه: تحميل، استعلام، تكرار، وتنفيذ.

هل لديك أسئلة أو تريد مشاركة حالة استخدام مميزة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}