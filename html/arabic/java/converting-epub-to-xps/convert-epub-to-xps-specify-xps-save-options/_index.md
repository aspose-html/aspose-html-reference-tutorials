---
date: 2026-01-09
description: تعلم كيفية استخدام Aspose.HTML للغة Java لتحديد خيارات حفظ XPS وتحويل
  EPUB إلى XPS بكفاءة.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: تحديد خيارات حفظ Aspose HTML لتحويل EPUB إلى XPS
url: /ar/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد خيارات حفظ Aspose HTML لتحويل EPUB إلى XPS

تحويل مستند EPUB إلى XPS يمكن أن يكون جزءًا مفيدًا من سير عمل النشر، و **Aspose HTML Save Options** تمنحك تحكمًا دقيقًا في المخرجات. في هذا البرنامج التعليمي سنستعرض الخطوات الدقيقة اللازمة لتكوين خيارات الحفظ هذه باستخدام Aspose.HTML للـ Java وإنتاج ملف XPS عالي الجودة.

## إجابات سريعة
- **ماذا تفعل Aspose HTML Save Options؟** تتيح لك تخصيص حجم الصفحة، لون الخلفية، وإعدادات العرض الأخرى عند الحفظ إلى صيغ مثل XPS.  
- **ما المكتبة المطلوبة؟** Aspose.HTML للـ Java (أحدث إصدار).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **هل يمكنني تغيير أبعاد الصفحة؟** نعم – يمكنك تعيين أي عرض وارتفاع عبر `PageSetup`.  
- **هل التحويل سريع؟** بالنسبة لملفات EPUB النموذجية يكتمل التحويل خلال ثوانٍ على JVM حديثة.

## ما هي Aspose HTML Save Options؟
Aspose HTML Save Options هي مجموعة من الخصائص التي تتحكم في كيفية عرض وحفظ مستندات HTML أو EPUB أو غيرها من المستندات المستندة إلى الويب إلى صيغة هدف مثل XPS أو PDF أو ملفات الصور. تتيح لك تحديد تخطيط الصفحة، ألوان الخلفية، الهوامش، والمزيد، لضمان أن الملف الناتج يطابق متطلبات التصميم الخاصة بك.

## لماذا نستخدم Aspose.HTML للـ Java لتحويل EPUB إلى XPS؟
- **دقة عالية** – يحافظ على التخطيطات المعقدة، الخطوط، والرسومات المتجهة.  
- **تحكم برمجي** – أتمتة التحويلات الدفعية داخل تطبيقات Java.  
- **بدون تبعيات خارجية** – مكتبة Java صافية، لا مكونات أصلية.  
- **مخرجات قابلة للتخصيص** – بفضل خيارات الحفظ يمكنك تعديل XPS لتلبية احتياجاتك الدقيقة.

## المتطلبات المسبقة

قبل الغوص في الكود، تأكد من توفر ما يلي:

1. **بيئة تطوير Java** – JDK 8 أو أعلى مثبتة.  
2. **مكتبة Aspose.HTML للـ Java** – قم بتنزيلها من [رابط التحميل](https://releases.aspose.com/html/java/).  
3. **ملف EPUB** – ملف EPUB المصدر الذي تريد تحويله.  

وجود هذه العناصر سيمكنك من متابعة الخطوات دون انقطاع.

## استيراد الحزم

أولاً، استورد الفئات المطلوبة. ضع الاستيرادات في أعلى ملف مصدر Java الخاص بك:

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

هذه الاستيرادات تمنحك الوصول إلى محرك التحويل و **Aspose HTML Save Options** اللازمة لضبط الإعدادات بدقة.

## فتح ملف EPUB

بعد ذلك، افتح ملف EPUB الذي تريد تحويله. المساعد `Resources.input` يحمل ملفًا من مجلد موارد العرض التجريبي:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

استخدام كتلة `try‑with‑resources` يضمن إغلاق الدفق تلقائيًا.

## إنشاء خيارات حفظ XPS (تكوين حجم الصفحة والخلفية)

الآن نقوم بإنشاء كائن `XpsSaveOptions` ونخصصه. هنا تتألق **خيارات الحفظ** حقًا:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **حجم الصفحة** – تم تعيينه إلى 3000 × 1000 بكسل في هذا المثال؛ عدلها لتتناسب مع حجم الورق المستهدف.  
- **لون الخلفية** – `AliceBlue` يوضح كيفية تغيير خلفية القماش؛ يمكنك اختيار أي `Color`.  

هذه الإعدادات هي جزء من **Aspose HTML Save Options** التي تؤثر على مستند XPS النهائي.

## تحويل EPUB إلى XPS

أخيرًا، استدعِ المحول مع الدفق، الخيارات المكوَّنة، ومسار الإخراج:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

عند تنفيذ هذا السطر، يقرأ Aspose.HTML ملف EPUB، يطبق إعدادات الصفحة ولون الخلفية التي حددتها، ويكتب ملف XPS متوافق بالكامل.

## المشكلات الشائعة والنصائح

- **أبعاد الصفحة غير صحيحة** – تأكد من أن الأبعاد معبر عنها بالبكسل (أو استخدم `Length.fromInches`).  
- **الخطوط المفقودة** – قم بدمج الخطوط المطلوبة في EPUB أو ثبتها على مضيف JVM لتجنب fallback.  
- **الملفات الكبيرة** – بالنسبة لملفات EPUB الضخمة، زد حجم ذاكرة JVM (`-Xmx`) لتفادي `OutOfMemoryError`.  

## الخلاصة

باستخدام **Aspose HTML Save Options**، تحصل على تحكم دقيق في طريقة عرض EPUB إلى XPS. توضح الخطوات أعلاه كيفية ضبط حجم الصفحة، لون الخلفية، وإجراء التحويل ببضع أسطر من كود Java فقط. دمج هذا النمط في خطوط المعالجة الدفعية الخاصة بك سيساعد على أتمتة مهام النشر بفعالية.

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للـ Java؟**  
ج: هي مكتبة Java تمكّن المطورين من إنشاء، تحرير، عرض، وتحويل مستندات HTML، EPUB، وغيرها من المستندات المستندة إلى الويب دون الحاجة إلى متصفح.

**س: هل يمكنني استخدامه في مشروع تجاري؟**  
ج: نعم. للاستخدام في الإنتاج تحتاج إلى ترخيص صالح. يمكنك شراء واحد عبر [صفحة الشراء](https://purchase.aspose.com/buy).

**س: هل هناك نسخة تجريبية مجانية؟**  
ج: بالتأكيد. حمّل نسخة تجريبية من [هنا](https://releases.aspose.com/).

**س: أين يمكنني الحصول على الدعم؟**  
ج: يتوفر الدعم المجتمعي والرسمي عبر منتديات Aspose على [https://forum.aspose.com/](https://forum.aspose.com/).

**س: ما هي متطلبات النظام؟**  
ج: تحتاج إلى مجموعة تطوير Java (JDK) 8+ ونظام تشغيل مدعوم من قبل بيئة تشغيل Aspose. تأكد من أن بيئتك تلبي المتطلبات المذكورة مسبقًا.

---

**آخر تحديث:** 2026-01-09  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}