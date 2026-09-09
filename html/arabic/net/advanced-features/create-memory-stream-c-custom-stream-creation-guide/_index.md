---
category: general
date: 2025-12-27
description: إنشاء تدفق الذاكرة في C# بسرعة مع دليل خطوة بخطوة. تعلم كيفية إنشاء التدفق،
  التعامل مع الموارد، وتنفيذ إنشاء تدفق مخصص في .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: ar
og_description: إنشاء تدفق الذاكرة في C# في ثوانٍ. يوضح هذا الدرس كيفية إنشاء التدفق،
  وإدارة الموارد، وبناء إنشاء تدفق مخصص باستخدام واجهات برمجة التطبيقات الحديثة في
  .NET.
og_title: إنشاء تدفق الذاكرة C# – دليل شامل لإنشاء تدفق مخصص
tags:
- stream
- csharp
- .net
- resource-handling
title: إنشاء تدفق الذاكرة C# – دليل إنشاء تدفق مخصص
url: /ar/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء تدفق الذاكرة c# – دليل إنشاء تدفق مخصص

هل احتجت يومًا إلى **إنشاء تدفق الذاكرة c#** لكنك لم تكن متأكدًا أي واجهة برمجة تطبيقات تختار؟ لست وحدك. في العديد من المشاريع القديمة ستجد `IOutputStorage`، بينما تفضّل القواعد الحديثة `ResourceHandler`. على أي حال، الهدف هو نفسه: إنتاج `Stream` يمكن لإطار عملك استهلاكه.

في هذا الدرس ستتعلم **كيفية إنشاء تدفق**، **كيفية التعامل مع الموارد** بأمان، وإتقان **إنشاء تدفق مخصص** لكل من الإصدارات قبل 24.2 وما بعد 24.2 من المكتبة. في النهاية ستحصل على مثال عملي يمكنك إدراجه في أي حل .NET—بدون مراجع غامضة، فقط C# نقي.

## ما ستحصل عليه

- مقارنة واضحة بين نمط `IOutputStorage` القديم ونهج `ResourceHandler` الحديث.  
- كود كامل جاهز للنسخ واللصق يتجميع على .NET 6+ (أو أقدم إذا احتجت).  
- نصائح للحالات الخاصة مثل تحرير التدفقات، التعامل مع أحمال كبيرة، واختبار التدفق المخصص الخاص بك.

> **نصيحة احترافية:** إذا كنت تستهدف .NET 8، فإن `ResourceHandler` الأحدث يمنحك دعمًا مدمجًا للـ async، مما يمكن أن يقلل من المليثانية في سيناريوهات الأداء العالي.

## إنشاء تدفق الذاكرة c# – النهج القديم (قبل 24.2)

عندما تكون عالقًا في نسخة قديمة من المكتبة، العقد الذي يجب أن تفي به هو `IOutputStorage`. الواجهة تطلب فقط طريقة تُعيد `Stream` لاسم مورد معين.

```csharp
using System;
using System.IO;

// Step 1: Implement the old IOutputStorage contract.
public class MyStorage : IOutputStorage
{
    /// <summary>
    /// Returns a stream for the requested resource name.
    /// In a real app you might open a file, a network socket,
    /// or generate data on the fly.
    /// </summary>
    /// <param name="name">Logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public Stream CreateStream(string name)
    {
        // Custom stream creation logic.
        // Here we simply return an in‑memory stream.
        // You could also wrap a FileStream if you prefer.
        return new MemoryStream();
    }
}
```

### لماذا هذا يعمل

- **عقد الواجهة** – سيستدعي الإطار `CreateStream` كلما احتاج إلى كتابة مخرجات.  
- **المرونة** – لأنك تُعيد `Stream`، يمكنك استبدال `MemoryStream` بـ `FileStream` أو حتى تدفق مؤقت مخصص لاحقًا دون تعديل باقي الكود.  
- **أمان الموارد** – المتصل مسؤول عن تحرير (`Dispose`) التدفق المُرجع، وهذا هو السبب في عدم استدعائنا لـ `Dispose` داخل الطريقة.

