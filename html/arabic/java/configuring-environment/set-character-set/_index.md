---
date: 2026-02-04
description: تعلم كيفية تعيين مجموعة الأحرف في Aspose.HTML للغة Java، وتحويل HTML
  إلى PDF، وضمان الترميز الصحيح للنص وعرضه بشكل سليم.
linktitle: Set Character Set in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: كيفية تعيين مجموعة الأحرف في Aspose.HTML للـ Java
url: /ar/java/configuring-environment/set-character-set/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين مجموعة الأحرف في Aspose.HTML لـ Java

## المقدمة
إذا كنت تعمل مع مستندات HTML في Java، فإن **معرفة كيفية تعيين مجموعة الأحرف** بشكل صحيح أمر أساسي لضمان الترميز الصحيح للنص وعرضه بشكل سليم. في هذا الدليل خطوة بخطوة سنستعرض كيفية تكوين مجموعة الأحرف باستخدام Aspose.HTML لـ Java، ثم نوضح لك كيفية **تحويل HTML إلى PDF** بحيث يكون الناتج مطابقًا تمامًا لما تريد. فهم **كيفية تعيين مجموعة الأحرف** يساعدك على تجنب النص المشوش عند إجراء تحويل *HTML إلى PDF Java*.

## إجابات سريعة
- **ماذا يعني “charset”؟** يحدد ترميز الأحرف (مثل ISO‑8859‑1، UTF‑8) المستخدم لتفسير النص في المستند.  
- **لماذا نعين charset في Aspose.HTML؟** لضمان أن الأحرف الخاصة تُعرض بشكل صحيح عند تحويل HTML إلى PDF أو صيغ أخرى.  
- **ما هي مجموعة الأحرف المستخدمة في هذا المثال؟** `ISO‑8859‑1` (يتم تعيينها عبر `setCharSet`).  
- **هل يمكنني تحويل HTML إلى PDF بعد تعيين مجموعة الأحرف؟** نعم – ينتهي الدليل بتحويل إلى PDF باستخدام `Converter.convertHTML`.  
- **هل أحتاج إلى ترخيص؟** تتوفر نسخة تجريبية مجانية؛ يلزم وجود ترخيص تجاري للاستخدام في بيئة الإنتاج.

## كيفية تعيين مجموعة الأحرف في Aspose.HTML لـ Java
تعيين مجموعة الأحرف خطوة صغيرة لكنها حاسمة قبل بدء **تحويل Aspose.HTML إلى PDF**. فيما يلي نوضح العملية في خطوات مرقمة واضحة لتتمكن من المتابعة دون فقدان أي تفاصيل.

## ما هي مجموعة الأحرف ولماذا تهم؟
مجموعة الأحرف (character set) تربط تسلسلات البايتات بالأحرف القابلة للقراءة. استخدام مجموعة أحرف غير صحيحة قد يفسد النص، خاصةً للغات التي تحتوي على أحرف مُعَلمة أو نصوص غير لاتينية. تعيين مجموعة الأحرف الصحيحة يضمن أن يتم تحليل HTML كما قصده المؤلف، وهو أمر أساسي عندما تقوم لاحقًا **بإنشاء PDF من HTML**.

## لماذا نعين مجموعة الأحرف عند تحويل HTML إلى PDF في Java؟
- **عرض دقيق** – تظهر الأحرف كما صُممت تمامًا، دون تشويش.  
- **دعم التعريب** – يمكنك التعامل بأمان مع مجموعات الأحرف ISO‑8859‑1، UTF‑8، Windows‑1252، وغيرها.  
- **نتائج ثابتة** – عملية *تحويل Aspose.HTML إلى PDF* تحترم مجموعة الأحرف التي تحددها، مما يمنحك نتائج متوقعة عبر المنصات المختلفة.

## المتطلبات المسبقة
قبل الغوص في الشيفرة، تأكد من توفر ما يلي:

