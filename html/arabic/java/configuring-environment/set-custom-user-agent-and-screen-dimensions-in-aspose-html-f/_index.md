---
category: general
date: 2026-09-29
description: قم بتعيين وكيل مستخدم مخصص في Aspose.HTML للغة Java وتعلم كيفية ضبط حجم
  الشاشة الافتراضية للحصول على عرض HTML دقيق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: ar
lastmod: 2026-09-29
og_description: قم بتعيين وكيل مستخدم مخصص في Aspose.HTML للـ Java وتعرّف على كيفية
  ضبط حجم الشاشة الافتراضية للحصول على عرض HTML دقيق.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: تعيين وكيل مستخدم مخصص وأبعاد الشاشة في Aspose.HTML للغة Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: تعيين وكيل مستخدم مخصص وأبعاد الشاشة في Aspose.HTML لجافا
url: /ar/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين وكيل مستخدم مخصص وأبعاد الشاشة في Aspose.HTML للـ Java

إذا كنت بحاجة إلى **تعيين وكيل مستخدم مخصص** أثناء عرض HTML باستخدام Aspose.HTML للـ Java، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. من خلال تكوين sandbox ستحصل أيضًا على القدرة على **تعيين حجم الشاشة الافتراضي**، مما يضمن أن التخطيط يتطابق مع مساحة عرض المتصفح الحقيقية.

ستنتهي من هذا البرنامج التعليمي ببرنامج كامل قابل للتنفيذ يقوم **بتحديد وكيل المستخدم**، **بتعيين عرض الشاشة**، و**بتعيين ارتفاع الشاشة**. لا تحتاج إلى أدوات خارجية—فقط Aspose.HTML للـ Java وبيئة تشغيل Java 8+.

## ما ستتعلمه

* كيفية إنشاء `SandboxConfiguration` لعزل عملية العرض.
* كيفية **تعيين وكيل مستخدم مخصص** ولماذا يهم ذلك للصفحات المتجاوبة.
* كيفية **تعيين حجم الشاشة الافتراضي** (عرض الشاشة وارتفاعها) للحصول على تخطيط دقيق.
* كيفية تحميل ملف HTML داخل الـ sandbox وحفظ النتيجة المعالجة.
* المشكلات الشائعة ونصائح أفضل الممارسات للعرض داخل sandbox.

> **المتطلبات المسبقة** – تحتاج إلى ترخيص صالح لـ Aspose.HTML للـ Java، Java 8 أو أحدث، وبيئة تطوير متكاملة (IntelliJ IDEA، Eclipse، أو VS Code). يستخدم المثال ملف `input.html` محلي، لكن أي URL قابل للوصول يعمل.

![مخطط تدفق Sandbox](sandbox-flow.png "مثال تعيين وكيل مستخدم مخصص في Java")

## الخطوة 1: إنشاء تكوين sandbox (الأساس)

العزل sandbox يعزل بيئة العرض عن JVM المضيف، وهو أمر أساسي عندما تريد **تعيين وكيل مستخدم مخصص** أو تغيير حجم مساحة العرض.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*لماذا هذه الخطوة؟*  
`SandboxConfiguration` يحتوي على جميع خيارات العرض، بما في ذلك **أبعاد الشاشة** وسلاسل **user‑agent**. من خلال تكوينه قبل تحميل المستند، تضمن أن محرك HTML يحترم تلك الإعدادات من الطلب الأول.

## الخطوة 2: تعيين أبعاد الشاشة لمحاكاة جهاز حقيقي

غالبًا ما تقرأ المواقع المتجاوبة `window.innerWidth` و `window.innerHeight`. لجعل المحرك يعتقد أنه يعمل على شاشة 1024 × 768، عليك **تعيين حجم الشاشة الافتراضي**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*لماذا هذا مهم* – إذا تجاهلت **تعيين أبعاد الشاشة**، قد يستخدم العارض مساحة عرض صغيرة افتراضيًا، مما يؤدي إلى اختيار استعلامات وسائط CSS لتطبيق تخطيط الهاتف المحمول. من خلال **تعيين عرض الشاشة** و**تعيين ارتفاع الشاشة** صراحةً، تتحكم في القواعد التي تُطبق.

## الخطوة 3: تحديد سلسلة وكيل مستخدم مخصص

بعض صفحات الويب تقدم محتوى مختلف بناءً على رأس الـ user‑agent. لت **تحديد وكيل المستخدم** ببساطة قم بتعيينه في تكوين الـ sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*لماذا استخدام وكيل مستخدم مخصص؟*  
يمكن لسلسلة مخصصة تجاوز اكتشاف الروبوتات، تفعيل ميزات مخصصة لأجهزة سطح المكتب، أو اختبار كيفية تصرف الموقع لإصدار متصفح معين. يقوم محرك Aspose بتمرير هذه القيمة مع كل طلب HTTP يتم أثناء تحميل الموارد الخارجية (CSS، الصور، السكريبتات).

## الخطوة 4: تحميل مستند HTML داخل الـ sandbox