### الأخطاء الشائعة

| المشكلة | ما يحدث | الحل |
|-------|--------------|-----|
| إرجاع تدفق مغلق | سيتلقى المستهلكون استثناء `ObjectDisposedException` عند الكتابة. | تأكد من أن التدفق **مفتوح** عند تسليمه. |
| نسيان ضبط `Position = 0` بعد الكتابة | تظهر البيانات فارغة عند القراءة لاحقًا. | استدعِ `stream.Seek(0, SeekOrigin.Begin)` قبل الإرجاع إذا قمت بملء التدفق مسبقًا. |
| استخدام `MemoryStream` كبير للملفات الضخمة | تسبب في تعطل بسبب نفاد الذاكرة. | تحول إلى `FileStream` مؤقت أو تدفق مؤقت مخصص. |

## إنشاء تدفق الذاكرة c# – النهج الحديث (24.2+)

بدءًا من الإصدار 24.2 قدمت المكتبة `ResourceHandler`. بدلاً من واجهة، الآن ترث من فئة أساسية وتُعيد تعريف طريقة واحدة. هذا يمنحك نقطة دخول أنظف ومتوافقة مع الـ async.

```csharp
using System;
using System.IO;

// Step 2: Inherit from the new ResourceHandler base class.
public class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by the framework to obtain a stream for a resource.
    /// </summary>
    /// <param name="name">The logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public override Stream HandleResource(string name)
    {
        // Your custom stream creation logic goes here.
        // For demonstration we use a MemoryStream.
        return new MemoryStream();
    }

    // Optional async version (available in 24.2+)
    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        // Simulate async work, e.g., fetching data from a service.
        await Task.Delay(10, ct);
        return new MemoryStream();
    }
}
```

### لماذا تفضيل `ResourceHandler`

- **دعم الـ async** – تسمح طريقة `HandleResourceAsync` لك بأداء عمليات I/O دون حجب الخيوط.  
- **معالجة الأخطاء المدمجة** – الفئة الأساسية تلتقط الاستثناءات وتحولها إلى رموز خطأ خاصة بالإطار.  
- **مستقبلية** – الإصدارات الأحدث تضيف نقاط ربط (مثل التسجيل، القياس) التي تعمل فقط مع نمط المعالج.

### معالجة الحالات الخاصة

1. **تحرير الموارد** – الإطار يحرّر التدفق بعد الانتهاء، ولكن إذا قمت بلف مورد قابل للتحرير آخر (مثل `FileStream`) يجب أن تنفذ كتلة `using` داخل الطريقة وتُعيد غلافًا يمرّر `Dispose`.  
2. **حجم البيانات الكبير** – إذا توقعت أحمالًا > 100 ميغابايت، استبدل `MemoryStream` بـ `FileStream` يشير إلى ملف مؤقت. مثال:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **الاختبار** – اختبر معالجك وحدةً عن طريق حقن `IServiceProvider` مزيف إذا كانت الفئة الأساسية تستخرج الخدمات من DI. تحقق من أن `HandleResource` تُعيد تدفقًا يمكن الكتابة إليه والقراءة منه.

## كيفية إنشاء تدفق – ورقة غش سريعة

| السيناريو | واجهة برمجة التطبيقات الموصى بها | كود مثال |
|----------|----------------|-------------|
| بيانات بسيطة في الذاكرة | `MemoryStream` | `new MemoryStream()` |
| ملفات مؤقتة كبيرة | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| مصدر شبكي | `NetworkStream` | `new NetworkStream(socket)` |
| تخزين مؤقت مخصص | Derive from `Stream` | See [Microsoft docs] for custom stream implementation |

**ملاحظة:** دائمًا اضبط `stream.Position = 0` قبل الإرجاع إذا قمت بملء التدفق مسبقًا؛ وإلا سيعتقد القارئ اللاحق أن التدفق فارغ.

## توضيح الصورة

