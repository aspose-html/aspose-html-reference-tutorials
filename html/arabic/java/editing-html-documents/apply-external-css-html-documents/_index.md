---
title: تطبيق CSS خارجي على مستندات HTML في Aspose.HTML لـ Java
linktitle: تطبيق CSS خارجي على مستندات HTML في Aspose.HTML لـ Java
second_title: معالجة HTML باستخدام Java مع Aspose.HTML
description: اكتشف كيفية تطبيق CSS خارجي على مستندات HTML باستخدام Aspose.HTML for Java! اتبع هذا الدليل خطوة بخطوة للحصول على برنامج تعليمي كامل.
weight: 12
url: /ar/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق CSS خارجي على مستندات HTML في Aspose.HTML لـ Java

## مقدمة
عند العمل مع مستندات HTML، يمكن أن يحدث تطبيق الأنماط فرقًا كبيرًا في العرض وتجربة المستخدم. إذا كنت تتعمق في Java وترغب في معرفة كيفية تطبيق أنماط CSS الخارجية على مستندات HTML الخاصة بك باستخدام مكتبة Aspose.HTML، فأنت في المكان المناسب! يهدف هذا الدليل إلى توضيح العملية خطوة بخطوة، مما يجعلها سهلة حتى لأولئك الذين قد يكونون جددًا على Java أو CSS.
## المتطلبات الأساسية
قبل الغوص في الكود، هناك بعض الأشياء التي ستحتاج إلى وضعها في مكانها:
### 1. مجموعة تطوير جافا (JDK)
 تأكد من تثبيت JDK على جهازك. يمكنك تنزيل أحدث إصدار من[موقع جافا الخاص بشركة أوراكل](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML لجافا
ستحتاج إلى إعداد Aspose.HTML لـ Java. إذا لم تقم بذلك بعد، فتوجه إلى[صفحة تنزيلات Aspose](https://releases.aspose.com/html/java/) وأمسك بالمكتبة.
### 3. IDE أو محرر النصوص
اختر بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA، أو Eclipse، أو حتى محرر نصوص بسيط لكتابة كود Java الخاص بك.
### 4. المعرفة الأساسية بلغة جافا
من المؤكد أن التعرف على أساسيات برمجة Java وCSS سيساعدك على المتابعة بشكل أكثر راحة.
## استيراد الحزم
بمجرد إعداد كل شيء، فإن الخطوة التالية هي استيراد الحزم اللازمة في مشروع Java الخاص بك. إليك ما تحتاجه:
```java
import com.aspose.html.HTMLDocument;
```
ستتيح لك هذه الاستيرادات معالجة مستندات HTML وتقديمها بتنسيقات مختلفة، مثل PDF.

سنقوم بتقسيم البرنامج التعليمي الخاص بنا إلى خطوات يمكن إدارتها. سترشدك كل خطوة خلال عملية تطبيق أنماط CSS الخارجية على مستند HTML باستخدام Aspose.HTML for Java.
## الخطوة 1: إنشاء مستند HTML
أولاً، نحتاج إلى إنشاء مستند HTML. سنبدأ بتحديد المحتوى باستخدام بنية HTML بسيطة.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 هنا، قمنا بتعريف بنية HTML الأساسية، بما في ذلك`<div>` مع فقرتين.`HTMLDocument` يتم استخدام class لإنشاء تمثيل مستند لمحتوى HTML الخاص بنا.
## الخطوة 2: إنشاء عنصر النمط
 بعد ذلك، سنقوم بإنشاء`style` عنصر لحمل قواعد CSS الخاصة بنا.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 استخدام`createElement` طريقة`HTMLDocument` نحن ننشئ جديدا`<style>` العنصر وتعيين محتواه ليشمل تعريفات CSS الخاصة بنا لفئتين:`frame1` و`frame2`. تحدد هذه الفئات الهوامش والحشو والأبعاد وألوان الخلفية وعائلات الخطوط وألوان النص.
## الخطوة 3: إضافة النمط إلى رأس المستند
الآن بعد أن أصبح لدينا CSS في مكانه، نحتاج إلى إضافة عنصر النمط إلى رأس المستند.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 نستعيد رأس المستند ونضيف إليه المستند الذي تم إنشاؤه حديثًا`style` يدمج هذا الإجراء بشكل فعال CSS الخاص بنا في مستند HTML، مما يسمح له بتصميم محتوى HTML الخاص بنا.
## الخطوة 4: تطبيق الفئات على عناصر HTML
بعد ذلك، سنقوم بتطبيق فئات CSS المحددة مسبقًا على عناصر الفقرة الخاصة بنا.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

هنا، نصل إلى عناصر الفقرة الأولى والأخيرة في المستند ونقوم بتعيين فئات CSS التي أنشأناها لها. يضمن هذا التعيين التزامها بالأنماط المحددة في CSS الخاص بنا.
## الخطوة 5: تعيين خصائص النمط الإضافية
لتحسين المظهر بشكل أكبر، سنقوم بتعيين خصائص نمط إضافية لفقراتنا.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

في هذه الخطوة، نقوم بضبط أنماطنا. يتم تكبير حجم الخط في الفقرة الأولى وتمركزه، بينما يتم تحديد لون الفقرة الأخيرة وحجم الخط وعائلة الخط. يعد هذا التحسين أمرًا بالغ الأهمية لسهولة القراءة والجاذبية الجمالية.
## الخطوة 6: حفظ مستند HTML
بمجرد تطبيق أنماطنا، حان الوقت لحفظ مستند HTML.
```java
document.save("edit-internal-css.html");
```

 هنا، نستخدم`save` طريقة`HTMLDocument` فئة لكتابة محتوى HTML المعدل إلى ملف، وبالتالي الحفاظ على أنماطنا وتغييراتنا.
## الخطوة 7: تحويل المستند إلى PDF
وأخيرًا، دعنا نحوّل المستند إلى تنسيق PDF لإخراجه.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 استخدام`PdfDevice` في الصف، نقوم بإعداد عرض مستند HTML الخاص بنا في شكل PDF. هذه الخطوة مهمة عندما تريد مشاركة المستند المصمم بتنسيق يمكن الوصول إليه عالميًا.
## خاتمة
والآن، أصبح بإمكانك تطبيق CSS خارجي على مستندات HTML باستخدام Aspose.HTML for Java، وهو أمر بسيط ومجزٍ! فباستخدام بضعة أسطر فقط من التعليمات البرمجية، يمكنك تحويل النص العادي إلى مستندات جذابة بصريًا وذات تصميم احترافي. لذا، سواء كنت تقوم بالتصميم للاستخدام الشخصي أو إنشاء التقارير أو تطوير محتوى الويب، فإن فهم كيفية التعامل مع HTML وCSS في Java يعد مهارة قوية يجب أن تكون ضمن مجموعة أدواتك.
## الأسئلة الشائعة
### ما هو Aspose.HTML لـ Java؟
Aspose.HTML for Java هي مكتبة قوية تسمح للمطورين بالعمل مع مستندات HTML في تطبيقات Java، وتوفر مجموعة واسعة من الميزات، من معالجة HTML إلى العرض.
### هل أحتاج إلى اتصال بالإنترنت لاستخدام Aspose.HTML؟
لا، بمجرد تنزيل ملفات المكتبة الضرورية، يمكنك استخدام Aspose.HTML دون الاتصال بالإنترنت.
### هل يمكنني تطبيق ملفات CSS متعددة على مستند HTML؟
 نعم، يمكنك إنشاء العديد من`<link>` العناصر وإضافتها إلى رأس المستند لملفات CSS المختلفة.
### هل هناك فرق بين CSS الداخلي والخارجي؟
نعم! يتم تعريف CSS الداخلي داخل مستند HTML، بينما يتم وضع CSS الخارجي في ملف منفصل وربطه بالمستند.
### كيف يمكنني الحصول على الدعم لـ Aspose.HTML لـ Java؟
 يمكنك الوصول إلى دعم المجتمع من خلال[منتدى اسبوس](https://forum.aspose.com/c/html/29) لأي أسئلة أو مشاكل قد تواجهها.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
