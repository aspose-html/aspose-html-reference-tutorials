---
date: 2026-02-12
description: تعلم كيفية إضافة CSS إلى مستندات HTML باستخدام Aspose.HTML للغة Java،
  بما في ذلك كيفية إلحاق النمط إلى الوسم head وتعيين فئة CSS في Java.
linktitle: Add CSS to HTML Documents with Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: إضافة CSS إلى مستندات HTML باستخدام Aspose.HTML للـ Java
url: /ar/java/editing-html-documents/apply-external-css-html-documents/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة CSS إلى مستندات HTML باستخدام Aspose.HTML للغة Java

## المقدمة
عند العمل مع مستندات HTML، معرفة **كيفية إضافة CSS إلى HTML** يمكن أن تُحدث فرقًا كبيرًا في العرض وتجربة المستخدم. إذا كنت تتعمق في Java وتريد تعلم كيفية تطبيق أنماط CSS خارجية على مستندات HTML باستخدام مكتبة Aspose.HTML، فأنت في المكان الصحيح! يوضح هذا الدليل العملية خطوة بخطوة، بحيث يمكن للمطورين الجدد على Java أو CSS المتابعة بثقة.

## الإجابات السريعة
- **ماذا يفعل Aspose.HTML للغة Java؟** يتيح لك إنشاء وتحرير وعرض مستندات HTML مباشرةً من كود Java.  
- **هل يمكنني تطبيق CSS خارجي؟** نعم – يمكنك إلحاق النمط إلى head، ربط ملفات خارجية، أو حقن سلاسل CSS.  
- **هل أحتاج إلى اتصال بالإنترنت؟** لا، كل شيء يعمل محليًا بعد تنزيل المكتبة.  
- **ما صيغ الإخراج المدعومة؟** يمكن عرض HTML إلى PDF أو صور أو الاحتفاظ به كـ HTML.  
- **هل يلزم ترخيص للاستخدام في الإنتاج؟** يلزم ترخيص تجاري للاستخدام في الإنتاج؛ تتوفر نسخة تجريبية مجانية.

## ما هو “إضافة CSS إلى HTML”؟
إضافة CSS إلى HTML تعني إرفاق قواعد النمط—سواءً كانت داخلية، داخل المستند، أو خارجية—بمستند HTML بحيث تعرف المتصفحات كيفية عرض العناصر (الألوان، الخطوط، التخطيط، إلخ). باستخدام Aspose.HTML للغة Java يمكنك حقن هذه الأنماط برمجيًا دون الحاجة إلى فتح المتصفح.

## لماذا تستخدم Aspose.HTML للغة Java لإضافة CSS؟
- **تحكم كامل** – تعديل DOM، حقن عناصر النمط، وتعيين الفئات مباشرةً من Java.  
- **بدون تبعيات خارجية** – يعمل دون اتصال، مثالي للخدمات الخلفية.  
- **تحويل إلى PDF** – تحويل HTML المنسق إلى PDF قابل للطباعة بسطر واحد من الكود.  

## المتطلبات المسبقة
قبل الغوص في الكود، تأكد من توفر ما يلي:

### 1. مجموعة تطوير Java (JDK)
تأكد من تثبيت JDK على جهازك. يمكنك تنزيل أحدث نسخة من [موقع Oracle للـ Java](https://www.oracle.com/java/technologies/javase-downloads.html).

### 2. Aspose.HTML للغة Java
ستحتاج إلى إعداد Aspose.HTML للغة Java. إذا لم تقم بذلك بعد، توجه إلى [صفحة تنزيل Aspose](https://releases.aspose.com/html/java/) واحصل على المكتبة.

### 3. بيئة تطوير متكاملة أو محرر نصوص
اختر بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse، أو حتى محرر نصوص بسيط لكتابة كود Java الخاص بك.

### 4. معرفة أساسية بـ Java و CSS
الإلمام ببرمجة Java وأساسيّات CSS سيساعدك على متابعة الشرح بسهولة أكبر.

## استيراد الحزم
بعد إعداد كل شيء، الخطوة التالية هي استيراد الحزم اللازمة في مشروع Java الخاص بك. إليك ما تحتاجه:

```java
import com.aspose.html.HTMLDocument;
```

تسمح لك هذه الاستيرادات بالتعامل مع مستندات HTML وتحويلها إلى صيغ مختلفة، مثل PDF.

سنقسم الشرح إلى خطوات قابلة للإدارة. كل خطوة ستقودك خلال عملية **إضافة CSS إلى HTML** باستخدام Aspose.HTML للغة Java.

## الخطوة 1: إنشاء مستند HTML في Java
أولاً، نحتاج إلى إنشاء مستند HTML الخاص بنا. سنبدأ بتعريف المحتوى باستخدام بنية HTML بسيطة.

```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

هنا، عرّفنا بنية HTML أساسية، تشمل `<div>` يحتوي على فقرتين. تُستخدم فئة `HTMLDocument` لإنشاء تمثيل للمستند من محتوى HTML الخاص بنا.

## الخطوة 2: إنشاء عنصر نمط (Style)
بعد ذلك، سننشئ عنصر `style` لحفظ قواعد CSS الخاصة بنا.

```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

باستخدام طريقة `createElement` في `HTMLDocument`، ننشئ عنصر `<style>` جديد ونضع محتواه ليشمل تعريفات CSS لفئتين: `frame1` و `frame2`. تحدد هذه الفئات الهوامش، الحشو، الأبعاد، ألوان الخلفية، عائلات الخطوط، وألوان النص.

## الخطوة 3: إلحاق النمط إلى head
الآن بعد أن أصبح لدينا CSS جاهزًا، نحتاج إلى **إلحاق النمط إلى head** حتى يتمكن المتصفح (أو محرك Aspose) من تطبيقه.

```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

نسترجع عنصر `head` في المستند ونلحق به عنصر `style` الذي أنشأناه حديثًا. يدمج هذا الإجراء CSS في مستند HTML، مما يسمح له بتنسيق محتوى HTML.

## الخطوة 4: تعيين فئة CSS في Java
بعد ذلك، سنطبق الفئات CSS التي عرّفناها مسبقًا على عناصر الفقرات في المستند.

```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

هنا، نصل إلى أول وآخر عنصر فقرة في المستند ونعيّن لهما فئات CSS التي أنشأناها. يضمن هذا التعيين أن تتبع الفقرات الأنماط المحددة في CSS.

## الخطوة 5: تعيين خصائص نمط إضافية
لتحسين المظهر أكثر، سنضيف خصائص نمط إضافية لفقراتنا.

```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

في هذه الخطوة، نقوم بضبط الأنماط بدقة. يتم تكبير حجم خط الفقرة الأولى وتوسيطه، بينما تُحدد الفقرة الأخيرة اللون، حجم الخط، وعائلة الخط. هذا التحسين مهم للقراءة والجاذبية البصرية.

## الخطوة 6: حفظ مستند HTML
بعد تطبيق الأنماط، حان الوقت لحفظ مستند HTML.

```java
document.save("edit-internal-css.html");
```

نستخدم طريقة `save` في فئة `HTMLDocument` لكتابة محتوى HTML المعدل إلى ملف، وبالتالي حفظ الأنماط والتغييرات التي أجريناها.

## الخطوة 7: تحويل HTML إلى PDF
أخيرًا، دعنا **نحول HTML إلى PDF** حتى تتمكن من مشاركة المستند المنسق بصيغة يمكن الوصول إليها عالميًا.

```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

باستخدام فئة `PdfDevice`، نُعدّ عملية تحويل مستند HTML إلى PDF. هذه الخطوة أساسية عندما تريد مشاركة المستند المنسق بصيغة قابلة للطباعة ومدعومة على نطاق واسع.

## حالات الاستخدام الشائعة
- **إنشاء تقارير تلقائية** – إنشاء تقارير HTML منسقة وتحويلها إلى PDF للتوزيع.  
- **قوالب البريد الإلكتروني** – إنشاء رسائل بريد إلكتروني HTML ذات هوية بصرية ثابتة، ثم تحويلها إلى PDF للأرشفة.  
- **معالجة دفعات** – تطبيق نفس CSS على عشرات ملفات HTML في مهمة خادم جانبية.

## استكشاف الأخطاء وإصلاحها والنصائح
- **عدم وجود عنصر head** – إذا أعادت `getElementsByTagName("head")` قيمة null، تأكد من أن سلسلة HTML الخاصة بك تحتوي على وسم `<head>`.  
- **عدم تطبيق CSS** – تحقق من أن أسماء الفئات في `setClassName` مطابقة تمامًا لتلك المعرفة في كتلة `<style>`.  
- **مشكلات في تحويل PDF** – تأكد من تطبيق ترخيص Aspose.HTML بشكل صحيح؛ وإلا قد يكون الناتج مائيًا.

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للغة Java؟**  
ج: Aspose.HTML للغة Java هي مكتبة قوية تسمح للمطورين بالعمل مع مستندات HTML في تطبيقات Java، وتوفر مجموعة واسعة من الميزات، من تعديل HTML إلى التحويل.

**س: هل أحتاج إلى اتصال بالإنترنت لاستخدام Aspose.HTML؟**  
ج: لا، بمجرد تنزيل ملفات المكتبة اللازمة، يمكنك استخدام Aspose.HTML دون اتصال.

**س: هل يمكنني تطبيق ملفات CSS متعددة على مستند HTML؟**  
ج: نعم، يمكنك إنشاء عدة عناصر `<link>` وإلحاقها بـ head المستند لربط ملفات CSS مختلفة.

**س: هل هناك فرق بين CSS الداخلي والخارجي؟**  
ج: نعم! يُعرّف CSS الداخلي داخل مستند HTML، بينما يُوضع CSS الخارجي في ملف منفصل ويتم ربطه بالمستند.

**س: كيف يمكنني الحصول على الدعم لـ Aspose.HTML للغة Java؟**  
ج: يمكنك الوصول إلى الدعم المجتمعي عبر [منتدى Aspose](https://forum.aspose.com/c/html/29) لأي أسئلة أو مشكلات قد تواجهها.

---

**آخر تحديث:** 2026-02-12  
**تم الاختبار مع:** Aspose.HTML للغة Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}