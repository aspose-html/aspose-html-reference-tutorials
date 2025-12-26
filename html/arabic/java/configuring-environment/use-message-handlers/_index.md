---
date: 2025-12-10
description: تعلم كيفية استخدام Aspose لمعالجة الروابط المكسورة في Java، وتحويل HTML
  إلى PNG، وتحميل مستند HTML في Java باستخدام Aspose.HTML for Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: كيفية استخدام معالجات رسائل Aspose.HTML في جافا
url: /ar/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام معالجات الرسائل Aspose.HTML في Java

## مقدمة
في هذا الدرس، يتم توضيح **كيفية استخدام aspose** لمعالجة الموارد المفقودة في HTML خطوة بخطوة. سنقوم بإنشاء مستند HTML بسيط يشير إلى صورة مفقودة، نرفق معالج رسائل مخصص، ونظهر لك كيفية **load html document java** مع التعامل السلس مع الروابط المعطوبة. في النهاية، سترى أيضًا كيفية **convert html to png** باستخدام Aspose.HTML، مما يمنحك صورة كاملة عن تحويل HTML إلى صورة في Java.

## إجابات سريعة
- **ما هو الغرض الأساسي من معالج الرسائل؟** اعتراض عمليات الشبكة والتفاعل مع رموز الحالة مثل الموارد المفقودة.  
- **هل يمكن لـ Aspose.HTML تحويل HTML إلى PNG؟** نعم، باستخدام `Converter.convertHTML` يمكنك إجراء تحويل HTML إلى صورة.  
- **هل أحتاج إلى ترخيص لهذا المثال؟** الترخيص المؤقت يزيل حدود التقييم؛ الترخيص الدائم مطلوب للإنتاج.  
- **ما نسخة Java المدعومة؟** أي JDK 8+ (الدرس يستخدم JDK 11).  
- **هل من الممكن معالجة روابط معطوبة متعددة؟** بالتأكيد – يمكنك ربط عدة معالجات لإدارة سيناريوهات مختلفة.

