---
date: 2025-12-03
description: تعلم كيفية تكوين الخطوط لتحويل HTML إلى PDF باستخدام Java و Aspose.HTML.
  إنشاء PDF من HTML باستخدام خطوط مخصصة، ورخصة Aspose مؤقتة، وإعدادات تحويل متقدمة.
language: ar
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: تكوين الخطوط لتحويل HTML إلى PDF في Java باستخدام Aspose.HTML
url: /java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تكوين الخطوط لـ HTML إلى PDF Java باستخدام Aspose.HTML

## المقدمة
عند العمل مع مستندات HTML في Java، يُعد تكوين الخطوط بشكل صحيح أمرًا أساسيًا لإنشاء تحويلات **html to pdf java** جذابة بصريًا وسهلة القراءة. سواءً كنت تُنشئ تقارير، تبني صفحات ويب، أو تُحول مستندات، فإن إعداد الخط المناسب يمكن أن يُحدث فرقًا كبيرًا في جودة ملف PDF النهائي. في هذا الدليل سنستعرض العملية بالكامل — من إعداد بيئة التطوير إلى تحويل HTML إلى PDF باستخدام خطوط مخصصة — حتى تتمكن من إنتاج ملفات PDF بمظهر احترافي ببضع أسطر من الشيفرة. هيا نبدأ!

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا الدرس؟** تكوين الخطوط لتحويل HTML إلى PDF في Java باستخدام Aspose.HTML.  
- **أي مكتبة تتولى عملية التحويل؟** Aspose.HTML for Java (فئة `Converter`).  
- **هل أحتاج إلى ترخيص؟** ترخيص Aspose المؤقت يزيل قيود التقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **أين يجب وضع الخطوط المخصصة؟** في مجلد يُشار إليه بـ `FontsLookupFolder`، مثل مجلد `fonts` بجوار مشروعك.  
- **هل يمكنني تخصيص مخرجات PDF؟** نعم — استخدم `PdfSaveOptions` لضبط حجم الصفحة، الهوامش، والمزيد.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من توفر ما يلي:

