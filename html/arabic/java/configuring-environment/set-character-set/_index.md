---
date: 2025-12-04
description: تعلم كيفية تعيين مجموعة الأحرف في Aspose.HTML للغة Java، وتحويل HTML
  إلى PDF، وضمان الترميز الصحيح للنص وعرضه.
linktitle: Set Character Set in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: كيفية تعيين مجموعة الأحرف في Aspose.HTML للـ Java
url: /ar/java/configuring-environment/set-character-set/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين مجموعة الأحرف في Aspose.HTML للـ Java

## مقدمة
إذا كنت تعمل مع مستندات HTML في Java، فإن **معرفة كيفية تعيين مجموعة الأحرف** بشكل صحيح أمر أساسي لضمان ترميز النص وعرضه بشكل سليم. في هذا الدليل خطوة بخطوة، سنستعرض كيفية تكوين مجموعة الأحرف باستخدام Aspose.HTML للـ Java، ثم نوضح لك كيفية **تحويل HTML إلى PDF** بحيث يكون المخرجات مطابقة تمامًا لما هو مقصود.

## إجابات سريعة
- **ماذا يعني “charset”؟** يحدد ترميز الأحرف (مثال: ISO‑8859‑1، UTF‑8) المستخدم لتفسير النص في المستند.  
- **لماذا يتم تعيين مجموعة الأحرف في Aspose.HTML؟** لضمان عرض الأحرف الخاصة بشكل صحيح عند تحويل HTML إلى PDF أو صيغ أخرى.  
- **ما هي مجموعة الأحرف المستخدمة في هذا المثال؟** `ISO‑8859‑1` (تم تعيينها عبر `setCharSet`).  
- **هل يمكنني تحويل HTML إلى PDF بعد تعيين مجموعة الأحرف؟** نعم – ينتهي الدليل بتحويل إلى PDF باستخدام `Converter.convertHTML`.  
- **هل أحتاج إلى ترخيص؟** تتوفر نسخة تجريبية مجانية؛ ويتطلب الاستخدام في الإنتاج ترخيصًا تجاريًا.

## ما هي مجموعة الأحرف ولماذا هي مهمة؟
مجموعة الأحرف (character set) تقوم بربط تسلسلات البايتات بالأحرف القابلة للقراءة. استخدام مجموعة أحرف غير صحيحة قد يؤدي إلى تشويه النص، خاصةً للغات التي تحتوي على أحرف مُعَلَّقة أو نصوص غير لاتينية. تعيين مجموعة الأحرف الصحيحة يضمن أن يتم تحليل HTML تمامًا كما قصده المؤلف، وهو أمر حاسم عندما تقوم لاحقًا **بإنشاء PDF من HTML**.

## المتطلبات المسبقة
قبل الغوص في الشيفرة، تأكد من توفر ما يلي:

