---
category: general
date: 2025-12-27
description: C# में मेमोरी स्ट्रीम जल्दी बनाएं, चरण-दर-चरण गाइड के साथ। सीखें कैसे
  स्ट्रीम बनाएं, संसाधनों को संभालें, और .NET में कस्टम स्ट्रीम निर्माण लागू करें।
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: hi
og_description: सेकंड में C# मेमोरी स्ट्रीम बनाएं। यह ट्यूटोरियल दिखाता है कि स्ट्रीम
  कैसे बनाएं, संसाधनों को कैसे संभालें, और आधुनिक .NET APIs के साथ कस्टम स्ट्रीम निर्माण
  कैसे करें।
og_title: मेमोरी स्ट्रीम बनाएं C# – पूर्ण कस्टम स्ट्रीम गाइड
tags:
- stream
- csharp
- .net
- resource-handling
title: मेमोरी स्ट्रीम बनाएं C# – कस्टम स्ट्रीम निर्माण गाइड
url: /hi/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create memory stream c# – कस्टम स्ट्रीम निर्माण गाइड

क्या आपको कभी **create memory stream c#** बनाने की ज़रूरत पड़ी लेकिन नहीं पता था कि कौन सा API चुनें? आप अकेले नहीं हैं। कई लेगेसी प्रोजेक्ट्स में आपको `IOutputStorage` मिलेगा, जबकि नए कोडबेस `ResourceHandler` को प्राथमिकता देते हैं। किसी भी तरह, लक्ष्य वही है: एक `Stream` बनाना जिसे आपका फ्रेमवर्क उपयोग कर सके।

इस ट्यूटोरियल में आप सीखेंगे **how to create stream** ऑब्जेक्ट्स, **how to handle resources** को सुरक्षित रूप से कैसे संभालें, और **custom stream creation** में महारत हासिल करेंगे, चाहे लाइब्रेरी का प्री‑24.2 संस्करण हो या 24.2+ संस्करण। अंत तक आपके पास एक कार्यशील उदाहरण होगा जिसे आप किसी भी .NET सॉल्यूशन में डाल सकते हैं—कोई रहस्यमय रेफ़रेंसेज़ नहीं, सिर्फ शुद्ध C#।

## आप क्या सीखेंगे

- लेगेसी `IOutputStorage` पैटर्न और आधुनिक `ResourceHandler` एप्रोच की स्पष्ट तुलना।  
- पूर्ण, कॉपी‑पेस्ट‑रेडी कोड जो .NET 6+ (या यदि आवश्यक हो तो पुराना) के खिलाफ कम्पाइल होता है।  
- ऐसे किनारे के मामलों के टिप्स जैसे स्ट्रीम्स को डिस्पोज़ करना, बड़े पेलोड को संभालना, और आपके कस्टम स्ट्रीम का परीक्षण करना।  

> **Pro tip:** यदि आप .NET 8 को टार्गेट कर रहे हैं, तो नया `ResourceHandler` बिल्ट‑इन async सपोर्ट देता है, जो हाई‑थ्रूपुट परिदृश्यों में मिलीसेकंड बचा सकता है।

## Create memory stream c# – लेगेसी एप्रोच (pre‑24.2)

जब आप लाइब्रेरी के पुराने संस्करण पर फंसे होते हैं, तो आपको जो कॉन्ट्रैक्ट पूरा करना होता है वह `IOutputStorage` है। इंटरफ़ेस केवल एक मेथड मांगता है जो दिए गए रिसोर्स नाम के लिए एक `Stream` रिटर्न करता है।

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

### यह क्यों काम करता है

