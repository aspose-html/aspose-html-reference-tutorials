---
category: general
date: 2026-03-26
description: مثال على top level await يُظهر await delay في جافاسكريبت، وفئة زيادة
  العداد، وحقول الفئة العامة في جافاسكريبت في عرض حي.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: ar
og_description: مثال على top level await يوضح await delay في جافاسكريبت، وفئة زيادة
  العداد، والحقول العامة للفئات في جافاسكريبت في دليل مختصر.
og_title: مثال على await على المستوى الأعلى – استخدام await delay في جافا سكريبت
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: مثال على await على المستوى الأعلى – استخدام await لتأخير في جافا سكريبت
url: /ar/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال على top level await – استخدام await delay في JavaScript

هل تساءلت يومًا كيف تُوقف تنفيذ الوحدة دون تغليف كل شيء في IIFE غير متزامن؟ هذا بالضبط ما يتيح لك **top level await example** القيام به. في هذا الدرس سنستعرض صفحة ويب صغيرة تستخدم `await delay javascript` لتأخير العمل، ثم ننشئ `increment counter class` التي تستفيد من **public class fields javascript**. في النهاية ستحصل على مقطع كامل يمكن نسخه ولصقه ويعمل في أي متصفح حديث.

سنغطي كل شيء من تعريف فئة بحقل عام إلى ربط مساعد تأخير بسيط يعتمد على الـ Promise. لا مكتبات خارجية، لا خطوة بناء—فقط HTML عادي، `<script type="module">`، وأحدث ميزات ECMAScript. إذا كنت بالفعل مرتاحًا مع الدوال غير المتزامنة، سترى لماذا يشعر top‑level await كامتداد طبيعي. إذا كنت جديدًا على بنية **javascript class public field**، لا تقلق—نشرح السبب وراء كل سطر.

## ما ستتعلمه

- كيف يعمل **top level await example** داخل سكريبت وحدة.
- النمط الخاص بمساعد `await delay javascript` الذي يحاكي `setTimeout` باستخدام الـ Promises.
- كيفية كتابة **increment counter class** التي تستخدم حقلًا عامًا (`count`) وكتلة تهيئة ثابتة.
- ناتج الـ console المتوقع وكيفية التحقق من أن الكتلة الثابتة تُنفّذ قبل باقي السكريبت.
- نصائح لتصحيح المشكلات الشائعة، مثل المتصفحات القديمة التي لا تدعم top‑level await.

> **Pro tip:** المتصفحات الحديثة (Chrome 106+، Firefox 102+، Edge 106+) تدعم بالفعل top‑level await. إذا كنت بحاجة لدعم بيئات أقدم، فكر في التجميع باستخدام أداة مثل Vite أو Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

الجزء الأول من عرضنا هو فئة تخزن عدادًا رقميًا. لاحظ السطر `count = 0;`—هذا هو بناء **public class fields javascript** الذي تم تقديمه في ES2022. إنه ينشئ خاصية للنسخة دون الحاجة إلى مُنشئ.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Why a static block?** يتيح لنا تشغيل منطق تهيئة لمرة واحدة (مثل التسجيل) في اللحظة التي يتم فيها تحليل الوحدة، *قبل* أي top‑level await. هذا يضمن ظهور الرسالة أولًا في الـ console، مما يثبت أن الفئة تم تقييمها مبكرًا.

## Step 2 – Create an `await delay javascript` Helper

بعد ذلك نحتاج إلى دالة تأخير صغيرة تعتمد على الـ Promise. هي في الأساس غلاف حول `setTimeout`، لكن إرجاع Promise يجعلها قابلة للانتظار.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** إذا كان `ms` سالبًا أو ليس رقمًا، فإن `setTimeout` يتعامل معه كـ `0`. يمكنك إضافة تحقق، لكن للعرض التوضيحي يبقى السطر الواحد أكثر قابلية للقراءة.

## Step 3 – Use Top‑Level Await to Pause Execution

