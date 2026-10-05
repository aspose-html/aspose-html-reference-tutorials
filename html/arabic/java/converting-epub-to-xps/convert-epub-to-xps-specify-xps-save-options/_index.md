---
date: 2026-03-29
description: تعلم كيفية استخدام Aspose.HTML للغة Java لتحديد خيارات حفظ XPS، وتحويل
  EPUB إلى XPS، ومعالجة الترخيص.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: كيفية استخدام خيارات حفظ Aspose HTML لتحويل EPUB إلى XPS
url: /ar/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام خيارات حفظ Aspose HTML لتحويل EPUB إلى XPS

في هذا الدليل سنوضح **كيفية استخدام Aspose** HTML Save Options لتحويل مستند EPUB إلى XPS مع تحكم كامل في أبعاد الصفحة، لون الخلفية، واعتبارات الترخيص. سواءً كنت تبني خط أنابيب معالجة دفعات أو أداة تحويل لمرة واحدة، ستساعدك هذه الخطوات على الحصول على نتائج موثوقة بسرعة.

## إجابات سريعة
- **ماذا تفعل خيارات حفظ Aspose HTML؟** تتيح لك تخصيص حجم الصفحة، لون الخلفية، وإعدادات العرض الأخرى عند الحفظ إلى صيغ مثل XPS.  
- **ما المكتبة المطلوبة؟** Aspose.HTML for Java (الإصدار الأخير).  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **هل يمكنني تغيير أبعاد الصفحة؟** نعم – يمكنك ضبط أي عرض وارتفاع عبر `PageSetup`.  
- **هل التحويل سريع؟** بالنسبة لملفات EPUB النموذجية يكتمل التحويل خلال ثوانٍ على JVM حديث.

## ما هو “كيفية استخدام Aspose” في هذا السياق؟
تشير العبارة **كيفية استخدام Aspose** إلى الخطوات العملية للاستفادة من مكتبة Aspose.HTML لمعالجة وتحويل المستندات المستندة إلى الويب. في هذا الدرس نركز على **aspose html save options** التي تتيح لك ضبط الإخراج بدقة عندما **تحول EPUB إلى XPS**.

## لماذا نستخدم Aspose.HTML for Java لتحويل EPUB إلى XPS؟
- **دقة عالية** – يحافظ على التخطيطات المعقدة، الخطوط، والرسومات المتجهية.  
- **تحكم برمجي** – أتمتة التحويلات الدفعية داخل تطبيقات Java.  
- **بدون تبعيات خارجية** – مكتبة Java صافية، لا مكونات أصلية.  
- **إخراج قابل للتخصيص** – بفضل خيارات الحفظ يمكنك تعديل XPS وفق احتياجاتك الدقيقة، مثل **تحديد أبعاد الصفحة** أو تعيين خلفية مخصصة.  

## المتطلبات المسبقة

قبل الغوص في الكود، تأكد من توفر ما يلي:

1. **بيئة تطوير Java** – JDK 8 أو أعلى مثبت.  
2. **مكتبة Aspose.HTML for Java** – قم بتنزيلها من [رابط التحميل](https://releases.aspose.com/html/java/).  
3. **ملف EPUB** – ملف EPUB المصدر الذي تريد **تحويل EPUB إلى XPS**.  

وجود هذه العناصر سيمكنك من متابعة الخطوات دون انقطاع.

## استيراد الحزم

First, import the required classes. Place the imports at the top of your Java source file:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

تمنحك هذه الاستيرادات الوصول إلى محرك التحويل و **Aspose HTML Save Options** اللازمة لضبط الإعدادات بدقة.

## فتح ملف EPUB

Next, open the EPUB you want to convert. The `Resources.input` helper loads a file from the demo resources folder:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

استخدام كتلة try‑with‑resources يضمن إغلاق الدفق تلقائيًا.

## إنشاء XpsSaveOptions (تكوين حجم الصفحة والخلفية)

Now we create an `XpsSaveOptions` instance and customize it. This is where the **save options** really shine:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **حجم الصفحة** – تم ضبطه على 3000 × 1000 بكسل في هذا المثال؛ عدّل ليتطابق مع حجم الورق المستهدف أو استخدم `Length.fromInches` **لتحديد أبعاد الصفحة** بالبوصة.  
- **لون الخلفية** – `AliceBlue` يوضح كيفية تغيير خلفية القماش؛ يمكنك اختيار أي `Color`.  

هذه الإعدادات هي جزء من **aspose html save options** التي تؤثر على مستند XPS النهائي.

## تحويل EPUB إلى XPS

Finally, invoke the converter with the stream, the configured options, and an output path:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

عند تشغيل هذا السطر، يقرأ Aspose.HTML ملف EPUB، يطبق إعداد الصفحة ولون الخلفية المحددين، ويكتب ملف XPS متوافق بالكامل.

## المشكلات الشائعة والنصائح
- **أبعاد الصفحة غير صحيحة** – تأكد من أن الأبعاد معبر عنها بالبكسل (أو استخدم `Length.fromInches`).  
- **الخطوط مفقودة** – دمج الخطوط المطلوبة في EPUB أو تثبيتها على مضيف JVM لتجنب التحويل إلى الخط الافتراضي.  
- **ملفات كبيرة** – بالنسبة لملفات EPUB الكبيرة جدًا، زد حجم ذاكرة JVM (`-Xmx`) لتجنب `OutOfMemoryError`.  
- **ترخيص Aspose HTML** – تأكد من تحميل ترخيص صالح قبل التحويل؛ وإلا سيظهر علامة مائية تجريبية.

## الخلاصة

من خلال الاستفادة من **Aspose HTML Save Options**، تحصل على تحكم دقيق في طريقة تحويل EPUB إلى XPS. الخطوات أعلاه توضح لك **كيفية تحويل EPUB**، ضبط **أبعاد الصفحة**، تغيير الخلفية، وإجراء التحويل ببضع أسطر من كود Java فقط. دمج هذا النمط في خطوط معالجة الدفعات الخاصة بك لأتمتة مهام النشر بفعالية.

## الأسئلة المتكررة

**س: ما هو Aspose.HTML for Java؟**  
ج: هي مكتبة Java تمكّن المطورين من إنشاء، تحرير، عرض، وتحويل HTML، EPUB، وغيرها من المستندات المستندة إلى الويب دون الحاجة إلى متصفح.

**س: هل يمكنني استخدام هذا في مشروع تجاري؟**  
ج: نعم. للاستخدام في الإنتاج تحتاج إلى ترخيص صالح. يمكنك شراء واحد من [صفحة الشراء](https://purchase.aspose.com/buy).

**س: هل يتوفر نسخة تجريبية مجانية؟**  
ج: بالطبع. قم بتنزيل نسخة تجريبية من [هنا](https://releases.aspose.com/).

**س: أين يمكنني الحصول على الدعم؟**  
ج: يتوفر دعم المجتمع والمساعدة الرسمية عبر منتديات Aspose على [https://forum.aspose.com/](https://forum.aspose.com/).

**س: ما هي متطلبات النظام؟**  
ج: تحتاج إلى مجموعة تطوير Java (JDK) 8+ ونظام تشغيل مدعوم من وقت تشغيل Aspose. تأكد من أن بيئتك تلبي المتطلبات المذكورة سابقًا.

---

**آخر تحديث:** 2026-03-29  
**تم الاختبار مع:** Aspose.HTML for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}