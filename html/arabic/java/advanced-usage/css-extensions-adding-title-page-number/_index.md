---
date: 2025-12-05
description: تعلم كيفية ضبط هوامش صفحة HTML في Java باستخدام Aspose.HTML، وإضافة أرقام
  الصفحات والعناوين إلى مستنداتك.
language: ar
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: كيفية ضبط هوامش صفحة HTML في Java باستخدام Aspose.HTML
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين هوامش صفحة HTML في Java باستخدام Aspose.HTML

## إجابات سريعة
- **ما المكتبة المطلوبة؟** Aspose.HTML for Java  
- **هل يمكنني التحكم في الهوامش برمجياً؟** نعم، عبر قاعدة CSS `@page` في ورقة الأنماط الخاصة بالمستخدم  
- **ما صيغ الإخراج التي تدعم الهوامش؟** XPS، PDF، وغيرها من صيغ الرسوم النقطية  
- **هل أحتاج إلى ترخيص للاستخدام الإنتاجي؟** يلزم وجود ترخيص Aspose.HTML صالح للاستخدام غير التجريبي  
- **هل هذا متوافق مع Java 11+؟** بالتأكيد – المكتبة تعمل مع إصدارات Java الحديثة  

## ما هو “تعيين هوامش صفحة HTML في Java”؟
تعني تعيين هوامش صفحة HTML في Java ضبط محرك العرض (الموفر من قبل Aspose.HTML) لتطبيق خصائص صندوق الصفحة CSS قبل تحويل المستند إلى صيغة قابلة للطباعة مثل XPS أو PDF. من خلال تعريف قاعدة `@page` مخصصة يمكنك التحكم في منطقة الطباعة، أرقام الصفحات، ومحتوى الرأس/التذييل.

## لماذا نستخدم Aspose.HTML للتحكم في الهوامش؟
- **تخطيط دقيق** – CSS `@page` يمنحك تحكمًا دقيقًا بالبكسل في الهوامش والرؤوس والتذييلات.  
- **اتساق عبر الصيغ** – تعريفات الهوامش نفسها تعمل مع XPS، PDF، ومخرجات الصور.  
- **بدون اعتماد على المتصفح** – يتم العرض على جانب الخادم، لذا لا تحتاج إلى متصفح بدون واجهة.  

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

1. **بيئة تطوير Java** – JDK 11 أو أحدث مثبتة.  
2. **Aspose.HTML for Java** – قم بتحميل وتثبيت المكتبة من [here](https://releases.aspose.com/html/java/).  

## استيراد الحزم

للبدء، استورد الفئات اللازمة من Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## كيفية تعيين هوامش صفحة HTML في Java – دليل خطوة بخطوة

### الخطوة 1: تهيئة الإعدادات وتعريف هوامش الصفحة المخصصة

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

في هذا الجزء نقوم بإنشاء كائن `Configuration`، الحصول على `IUserAgentService`، وإدخال قاعدة CSS `@page` التي تحدد الهوامش، عداد الصفحة في أسفل اليمين، وعنوان المستند في أعلى الوسط.

### الخطوة 2: إنشاء مستند HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

هنا نقوم بإنشاء كائن `HTMLDocument` مع مقتطف بسيط “Hello World”. يتم تطبيق نفس التكوين من الخطوة 1، لذا يتم احترام الهوامش المخصصة عند عرض المستند.

### الخطوة 3: العرض إلى ملف XPS (أو أي إخراج مدعوم)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

تقوم هذه الخطوة بإنشاء `XpsDevice` يكتب الصفحات المعروضة إلى `output.xps`. ستظهر الهوامش، أرقام الصفحات، والعنوان الذي حددته مسبقًا في الملف النهائي.

## مشاكل شائعة ونصائح

- **الهوامش لا تتغير** – تأكد من عدم تجاوز قاعدة `@page` بواسطة أوراق أنماط أخرى. استدعاء `setUserStyleSheet` يجبرها على أن تكون ذات أولوية قصوى.  
- **أرقام الصفحات تظهر “NaN”** – تحقق من أنك تستخدم Aspose.HTML الإصدار 23.10 أو أحدث؛ الإصدارات الأقدم لا تحتوي على دالة `currentPageNumber()`.  
- **ملف الإخراج فارغ** – تأكد من أن مسار `Resources.output` يتم حله بشكل صحيح وأن لديك أذونات كتابة.  

## الأسئلة المتكررة

### س1: ما هو Aspose.HTML for Java؟
**ج:** Aspose.HTML for Java هي مكتبة Java توفر أدوات قوية للعمل مع مستندات HTML في تطبيقات Java، بما في ذلك التحويل، العرض، والتلاعب.

### س2: هل يمكنني تخصيص هوامش الصفحة أكثر؟
**ج:** نعم، فقط قم بتحرير CSS داخل `setUserStyleSheet`. يمكنك تغيير أي من قيم `margin-*` أو إضافة صناديق `@top-*` / `@bottom-*` إضافية.

### س3: كيف يمكنني إضافة محتوى إضافي إلى مستند HTML؟
**ج:** استبدل السلسلة في `new HTMLDocument("<div>Hello World!!!</div>", …)` بترميز HTML الخاص بك، أو حمّل ملفًا خارجيًا باستخدام المُنشئ `HTMLDocument(String url, …)`.

### س4: هل Aspose.HTML for Java متوافق مع صيغ مستندات أخرى؟
**ج:** بالتأكيد. يمكن عرض نفس `HTMLDocument` إلى PDF، XPS، صور، أو حتى EPUB عن طريق تبديل جهاز الإخراج (مثل `PdfDevice`، `PngDevice`).

### س5: هل أحتاج إلى ترخيص لاستخدام Aspose.HTML for Java؟
**ج:** نعم، يلزم وجود ترخيص للاستخدام الإنتاجي. يمكنك الحصول على نسخة تجريبية أو شراء ترخيص من [here](https://purchase.aspose.com/buy) أو [here](https://releases.aspose.com/).

### س6: كيف يمكنني تعيين هوامش مختلفة للصفحات الفردية والزوجية؟
**ج:** استخدم الفئات الزائفة `@page :left` و `@page :right` داخل ورقة الأنماط لتحديد هوامش مميزة للصفحات اليسرى (الزوجية) واليمنى (الفردية).

### س7: هل يمكنني تضمين خطوط مخصصة في المستند المعروض؟
**ج:** نعم. أضف قواعد `@font-face` إلى ورقة الأنماط الخاصة بالمستخدم وارجع إلى الخطوط في محتوى HTML الخاص بك.

## الخلاصة

لقد أتقنت الآن **كيفية تعيين هوامش صفحة HTML في Java** باستخدام Aspose.HTML، وتعرف كيف تضيف أرقام الصفحات وعنوانًا لجعل مستنداتك تبدو احترافية. لا تتردد في تجربة صناديق `@page` إضافية، خطوط مخصصة، أو صيغ إخراج مختلفة لتلبية احتياجات مشروعك.

إذا واجهت أي تحديات، فإن الوثائق الرسمية لـ [Aspose.HTML for Java](https://reference.aspose.com/html/java/) ومنتدى الدعم الخاص بـ [Aspose](https://forum.aspose.com/) هما أماكن ممتازة للحصول على المساعدة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---