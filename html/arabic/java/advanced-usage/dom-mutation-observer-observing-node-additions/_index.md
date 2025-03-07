---
title: مراقب طفرة DOM مع Aspose.HTML لـ Java
linktitle: DOM Mutation Observer - مراقبة إضافات العقد
second_title: معالجة HTML باستخدام Java مع Aspose.HTML
description: تعرف على كيفية استخدام Aspose.HTML for Java لتنفيذ DOM Mutation Observer في هذا الدليل خطوة بخطوة. راقب تغييرات DOM وتفاعل معها بفعالية.
weight: 11
url: /ar/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مراقب طفرة DOM مع Aspose.HTML لـ Java


هل أنت مطور Java وتبحث عن مراقبة التغييرات في نموذج كائن المستند (DOM) لمستند HTML والاستجابة لها؟ يوفر Aspose.HTML for Java حلاً قويًا لهذه المهمة. في هذا الدليل التفصيلي، سنستكشف كيفية استخدام Aspose.HTML for Java لإنشاء مستند HTML ومراقبة إضافات العقد باستخدام Mutation Observer. سيرشدك هذا البرنامج التعليمي خلال العملية، ويقسم كل مثال إلى خطوات متعددة. بحلول النهاية، ستتمكن من تنفيذ DOM Mutation Observers في مشاريع Java الخاصة بك بسهولة.

## المتطلبات الأساسية

قبل أن نتعمق في استخدام Aspose.HTML لـ Java، دعنا نتأكد من توفر المتطلبات الأساسية اللازمة لديك:

1. بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.

2.  Aspose.HTML for Java: ستحتاج إلى تنزيل Aspose.HTML for Java وتثبيته. يمكنك العثور على رابط التنزيل[هنا](https://releases.aspose.com/html/java/).

3. IDE (بيئة التطوير المتكاملة): استخدم بيئة التطوير المتكاملة Java المفضلة لديك، مثل IntelliJ IDEA أو Eclipse، لكتابة وتشغيل كود Java.

## استيراد الحزم

للبدء في استخدام Aspose.HTML for Java، يتعين عليك استيراد الحزم المطلوبة إلى كود Java الخاص بك. إليك كيفية القيام بذلك:

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

// إنشاء مستند HTML فارغ
HTMLDocument document = new HTMLDocument();
```

الآن بعد أن قمت باستيراد الحزم المطلوبة، دعنا ننتقل إلى الدليل خطوة بخطوة لتنفيذ DOM Mutation Observer في Java.

## الخطوة 1: إنشاء مثيل لمراقب الطفرة

أولاً، تحتاج إلى إنشاء مثيل لمراقب الطفرات. سيراقب هذا المراقب التغييرات في DOM وينفذ وظيفة استدعاء عند حدوث الطفرات.

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

في هذه الخطوة، نقوم بإنشاء مراقب باستخدام دالة استرجاع تقوم بطباعة رسالة عند إضافة عقد إلى DOM.

## الخطوة 2: تكوين المراقب

الآن، دعنا نكوّن المراقب بالخيارات المطلوبة. نريد مراقبة تغييرات القائمة الفرعية وتغييرات الشجرة الفرعية، بالإضافة إلى التغييرات في بيانات الأحرف.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// مرر العقدة المستهدفة للمراقبة باستخدام التكوين المحدد
observer.observe(document.getBody(), config);
```

 هنا، قمنا بتعيين`config` كائن لتمكين ملاحظة تغييرات بيانات القائمة الفرعية والشجرة الفرعية والحرف. ثم نمرر العقدة المستهدفة (في هذه الحالة، العقدة الموجودة في المستند)`<body>`) والتكوين للمراقب.

## الخطوة 3: تعديل DOM

الآن، سنقوم بإجراء بعض التغييرات على DOM لتشغيل المراقب. سنقوم بإنشاء عنصر فقرة وإضافته إلى نص المستند.

