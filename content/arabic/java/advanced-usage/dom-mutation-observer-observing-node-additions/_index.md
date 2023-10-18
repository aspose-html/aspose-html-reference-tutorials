---
title: DOM Mutation Observer مع Aspose.HTML لـ Java
linktitle: DOM Mutation Observer - مراقبة إضافات العقدة
second_title: معالجة Java HTML باستخدام Aspose.HTML
description: تعرف على كيفية استخدام Aspose.HTML لـ Java لتنفيذ DOM Mutation Observer في هذا الدليل التفصيلي خطوة بخطوة. مراقبة تغييرات DOM والتفاعل معها بشكل فعال.
type: docs
weight: 11
url: /ar/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

هل أنت مطور Java وتتطلع إلى ملاحظة التغييرات في نموذج كائن المستند (DOM) لمستند HTML والتفاعل معها؟ يوفر Aspose.HTML for Java حلاً قويًا لهذه المهمة. في هذا الدليل التفصيلي، سنستكشف كيفية استخدام Aspose.HTML لـ Java لإنشاء مستند HTML ومراقبة إضافات العقدة باستخدام Mutation Observer. سيرشدك هذا البرنامج التعليمي خلال العملية، حيث سيقسم كل مثال إلى خطوات متعددة. في النهاية، ستتمكن من تنفيذ DOM Mutation Observers في مشاريع Java الخاصة بك بسهولة.

## المتطلبات الأساسية

قبل أن نتعمق في استخدام Aspose.HTML لـ Java، دعنا نتأكد من أن لديك المتطلبات الأساسية اللازمة:

1. بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.