![مخطط يوضح عملية إنشاء تدفق الذاكرة c#](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* مخطط يوضح عملية إنشاء تدفق الذاكرة c#

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق كونسول بسيط يوضح كل من النهجين القديم والحديث. يمكنك نسخه ولصقه في مشروع كونسول .NET 6 جديد وتشغيله كما هو.

```csharp
using System;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

// -------------------------------------------------
// Legacy implementation (pre‑24.2)
// -------------------------------------------------
public class MyStorage : IOutputStorage
{
    public Stream CreateStream(string name) => new MemoryStream();
}

// -------------------------------------------------
// Modern implementation (24.2+)
// -------------------------------------------------
public class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string name) => new MemoryStream();

    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        await Task.Delay(10, ct); // simulate async work
        return new MemoryStream();
    }
}

// -------------------------------------------------
// Demo program
// -------------------------------------------------
class Program
{
    static async Task Main()
    {
        // Legacy usage
        IOutputStorage legacy = new MyStorage();
        using (var legacyStream = legacy.CreateStream("legacy"))
        using (var writer = new StreamWriter(legacyStream))
        {
            writer.Write("Hello from legacy API!");
            writer.Flush();
            legacyStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(legacyStream).ReadToEnd());
        }

        // Modern sync usage
        var handler = new MyHandler();
        using (var modernStream = handler.HandleResource("modern"))
        using (var writer = new StreamWriter(modernStream))
        {
            writer.Write("Hello from modern API!");
            writer.Flush();
            modernStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(modernStream).ReadToEnd());
        }

        // Modern async usage
        using (var asyncStream = await handler.HandleResourceAsync("async"))
        using (var writer = new StreamWriter(asyncStream))
        {
            await writer.WriteAsync("Hello from async API!");
            await writer.FlushAsync();
            asyncStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(await new StreamReader(asyncStream).ReadToEndAsync());
        }
    }
}
```

**المخرجات المتوقعة**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

يعرض البرنامج ثلاث طرق لـ **كيفية إنشاء تدفق**: `IOutputStorage` القديم، `HandleResource` المتزامن الجديد، و `HandleResourceAsync` غير المتزامن. جميعها تُعيد `MemoryStream`، مما يثبت أن إنشاء تدفق مخصص يعمل بغض النظر عن الإصدار المستهدف.

## الأسئلة المتكررة (FAQ)

**س: هل يجب علي استدعاء `Dispose` على التدفق الذي أحصل عليه؟**  
ج: الإطار (أو الكود المستدعي) هو المسؤول عن تحريره. إذا قمت بلف مورد قابل للتحرير آخر داخل التدفق المُرجع، تأكد من أنه يمرّر استدعاء `Dispose`.

**س: هل يمكنني إرجاع تدفق للقراءة فقط؟**  
ج: نعم، لكن العقد عادةً يتوقع تدفقًا قابلًا للكتابة. إذا كنت تحتاج فقط للقراءة، نفّذ `CanWrite => false` ووثّق القيد.

**س: ماذا لو كان بياناتي أكبر من الذاكرة المتاحة؟**  
ج: تحول إلى `FileStream` مدعوم بملف مؤقت، أو نفّذ تدفقًا مؤقتًا مخصصًا يكتب إلى القرص على شكل قطع.

**س: هل هناك فرق في الأداء بين النهجين؟**  
ج: `ResourceHandler` الحديث يضيف حملاً بسيطًا بسبب منطق الفئة الأساسية الإضافية، لكن النسخة غير المتزامنة يمكن أن تحسّن بشكل كبير من معدل النقل تحت مستويات عالية من التزامن.

## الخلاصة

لقد غطينا للتو **إنشاء تدفق الذاكرة c#** من كل زاوية قد تصادفها في الواقع. الآن تعرف **كيفية إنشاء تدفق** باستخدام نمط `IOutputStorage` القديم وفئة `ResourceHandler` الحديثة، بالإضافة إلى أنك رأيت نصائح عملية لـ **كيفية التعامل مع الموارد** بمسؤولية وتوسيع النمط باستخدام **إنشاء تدفق مخصص** للملفات الكبيرة أو السيناريوهات غير المتزامنة. Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}