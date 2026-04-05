---
category: general
date: 2026-03-25
description: تعيين رأس التفويض وتحميل HTML من عنوان URL باستخدام Aspose.HTML في Java.
  تعلّم كيفية تعيين رأس القبول، وتكوين رؤوس مخصصة، وإضافة رؤوس HTTP بأسلوب Java.
draft: false
keywords:
- set authorization header
- load html from url
- set accept header
- configure custom headers
- add http headers java
language: ar
og_description: قم بتعيين رأس التفويض بسرعة وأمان. يوضح هذا الدليل كيفية تحميل HTML
  من عنوان URL، وتعيين رأس القبول، وتكوين رؤوس مخصصة، وإضافة رؤوس HTTP باستخدام Java.
og_title: تعيين رأس التفويض في جافا – تحميل HTML من عنوان URL
tags:
- Java
- HTTP
- Aspose.HTML
- Web Scraping
title: تعيين رأس التفويض في جافا – دليل كامل لتحميل HTML من عنوان URL
url: /ar/java/message-handling-networking/set-authorization-header-in-java-complete-guide-to-load-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين رأس التفويض – تحميل HTML من URL باستخدام Aspose.HTML

هل احتجت يومًا إلى **set authorization header** عند جلب صفحة ويب محمية في Java؟ ربما كنت تجلب تقريرًا من API داخلي، أو تقوم باستخلاص لوحة تحكم لا يمكن فتحها إلا برمز الخدمة الخاص بك. الخبر السار هو أنك لست مضطرًا لكتابة كود `HttpURLConnection` منخفض المستوى. باستخدام Aspose.HTML يمكنك إرفاق رؤوس HTTP مخصصة—*بما في ذلك* رأس `Authorization` المهم—مباشرةً إلى محمل المستند.

في هذا الدرس سنستعرض مثالًا واقعيًا يقوم **sets the authorization header**، **sets the accept header**، و **configures custom headers** حتى تتمكن من **load HTML from URL** بأمان. في النهاية ستحصل على فئة Java جاهزة للتنفيذ تطبع عنوان الصفحة، وستفهم كيفية **add HTTP headers Java** للاتصالات المستقبلية.

## ما ستحتاجه

- Java 17 أو أحدث (الكود يعمل على أي JDK حديث)
- مكتبة Aspose.HTML لـ Java (متاحة عبر Maven Central)
- رمز حامل (Bearer) صالح أو أي بيانات اعتماد أخرى تحتاج لإرسالها
- بيئة تطوير متكاملة (IDE) أو محرر نصوص بسيط + سطر الأوامر

## الخطوة 1: تثبيت تبعية Aspose.HTML

أولاً، تأكد من أن ملف JAR الخاص بـ Aspose.HTML موجود في مسار الفئات (classpath). في مشروع Maven، أضف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضّل Gradle:

```groovy
implementation 'com.aspose:aspose-html:23.9'
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث تجلب تحسينات في الأداء ودعم TLS أفضل.

## الخطوة 2: إنشاء خريطة (Map) للرؤوس المخصصة

لـ **set authorization header** و **set accept header**، تحتاج إلى `Map<String, String>` يحتوي على اسم كل رأس وقيمته. سيتم تمرير هذه الخريطة إلى المحمل لاحقًا.

```java
// Step 2: Define the custom HTTP headers required by the remote page
Map<String, String> customHeaders = new HashMap<>();
customHeaders.put("Authorization", "Bearer abcdef123456"); // <-- set authorization header
customHeaders.put("Accept", "text/html");                // <-- set accept header
```

هنا نضيف صراحةً **add HTTP headers Java** باستخدام `HashMap` المألوف. يمكنك إضافة عدد من الرؤوس كما يتوقع الـ API—`User-Agent`، `Cookie`، إلخ—عن طريق استدعاء `put` مرة أخرى.

## الخطوة 3: إرفاق الرؤوس إلى خيارات تحميل HTML

تُظهر Aspose.HTML فئة `HTMLDocumentLoadOptions`. باستدعاء `setCustomHeaders` نخبر المكتبة بإضافة خريطتنا إلى كل طلب.

```java
// Step 3: Attach the headers to the HTML load options
HTMLDocumentLoadOptions loadOptions = new HTMLDocumentLoadOptions();
loadOptions.setCustomHeaders(customHeaders); // configure custom headers
```

كائن `loadOptions` الآن يحمل تعليمات **configure custom headers**. عندما يتم جلب المستند، تقوم Aspose.HTML تلقائيًا بإضافة سطري `Authorization` و `Accept` إلى طلب HTTP.

## الخطوة 4: تحميل الصفحة المؤمنة

الآن نقوم فعليًا بـ **load HTML from URL**. مُنشئ `HTMLDocument` يقبل عنوان URL الهدف و `loadOptions` التي أعددناها للتو.

```java
// Step 4: Load the secured HTML page using the configured options
try (HTMLDocument document = new HTMLDocument(
        "https://api.example.com/secured-page.html", loadOptions)) {

    // Step 5: Use the loaded document – here we simply print its title
    System.out.println("Page title: " + document.getTitle());
}
```

نظرًا لأننا وضعنا `HTMLDocument` داخل كتلة try‑with‑resources، يتم إغلاق المستند تلقائيًا، مما يحرّر مقابس الشبكة والذاكرة. ستنجح العملية فقط إذا كانت قيمة **set authorization header** صالحة؛ وإلا ستحصل على خطأ 401.

### النتيجة المتوقعة

```
Page title: Secure Dashboard
```

إذا رأيت العنوان مطبوعًا، فقد نجحت في **set authorization header**، **set accept header**، و **load HTML from URL** في تدفق واحد نظيف.

## الخطوة 5: معالجة الحالات الحدية والمشكلات الشائعة

### 5.1 الرموز المنتهية الصلاحية

غالبًا ما تنتهي صلاحية الرموز بعد ساعة. إذا حصلت على `401 Unauthorized`، قم بتجديد الرمز أولاً، ثم أعد بناء خريطة `customHeaders`. يمكن لطريقة مساعدة سريعة أن تُركز هذه المنطق:

```java
private static Map<String, String> buildHeaders(String token) {
    Map<String, String> map = new HashMap<>();
    map.put("Authorization", "Bearer " + token);
    map.put("Accept", "text/html");
    return map;
}
```

### 5.2 عمليات إعادة التوجيه والكوكيز

تتبع Aspose.HTML عمليات إعادة التوجيه بشكل افتراضي، لكن الكوكيز لا تُحفظ عبر عمليات إعادة التوجيه ما لم تقم بتمكينها صراحةً:

```java
loadOptions.setEnableCookies(true);
```

### 5.3 تصحيح الطلبات

إذا استمرت الصفحة في عدم التحميل، فعّل تسجيل الطلبات:

```java
loadOptions.setEnableNetworkLogging(true);
loadOptions.setNetworkLogFile("network.log");
```

افحص `network.log` للتحقق من وجود رأس `Authorization`.

## الخطوة 6: مثال كامل يعمل

فيما يلي الفئة الكاملة الجاهزة للتنفيذ في Java. الصقها في IDE الخاص بك، استبدل الرمز النائب (placeholder) وعنوان URL، ثم اضغط **Run**.

```java
import com.aspose.html.*;
import java.util.*;

