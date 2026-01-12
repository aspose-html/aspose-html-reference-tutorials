---
date: 2026-01-02
description: تعلم كيفية استخراج الصور من ملفات EPUB باستخدام Aspose.HTML للغة Java
  وتحويل EPUB إلى ملفات صور من خلال هذا الدليل خطوة بخطوة.
linktitle: Specifying Custom Stream Provider for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: استخراج الصور من EPUB – تحديد موفر تدفق مخصص
url: /ar/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الصور من EPUB – تحديد موفر تدفق مخصص لتحويل EPUB إلى صورة

هل أنت مستعد لاستغلال قوة Aspose.HTML for Java **لاستخراج الصور من ملفات EPUB**؟ سيوجهك هذا الدليل الشامل خلال العملية بالكامل، خطوة بخطوة. سواء كنت مطورًا متمرسًا يبحث عن **تحويل EPUB إلى صيغ صور** أو كنت مبتدئًا، فنحن هنا لتلبية احتياجاتك.

## إجابات سريعة
- **ما الذي يعلّمه هذا الدرس؟** كيفية استخراج الصور من EPUB وحفظها كملفات JPEG باستخدام موفر تدفق مخصص.  
- **ما المكتبة المطلوبة؟** Aspose.HTML for Java.  
- **هل أحتاج إلى ترخيص؟** يلزم الحصول على ترخيص مؤقت أو كامل للاستخدام في الإنتاج.  
- **ما صيغة الإخراج المعروضة؟** JPEG (يمكنك التبديل إلى PNG أو BMP، إلخ، عن طريق تغيير `ImageFormat`).  
- **كم عدد أسطر الشيفرة؟** فقط خمس كتل شفرة مختصرة – كل ما تبقى هو إرشادات باللغة الإنجليزية.

## كيف تستخرج الصور من EPUB باستخدام موفر تدفق مخصص؟
قبل الغوص في الشيفرة، دعنا نفهم لماذا يُعد **موفر التدفق المخصص** مفيدًا. من خلال توجيه مخرجات التحويل إلى تدفقات الذاكرة بدلاً من نظام الملفات، تحصل على سيطرة كاملة على مكان وكيفية تخزين بيانات الصورة—مناسب تمامًا لخدمات الويب، وظائف السحابة، أو أي سيناريو ترغب فيه بتجنب الملفات المؤقتة.

## المتطلبات المسبقة

