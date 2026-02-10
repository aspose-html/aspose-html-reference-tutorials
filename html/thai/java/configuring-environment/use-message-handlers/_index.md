---
date: 2026-02-10
description: เรียนรู้วิธีใช้ Aspose เพื่อจัดการลิงก์ที่เสียใน Java, แปลง HTML เป็น
  PNG และโหลดเอกสาร HTML ใน Java ด้วย Aspose.HTML for Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: แปลง HTML เป็น PNG ด้วย Aspose.HTML Message Handlers ใน Java
url: /th/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น PNG ด้วย Aspose.HTML Message Handlers ใน Java

## บทนำ
ในบทเรียนนี้คุณจะได้ค้นพบ **how to convert HTML to PNG** พร้อมกับการจัดการทรัพยากรที่หายไปอย่างราบรื่นโดยใช้ Aspose.HTML สำหรับ Java เราจะอธิบายขั้นตอนการสร้างหน้า HTML ขนาดเล็กที่อ้างอิงรูปภาพที่ไม่มีอยู่, การเชื่อมต่อ **custom message handler** เพื่อ **intercept network requests**, การกำหนดค่า **network service**, การโหลดเอกสาร, และสุดท้ายการทำ **html to image conversion** เมื่อเสร็จคุณจะมีรูปแบบที่มั่นคงสำหรับทั้ง **handle broken links java** และการสร้าง PNG คุณภาพสูง—เหมาะสำหรับรายงาน, รูปย่อ, หรือพรีวิวอีเมล

## คำตอบสั้น
- **What does a message handler do?** มันทำการ **intercept network operations** (เช่น การร้องขอรูปภาพ) และให้คุณตอบสนองต่อรหัสสถานะเช่น 404.  
- **Can Aspose.HTML convert HTML to PNG?** ใช่—`Converter.convertHTML` ทำการแปลงในหนึ่งคำสั่ง.  
- **Do I need a license for this example?** ใบอนุญาตชั่วคราวจะลบข้อจำกัดการประเมิน; จำเป็นต้องมีใบอนุญาตถาวรสำหรับการใช้งานในผลิตภัณฑ์.  
- **Which Java version works?** JDK 8 ขึ้นไป (ตัวอย่างทำงานบน JDK 11).  
- **Can I configure the network service?** แน่นอน—ใช้ `configuration.getService(INetworkService.class)` เพื่อเพิ่ม handler ของคุณ.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม, ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้พร้อม:

1. **Java Development Kit (JDK)** – ดาวน์โหลดจาก [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – รับไลบรารีจาก [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse หรือ NetBeans ใช้งานได้ดี.  
4. **Basic Java knowledge** – คุณควรคุ้นเคยกับคลาส, try‑with‑resources, และการจัดการข้อยกเว้น.  
5. **Temporary License** – หากคุณอยู่ในช่วงทดลอง, รับ [temporary license](https://purchase.aspose.com/temporary-license/) เพื่อหลีกเลี่ยงลายน้ำ.

## นำเข้าแพ็กเกจ
ขั้นแรก, นำเข้าคลาส Java I/O ที่เราต้องการสำหรับการจัดการไฟล์ ส่วนคลาส Aspose ที่เหลือจะถูกอ้างอิงด้วยชื่อเต็มในภายหลัง, ทำให้รายการ import ดูเรียบร้อย.

```java
import java.io.IOException;
```

## ขั้นตอนที่ 1: เตรียมโค้ด HTML
เราจะสร้างส่วนย่อย HTML ขั้นต่ำที่อ้างอิงรูปภาพที่ไม่มีอยู่โดยเจตนา สิ่งนี้จะทำให้ handler ของเราถูกเรียกเมื่อเอนจินพยายามดึงทรัพยากร.

```java
String code = "<img src='missing.jpg'>";
```

## ขั้นตอนที่ 2: เขียนโค้ด HTML ลงไฟล์
ต่อไป, เราจะบันทึกส่วนย่อยนี้เป็น *document.html* การใช้บล็อก try‑with‑resources จะรับประกันว่า `FileWriter` ปิดอย่างถูกต้อง.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## ขั้นตอนที่ 3: เขียน Custom Message Handler
ตอนนี้เราจะสร้าง **custom message handler** ที่ตรวจสอบสถานะ HTTP ของทุกการร้องขอเครือข่าย หากการตอบกลับไม่ใช่ `200` เราจะบันทึกคำเตือนอย่างเป็นมิตร สังเกตการเรียก `invoke(context);` ที่ส่วนท้าย—มันจะส่งต่อคำขอไปยัง handler ถัดไปในลำดับ, ป้องกันการวนลูป.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## ขั้นตอนที่ 4: กำหนดค่า Network Service
เพื่อให้ Aspose.HTML รู้จัก handler ของเรา, เราจะดึง **network service** จากอ็อบเจกต์ `Configuration` แล้วเพิ่ม handler ลงในคอลเลกชันของมัน นี่คือขั้นตอนที่เราจะ **configure network service** เพื่อพฤติกรรมแบบกำหนดเอง.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## ขั้นตอนที่ 5: โหลดเอกสาร HTML
เมื่อการกำหนดค่าเรียบร้อย, เราจะโหลด *document.html* เอนจินจะใช้ network service ของเรา, ดังนั้นคำขอรูปภาพที่หายไปจะถูกดักโดย handler ที่เราเพิ่มไว้.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## ขั้นตอนที่ 6: แปลง HTML เป็น PNG
นี่คือหัวใจของกระบวนการ **html to image conversion** เมธอด `Converter.convertHTML` รับ `HTMLDocument` ที่โหลดแล้ว, `ImageSaveOptions` ทางเลือก (ที่คุณสามารถปรับ DPI หรือคุณภาพ), และชื่อไฟล์ผลลัพธ์.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## ขั้นตอนที่ 7: ทำความสะอาดทรัพยากร
แนวปฏิบัติที่ดีของ Java กำหนดให้เราปล่อยทรัพยากรเนทีฟทั้งหมด บล็อก `finally` จะรับประกันว่า `Configuration` ถูกทำลายแม้จะมีข้อยกเว้นเกิดขึ้น.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## ทำไมต้องใช้ Message Handlers?
Message handlers ให้คุณ **fine‑grained control** กับทุกการร้องขอเครือข่าย—ไม่ว่าจะเป็นรูปภาพ, CSS, JavaScript หรือไฟล์ฟอนต์ แทนที่จะให้ไลบรารีล้มเหลวโดยไม่มีข้อความ, คุณสามารถบันทึกทรัพยากรที่หายไป, ให้เนื้อหา fallback, หรือแม้กระทั่งลองร้องขอใหม่ สิ่งนี้ทำให้ pipeline การประมวลผล HTML ของคุณ **robust**, **production‑ready**, และง่ายต่อการดีบัก.

## ปัญหาทั่วไปและวิธีแก้
- **Handler recursion** – เรียก `invoke(context);` เพียงครั้งเดียวเพื่อหลีกเลี่ยงลูปไม่มีที่สิ้นสุด.  
- **Missing license** – หากไม่มีใบอนุญาตที่ถูกต้อง PNG ผลลัพธ์จะมีลายน้ำ.  
- **Incorrect file paths** – ใช้เส้นทางแบบ absolute หรือกำหนด working directory ให้ถูกต้องเมื่อโหลด `document.html`.  
- **Unsupported resource types** – ตรวจสอบให้แน่ใจว่าแหล่งข้อมูลที่คุณต้องการดัก (รูปภาพ, CSS ฯลฯ) ถูกเรียกโดยเอนจิน HTML จริงๆ.

## คำถามที่พบบ่อย

**Q: Can I chain multiple message handlers?**  
A: ใช่, คุณสามารถเพิ่มหลาย handler ลงในคอลเลกชัน `network.getMessageHandlers()`; พวกมันจะทำงานตามลำดับที่เพิ่ม.

**Q: Does the handler work for CSS or script resources as well?**  
A: แน่นอน—การร้องขอเครือข่ายใดๆ ที่ทำโดยเอนจิน HTML (รูปภาพ, CSS, JS, ฟอนต์) จะผ่าน handler.

**Q: How do I change the HTTP request before it’s sent?**  
A: สร้าง handler ที่แก้ไข `context.getRequest()` ก่อนเรียก `invoke(context)`.

**Q: Is there a way to suppress the warning for specific URLs?**  
A: ภายใน handler, ตรวจสอบ `context.getRequest().getRequestUri()` และข้ามการบันทึกตามเงื่อนไข.

**Q: What version of Aspose.HTML is required for these APIs?**  
A: โค้ดทำงานกับ Aspose.HTML for Java 22.10 ขึ้นไป.

## สรุป
ตอนนี้คุณมีตัวอย่างครบวงจรของ **how to convert HTML to PNG** พร้อมกับการใช้ **custom message handler** เพื่อ **intercept network requests** และ **handle broken links java** ด้วยการกำหนดค่า network service, โหลดเอกสาร, และเรียกใช้ converter, คุณสามารถสร้างภาพ PNG thumbnail หรือ screenshot หน้าเต็มได้อย่างเชื่อถือในแอปพลิเคชัน Java ใดก็ได้.

---

**Last Updated:** 2026-02-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}