- **Interface contract** – फ्रेमवर्क जब भी आउटपुट लिखने की ज़रूरत होगी, `CreateStream` को कॉल करेगा।  
- **Flexibility** – क्योंकि आप एक `Stream` रिटर्न करते हैं, आप बाद में `MemoryStream` को `FileStream` या यहाँ तक कि कस्टम बफ़र्ड स्ट्रीम से बदल सकते हैं बिना बाकी कोड को छुए।  
- **Resource safety** – कॉलर को रिटर्न किए गए स्ट्रीम को डिस्पोज़ करने की ज़िम्मेदारी होती है, इसलिए हम मेथड के अंदर `Dispose` नहीं कॉल करते।  

### सामान्य pitfalls

| समस्या | क्या होता है | समाधान |
|--------|--------------|--------|
| बंद स्ट्रीम रिटर्न करना | उपभोक्ताओं को लिखते समय `ObjectDisposedException` मिलेगा। | स्ट्रीम को हैंड ऑफ़ करते समय **खुला** रखें। |
| लिखने के बाद `Position = 0` सेट करना भूल जाना | डेटा बाद में पढ़ने पर खाली दिखाई देता है। | यदि आप पहले से डेटा डालते हैं तो रिटर्न करने से पहले `stream.Seek(0, SeekOrigin.Begin)` कॉल करें। |
| बड़ी फ़ाइलों के लिए बहुत बड़ा `MemoryStream` उपयोग करना | मेमोरी खत्म होने के कारण क्रैश। | एक टेम्पररी `FileStream` या कस्टम बफ़र्ड स्ट्रीम में स्विच करें। |

## Create memory stream c# – मॉडर्न एप्रोच (24.2+)

वर्ज़न 24.2 से लाइब्रेरी ने `ResourceHandler` पेश किया। अब आप इंटरफ़ेस की बजाय एक बेस क्लास को इनहेरिट करते हैं और एक ही मेथड को ओवरराइड करते हैं। इससे आपको एक साफ़, async‑फ्रेंडली एंट्री पॉइंट मिलता है।

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

### `ResourceHandler` को क्यों पसंद करें

- **Async support** – `HandleResourceAsync` मेथड आपको थ्रेड्स को ब्लॉक किए बिना I/O करने देता है।  
- **Built‑in error handling** – बेस क्लास एक्सेप्शन को पकड़ता है और उन्हें फ्रेमवर्क‑स्पेसिफिक एरर कोड में बदल देता है।  
- **Future‑proof** – नए रिलीज़ में हुक्स (जैसे लॉगिंग, टेलीमेट्री) जोड़ते हैं जो केवल हैंडलर पैटर्न के साथ काम करते हैं।  

### किनारे के मामलों का हैंडलिंग

1. **Disposal** – फ्रेमवर्क स्ट्रीम को उपयोग के बाद डिस्पोज़ कर देता है, लेकिन यदि आप किसी अन्य डिस्पोज़ेबल (जैसे `FileStream`) को रैप करते हैं तो आपको मेथड के अंदर एक `using` ब्लॉक लागू करना चाहिए और ऐसा रैपर रिटर्न करना चाहिए जो `Dispose` को फ़ॉरवर्ड करे।  
2. **Large payloads** – यदि आप > 100 MB पेलोड की उम्मीद करते हैं, तो `MemoryStream` को एक टेम्प फ़ाइल की ओर इशारा करने वाले `FileStream` से बदलें। उदाहरण:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – यदि बेस क्लास DI से सर्विसेज लेता है तो एक मॉक `IServiceProvider` इंजेक्ट करके अपने हैंडलर का यूनिट‑टेस्ट करें। यह सत्यापित करें कि `HandleResource` एक ऐसा स्ट्रीम रिटर्न करता है जिसे लिखा और पढ़ा जा सकता है।  

## How to create stream – एक त्वरित चीट शीट

| परिदृश्य | सिफ़ारिश किया गया API | उदाहरण कोड |
|----------|------------------------|-------------|
| सरल इन‑मेमोरी डेटा | `MemoryStream` | `new MemoryStream()` |
| बड़ी टेम्पररी फ़ाइलें | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| नेटवर्क‑आधारित स्रोत | `NetworkStream` | `new NetworkStream(socket)` |
| कस्टम बफ़रिंग | Derive from `Stream` | [Microsoft docs] देखें कस्टम स्ट्रीम इम्प्लीमेंटेशन के लिए |

