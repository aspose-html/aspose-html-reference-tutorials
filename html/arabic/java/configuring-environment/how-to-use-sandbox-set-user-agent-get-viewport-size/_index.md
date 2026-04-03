---
category: general
date: 2026-04-03
description: تعرّف على كيفية استخدام sandbox في Aspose.HTML Java لتعيين وكيل المستخدم،
  وتعيين الحجم، والحصول على حجم نافذة العرض فورًا. يتضمن الكود الكامل، والشروحات،
  والنصائح.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: ar
og_description: تعلم كيفية استخدام sandbox في Aspose.HTML Java لتعيين وكيل المستخدم،
  وتحديد الحجم، والحصول على حجم نافذة العرض فورًا. دليل كامل مع الشيفرة وأفضل الممارسات.
og_title: كيفية استخدام Sandbox – تعيين وكيل المستخدم والحصول على حجم العرض
tags:
- AsposeHTML
- Java
- Sandbox
title: كيفية استخدام Sandbox – تعيين وكيل المستخدم والحصول على حجم نافذة العرض
url: /ar/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Sandbox – تعيين وكيل المستخدم والحصول على حجم نافذة العرض

هل تساءلت يومًا **كيفية استخدام sandbox** عند عرض HTML باستخدام Aspose.HTML for Java؟ ربما واجهت صعوبة في محاكاة حجم شاشة محدد أو تحتاج إلى تزوير سلسلة وكيل المستخدم حتى يتصرف الموقع كما لو أنه يُزار من متصفح هاتف محمول.  

الخبر السار هو أن واجهة برمجة تطبيقات sandbox تتيح لك فعل ذلك بالضبط، ويمكنك أيضًا استخراج حجم نافذة العرض المحسوب بعد تحميل الصفحة. في هذا الدرس سنستعرض إنشاء sandbox، ضبط الحجم، تعيين وكيل مستخدم مخصص، تحميل صفحة عن بُعد، وأخيرًا قراءة أبعاد نافذة العرض. في النهاية ستعرف **كيفية تعيين الحجم**، **كيفية الحصول على نافذة العرض**، ولماذا هذه الخطوات مهمة للحصول على عرض رأسية موثوق.

> **فوز سريع:** ستحصل على فئة Java قابلة للتنفيذ تطبع شيئًا مثل `Viewport: 1280×800` في ثوانٍ.

---

## ما ستحتاجه

- **Aspose.HTML for Java** الإصدار 24.6 أو أحدث (الواجهة التي نستخدمها تم تقديمها في 24.5).  
- مجموعة تطوير Java 17+ (أي JDK حديث يعمل).  
- بيئة تطوير متكاملة أو محرر نصوص بسيط—لا تحتاج إلى إضافات خاصة.  
- اتصال بالإنترنت إذا أردت تحميل عنوان URL خارجي مثل `https://example.com`.

هذا كل شيء. لا يلزم أي سحر Maven/Gradle؛ يمكنك إيداع ملفات JAR على مسار الفئة يدويًا إذا فضلت ذلك.  

---

## كيفية استخدام Sandbox – نظرة عامة

يعزل sandbox محرك العرض عن نظام التشغيل المضيف، مما يتيح لك تعريف شاشة افتراضية (العرض، الارتفاع، DPI) وسلسلة **وكيل المستخدم** مخصصة. فكر فيه كنافذة متصفح مصغرة تعيش بالكامل في الذاكرة. عندما تطلب لاحقًا من `HTMLDocument` العرض الافتراضي، يُبلغ المحرك عن **حجم نافذة العرض** الذي حسبه بناءً على إعدادات sandbox.  

فيما يلي تدفق عالي المستوى:

1. **إنشاء** `DocumentSandbox` وتكوين العرض، الارتفاع، DPI، ووكيل المستخدم.  
2. **تحميل** `HTMLDocument` داخل ذلك sandbox.  
3. **استعلام** العرض الافتراضي للمستند للحصول على حجم نافذة العرض.  

لنغص في كل خطوة.

---

## الخطوة 1: إنشاء Sandbox وتعيين الحجم