## المتطلبات المسبقة
1. Java Development Kit (JDK): تأكد من تثبيت JDK على نظامك. يمكنك تنزيله من [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: تحتاج إلى تثبيت Aspose.HTML for Java. يمكنك تنزيله من [Aspose releases page](https://releases.aspose.com/html/java/).
3. IDE: استخدم بيئة التطوير المتكاملة المفضلة لديك مثل IntelliJ IDEA أو Eclipse أو NetBeans.
4. معرفة أساسية بـ Java: الإلمام ببرمجة Java ضروري لمتابعة هذا الدرس بفعالية.
5. ترخيص مؤقت: إذا كنت تستخدم النسخة التجريبية من Aspose.HTML، فكر في الحصول على [temporary license](https://purchase.aspose.com/temporary-license/) لتجنب أي قيود أثناء التطوير.

## استيراد الحزم
قبل أن نبدأ، تأكد من استيراد الحزم الضرورية إلى مشروع Java الخاص بك. فيما يلي الاستيرادات الأساسية التي ستحتاجها:
```java
import java.io.IOException;
```
هذه الاستيرادات ستمنحك الوصول إلى الفئات والطرق المطلوبة لمعالجة عمليات الشبكة، إنشاء مستندات HTML، وإجراء تحويل HTML إلى PNG.

## الخطوة 1: إعداد كود HTML
أول شيء نحتاجه هو مقطع HTML بسيط يشير إلى ملف صورة. سنشير عمدًا إلى صورة غير موجودة لتفعيل آلية معالجة الأخطاء.
```java
String code = "<img src='missing.jpg'>";
```
هذا الكود ينشئ وسم `<img>` يشير إلى `missing.jpg`. نظرًا لأن الصورة مفقودة، ستعيد خدمة الشبكة رمز حالة غير 200، والذي سيلتقطه معالجنا المخصص.

## الخطوة 2: كتابة كود HTML إلى ملف
بعد ذلك، نحتاج إلى حفظ مقطع HTML حتى يتمكن Aspose.HTML من تحميله كمستند.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
باستخدام `FileWriter` نحفظ HTML إلى **document.html**. يصبح هذا الملف المصدر لخطوة **load html document java** لاحقًا.

## الخطوة 3: إنشاء معالج رسائل مخصص
الآن لننشئ معالج رسائل مخصص يتفاعل عندما لا يمكن العثور على الصورة. يتحقق المعالج من رمز حالة HTTP ويطبع رسالة ودية.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
طريقة `invoke` تفحص `context.getResponse().getStatusCode()`. إذا لم يكن **200**، نطبع تحذير واضح بأن الملف مفقود. الاستدعاء النهائي `invoke(context);` يمرر التحكم إلى المعالج التالي في السلسلة.

## الخطوة 4: تكوين خدمة الشبكة
لجعل Aspose.HTML على علم بمعالجنا، نقوم بتسجيله مع خدمة الشبكة عبر فئة `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
هنا ننشئ كائن `Configuration`، نسترجع `INetworkService`، ونضيف معالجنا المخصص إلى مجموعته. هذا يضمن تشغيل المعالج أثناء أي طلب شبكة، مثل تحميل الصور.

## الخطوة 5: تحميل مستند HTML
مع جاهزية التكوين، يمكننا الآن تحميل ملف HTML الذي أنشأناه مسبقًا. توضح هذه الخطوة **load html document java** بينما تُفعّل الصورة المفقودة معالجنا.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
منشئ `HTMLDocument` يستقبل كلًا من مسار الملف و`configuration` المخصص. عندما يحلل المستند وسم `<img>`، تحاول خدمة الشبكة جلب `missing.jpg`، تتلقى 404، ويطبع معالجنا التحذير.

## الخطوة 6: تحويل HTML إلى PNG
لتوضيح القدرات الأوسع لـ Aspose.HTML، سنحول المستند المحمل إلى صورة PNG. هذا سيناريو كلاسيكي لـ **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` يأخذ `HTMLDocument`، و`ImageSaveOptions` اختيارية (حيث يمكنك ضبط DPI، الجودة، إلخ)، واسم ملف الإخراج. النتيجة هي صورة نقطية للـ HTML المرسوم.

## الخطوة 7: تنظيف الموارد
إدارة الموارد بشكل صحيح أمر أساسي في أي تطبيق Java. نقوم بتحرير كل من `Configuration` و`HTMLDocument` لتجنب تسرب الذاكرة.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
تغليف عملية التنظيف داخل كتلة `finally` يضمن تنفيذها حتى إذا حدث استثناء في وقت سابق.

## لماذا نستخدم معالجات الرسائل؟
معالجات الرسائل تمنحك تحكمًا دقيقًا في عمليات الشبكة مثل **handle broken links java**. بدلاً من السماح للمكتبة بالفشل صامتًا، يمكنك تسجيل الأخطاء، إعادة المحاولة، استبدال الموارد، أو توفير محتوى احتياطي—مما يجعل معالجة HTML قوية وجاهزة للإنتاج.

## المشكلات الشائعة والحلول
- **تكرار المعالج** – تأكد من استدعاء `invoke(context);` مرة واحدة فقط لتجنب الحلقات اللانهائية.  
- **ترخيص مفقود** – بدون ترخيص صالح، قد ينتج عن التحويل صورة مائية.  
- **أخطاء مسار الملف** – استخدم مسارات مطلقة أو اضبط دليل العمل بشكل صحيح عند تحميل `document.html`.

## الأسئلة المتكررة

**س: هل يمكنني ربط عدة معالجات رسائل؟**  
ج: نعم، يمكنك إضافة عدة معالجات إلى مجموعة `network.getMessageHandlers()`؛ سيتم تنفيذها بالترتيب الذي أضيفت فيه.

**س: هل يعمل المعالج مع موارد CSS أو السكريبت أيضًا؟**  
ج: بالتأكيد—أي طلب شبكة يتم بواسطة محرك HTML (صور، CSS، JS، خطوط) يمر عبر المعالج.

**س: كيف يمكنني تعديل طلب HTTP قبل إرساله؟**  
ج: نفّذ معالجًا يغيّر `context.getRequest()` قبل استدعاء `invoke(context)`.

**س: هل هناك طريقة لتجاهل التحذير لعناوين URL محددة؟**  
ج: داخل المعالج، افحص `context.getRequest().getRequestUri()` وتخطى السجل بشكل شرطي.

**س: ما نسخة Aspose.HTML المطلوبة لهذه الواجهات البرمجية؟**  
ج: يعمل الكود مع Aspose.HTML for Java 22.10 وما بعده.

## الخلاصة
وهنا لديك دليل شامل حول **كيفية استخدام aspose** لمعالجات الرسائل في Java. غطينا إنشاء ملف HTML، ربط معالج مخصص بـ **handle broken links java**، تحميل المستند، وإجراء **convert html to png**. باستخدام هذا النمط يمكنك إدارة الموارد المفقودة بثقة، فرض سياسات مخصصة، وتوسيع قدرات الشبكة في Aspose.HTML في أي تطبيق Java.

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}