الآن بعد أن تم تكوين الـ sandbox بالكامل، قم بتحميل ملف HTML. المُنشئ الذي يأخذ مسار ملف و`SandboxConfiguration` يطبق تلقائيًا جميع الإعدادات التي عرّفناها.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

إذا كنت بحاجة للتحميل من URL بعيد، استبدل مسار الملف بسلسلة URL—ستظل Aspose.HTML تحترم **وكيل المستخدم المخصص** و**أبعاد الشاشة**.

## الخطوة 5: حفظ الناتج المعالج

بعد انتهاء تحميل المستند، يمكنك حفظه بأي تنسيق مدعوم. هنا نكتب ملف HTML داخل sandbox يعكس أي تغييرات في DOM ناتجة عن الإعدادات المخصصة.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

سيحتوي الملف المحفوظ على نفس العلامات، لكن أي سكريبتات استعلمت عن `navigator.userAgent` أو فحصت `window.innerWidth` سترى الآن القيم التي قدمتها.

## مثال كامل قابل للتنفيذ

جمع جميع الخطوات معًا يمنحك برنامجًا مستقلًا يمكنك نسخه، لصقه، وتشغيله.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينشئ `sandboxed_output.html`. إذا فتحته في متصفح وفحصت `navigator.userAgent` عبر وحدة التحكم، سترى **AsposeHTML/1.0**. بالمثل، سيظهر `window.innerWidth` القيمة **1024**، مما يؤكد أن **تعيين أبعاد الشاشة** عمل كما هو مقصود.

## أسئلة شائعة ومعالجة الحالات الطرفية

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو قامت الصفحة بتحميل موارد إضافية من نطاق مختلف؟** | يقوم الـ sandbox بتمرير **وكيل المستخدم المخصص** مع كل طلب، لكن سياسات المصدر المتقاطع لا تزال سارية. استخدم `sandboxConfig.setAllowCrossDomain(true)` إذا كنت بحاجة لتخفيف تلك القيود. |
| **هل يمكنني تغيير حجم الشاشة بعد تحميل المستند؟** | لا. تُقرأ أبعاد الشاشة أثناء تمريرة التخطيط الأولية. لتصوير بحجم مختلف، أنشئ `SandboxConfiguration` جديدًا وأعد تحميل المستند. |
| **هل أحتاج إلى استدعاء `document.close()`؟** | `HTMLDocument` يطبق `AutoCloseable`. استخدام كتلة try‑with‑resources يضمن التنظيف المناسب، لكن استدعاء `close()` صريح اختياري في السكريبتات البسيطة. |
| **كيف يختلف هذا عن تعيين وكيل المستخدم في عميل HTTP؟** | تعيين وكيل المستخدم على الـ sandbox يؤثر على **جميع** طلبات الموارد التي يقوم بها محرك HTML، وليس فقط طلب HTML الأولي. هذا يحاكي المتصفح الحقيقي بشكل أقرب. |
| **هل الـ sandbox آمن للـ HTML غير الموثوق به؟** | نعم. الـ sandbox يعزل الوصول إلى نظام الملفات ويحد من المكالمات الشبكية وفقًا للتكوين، مما يقلل من خطر السكريبتات الخبيثة التي تؤثر على JVM المضيف. |

## نصائح احترافية

* **إعادة استخدام التكوينات** – إذا قمت بعرض العديد من الصفحات بنفس مساحة العرض، أنشئ `SandboxConfiguration` واحدًا وأعد استخدامه لتجنب عبء إنشاء الكائنات.
* **التصحيح باستخدام السجلات** – فعّل سجلات Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) لتعرف أي موارد تم جلبها باستخدام وكيل المستخدم المخصص.
* **الدمج مع استعلامات وسائط CSS** – من خلال تعديل **تعيين عرض الشاشة** يمكنك اختبار سلوك التصميم المتجاوب على الأجهزة اللوحية، الهواتف، أو شاشات الحواسيب الكبيرة دون فتح متصفح حقيقي.

## الخلاصة

أنت الآن تعرف كيف **تعيين وكيل مستخدم مخصص** و**تعيين أبعاد الشاشة** عند عرض HTML باستخدام Aspose.HTML للـ Java. من خلال تكوين sandbox، تعزل البيئة، تتحكم في مساحة العرض، وتضمن أن الموارد الخارجية ترى رؤوس الطلبات التي تحددها بالضبط. هذه التقنية أساسية لاختبار التخطيطات المتجاوبة، تجاوز حواجز الروبوتات، أو إعادة إنتاج ميزات سطح المكتب فقط في خطوط الأنابيب الآلية.

بعد ذلك، قد تستكشف **كيفية تعيين ملفات تعريف الارتباط المخصصة** أو **التقاط لقطات شاشة مُصدرة** باستخدام واجهة برمجة تطبيقات العرض في Aspose.HTML—كلا المفهومين يبنيان على نمط تكوين sandbox نفسه الذي تعلمته الآن.

برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [العرض بدقة DPI عالية في Java – التقاط لقطات شاشة للويب مع وكيل مستخدم مخصص](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [كيفية تحميل HTML، تعيين DPI للجهاز وقراءة لون الخلفية](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [إنشاء ملف HTML في Java وإعداد خدمة الشبكة (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}