1. **Java Development Kit (JDK)** – أي نسخة حديثة من JDK (8+). حمّلها من [موقع Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – احصل على أحدث مكتبة من [صفحة إصدارات Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA، Eclipse، أو أي بيئة تطوير Java تفضلها.

## استيراد الحزم
نحتاج فقط إلى استيراد واحد للمثال، لكن فئات Aspose.HTML يتم الإشارة إليها مباشرة لاحقًا.

```java
import java.io.IOException;
```

تتضمن هذه الاستيرادات جميع الفئات الأساسية التي ستحتاجها لـ **java set character set**، ومعالجة مستند HTML، وتحويله إلى PDF.

## الخطوة 1: إنشاء كود HTML
أولاً، أنشئ ملف HTML بسيط سنقوم بمعالجته لاحقًا.

```java
String code = "<h1>Character Set</h1>\r\n" +
    "<p>The <b>CharSet</b> property sets the primary character-set for a document.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

- **محتوى HTML** – المتغيّر `code` يحتوي على مقتطف HTML بسيط يتضمن عنوانًا وفقرة.  
- **FileWriter** – يكتب سلسلة HTML إلى `document.html`، لتصبح مصدر التحويل.

## الخطوة 2: تكوين مجموعة الأحرف
الآن نقوم بإنشاء كائن `Configuration` سيحمل إعداداتنا المخصصة.

```java
// Create an instance of Configuration
Configuration configuration = new Configuration();
```

فئة `Configuration` هي نقطة الدخول لتخصيص طريقة تحليل وعرض مستندات Aspose.HTML.

## الخطوة 3: الوصول إلى خدمة وكيل المستخدم وتعديلها
يتم تعريف مجموعة الأحرف عبر `IUserAgentService`. هنا نوضح أيضًا استدعاء **set iso-8859-1 encoding**.

```java
try {
    // Get the IUserAgentService
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set ISO-8859-1 encoding to parse the document
    userAgent.setCharSet("ISO-8859-1");
```

- **IUserAgentService** – تدير إعدادات مستوى وكيل المستخدم، بما في ذلك مجموعة الأحرف.  
- **setCharSet** – يطبق مجموعة الأحرف `ISO‑8859‑1`، مما يضمن تفسير HTML بشكل صحيح.

## الخطوة 4: تهيئة مستند HTML
بعد تكوين مجموعة الأحرف، قم بتحميل ملف HTML باستخدام نفس كائن `Configuration`.

```java
    // Initialize an HTML document with the specified configuration
    HTMLDocument document = new HTMLDocument("document.html", configuration);
```

الآن يمثل `HTMLDocument` الملف المصدر، تم تحليله باستخدام مجموعة الأحرف `ISO‑8859‑1`.

## الخطوة 5: تحويل HTML إلى PDF
أخيرًا، حوّل المستند إلى PDF. هذا يُظهر **aspose html convert pdf** عمليًا.

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

- **Converter.convertHTML** – ينفّذ التحويل الفعلي إلى PDF.  
- **PdfSaveOptions** – يتيح لك تعديل إعدادات PDF إذا لزم الأمر.  
- **تنظيف الموارد** – استدعاءات `dispose()` تُحرّر الموارد الأصلية، مما يمنع تسرب الذاكرة.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| أحرف مشوشة في PDF | تعيين مجموعة أحرف خاطئة (مثل UTF‑8 الافتراضي) | استخدم `userAgent.setCharSet("ISO-8859-1")` أو مجموعة الأحرف المناسبة لمصدر النص. |
| `NullPointerException` على `document` | تم إتلاف `configuration` قبل استخدام المستند | تأكد من استدعاء `configuration.dispose()` **بعد** الانتهاء من استخدام `HTMLDocument`. |
| فقدان الخطوط | مجموعة الأحرف المستهدفة تتطلب خطوطًا غير مثبتة | ثبّت الخط المطلوب أو دمجه عبر `PdfSaveOptions` (مثال: `setEmbedStandardFonts(true)`). |

## الأسئلة المتكررة

**س: ما هي مجموعة الأحرف، ولماذا هي مهمة؟**  
ج: مجموعة الأحرف تربط قيم البايت بالأحرف. استخدام مجموعة الأحرف الصحيحة يمنع فساد النص، خاصةً للغات غير ASCII.

**س: هل يمكنني استخدام مجموعة أحرف مختلفة عن ISO‑8859‑1؟**  
ج: بالطبع. يدعم Aspose.HTML العديد من الترميزات (UTF‑8، Windows‑1252، وغيرها). ما عليك سوى استبدال `"ISO-8859-1"` بالقيمة المطلوبة في `setCharSet`.

**س: هل يمكن تحويل صيغ أخرى غير PDF؟**  
ج: نعم. يمكن لـ Aspose.HTML تحويل HTML إلى XPS، DOCX، PNG، JPEG، وغيرها عبر استبدال `PdfSaveOptions` بفئة خيارات الحفظ المناسبة.

**س: هل يجب أن أتعامل مع تنظيف الموارد يدويًا؟**  
ج: رغم أن جامع القمامة في Java يساعد، يُفضَّل استدعاء `dispose()` على `Configuration` و`HTMLDocument` لتحرير الموارد الأصلية فورًا.

**س: أين يمكنني الحصول على نسخة تجريبية مجانية من Aspose.HTML لـ Java؟**  
ج: حمّل نسخة تجريبية من [صفحة إصدارات Aspose](https://releases.aspose.com/).

## الخلاصة
أنت الآن تعرف **كيفية تعيين مجموعة الأحرف** في Aspose.HTML لـ Java وكيفية **تحويل HTML إلى PDF** مع الترميز الصحيح. التعامل السليم مع مجموعة الأحرف أمر حيوي للتعريب ويضمن أن تمثّل ملفات PDF الخاصة بك المحتوى الأصلي بدقة. لا تتردد في تجربة مجموعات أحرف أخرى أو صيغ إخراج مختلفة لتناسب احتياجات مشروعك، سواء كنت تقوم بسير عمل *HTML إلى PDF Java* أو تحويل أوسع **Aspose HTML PDF conversion**.

---

**آخر تحديث:** 2026-02-04  
**تم الاختبار مع:** Aspose.HTML for Java 24.12 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}