---
date: 2026-02-04
description: تعلم كيفية استخدام Aspose.HTML لتكوين الخطوط، وتطبيق CSS مخصص، واستخدام
  ترخيص مؤقت، وإنشاء PDF من HTML في Java.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: كيفية استخدام Aspose.HTML لتكوين الخطوط لتحويل HTML إلى PDF في Java
url: /ar/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تكوين الخطوط لتحويل HTML‑to‑PDF في Java باستخدام Aspose.HTML

## المقدمة
في هذا البرنامج التعليمي ستكتشف **كيفية استخدام Aspose.HTML** لتكوين الخطوط لتحويل HTML إلى PDF في Java. عند العمل مع مستندات HTML، يضمن إعداد الخطوط الصحيحة أن يبدو ملف PDF الناتج مطابقًا تمامًا للصفحة الويب الأصلية—مع الحفاظ على ألوان العلامة التجارية، والطباعة، والتخطيط. سواء كنت تبني تقارير، فواتير، أو أي خط أنابيب لتوليد المستندات، فإن تكوين الخطوط بشكل صحيح هو المفتاح للحصول على ملفات PDF ذات مظهر احترافي. دعنا نتبع العملية بالكامل، من إعداد البيئة إلى تحويل HTML إلى PDF باستخدام خطوط مخصصة وCSS.

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا البرنامج التعليمي؟** تكوين الخطوط لتحويل HTML‑to‑PDF في Java باستخدام Aspose.HTML.  
- **أي مكتبة تتولى عملية التحويل؟** Aspose.HTML for Java (فئة `Converter`).  
- **هل أحتاج إلى ترخيص؟** ترخيص Aspose المؤقت يزيل حدود التقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **أين يجب وضع الخطوط المخصصة؟** في مجلد يُشار إليه بـ `FontsLookupFolder`، مثل مجلد `fonts` بجوار مشروعك.  
- **هل يمكنني تخصيص مخرجات PDF؟** نعم—استخدم `PdfSaveOptions` لضبط حجم الصفحة، الهوامش، والمزيد.

## كيفية استخدام Aspose.HTML لتكوين الخطوط
سوف نشرح أدناه لماذا يعتبر التعامل مع الخطوط مهمًا، وكيفية تطبيق CSS مخصص، وكيفية **استخدام ترخيص مؤقت** لفتح جميع الوظائف أثناء اختبار الحل.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من توفر ما يلي:

1. **Java Development Kit (JDK) 1.8+** – الكود يعمل على أي JDK حديث.  
2. **Aspose.HTML for Java** – حمّل أحدث ملف JAR من [موقع Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA، Eclipse، أو أي محرر يدعم Java.  
4. **معرفة أساسية بـ Java** – يجب أن تكون مرتاحًا مع الفئات، الطرق، وملفات الإدخال/الإخراج.  
5. **ترخيص Aspose.HTML** – [ترخيص مؤقت](https://purchase.aspose.com/temporary-license/) سيزيل قيود التقييم.

## استيراد الحزم
أولاً، استورد فئات Java الأساسية وفئات Aspose.HTML التي ستحتاجها.  

```java
import java.io.IOException;
```

تمنحك هذه الاستيرادات إمكانية الوصول إلى معالجة الملفات وواجهة برمجة تطبيقات Aspose.HTML.

## ما هو **html to pdf java** ولماذا يعتبر تكوين الخطوط مهمًا؟
عملية **html to pdf java** تقوم بتحويل مستند HTML إلى صفحة PDF. الخطوط جزء أساسي من عملية العرض لأنها تؤثر على التخطيط، وتباعد الأسطر، والدقة البصرية. من خلال توجيه Aspose.HTML إلى مجلد خطوط مخصص، تضمن أن يستخدم PDF الخطوط الدقيقة التي صممتها للصفحة الويب، مما يلغي الخطوط الاحتياطية ويحافظ على اتساق العلامة التجارية.

## دليل خطوة بخطوة

### الخطوة 1: إنشاء محتوى HTML
سنبدأ بإنشاء ملف HTML بسيط سنقوم لاحقًا بتحويله إلى PDF.

#### 1.1 كتابة كود HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

تُعرّف هذه الشريحة عنوانًا وفقرة. يمكنك توسيع HTML بإضافة المزيد من العناصر إذا رغبت في اختبار أنماط إضافية.

#### 1.2 حفظ HTML إلى ملف
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

يقوم `FileWriter` بكتابة السلسلة إلى `user-agent-fontsetting.html` في مجلد مشروعك. بعد هذه الخطوة ستحصل على ملف HTML فعلي جاهز للمعالجة.

### الخطوة 2: تكوين بيئة Aspose.HTML
الآن سنقوم بإعداد كائن `Configuration` الخاص بـ Aspose.HTML، والذي يتيح لنا التحكم في طريقة عرض HTML.

#### 2.1 إنشاء نسخة من Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

كائن `Configuration` هو نقطة الدخول لتخصيص خيارات العرض مثل معالجة الخطوط وسلوك وكيل المستخدم.

#### 2.2 الوصول إلى خدمة وكيل المستخدم
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

تدير `IUserAgentService` أوراق الأنماط، الخطوط، وتفاصيل العرض الأخرى. سنستخدمها لإدخال CSS مخصص وتحديد مجلد الخطوط الخاص بنا.

### الخطوة 3: تطبيق الأنماط والخطوط المخصصة
مع إعداد البيئة جاهزًا، يمكننا الآن إضافة قواعد CSS وإخبار Aspose.HTML بمكان وجود الخطوط.

#### 3.1 تعيين CSS مخصص
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

يقوم هذا الـ CSS بتلوين العنوان باللون البني والفقرة بالرمادي. يمكنك إضافة أي قواعد CSS صالحة هنا—يدعم Aspose.HTML مواصفة CSS2.1 بالكامل والعديد من ميزات CSS3. *(هذا مثال على **apply custom css**.)*

#### 3.2 الإشارة إلى مجلد الخطوط المخصص
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

ضع أي ملفات `.ttf` أو `.otf` تريد استخدامها داخل مجلد باسم `fonts` يقع في جذر مشروعك. سيقوم Aspose.HTML بتحميل هذه الخطوط تلقائيًا أثناء العرض.

> **نصيحة احترافية:** إذا كان لديك عدة عائلات خطوط، حافظ على تنظيمها في مجلدات فرعية وأضف كل مجلد أصل إلى `FontsLookupFolder` باستخدام قائمة مفصولة بفواصل منقوطة.

### الخطوة 4: تحميل مستند HTML مع التكوين
الآن نقوم بتحميل ملف HTML الذي أنشأناه مسبقًا، مع تطبيق التكوين المخصص الذي بنيناه.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

يمثل كائن `HTMLDocument` الآن HTML المُنسق جاهزًا للتحويل.

### الخطوة 5: تحويل HTML إلى PDF
أخيرًا، نقوم بأداء **aspose html pdf conversion** لإنتاج ملف PDF يحترم خطوطنا وأنماطنا المخصصة.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

يتيح لك كائن `PdfSaveOptions` ضبط إعدادات الإخراج مثل حجم الصفحة، الضغط، والبيانات الوصفية. بالنسبة للتحويل الأساسي، تعمل الإعدادات الافتراضية بشكل مثالي.

### الخطوة 6: تنظيف الموارد
التخلص السليم يمنع تسرب الذاكرة، خاصةً عند معالجة مستندات متعددة في تطبيق طويل التشغيل.

#### 6.1 تحرير HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 تحرير Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

تُحرّر هذه الاستدعاءات الموارد الأصلية التي خصصها Aspose.HTML.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **الخطوط لا تظهر** | تأكد من أن مجلد `fonts` مُشار إليه بشكل صحيح ويحتوي على ملفات `.ttf`/`.otf` صالحة. استخدم مسارات مطلقة إذا كان المجلد خارج دليل المشروع. |
| **PDF يظهر فارغًا** | تحقق من صحة مسار ملف HTML وأن الملف قابل للقراءة. تأكد من تمرير كائن `Configuration` إلى مُنشئ `HTMLDocument`. |
| **استثناء الترخيص** | طبّق ترخيصًا مؤقتًا أو كاملًا قبل استدعاء أي من واجهات Aspose. ضع ملف الترخيص في مسار الـ classpath وحمّله باستخدام `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **عرض CSS غير متوقع** | يدعم Aspose.HTML معظم CSS لكنه لا يدعم جميع الميزات الحديثة (مثل CSS Grid). بسط الأنماط أو استخدم خصائص CSS مدعومة. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام أي خط مع Aspose.HTML for Java؟**  
ج: نعم، أي خط TrueType (`.ttf`) أو OpenType (`.otf`) يدعمه نظام التشغيل يمكن استخدامه. ما عليك سوى وضع الملفات في المجلد الذي تحدده بـ `FontsLookupFolder`.

**س: هل أحتاج إلى ترخيص لاستخدام Aspose.HTML for Java؟**  
ج: يمكنك تقييم المكتبة بدون ترخيص، لكن [ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/) يزيل حدود التقييم. للإنتاج، يلزم ترخيص كامل.

**س: كيف يمكنني تخصيص مخرجات PDF؟**  
ج: مرّر كائن `PdfSaveOptions` المكوَّن إلى `convertHTML`. يمكنك ضبط حجم الصفحة، الهوامش، مستوى الضغط، والمزيد.

**س: هل يمكن تطبيق أنماط CSS أكثر تعقيدًا؟**  
ج: نعم، يدعم Aspose.HTML مجموعة واسعة من CSS. تعمل المحددات المعقدة، استعلامات الوسائط، والصفوف الزائفة كما في المتصفح، رغم أن بعض ميزات CSS3/4 الحديثة قد لا تكون مدعومة بالكامل.

**س: أين يمكنني العثور على مزيد من الأمثلة والوثائق؟**  
ج: زر صفحة [توثيق Aspose.HTML for Java الرسمية](https://reference.aspose.com/html/java/) للحصول على مراجع API مفصلة وعينات كود إضافية.

**س: كيف يؤثر الترخيص المؤقت لـ Aspose على التحويل؟**  
ج: يرفع الترخيص المؤقت حد الـ 10 صفحات والعلامة المائية التي تظهر في وضع التقييم، مما يسمح لك باختبار سير عمل **aspose html pdf conversion** بالكامل.

---

**آخر تحديث:** 2026-02-04  
**تم الاختبار مع:** Aspose.HTML for Java 24.12 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}