1. **بيئة تطوير Java** – تأكد من تثبيت Java بشكل صحيح على نظامك. يمكنك تنزيل Java من الموقع.  
2. **مكتبة Aspose.HTML for Java** – ستحتاج إلى الحصول على مكتبة Aspose.HTML for Java. يمكنك العثور عليها [هنا](https://releases.aspose.com/html/java/).  
3. **توثيق Aspose.HTML** – يمكن العثور على توثيق Aspose.HTML for Java [هنا](https://reference.aspose.com/html/java/).  
4. **IDE (بيئة التطوير المتكاملة)** – يمكنك اختيار أي IDE متوافق مع Java مثل Eclipse أو IntelliJ IDEA.

## استيراد الحزم

في هذا القسم، سنرشدك خلال عملية استيراد الحزم اللازمة للبدء باستخدام Aspose.HTML for Java.

## فتح ملف EPUB موجود

أولاً، تحتاج إلى فتح ملف EPUB موجود للقراءة. إليك الطريقة:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

## إنشاء MemoryStreamProvider

لتحويل EPUB إلى صورة، ستحتاج إلى إنشاء نسخة من `MemoryStreamProvider`:

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

## تحويل EPUB إلى صورة

الآن، لنحول ملف EPUB إلى صورة باستخدام `MemoryStreamProvider`. هذه الخطوة **تحول EPUB إلى JPEG** (يمكنك تغيير الصيغة إلى PNG أو BMP إذا لزم الأمر).

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

## الوصول إلى تدفقات الذاكرة

يمكنك الوصول إلى تدفقات الذاكرة التي تحتوي على بيانات الصورة الناتجة:

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

## تفريغ الصفحة إلى ملف إخراج

أخيرًا، تحتاج إلى كتابة كل تدفق صورة إلى ملف فعلي. هذا المثال يحفظ الصفحات كملفات JPEG منفصلة:

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## لماذا تحويل EPUB إلى JPEG؟

- **التوافق الشامل** – يمكن عرض صور JPEG على أي جهاز أو منصة تقريبًا.  
- **سهولة التكامل** – استخدم الصور المستخرجة في صفحات الويب، التطبيقات المحمولة، أو الوثائق دون الحاجة إلى قارئ EPUB.  
- **الأداء** – عرض صورة ثابتة أسرع من تحميل EPUB كامل، وهو مفيد للصور المصغرة أو المعاينات.

## المشكلات الشائعة والنصائح

- **إدارة الذاكرة** – احرص دائمًا على إغلاق التدفقات (`try‑with‑resources` مستخدم أعلاه) لتجنب تسرب الذاكرة.  
- **EPUBs الكبيرة** – بالنسبة للكتب التي تحتوي على عدد كبير من الصفحات، فكر في معالجة التدفقات على دفعات للحفاظ على استهلاك الذاكرة منخفضًا.  
- **جودة الصورة** – اضبط `ImageSaveOptions` (مثلاً، خاصية `Quality`) إذا كنت بحاجة إلى إخراج بدقة أعلى.

## الخلاصة

تهانينا! لقد تعلمت بنجاح كيفية **استخراج الصور من EPUB** باستخدام Aspose.HTML for Java وموفر تدفق مخصص. هذه الطريقة القوية تمنحك مرونة في معالجة بيانات الصورة بالضبط حيث تحتاجها—سواء كان ذلك حفظًا على القرص، أو إرسالًا عبر الشبكة، أو تخزينًا في قاعدة بيانات.

## الأسئلة المتكررة

### 1. ما هو Aspose.HTML for Java؟

Aspose.HTML for Java هي مكتبة تسمح لمطوري Java بالعمل مع HTML وEPUB وغيرها من الصيغ المتعلقة بالويب.

### 2. أين يمكنني العثور على توثيق Aspose.HTML for Java؟

يمكنك العثور على التوثيق [هنا](https://reference.aspose.com/html/java/).

### 3. هل هناك نسخة تجريبية مجانية متاحة؟

نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML for Java [هنا](https://releases.aspose.com/).

### 4. كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML for Java؟

يمكنك الحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

### 5. أين يمكنني الحصول على الدعم لـ Aspose.HTML for Java؟

يمكنك العثور على الدعم في [منتديات Aspose](https://forum.aspose.com/).

## أسئلة متكررة إضافية

**س: كيف أحول EPUB إلى PNG بدلاً من JPEG؟**  
ج: غيّر `ImageFormat` في `ImageSaveOptions` إلى `ImageFormat.Png` وعدّل امتداد الملف وفقًا لذلك.

**س: هل يمكنني استخراج صفحات محددة فقط من EPUB؟**  
ج: نعم، عن طريق التكرار على مجموعة `lStream` واختيار الفهارس المطلوبة قبل الكتابة إلى الملفات.

**س: هل من الممكن تشغيل هذا التحويل في وظيفة سحابية دون كتابة إلى القرص؟**  
ج: بالتأكيد. بما أن مخرجات التحويل مخزنة في تدفقات الذاكرة، يمكنك إرجاع مصفوفات البايت مباشرة من وظيفتك السحابية.

**س: هل يدعم Aspose.HTML ملفات EPUB المحمية بـ DRM؟**  
ج: يمكن للمكتبة فتح ملفات EPUB غير المشفرة. بالنسبة للملفات المحمية بـ DRM، سيتعين عليك إزالة الحماية قبل التحويل.

**س: ما هو إصدار Aspose.HTML المطلوب لهذه الميزة؟**  
ج: فئة `MemoryStreamProvider` متاحة في Aspose.HTML 22.9 وما بعده.

---

**آخر تحديث:** 2026-01-02  
**تم الاختبار مع:** Aspose.HTML for Java 23.10  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}