```java
// إنشاء عنصر فقرة وإضافته إلى نص المستند
Element p = document.createElement("p");
document.getBody().appendChild(p);

// إنشاء نص وإضافته إلى الفقرة
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

في هذه الخطوة نقوم بإنشاء عنصر فقرة HTML وإضافته إلى نص المستند، ثم نقوم بإنشاء عقدة نصية تحتوي على "Hello World" وإضافتها إلى الفقرة.

## الخطوة 4: انتظار الملاحظات (بشكل غير متزامن)

نظرًا لأن الطفرات تتم ملاحظتها بشكل غير متزامن، فنحن بحاجة إلى الانتظار لحظة للسماح للمراقب بالتقاط التغييرات. سنستخدم`synchronized` و`wait` ولتحقيق هذه الغاية، كما هو موضح أدناه.

```java
// نظرًا لأن الطفرات تعمل في وضع غير متزامن، فانتظر لبضع ثوانٍ
synchronized (this) {
    wait(5000);
}
```

هنا ننتظر لمدة 5 ثوان للتأكد من أن المراقب لديه فرصة لالتقاط أي طفرة.

## الخطوة 5: توقف عن المراقبة

أخيرًا، عندما تنتهي من المراقبة، من الضروري فصل المراقب لتحرير الموارد.

```java
// توقف عن المراقبة
observer.disconnect();
```

مع هذه الخطوة، تكون قد أكملت عملية الملاحظة ويمكنك تنظيف الموارد.

## خاتمة

في هذا البرنامج التعليمي، شرحنا عملية استخدام Aspose.HTML لـ Java لتنفيذ DOM Mutation Observer. لقد تعلمت كيفية إنشاء مراقب وتكوينه وإجراء تغييرات على DOM وانتظار الملاحظات والتوقف عن المراقبة. الآن، لديك المهارات اللازمة لتطبيق DOM Mutation Observers في مشاريع Java لمراقبة التغييرات في DOM لمستندات HTML والاستجابة لها بشكل فعال.

إذا كان لديك أي أسئلة أو واجهت أي مشكلات، فلا تتردد في طلب المساعدة في[منتدى Aspose.HTML](https://forum.aspose.com/) بالإضافة إلى ذلك، يمكنك الوصول إلى[التوثيق](https://reference.aspose.com/html/java/) للحصول على معلومات مفصلة حول Aspose.HTML لـ Java.

## الأسئلة الشائعة

### س1: ما هو مراقب طفرة DOM؟

A1: إن DOM Mutation Observer هي ميزة JavaScript تتيح لك مراقبة التغييرات في Document Object Model (DOM) لمستند HTML. وهي توفر طريقة للتفاعل مع الإضافات أو الحذف أو التعديلات التي تطرأ على عقد DOM في الوقت الفعلي.

### س2: هل يمكنني استخدام Aspose.HTML لـ Java في مشاريعي التجارية؟

 ج2: نعم، يمكنك استخدام Aspose.HTML لـ Java في المشاريع التجارية. يمكنك العثور على معلومات الترخيص والشراء[هنا](https://purchase.aspose.com/buy).

### س3: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML لـ Java؟

 ج3: نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML لـ Java[هنا](https://releases.aspose.com/)يتيح لك هذا استكشاف ميزاته وقدراته قبل إجراء عملية شراء.

### س4: ما هي فائدة مراقبة تغييرات بيانات الشخصية باستخدام مراقب الطفرة؟

أ4: إن مراقبة تغييرات بيانات الأحرف مفيدة في السيناريوهات التي تريد فيها مراقبة التغييرات في محتوى النص لعناصر HTML والاستجابة لها. على سبيل المثال، يمكنك استخدامها لتتبع إدخالات المستخدم في نماذج الويب والاستجابة لها.

### س5: كيف أتخلص من الموارد عند استخدام Aspose.HTML لـ Java؟

 ج5: من المهم تحرير الموارد عند الانتهاء منها. في مثالنا، استخدمنا`document.dispose()` لتنظيف الموارد المرتبطة بمستند HTML. تأكد من التخلص من أي كائنات وموارد تقوم بإنشائها لتجنب تسرب الذاكرة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