**Note:** यदि आप स्ट्रीम को पहले से भरते हैं तो रिटर्न करने से पहले हमेशा `stream.Position = 0` सेट करें; अन्यथा डाउनस्ट्रीम रीडर्स को स्ट्रीम खाली लगेगा।

## चित्रण

![Create memory stream c# प्रक्रिया दिखाने वाला डायग्राम](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* create memory stream c# प्रक्रिया दिखाने वाला डायग्राम

## पूर्ण चलाने योग्य उदाहरण

नीचे एक न्यूनतम कंसोल ऐप है जो लेगेसी और मॉडर्न दोनों एप्रोच को दर्शाता है। आप इसे कॉपी‑पेस्ट करके एक नए .NET 6 कंसोल प्रोजेक्ट में डाल सकते हैं और जैसा है वैसा चला सकते हैं।

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

**अपेक्षित आउटपुट**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

यह प्रोग्राम तीन तरीकों से **how to create stream** दिखाता है: पुराना `IOutputStorage`, नया सिंक्रोनस `HandleResource`, और असिंक्रोनस `HandleResourceAsync`। सभी तीन एक `MemoryStream` रिटर्न करते हैं, यह सिद्ध करता है कि कस्टम स्ट्रीम निर्माण लक्ष्य किए गए संस्करण की परवाह किए बिना काम करता है।

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**Q: क्या मुझे प्राप्त स्ट्रीम पर `Dispose` कॉल करने की ज़रूरत है?**  
A: फ्रेमवर्क (या आपका कॉलिंग कोड) डिस्पोज़ल के लिए ज़िम्मेदार है। यदि आप रिटर्न किए गए स्ट्रीम के अंदर कोई अन्य डिस्पोज़ेबल रैप करते हैं, तो सुनिश्चित करें कि वह `Dispose` कॉल को फ़ॉरवर्ड करे।

**Q: क्या मैं रीड‑ओनली स्ट्रीम रिटर्न कर सकता हूँ?**  
A: हाँ, लेकिन कॉन्ट्रैक्ट आमतौर पर एक राइटेबल स्ट्रीम की अपेक्षा करता है। यदि आपको केवल पढ़ना है, तो `CanWrite => false` इम्प्लीमेंट करें और इस सीमा को डॉक्यूमेंट करें।

**Q: अगर मेरा डेटा उपलब्ध RAM से बड़ा है तो क्या करें?**  
A: एक टेम्पररी फ़ाइल पर आधारित `FileStream` में स्विच करें, या एक कस्टम बफ़र्ड स्ट्रीम इम्प्लीमेंट करें जो डेटा को चंक्स में डिस्क पर लिखे।

**Q: क्या दोनों एप्रोच में कोई प्रदर्शन अंतर है?**  
A: मॉडर्न `ResourceHandler` अतिरिक्त बेस‑क्लास लॉजिक के कारण थोड़ा ओवरहेड जोड़ता है, लेकिन async वर्ज़न उच्च समवर्तीता पर थ्रूपुट को काफी बढ़ा सकता है।

## निष्कर्ष

हमने अभी **create memory stream c#** को हर उस पहलू से कवर किया है जो आप वास्तविक दुनिया में मिल सकते हैं। अब आप दोनों लेगेसी `IOutputStorage` पैटर्न और नए `ResourceHandler` क्लास का उपयोग करके **how to create stream** करना जानते हैं, साथ ही **how to handle resources** को जिम्मेदारी से संभालने के व्यावहारिक टिप्स और बड़े फ़ाइलों या async परिदृश्यों के लिए **custom stream creation** को विस्तारित करने के तरीके देखे हैं।  
Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}