أولاً، نقوم بإنشاء sandbox ونخبره بحجم الشاشة الافتراضية. هنا تجيب على سؤال **كيفية تعيين الحجم** للعرض بدون رأسية.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **نصيحة محترف:** إذا كنت تختبر تخطيطًا استجابياً، جرّب عرضًا ضيقًا مثل `360` لمحاكاة هاتف، أو عرضًا واسعًا مثل `1920` لسطح مكتب. يحترم sandbox قيمة DPI التي تحددها، لذا فإن شاشة عالية الكثافة (مثلاً 144 DPI) ستؤثر على استعلامات الوسائط التي تستخدم `device-pixel-ratio`.

---

## الخطوة 2: تعيين وكيل المستخدم للـ Sandbox

لماذا نهتم بـ **وكيل المستخدم** المخصص؟ بعض المواقع تقدم تعليمات برمجية أو سكريبتات مختلفة بناءً على المتصفح المُبلغ عنه. عبر استدعاء `setUserAgent` يمكنك إقناع الصفحة بأنها تُزار من Chrome أو Firefox أو جهاز محمول.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

الآن ستعتقد الصفحة أنها تُعرض على iPhone. إذا احتجت إلى **تعيين وكيل المستخدم** إلى الإعداد الافتراضي مرة أخرى، ما عليك سوى إعادة استخدام السلسلة السابقة “AsposeHTML/24.6 …”.

---

## الخطوة 3: تحميل مستند HTML داخل الـ Sandbox

مع جاهزية sandbox، يمكننا تحميل أي عنوان URL أو ملف HTML محلي. يأخذ مُنشئ `HTMLDocument` الـ sandbox كمعامل ثانٍ، مما يربط الاثنين معًا.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

يضمن كتلة `try‑with‑resources` التخلص من المستند بشكل صحيح، محرّرًا الموارد الأصلية التي يخصصها Aspose.HTML في الخلفية.

---

## الخطوة 4: الحصول على حجم نافذة العرض من المستند

هذه هي اللحظة التي انتظرتها: استخراج **حجم نافذة العرض** الذي حسبه محرك العرض. هذا يجيب على سؤال **كيفية الحصول على نافذة العرض** بعد ترتيب الصفحة.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
Viewport: 1280×800
```

إذا غيرت أبعاد sandbox في الخطوة 1، ستعكس الأرقام المطبوعة القيم الجديدة—مثالي لاختبارات آلية تتحقق من نقاط الانكسار الاستجابية.

---

## مثال كامل يعمل

فيما يلي الفئة الكاملة الجاهزة للتنفيذ التي تجمع كل الأجزاء معًا. انسخها والصقها في ملف باسم `SandboxExample.java`، أضف ملفات JAR الخاصة بـ Aspose.HTML إلى مسار الفئة، ونفّذ `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**الناتج المتوقع** (مع افتراض إعدادات sandbox المذكورة أعلاه):

```
Viewport: 1280×800
```

إذا عينت عرضًا/ارتفاعًا مختلفًا في sandbox، سيتغير الناتج وفقًا لذلك—تمامًا ما تحتاجه عند اختبار تصاميم استجابية.

---

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو استخدمت الصفحة `window.innerWidth` بدلاً من استعلامات CSS؟

حجم الشاشة الافتراضية في sandbox يؤثر على كل من تخطيط CSS و`window.innerWidth/innerHeight` في JavaScript. لذا فإن **كيفية الحصول على نافذة العرض** عبر JavaScript ستُعيد نفس الأرقام التي تراها في وحدة تحكم Java.

### هل يمكن تشغيل عدة sandboxes بالتوازي؟

نعم. كل نسخة من `DocumentSandbox` مستقلة، لذا يمكنك إنشاء مجموعة من الخيوط، ومنح كل خيط sandbox خاص به بأبعاد مختلفة، وعرض عشرات الصفحات في وقت واحد. فقط تذكّر أن تحافظ على أمان ملفات JAR في بيئة متعددة الخيوط (هي كذلك).

### هل يؤثر إعداد DPI على تكبير الصور؟

بالطبع. DPI أعلى يجعل بكسل CSS واحد يطابق المزيد من بكسلات الجهاز، مما قد يجعل الصور عالية الدقة تظهر أكثر وضوحًا. إذا كنت تختبر موارد بنمط Retina، جرّب `sandbox.setDeviceDpi(144)`.

### كيف أتعامل مع شهادات HTTPS ذاتية التوقيع

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}