public class UrlWithHeaders {
    public static void main(String[] args) throws Exception {

        // Step 2: Define the custom HTTP headers required by the remote page
        Map<String, String> customHeaders = new HashMap<>();
        customHeaders.put("Authorization", "Bearer abcdef123456"); // set authorization header
        customHeaders.put("Accept", "text/html");                // set accept header

        // Step 3: Attach the headers to the HTML load options
        HTMLDocumentLoadOptions loadOptions = new HTMLDocumentLoadOptions();
        loadOptions.setCustomHeaders(customHeaders); // configure custom headers

        // Optional: enable cookie handling and network logging for debugging
        loadOptions.setEnableCookies(true);
        loadOptions.setEnableNetworkLogging(true);
        loadOptions.setNetworkLogFile("network.log");

        // Step 4: Load the secured HTML page using the configured options
        try (HTMLDocument document = new HTMLDocument(
                "https://api.example.com/secured-page.html", loadOptions)) {

            // Step 5: Use the loaded document – here we simply print its title
            System.out.println("Page title: " + document.getTitle());
        }
    }
}
```

> **ملاحظة:** الكود أعلاه **adds HTTP headers Java**‑style، يحمل الصفحة، ويطبع العنوان. لا مكتبات إضافية، ولا معالجة يدوية للمقابس.

## نظرة بصرية

![مخطط يوضح كيفية تعيين رأس التفويض في Java باستخدام Aspose.HTML](/images/set-authorization-header-java.png)

تُظهر الرسمة التدفق: *Header Map → Load Options → HTMLDocument → Page Title*.

## الأسئلة المتكررة

- **هل يمكنني استخدام نظام مصادقة مختلف؟**  
  بالتأكيد. فقط استبدل قيمة الرأس—مثلاً `customHeaders.put("Authorization", "Basic " + base64Creds);`.

- **ماذا لو أعاد الـ API JSON بدلًا من HTML؟**  
  تتوقع Aspose.HTML HTML، لذا بالنسبة لـ JSON ستنتقل إلى `HttpClient` عادي. يظل نمط **add http headers java** كما هو.

- **هل هذا النهج آمن للـ thread؟**  
  كائن `HTMLDocumentLoadOptions` لا يُشارك بين الـ threads. أنشئ كائن خيارات جديد لكل طلب لضمان الأمان.

## الخلاصة

أنت الآن تعرف كيف تقوم بـ **set authorization header**، **set accept header**، و **configure custom headers** حتى تتمكن من **load HTML from URL** باستخدام Aspose.HTML في Java. يوضح المثال الكامل سير العمل بالكامل—من بناء خريطة الرؤوس إلى طباعة عنوان الصفحة—مع تغطية الحالات الحدية مثل انتهاء صلاحية الرمز وتعامل الكوكيز.

بعد ذلك، قد ترغب في **add HTTP headers Java** لطلبات POST، أو تحليل DOM المسترجع، أو دمج هذا المقتطف في إطار عمل أكبر لاستخلاص الويب. مهما كان اختيارك، يبقى النمط نفسه: أنشئ خريطة رؤوس، أرفقها عبر `HTMLDocumentLoadOptions`، ودع Aspose.HTML يتولى العمل الشاق.

برمجة سعيدة، ولتُعيد مكالمات HTTP الخاصة بك دائمًا البيانات التي تحتاجها!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}