1. **مجموعة تطوير Java (JDK)** – أي نسخة حديثة من JDK (8+). قم بالتنزيل من [موقع Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML للـ Java** – احصل على أحدث مكتبة من [صفحة إصدارات Aspose](https://releases.aspose.com/html/java/).  
3. **بيئة التطوير المتكاملة (IDE)** – IntelliJ IDEA أو Eclipse أو أي بيئة تطوير متوافقة مع Java تفضلها.

## استيراد الحزم
نحتاج فقط إلى استيراد واحد للمثال، لكن فئات Aspose.HTML سيتم الإشارة إليها مباشرة لاحقًا.

```java
import java.io.IOException;
```

تتضمن هذه الاستيرادات جميع الفئات الأساسية التي ستحتاجها لتعيين مجموعة الأحرف، ومعالجة مستند HTML، وتحويله إلى PDF.

## الخطوة 1: إنشاء شفرة HTML
أولاً، أنشئ ملف HTML بسيط سنقوم بمعالجته لاحقًا.

```java
String code = "<h1>Character Set</h1>\r\n" +
    "<p>The <b>CharSet</b> property sets the primary character-set for a document.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

- **محتوى HTML** – المتغير `code` يحتوي على مقطع HTML بسيط يتضمن عنوانًا وفقرة.  
- **FileWriter** – يكتب سلسلة HTML إلى `document.html`، والتي تصبح المصدر لتحويلنا.

## الخطوة 2: تكوين مجموعة الأحرف
الآن نقوم بإنشاء كائن `Configuration` الذي سيحمل إعداداتنا المخصصة.

```java
// Create an instance of Configuration
Configuration configuration = new Configuration();
```

فئة `Configuration` هي نقطة الدخول لتخصيص طريقة تحليل وعرض المستندات بواسطة Aspose.HTML.

## الخطوة 3: الوصول إلى خدمة وكيل المستخدم وتعديلها
يتم تعريف مجموعة الأحرف عبر `IUserAgentService`. هنا نوضح أيضًا استدعاء **set iso-8859-1 encoding**.

```java
try {
    // Get the IUserAgentService
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set ISO-8859-1 encoding to parse the document
    userAgent.setCharSet("ISO-8859-1");
```

- **IUserAgentService** – يدير إعدادات مستوى وكيل المستخدم، بما في ذلك مجموعة الأحرف.  
- **setCharSet** – يطبق مجموعة الأحرف `ISO‑8859‑1`، مما يضمن تفسير HTML بشكل صحيح.

## الخطوة 4: تهيئة مستند HTML
بعد تكوين مجموعة الأحرف، قم بتحميل ملف HTML باستخدام نفس كائن `Configuration`.

```java
    // Initialize an HTML document with the specified configuration
    HTMLDocument document = new HTMLDocument("document.html", configuration);
```

`HTMLDocument` الآن يمثل ملف المصدر، تم تحليله باستخدام مجموعة الأحرف `ISO‑8859‑1`.

## الخطوة 5: تحويل HTML إلى PDF
أخيرًا، قم بتحويل المستند إلى PDF. هذا يوضح **aspose html convert pdf** عمليًا.

```java
    try {
        // Convert HTML to PDF
        Converter.convertHTML(
                document,
                new PdfSaveOptions(),
                "user-agent-charset_out.pdf"
        );
    } finally {
        if (document != null) {
            document.dispose();
        }
    }
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- **Converter.convertHTML** – ينفذ التحويل الفعلي إلى PDF.  
- **PdfSaveOptions** – يتيح لك تعديل إعدادات PDF إذا لزم الأمر.  
- **تنظيف الموارد** – استدعاءات `dispose()` تحرر الموارد الأصلية، مما يمنع تسرب الذاكرة.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| حروف مشوشة في PDF | تم تعيين مجموعة أحرف خاطئة (مثال: UTF‑8 الافتراضي) | استخدم `userAgent.setCharSet("ISO-8859-1")` أو مجموعة الأحرف المناسبة لمصدر الملف. |
| `NullPointerException` على `document` | `configuration` تم إلغاؤه قبل استخدام المستند | تأكد من استدعاء `configuration.dispose()` **بعد** الانتهاء من استخدام `HTMLDocument`. |
| خطوط مفقودة | مجموعة الأحرف المستهدفة تتطلب خطوطًا غير مثبتة | قم بتثبيت الخط المطلوب أو تضمينه عبر `PdfSaveOptions` (مثال: `setEmbedStandardFonts(true)`). |

## الأسئلة المتكررة

**س: ما هي مجموعة الأحرف، ولماذا هي مهمة؟**  
ج: مجموعة الأحرف تربط قيم البايتات بالأحرف. استخدام مجموعة الأحرف الصحيحة يمنع تشويه النص، خاصةً للغات غير ASCII.

**س: هل يمكنني استخدام مجموعة أحرف مختلفة عن ISO‑8859‑1؟**  
ج: بالتأكيد. يدعم Aspose.HTML العديد من الترميزات (UTF‑8، Windows‑1252، إلخ). ما عليك سوى استبدال `"ISO-8859-1"` بالقيمة المطلوبة في `setCharSet`.

**س: هل يمكن تحويل صيغ أخرى غير PDF؟**  
ج: نعم. يمكن لـ Aspose.HTML تحويل HTML إلى XPS، DOCX، PNG، JPEG، وغيرها عبر استبدال `PdfSaveOptions` بفئة خيارات الحفظ المناسبة.

**س: هل يجب التعامل مع تنظيف الموارد يدويًا؟**  
ج: رغم أن جامع القمامة في Java يساعد، يجب عليك استدعاء `dispose()` صراحةً على `Configuration` و `HTMLDocument` لتحرير الموارد الأصلية فورًا.

**س: أين يمكنني الحصول على نسخة تجريبية مجانية من Aspose.HTML للـ Java؟**  
ج: قم بتنزيل نسخة تجريبية من [صفحة إصدارات Aspose](https://releases.aspose.com/).

## الخلاصة
أنت الآن تعرف **كيفية تعيين مجموعة الأحرف** في Aspose.HTML للـ Java وكيفية **تحويل HTML إلى PDF** باستخدام الترميز الصحيح. التعامل السليم مع مجموعة الأحرف أمر حيوي للتعريب ويضمن أن تمثل ملفات PDF الخاصة بك المحتوى الأصلي لـ HTML بدقة. لا تتردد في تجربة مجموعات أحرف أخرى أو صيغ إخراج مختلفة لتلبية احتياجات مشروعك.

**آخر تحديث:** 2025-12-04  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.12 (أحدث نسخة عند كتابة هذا الدليل)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}