1. **Java Development Kit (JDK) 1.8+** – الشيفرة تعمل على أي JDK حديث.  
2. **Aspose.HTML for Java** – حمّل أحدث JAR من [موقع Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA، Eclipse، أو أي محرر يدعم Java.  
4. **معرفة أساسية بـ Java** – يجب أن تكون مرتاحًا مع الفئات، الأساليب، وملفات الإدخال/الإخراج.  
5. **ترخيص Aspose.HTML** – [ترخيص مؤقت](https://purchase.aspose.com/temporary-license/) سيزيل قيود التقييم.

## استيراد الحزم
أولاً، استورد فئات Java الأساسية وفئات Aspose.HTML التي ستحتاجها.  
```java
import java.io.IOException;
```
هذه الاستيرادات تمنحك الوصول إلى معالجة الملفات وواجهة Aspose.HTML API.

## ما هو **html to pdf java** ولماذا يهم تكوين الخطوط؟
عملية **html to pdf java** تُحوّل مستند HTML إلى صفحة PDF. الخطوط جزء أساسي من عملية العرض لأنها تؤثر على التخطيط، تباعد الأسطر، والدقة البصرية. من خلال توجيه Aspose.HTML إلى مجلد خطوط مخصص، تضمن أن يستخدم PDF الخطوط الدقيقة التي صممتها لصفحة الويب، متجنبًا الخطوط الاحتياطية وحافظًا على تناسق العلامة التجارية.

## دليل خطوة بخطوة

### الخطوة 1: إنشاء محتوى HTML
سنبدأ بإنشاء ملف HTML بسيط سنحوّله لاحقًا إلى PDF.

#### 1.1 كتابة شيفرة HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```
هذه القطعة تُعرّف عنوانًا وفقرة. يمكنك توسيع HTML بإضافة المزيد من العناصر إذا رغبت في اختبار أنماط إضافية.

#### 1.2 حفظ HTML إلى ملف
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```
يكتب `FileWriter` السلسلة إلى `user-agent-fontsetting.html` في مجلد مشروعك. بعد هذه الخطوة ستحصل على ملف HTML فعلي جاهز للمعالجة.

### الخطوة 2: تكوين بيئة Aspose.HTML
الآن سنُعد كائن `Configuration` الخاص بـ Aspose.HTML، والذي يتيح لنا التحكم في طريقة عرض HTML.

#### 2.1 إنشاء نسخة من Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```
كائن `Configuration` هو نقطة الدخول لتخصيص خيارات العرض مثل معالجة الخطوط وسلوك وكيل المستخدم.

#### 2.2 الوصول إلى خدمة وكيل المستخدم
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```
`IUserAgentService` تُدير أوراق الأنماط، الخطوط، وتفاصيل العرض الأخرى. سنستخدمها لإدخال CSS مخصص وتحديد مجلد الخطوط الخاص بنا.

### الخطوة 3: تطبيق الأنماط والخطوط المخصصة
مع إعداد البيئة، يمكننا الآن إضافة قواعد CSS وإخبار Aspose.HTML بمكان وجود الخطوط.

#### 3.1 تعيين CSS مخصص
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```
هذا الـ CSS يُلون العنوان باللون البني والفقرة بالرمادي. يمكنك إضافة أي قواعد CSS صالحة هنا — Aspose.HTML يدعم مواصفة CSS2.1 بالكامل والعديد من ميزات CSS3.

#### 3.2 الإشارة إلى مجلد الخطوط المخصص
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```
ضع أي ملفات `.ttf` أو `.otf` تريد استخدامها داخل مجلد اسمه `fonts` في جذر مشروعك. سيقوم Aspose.HTML بتحميل هذه الخطوط تلقائيًا أثناء العرض.

> **نصيحة احترافية:** إذا كان لديك عائلات خطوط متعددة، رتبها في مجلدات فرعية وأضف كل مجلد أصل إلى `FontsLookupFolder` باستخدام قائمة مفصولة بفواصل منقوطة.

### الخطوة 4: تحميل مستند HTML مع التكوين
الآن نحمل ملف HTML الذي أنشأناه مسبقًا، مع تطبيق التكوين المخصص الذي بنيناه.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```
كائن `HTMLDocument` الآن يمثل HTML المُنسق جاهزًا للتحويل.

### الخطوة 5: تحويل HTML إلى PDF
أخيرًا، نقوم بتنفيذ **aspose html pdf conversion** لإنتاج ملف PDF يحترم خطوطنا المخصصة وأنماطنا.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```
كائن `PdfSaveOptions` يتيح لك تعديل إعدادات الإخراج مثل حجم الصفحة، الضغط، والبيانات الوصفية. للتحويل الأساسي، الإعدادات الافتراضية تعمل بشكل مثالي.

### الخطوة 6: تنظيف الموارد
التصريف السليم يمنع تسرب الذاكرة، خاصةً عند معالجة مستندات متعددة في تطبيق طويل التشغيل.

#### 6.1 تصريف HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 تصريف Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```
هذه الاستدعاءات تُحرّر الموارد الأصلية التي خصصتها Aspose.HTML.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **الخطوط لا تظهر** | تأكد من أن مجلد `fonts` مُشار إليه بشكل صحيح ويحتوي على ملفات `.ttf`/`.otf` صالحة. استخدم مسارات مطلقة إذا كان المجلد خارج دليل المشروع. |
| **PDF يظهر فارغًا** | تحقق من صحة مسار ملف HTML وأن الملف قابل للقراءة. تأكد من تمرير كائن `Configuration` إلى مُنشئ `HTMLDocument`. |
| **استثناء الترخيص** | طبّق ترخيصًا مؤقتًا أو كاملاً قبل استدعاء أي من واجهات Aspose. ضع ملف الترخيص في classpath وحمّله بـ `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **عرض CSS غير متوقع** | Aspose.HTML يدعم معظم CSS لكنه لا يدعم جميع الميزات الحديثة (مثل CSS Grid). بسط الأنماط أو استخدم خصائص CSS مدعومة. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام أي خط مع Aspose.HTML for Java؟**  
ج: نعم، أي خط TrueType (`.ttf`) أو OpenType (`.otf`) يدعمه نظام التشغيل يمكن استخدامه. ما عليك سوى وضع الملفات في المجلد الذي تحدده بـ `FontsLookupFolder`.

**س: هل أحتاج إلى ترخيص لاستخدام Aspose.HTML for Java؟**  
ج: يمكنك تجربة المكتبة بدون ترخيص، لكن [ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/) يزيل قيود التقييم. للإنتاج، يلزم ترخيص كامل.

**س: كيف يمكنني تخصيص مخرجات PDF؟**  
ج: مرّر كائن `PdfSaveOptions` مُكوّن إلى `convertHTML`. يمكنك ضبط حجم الصفحة، الهوامش، مستوى الضغط، وأكثر.

**س: هل يمكن تطبيق أنماط CSS أكثر تعقيدًا؟**  
ج: نعم، Aspose.HTML يدعم مجموعة واسعة من CSS. المحددات المعقدة، استعلامات الوسائط، والصفوف الزائفة تعمل كما في المتصفح، رغم أن بعض ميزات CSS3/4 الحديثة قد لا تكون مدعومة بالكامل.

**س: أين يمكنني العثور على المزيد من الأمثلة والوثائق؟**  
ج: زر صفحة [توثيق Aspose.HTML for Java الرسمية](https://reference.aspose.com/html/java/) للحصول على مراجع API مفصلة وعينات شيفرة إضافية.

**س: كيف يؤثر الترخيص المؤقت على عملية التحويل؟**  
ج: الترخيص المؤقت يرفع حد الـ 10 صفحات والعلامة المائية التي تظهر في وضع التقييم، مما يتيح لك اختبار سير عمل **aspose html pdf conversion** بالكامل.

## الخلاصة
تكوين الخطوط لـ **html to pdf java** باستخدام Aspose.HTML طريقة بسيطة لكنها قوية لضمان أن تحتفظ ملفات PDF بالمظهر والملمس الدقيق لصفحات الويب الخاصة بك. من خلال إعداد مجلد خطوط مخصص، وتطبيق CSS عبر خدمة وكيل المستخدم، والاستفادة من المحول المدمج، يمكنك إنشاء ملفات PDF عالية الجودة ببضع أسطر من الشيفرة فقط. سواءً كنت تبني تقارير، فواتير، أو أي خط أنابيب لتوليد المستندات، فإن هذا النهج يمنحك سيطرة كاملة على الطباعة والتخطيط.

---  
**آخر تحديث:** 2025-12-03  
**تم الاختبار مع:** Aspose.HTML for Java 24.12 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}