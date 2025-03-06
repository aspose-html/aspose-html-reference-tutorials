---
title: تعيين جدول أنماط المستخدم في Aspose.HTML لـ Java
linktitle: تعيين جدول أنماط المستخدم في Aspose.HTML لـ Java
second_title: معالجة HTML باستخدام Java مع Aspose.HTML
description: تعرف على كيفية تعيين جدول أنماط مستخدم مخصص في Aspose.HTML لـ Java، وتحسين تصميم المستندات وتحويل HTML إلى PDF بسهولة.
weight: 16
url: /ar/java/configuring-environment/set-user-style-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين جدول أنماط المستخدم في Aspose.HTML لـ Java

## مقدمة
هل سبق لك أن وجدت نفسك ترغب في تعديل مظهر مستندات HTML الخاصة بك بأسلوبك الفريد؟ تخيل أنك تقوم بإنشاء صفحة ويب، وتريد التأكد من ظهور العناوين بلون معين أو أن الفقرات لها مظهر متناسق عبر الأجهزة المختلفة. هنا يأتي دور أوراق أنماط المستخدم! في هذا البرنامج التعليمي، سنستكشف كيفية تعيين ورقة أنماط مستخدم مخصصة باستخدام Aspose.HTML لـ Java. سواء كنت تتطلع إلى إنشاء تصميم متماسك لمستنداتك أو مجرد تجربة أنماط مختلفة، فإن هذا الدليل سيرشدك خلال العملية بأكملها بطريقة بسيطة وجذابة.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل، دعنا نتأكد من أن لديك كل ما تحتاجه للمتابعة:
1.  Aspose.HTML لمكتبة Java: إذا لم تقم بتنزيلها بالفعل، فيمكنك تنزيلها من[صفحة إصدارات Aspose](https://releases.aspose.com/html/java/).
2. مجموعة تطوير Java (JDK): تأكد من تثبيت JDK 8 أو أعلى على جهازك.
3. بيئة التطوير المتكاملة (IDE): استخدم بيئة التطوير المتكاملة مثل IntelliJ IDEA، أو Eclipse، أو NetBeans لكتابة وتشغيل كود Java الخاص بك.
4. المعرفة الأساسية بلغة HTML وCSS: إن معرفة القليل من لغة HTML وCSS سوف تساعدك على فهم عملية التصميم بشكل أفضل.

## استيراد الحزم
للبدء في استخدام Aspose.HTML لـ Java، ستحتاج إلى استيراد الحزم الضرورية. ستتيح لك هذه الاستيرادات إنشاء مستندات HTML ومعالجتها، وتكوين خدمة وكيل المستخدم، ومعالجة التحويلات.
```java
import java.io.IOException;
```
## الخطوة 1: إنشاء مستند HTML
أولاً، ستحتاج إلى إنشاء مستند HTML حيث يمكنك تطبيق جدول الأنماط المخصص. تتضمن هذه الخطوة كتابة كود HTML بسيط إلى ملف.
 ستبدأ بكتابة بعض أكواد HTML الأساسية في ملف يسمى`document.html`سيكون هذا الملف بمثابة الأساس لأنماطك المخصصة.
```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```
 هنا، تقوم بإنشاء ملف HTML بسيط يحتوي على عنوان وفقرة.`FileWriter` يستخدم لكتابة هذا الكود في`document.html`.
## الخطوة 2: إعداد التكوين
تتضمن الخطوة التالية إعداد تكوين يسمح لك بتخصيص جدول أنماط المستخدم. يتم ذلك باستخدام`com.aspose.html.Configuration` فصل.
 يجب عليك إنشاء مثيل لـ`Configuration` فئة للوصول إلى الخدمات المختلفة التي يوفرها Aspose.HTML لـ Java.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```
ستعمل نسخة التكوين هذه بمثابة العمود الفقري لتطبيق الأنماط المخصصة.
## الخطوة 3: الوصول إلى خدمة وكيل المستخدم
 بمجرد إعداد التكوين، فإن الخطوة التالية هي الوصول إلى`IUserAgentService`. هذه الخدمة ضرورية لتعيين جدول الأنماط المخصص.
 باستخدام مثيل التكوين، سوف تسترد`IUserAgentService` الذي يسمح لك بتحديد الأنماط المخصصة.
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```
 هنا،`getService` يتم استخدام الطريقة للحصول على خدمة وكيل المستخدم، والتي سيتم استخدامها في الخطوة التالية لتطبيق الأنماط المخصصة.
## الخطوة 4: تحديد جدول أنماط المستخدم وتطبيقه
 الآن، حان الوقت لتحديد أنماط CSS المخصصة وتطبيقها على مستند HTML باستخدام`IUserAgentService`.

يمكنك تحديد أنماطك المخصصة باستخدام CSS ثم تعيين هذه الأنماط على`userAgent` خدمة.
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```
في هذا المثال، العنوان (`h1`) تم تصميمه بلون بني وحجم خط أكبر، بينما تم تصميم الفقرة (`p`) له خلفية فاتحة ونص رمادي. ثم يتم تعيين جدول الأنماط المخصص هذا لخدمة وكيل المستخدم.
## الخطوة 5: تهيئة مستند HTML باستخدام التكوين
بعد إعداد ورقة الأنماط المخصصة، تكون الخطوة التالية هي تهيئة مستند HTML باستخدام التكوين المحدد.

 سوف تقوم بإنشاء مثيل جديد لـ`HTMLDocument`، عن طريق تمرير مسار الملف والتكوين.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```
تطبق عملية التهيئة هذه ورقة أنماط المستخدم المخصصة على مستند HTML، مما يضمن انعكاس كافة الأنماط عند عرض المستند أو تحويله.
## الخطوة 6: تحويل HTML إلى PDF
أخيرًا، قد ترغب في تحويل مستند HTML المصمم إلى تنسيق مختلف، مثل PDF. يجعل Aspose.HTML for Java عملية التحويل هذه سهلة ومباشرة.

يمكنك بسهولة تحويل مستند HTML إلى PDF باستخدام`Converter` فصل.
```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```
 في هذه الخطوة،`convertHTML` تأخذ الطريقة المستند وبعض خيارات الحفظ واسم ملف الإخراج كمعلمات، وتحويل ملف HTML إلى ملف PDF مع الأنماط المطبقة.
## الخطوة 7: تنظيف الموارد
بعد التحويل، من الضروري تنظيف الموارد لتجنب تسرب الذاكرة.

 تأكد من التخلص منها`HTMLDocument` و`Configuration` الحالات بمجرد الانتهاء منها.
```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```
تضمن هذه الخطوة تحرير كافة الموارد بشكل صحيح، مما يحافظ على كفاءة تطبيقك.

## خاتمة
تهانينا! لقد نجحت في تعيين جدول أنماط مستخدم مخصص في Aspose.HTML for Java، وتطبيقه على مستند HTML، وتحويل هذا المستند إلى ملف PDF. تتيح لك هذه الميزة القوية التحكم الكامل في شكل مستندات HTML الخاصة بك، مما يجعلها أداة أساسية للمطورين الذين يعملون على إنشاء محتوى الويب أو أتمتة المستندات. سواء كنت مطورًا متمرسًا أو مبتدئًا، فإن هذا الدليل من شأنه أن يساعدك على الشعور بمزيد من الراحة عند استخدام Aspose.HTML for Java لتحسين تنسيق المستندات الخاصة بك.
## الأسئلة الشائعة
### هل يمكنني تطبيق أنماط مختلفة لعناصر HTML المختلفة؟  
بالتأكيد! يمكنك تحديد عدد الأنماط الذي تريده لعناصر HTML المختلفة في جدول أنماط المستخدم الخاص بك.
### ماذا لو كنت بحاجة إلى تغيير ورقة الأنماط بشكل ديناميكي؟  
بإمكانك تعديل جدول أنماط المستخدم في أي وقت قبل عرض المستند أو تحويله.
### هل من الممكن استخدام ملفات CSS خارجية مع Aspose.HTML لـ Java؟  
نعم، يمكنك ربط ملفات CSS الخارجية تمامًا كما تفعل في مستند HTML العادي.
### كيف يتعامل Aspose.HTML for Java مع خصائص CSS غير المدعومة؟  
يتم تجاهل خصائص CSS غير المدعومة ببساطة، مما يسمح بتطبيق بقية جدول الأنماط الخاص بك دون أخطاء.
### هل يمكنني تحويل HTML إلى تنسيقات أخرى غير PDF؟  
نعم، يدعم Aspose.HTML for Java تحويل HTML إلى تنسيقات مختلفة، بما في ذلك XPS، وTIFF، والمزيد.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
