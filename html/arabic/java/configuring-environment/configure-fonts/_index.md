---
date: 2026-04-05
description: تعلم كيفية إنشاء PDF من HTML، وتكوين الخطوط، وتطبيق CSS مخصص، واستخدام
  ترخيص مؤقت، وتحويل HTML إلى PDF في Java باستخدام Aspose.HTML.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: تكوين الخطوط في Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 'إنشاء ملف PDF من HTML: تكوين الخطوط باستخدام Aspose.HTML للغة Java'
url: /ar/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تكوين الخطوط لتحويل HTML إلى PDF في Java باستخدام Aspose.HTML

## مقدمة
في هذا الدرس ستكتشف كيفية **إنشاء PDF من HTML** باستخدام Aspose.HTML وتكوين الخطوط لتحويل HTML إلى PDF في Java. عند العمل مع مستندات HTML، يضمن إعداد الخطوط الصحيحة أن يبدو ملف PDF الناتج مطابقًا تمامًا للصفحة الويب الأصلية—مع الحفاظ على ألوان العلامة التجارية، والطباعة، والتخطيط. سواء كنت تبني تقارير، فواتير، أو أي خط أنابيب لتوليد المستندات، فإن تكوين الخطوط بشكل صحيح هو المفتاح للحصول على ملفات PDF ذات مظهر احترافي. دعنا نتبع العملية بالكامل، من إعداد البيئة إلى تحويل HTML إلى PDF باستخدام خطوط مخصصة وCSS.

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا الدرس؟** تكوين الخطوط لتحويل HTML إلى PDF في Java باستخدام Aspose.HTML.  
- **ما المكتبة التي تتعامل مع التحويل؟** Aspose.HTML for Java (فئة `Converter`).  
- **هل أحتاج إلى ترخيص؟** ترخيص Aspose المؤقت يزيل حدود التقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **أين يجب وضع الخطوط المخصصة؟** في مجلد يُشار إليه بواسطة `FontsLookupFolder`، مثل دليل `fonts` بجوار مشروعك.  
- **هل يمكنني تخصيص مخرجات PDF؟** نعم—استخدم `PdfSaveOptions` لتعديل حجم الصفحة، الهوامش، وأكثر.

## ما هو **إنشاء PDF من HTML** ولماذا تكوين الخطوط مهم؟
عملية **إنشاء PDF من HTML** تقوم بتحويل مستند HTML إلى صفحة PDF. الخطوط هي جزء أساسي من عملية العرض لأنها تؤثر على التخطيط، وتباعد الأسطر، والدقة البصرية. من خلال توجيه Aspose.HTML إلى مجلد خطوط مخصص، تضمن أن يستخدم ملف PDF الخطوط الدقيقة التي صممتها للصفحة الويب، مما يلغي الخطوط الاحتياطية ويحافظ على تناسق العلامة التجارية.

## لماذا نستخدم Aspose.HTML لتكوين الخطوط؟
- **عرض دقيق:** يدعم CSS2.1 والعديد من ميزات CSS3، لذا يبدو HTML الخاص بك كما هو في PDF.  
- **متعدد المنصات:** يعمل على أي نظام تشغيل يدعم Java 1.8+.  
- **مرونة الترخيص:** اختبر باستخدام ترخيص مؤقت، ثم انتقل إلى ترخيص كامل للإنتاج.  
- **الأداء:** تحويل سريع حتى للصفحات المعقدة.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من وجود ما يلي:

1. **مجموعة تطوير جافا (JDK) 1.8+** – الكود يعمل على أي JDK حديث.  
2. **Aspose.HTML for Java** – قم بتحميل أحدث JAR من [موقع Aspose](https://releases.aspose.com/html/java/).  
3. **بيئة تطوير متكاملة (IDE)** – IntelliJ IDEA، Eclipse، أو أي محرر متوافق مع Java.  
4. **معرفة أساسية بجافا** – يجب أن تكون مرتاحًا مع الفئات، والطرق، وإدخال/إخراج الملفات.  
5. **ترخيص Aspose.HTML** – ترخيص [مؤقت](https://purchase.aspose.com/temporary-license/) سيزيل قيود التقييم.

## استيراد الحزم
أولاً، استورد فئات Java الأساسية وAspose.HTML التي ستحتاجها.  

```java
import java.io.IOException;
```

تمنحك هذه الاستيرادات إمكانية الوصول إلى معالجة الملفات وواجهة برمجة تطبيقات Aspose.HTML.

## كيفية إضافة خطوط مخصصة لتوليد PDF
سوف نشرح أدناه لماذا معالجة الخطوط مهمة، وكيفية تطبيق CSS مخصص، وكيفية **استخدام ترخيص مؤقت** لفتح جميع الوظائف أثناء اختبار الحل.

## دليل خطوة بخطوة

### الخطوة 1: إنشاء محتوى HTML
سنبدأ بإنشاء ملف HTML بسيط سنقوم لاحقًا بتحويله إلى PDF.

#### 1.1 كتابة كود HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

هذا المقتطف يعرّف عنوانًا وفقرة. لا تتردد في توسيع HTML بمزيد من العناصر إذا كنت بحاجة لاختبار أنماط إضافية.

#### 1.2 حفظ HTML إلى ملف
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` يكتب السلسلة إلى `user-agent-fontsetting.html` في مجلد مشروعك. بعد هذه الخطوة ستحصل على ملف HTML فعلي جاهز للمعالجة.

### الخطوة 2: تكوين بيئة Aspose.HTML
الآن سنقوم بإعداد كائن Aspose.HTML `Configuration`، الذي يتيح لنا التحكم في كيفية عرض HTML.

#### 2.1 إنشاء مثيل Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

كائن `Configuration` هو نقطة الدخول لتخصيص خيارات العرض مثل معالجة الخطوط وسلوك وكيل المستخدم.

#### 2.2 الوصول إلى خدمة وكيل المستخدم
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` يدير أوراق الأنماط، الخطوط، وتفاصيل العرض الأخرى. سنستخدمه لإدخال CSS مخصص والإشارة إلى مجلد الخطوط الخاص بنا.

### الخطوة 3: تطبيق الأنماط والخطوط المخصصة
مع جاهزية البيئة، يمكننا الآن إضافة قواعد CSS وإخبار Aspose.HTML بمكان العثور على خطوطنا.

#### 3.1 تعيين CSS مخصص
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

هذا الـ CSS يلون العنوان باللون البني والفقرة بالرمادي. يمكنك إضافة أي قواعد CSS صالحة هنا—Aspose.HTML يدعم مواصفات CSS2.1 بالكامل والعديد من ميزات CSS3. *(هذا مثال على **تطبيق CSS مخصص**.)*

#### 3.2 الإشارة إلى مجلد الخطوط المخصص
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

ضع أي ملفات `.ttf` أو `.otf` تريد استخدامها داخل مجلد اسمه `fonts` موجود في جذر مشروعك. سيقوم Aspose.HTML بتحميل هذه الخطوط تلقائيًا أثناء العرض.

> **نصيحة احترافية:** إذا كان لديك عدة عائلات خطوط، حافظ على تنظيمها في مجلدات فرعية وأضف كل مجلد أب إلى `FontsLookupFolder` باستخدام قائمة مفصولة بفواصل منقوطة.

### الخطوة 4: تحميل مستند HTML مع التكوين
الآن نقوم بتحميل ملف HTML الذي أنشأناه سابقًا، مع تطبيق التكوين المخصص الذي بنيناه.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

كائن `HTMLDocument` الآن يمثل الـ HTML المنسق جاهزًا للتحويل.

### الخطوة 5: تحويل HTML إلى PDF
أخيرًا، نقوم بـ **تحويل Aspose HTML إلى PDF** لإنتاج ملف PDF يحترم خطوطنا المخصصة و أنماطنا.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

كائن `PdfSaveOptions` يتيح لك تعديل إعدادات الإخراج مثل حجم الصفحة، الضغط، والبيانات الوصفية. للتحويل الأساسي، تعمل الخيارات الافتراضية بشكل مثالي.

### الخطوة 6: تنظيف الموارد
التخلص السليم يمنع تسرب الذاكرة، خاصةً عند معالجة العديد من المستندات في تطبيق يعمل لفترة طويلة.

#### 6.1 التخلص من HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 التخلص من Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

هذه الاستدعاءات تحرّر الموارد الأصلية التي خصصتها Aspose.HTML.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **الخطوط لا تظهر** | تحقق من أن مجلد `fonts` مُشار إليه بشكل صحيح ويحتوي على ملفات `.ttf`/`.otf` صالحة. استخدم مسارات مطلقة إذا كان المجلد خارج دليل المشروع. |
| **PDF يبدو فارغًا** | تأكد من أن مسار ملف HTML صحيح والملف قابل للقراءة. تحقق من أن كائن `Configuration` يُمرّر إلى مُنشئ `HTMLDocument`. |
| **استثناء الترخيص** | طبق ترخيصًا مؤقتًا أو كاملًا لـ Aspose قبل استدعاء أي واجهات برمجة تطبيقات Aspose. ضع ملف الترخيص في classpath وحمّله باستخدام `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **عرض CSS غير متوقع** | Aspose.HTML يدعم معظم CSS لكن ليس جميع الميزات الحديثة (مثل CSS Grid). بسط الأنماط أو استخدم خصائص CSS المدعومة. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام أي خط مع Aspose.HTML لـ Java؟**  
ج: نعم، أي خط TrueType (`.ttf`) أو OpenType (`.odf`) يدعمه نظام التشغيل الخاص بك يمكن استخدامه. فقط ضع الملفات في المجلد الذي حددته باستخدام `FontsLookupFolder`.

**س: هل أحتاج إلى ترخيص لاستخدام Aspose.HTML لـ Java؟**  
ج: بالرغم من أنه يمكنك تقييم المكتبة بدون ترخيص، فإن [ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/) يزيل حدود التقييم. للإنتاج، يلزم ترخيص كامل.

**س: كيف يمكنني تخصيص مخرجات PDF؟**  
ج: مرّر مثيلًا مكوّنًا من `PdfSaveOptions` إلى `convertHTML`. يمكنك ضبط حجم الصفحة، الهوامش، مستوى الضغط، وأكثر.

**س: هل من الممكن تطبيق أنماط CSS أكثر تعقيدًا؟**  
ج: نعم، Aspose.HTML يدعم مجموعة واسعة من CSS. المحددات المعقدة، استعلامات الوسائط، والصفوف الزائفة تعمل كما في المتصفح، رغم أن بعض ميزات CSS3/4 الحديثة قد لا تكون مدعومة بالكامل.

**س: أين يمكنني العثور على مزيد من الأمثلة والوثائق؟**  
ج: زر صفحة الوثائق الرسمية لـ [Aspose.HTML for Java](https://reference.aspose.com/html/java/) للحصول على مراجع API مفصلة وعينات كود إضافية.

**س: كيف يؤثر الترخيص المؤقت لـ Aspose على التحويل؟**  
ج: الترخيص المؤقت يرفع حد الـ 10 صفحات والعلامة المائية التي تظهر في وضع التقييم، مما يسمح لك باختبار سير عمل **تحويل Aspose HTML إلى PDF** بالكامل.

**آخر تحديث:** 2026-04-05  
**تم الاختبار مع:** Aspose.HTML for Java 24.12 (الأحدث وقت كتابة هذا الدليل)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}