الآن يأتي نجم العرض: top‑level await. لأن سكريبتنا وحدة (`type="module"`)، يمكننا وضع `await` مباشرة في النطاق العلوي. هذا يوقف تنفيذ الوحدة حتى يُحل الـ Promise، مما يسمح لنا بالتحكم في ترتيب الآثار الجانبية.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Common question:** “هل يمكنني استخدام top‑level await داخل وسم `<script>` عادي؟” لا—فقط سكريبتات الوحدات تدعم ذلك. إذا نسيت `type="module"`، ستحصل على خطأ في الصياغة.

## Step 4 – Instantiate the Class, Increment, and Log the Result

أخيرًا نجمع كل شيء معًا: ننشئ نسخة، نستدعي `increment()`، ونطبع العدد النهائي. هذا يوضح **increment counter class** عمليًا.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### ناتج الـ Console المتوقع

```
Counter class initialized
Final count: 1
```

إذا فتحت الصفحة في DevTools، يجب أن ترى رسالة الكتلة الثابتة تظهر **قبل** انتهاء التأخير، مما يؤكد أن الفئة تم تقييمها أولًا.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

قد تتساءل لماذا لم نكتب:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

كلا النهجين يعملان، لكن **public class fields javascript** تمنحك بنية أنظف وأكثر إعلانية. يتم تعريف الحقل مرة واحدة، وليس داخل كل استدعاء للمُنشئ، مما قد يكون أسهل للقراءة عندما تكبر الفئة. بالإضافة إلى ذلك، لا يمكن وضع الكتل الثابتة داخل المُنشئ، لذا يصبح فصل منطق التهيئة أكثر طبيعية.

## Step 6 – Adapting the Example for Real‑World Apps

في الإنتاج غالبًا ما تحتاج إلى أكثر من عداد واحد. إليك بعض الأفكار السريعة:

- **Multiple counters:** خزنها في `Map` مع مفتاح معرف.
- **Persisted state:** استبدل `console.log` بكتابات `localStorage`.
- **Async initialization:** استخدم الكتلة الثابتة لجلب إعدادات من خادم قبل إنشاء أي نسخة.

كل هذه الأنماط لا تزال تستفيد من top‑level await، لأنك يمكنك جلب البيانات مرة واحدة عند تحميل الوحدة وضمان جاهزيتها لكل مستهلك.

## Frequently Asked Questions

**س: هل يعرقل top‑level await الوحدات الأخرى؟**  
ج: لا. كل وحدة تعمل بشكل مستقل. فقط الوحدة التي تحتوي على الـ await تُوقف؛ الوحدات الأخرى تواصل التحميل بالتوازي.

**س: ماذا لو رفض وعد التأخير؟**  
ج: رفض غير مُعالج سيُوقف تقييم الوحدة ويظهر كخطأ في الـ console. غلف الـ await داخل `try…catch` إذا كنت بحاجة إلى معالجة مرنة.

**س: هل كلمة `static` مطلوبة؟**  
ج: ليست للعداد نفسه، لكن الكتلة الثابتة طريقة مفيدة لإظهار أن الكود يُنفّذ *مرة* واحدة عند التحميل—ممتاز للتسجيل أو اكتشاف الميزات.

## Conclusion

لقد بنيت للتو **top level await example** يوضح `await delay javascript`، **increment counter class**، وقوة **public class fields javascript**. المقطع الكامل القابل للتنفيذ موجود أعلاه، وإخراج الـ console يثبت أن الكتلة الثابتة تُنفّذ قبل تشغيل الكود المتأخر.  

من هنا يمكنك تجربة تدفقات async أكثر تعقيدًا، استبدال التأخير باستدعاء API حقيقي، أو توسيع الفئة بطرق إضافية. تذكر أن JavaScript الحديثة تتيح لك معالجة الوحدات ككيانات async من الدرجة الأولى—بدون الحاجة إلى أطر إضافية.

برمجة سعيدة، ولا تتردد في مشاركة تنويعاتك في التعليقات. إذا وجدت هذا الدليل مفيدًا، شاركه مع زميل لا يزال يواجه صعوبات مع أنماط async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}