2.  Aspose.HTML لـ Java: ستحتاج إلى تنزيل Aspose.HTML لـ Java وتثبيته. يمكنك العثور على رابط التحميل[هنا](https://releases.aspose.com/html/java/).

3. IDE (بيئة التطوير المتكاملة): استخدم Java IDE المفضل لديك، مثل IntelliJ IDEA أو Eclipse، لكتابة تعليمات Java البرمجية وتشغيلها.

## حزم الاستيراد

للبدء في استخدام Aspose.HTML لـ Java، تحتاج إلى استيراد الحزم المطلوبة إلى كود Java الخاص بك. وإليك كيف يمكنك القيام بذلك:

```java
// استيراد الحزم الضرورية
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// قم بإنشاء مستند HTML فارغ
HTMLDocument document = new HTMLDocument();
```

الآن بعد أن قمت باستيراد الحزم المطلوبة، دعنا ننتقل إلى الدليل خطوة بخطوة لتنفيذ DOM Mutation Observer في Java.

## الخطوة 1: إنشاء مثيل مراقب الطفرة

أولاً، تحتاج إلى إنشاء مثيل Mutation Observer. سيراقب هذا المراقب التغييرات في DOM وينفذ وظيفة رد الاتصال عند حدوث الطفرات.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

في هذه الخطوة، نقوم بإنشاء مراقب بوظيفة رد الاتصال التي تطبع رسالة عند إضافة العقد إلى DOM.

## الخطوة 2: تكوين المراقب

الآن، لنقم بتكوين المراقب بالخيارات المطلوبة. نريد ملاحظة تغييرات القائمة الفرعية وتغييرات الشجرة الفرعية، بالإضافة إلى التغييرات في بيانات الأحرف.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// قم بتمرير العقدة المستهدفة للمراقبة بالتكوين المحدد
observer.observe(document.getBody(), config);
```

 وهنا قمنا بتعيين`config` كائن لتمكين مراقبة التغييرات في بيانات القائمة الفرعية والشجرة الفرعية والأحرف. نقوم بعد ذلك بتمرير العقدة المستهدفة (في هذه الحالة، عقدة المستند`<body>`) والتكوين للمراقب.

## الخطوة 3: تعديل DOM

الآن، سنقوم بإجراء بعض التغييرات على DOM لتشغيل المراقب. سنقوم بإنشاء عنصر فقرة وإلحاقه بنص المستند.

```java
// قم بإنشاء عنصر فقرة وألحقه بنص المستند
Element p = document.createElement("p");
document.getBody().appendChild(p);

// إنشاء نص وإلحاقه بالفقرة
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

في هذه الخطوة، نقوم بإنشاء عنصر فقرة HTML وإضافته إلى نص المستند. بعد ذلك، نقوم بإنشاء عقدة نصية تحتوي على محتوى "Hello World" ونلحقها بالفقرة.

## الخطوة 4: انتظر الملاحظات (بشكل غير متزامن)

وبما أن الطفرات يتم ملاحظتها بشكل غير متزامن، فنحن بحاجة إلى الانتظار للحظة للسماح للمراقب بالتقاط التغييرات. سوف نستخدم`synchronized` و`wait` لهذا الغرض، كما هو موضح أدناه.

```java
// بما أن الطفرات تعمل في الوضع غير المتزامن، انتظر بضع ثوانٍ
synchronized (this) {
    wait(5000);
}
```

وهنا، ننتظر لمدة 5 ثوان للتأكد من أن المراقب لديه فرصة لالتقاط أي طفرات.

## الخطوة 5: التوقف عن المراقبة

أخيرًا، عند الانتهاء من المراقبة، من الضروري فصل المراقب لتحرير الموارد.

```java
// توقف عن المراقبة
observer.disconnect();
```

بهذه الخطوة، تكون قد أكملت الملاحظة ويمكنك تنظيف الموارد.

## خاتمة

في هذا البرنامج التعليمي، تناولنا عملية استخدام Aspose.HTML لـ Java لتنفيذ DOM Mutation Observer. لقد تعلمت كيفية إنشاء مراقب وتكوينه وإجراء تغييرات على DOM وانتظار الملاحظات والتوقف عن المراقبة. الآن، لديك المهارات اللازمة لتطبيق DOM Mutation Observers في مشاريع Java الخاصة بك لمراقبة التغييرات في DOM لمستندات HTML والتفاعل معها بشكل فعال.

إذا كانت لديك أية أسئلة أو واجهت مشاكل، فلا تتردد في طلب المساعدة في[منتدى Aspose.HTML](https://forum.aspose.com/) . بالإضافة إلى ذلك، يمكنك الوصول إلى[توثيق](https://reference.aspose.com/html/java/) للحصول على معلومات تفصيلية حول Aspose.HTML لـ Java.

## الأسئلة الشائعة

### س1: ما هو مراقب طفرة DOM؟

ج1: يعتبر DOM Mutation Observer إحدى ميزات JavaScript التي تسمح لك بمراقبة التغييرات في نموذج كائن المستند (DOM) لمستند HTML. يوفر طريقة للتفاعل مع الإضافات أو الحذف أو التعديلات لعقد DOM في الوقت الفعلي.

### س2: هل يمكنني استخدام Aspose.HTML لـ Java في مشاريعي التجارية؟

 ج2: نعم، يمكنك استخدام Aspose.HTML لـ Java في المشاريع التجارية. يمكنك العثور على معلومات الترخيص والشراء[هنا](https://purchase.aspose.com/buy).

### س3: هل تتوفر نسخة تجريبية مجانية من Aspose.HTML لـ Java؟

 ج3: نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML لـ Java[هنا](https://releases.aspose.com/). يتيح لك ذلك استكشاف ميزاته وإمكانياته قبل إجراء عملية الشراء.

### س4: ما فائدة ملاحظة تغيرات بيانات الشخصية باستخدام مراقب الطفرات؟

ج4: ملاحظة تغييرات بيانات الأحرف مفيدة للسيناريوهات التي تريد فيها مراقبة التغييرات في محتوى النص لعناصر HTML والتفاعل معها. على سبيل المثال، يمكنك استخدامه لتتبع مدخلات المستخدم في نماذج الويب والرد عليها.

### س5: كيف يمكنني التخلص من الموارد عند استخدام Aspose.HTML لـ Java؟

 ج5: من المهم تحرير الموارد عند الانتهاء. في مثالنا استخدمنا`document.dispose()` لتنظيف الموارد المرتبطة بمستند HTML. تأكد من التخلص من أي كائنات وموارد تقوم بإنشائها لتجنب تسرب الذاكرة.