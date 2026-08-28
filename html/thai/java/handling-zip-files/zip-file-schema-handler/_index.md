---
date: 2026-06-29
description: เรียนรู้วิธีอ่าน zip entry java ด้วย Aspose.HTML สำหรับ Java และให้บริการไฟล์จาก
  zip archives. คู่มือนี้แสดงการ streaming zip archive ของ Java และการตอบสนองไฟล์
  zip ของ Java ด้วย custom schema handler.
keywords:
- read zip entry java
- serve files from zip
- java zip archive streaming
- custom schema handler
- Aspose.HTML for Java
linktitle: ตัวจัดการ Schema ไฟล์ ZIP ใน Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  headline: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  type: TechArticle
- description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  name: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  steps:
  - name: '**Java Development Kit (JDK) 8+** installed.'
    text: '**Java Development Kit (JDK) 8+** installed.'
  - name: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
    text: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
  - name: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
    text: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
  - name: Basic familiarity with Java collections and exception handling.
    text: Basic familiarity with Java collections and exception handling.
  type: HowTo
- questions:
  - answer: The current implementation targets ZIP files only. You can adapt the logic
      by swapping `java.util.zip.ZipFile` with a library that supports RAR/TAR, but
      you’ll need to handle their specific entry‑lookup APIs.
    question: Can I use this handler for other archive formats like RAR or TAR?
  - answer: A corrupted archive triggers an `IOException` during `GetFile`. Catch
      the exception and return a 500 response with a diagnostic message to keep the
      application stable.
    question: What happens if the ZIP file is corrupted?
  - answer: No. This handler is read‑only; it streams entries to the client. For write‑back
      scenarios you would need a separate writer component that creates a new ZIP
      file.
    question: Is it possible to modify files within the ZIP archive using this handler?
  - answer: Implement HTTP range requests by checking the `Range` header and sending
      partial streams. This allows browsers to request file chunks, reducing perceived
      latency.
    question: How can I improve performance when serving very large files?
  - answer: Yes, provided each request creates its own `ZipFile` instance (as shown).
      Avoid sharing mutable state between threads.
    question: Can this handler be used safely in a multi‑threaded environment?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: อ่าน ZIP Entry Java – ตัวจัดการ ZIP ใน Aspose.HTML
url: /th/java/handling-zip-files/zip-file-schema-handler/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# อ่าน ZIP Entry Java – ตัวจัดการ ZIP ใน Aspose.HTML

## บทนำ
เมื่อคุณสร้างเว็บแอปพลิเคชันที่ต้องดึงรูปภาพ, สคริปต์ หรือไฟล์สไตล์ชีตโดยตรงจากไฟล์ ZIP ที่บรรจุไว้, คุณไม่ต้องการเสียเวลาในการแตกไฟล์ไปยังโฟลเดอร์ชั่วคราวก่อน. **Read zip entry java** ช่วยให้คุณสตรีมรายการที่ร้องขอโดยตรงไปยังการตอบสนอง HTTP, ทำให้การใช้หน่วยความจำต่ำและความหน่วงเวลาน้อยที่สุด. ใน Aspose.HTML สำหรับ Java สิ่งนี้ทำได้ด้วย `ZIPFileSchemaMessageHandler`, ตัวจัดการสคีมที่กำหนดเองซึ่งเข้าใจสคีม `zip-file:` URI และให้บริการเนื้อหาแบบ on‑the‑fly. ด้านล่างเราจะพาเดินผ่านการทำงานทั้งหมด, อธิบายว่าทำไมการสตรีมจึงสำคัญ, และแสดงวิธีทำให้ตัวจัดการมีความทนทานพอสำหรับงานผลิต.

## คำตอบอย่างรวดเร็ว
- **ตัวจัดการทำอะไร?** มันให้บริการไฟล์โดยตรงจากไฟล์ ZIP โดยไม่ต้องแตกออกไปยังดิสก์, ใช้การตอบสนองแบบสตรีม.  
- **สคีม URI ที่ใช้คืออะไร?** `zip-file:` – สคีมที่กำหนดเองซึ่งลงทะเบียนกับชั้นเครือข่ายของ Aspose.HTML.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **สามารถจัดการไฟล์ขนาดใหญ่ได้หรือไม่?** ได้ – มันสตรีมเนื้อหาของรายการ, ดังนั้นแม้ไฟล์หลายร้อยเมกะไบต์ก็สามารถประมวลผลได้ด้วยการใช้หน่วยความจำเล็กน้อย.  
- **ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** ตัวจัดการเองไม่มีสถานะ; เพียงตรวจสอบให้แน่ใจว่าไฟล์ ZIP พื้นฐานไม่ได้ถูกแก้ไขพร้อมกัน.

## read zip entry java คืออะไร
การอ่าน ZIP entry ใน Java หมายถึงการค้นหาไฟล์เฉพาะภายในคอนเทนเนอร์ `.zip` และรับข้อมูลของมันเป็นสตรีม. คลาส `java.util.zip.ZipFile` ให้การอ่านแบบสุ่มเข้าถึง, ดังนั้นคุณสามารถดึงรายการเดียวออกมาได้โดยไม่ต้องโหลดทั้งไฟล์อาร์ไคฟ์. Aspose.HTML ให้คุณเชื่อมตรรกะนี้เข้ากับท่อ HTTP ผ่านตัวจัดการสคีมที่กำหนดเอง, ทำให้ URL `zip-file:` ธรรมดากลายเป็นการตอบสนอง HTTP ที่สมบูรณ์.

## ทำไมต้องใช้การสตรีม zip archive ใน Java
การสตรีม ZIP entry ช่วยหลีกเลี่ยงการโหลดไฟล์อาร์ไคฟ์ทั้งหมดเข้าสู่หน่วยความจำ, ซึ่งเป็นสิ่งสำคัญสำหรับแอปที่มีการเข้าชมสูงหรือสินทรัพย์ขนาดใหญ่เช่นภาพความละเอียดสูงหรือส่วนของวิดีโอ. Aspose.HTML สามารถให้บริการไฟล์ได้ถึง **2 GB** และจัดการอาร์ไคฟ์ที่มีหลายหมื่นรายการพร้อมกับการใช้หน่วยความจำของ JVM ต่ำ. การเข้าถึงแบบสุ่มของรูปแบบ ZIP หมายความว่าจะอ่านเฉพาะไบต์ที่จำเป็นเท่านั้น.

## ข้อกำหนดเบื้องต้น
1. **Java Development Kit (JDK) 8+** ติดตั้งแล้ว.  
2. IDE เช่น **IntelliJ IDEA**, **Eclipse**, หรือ **NetBeans**.  
3. **Aspose.HTML for Java** library – ดาวน์โหลดได้จาก **[here](https://releases.aspose.com/html/java/)** และเพิ่ม JAR(s) ไปยัง classpath ของโปรเจคของคุณ.  
4. ความคุ้นเคยพื้นฐานกับคอลเลกชันของ Java และการจัดการข้อยกเว้น.

## นำเข้าแพ็กเกจ
การนำเข้าต่อไปนี้ให้คุณเข้าถึงยูทิลิตี้เครือข่ายของ Aspose.HTML, การจัดการ MIME, และคลาส I/O มาตรฐานของ Java.

```java
import com.aspose.html.MimeType;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.StreamContent;
import com.aspose.html.utils.Stream;
```

## ขั้นตอนที่ 1: สร้างคลาส ZIP File Schema Handler
`CustomSchemaMessageHandler` เป็นคลาสฐานของ Aspose.HTML สำหรับจัดการสคีม URI ที่กำหนดเอง. โดยการสืบทอดจากมัน เราสามารถลงทะเบียนสคีม `zip-file` และชี้ไปยังไฟล์ ZIP จริงบนดิสก์.

**Definition anchor:** `ZIPFileSchemaMessageHandler` คือตัวจัดการที่เป็นคอนกรีตซึ่งแมป URI `zip-file:` ไปยังรายการภายในไฟล์ ZIP เฉพาะ.

คอนสตรัคเตอร์เก็บเส้นทางเต็มของไฟล์ ZIP และลงทะเบียนสคีมกับ `MessageHandlerRegistry`. การลงทะเบียนนี้ทำให้ตัวจัดการพร้อมใช้งานทั่วโลกสำหรับเราต์เตอร์คำขอภายในของ Aspose.HTML.

```java
public class ZIPFileSchemaMessageHandler extends CustomSchemaMessageHandler {
    private final String archive;
    protected ZIPFileSchemaMessageHandler(String archive) {
        super("zip-file");
        this.archive = archive;
    }
}
```

## ขั้นตอนที่ 2: แทนที่เมธอด `invoke`
เมธอด `invoke` จะถูกเรียกสำหรับทุกคำขอที่ตรงกับสคีม `zip-file:`. มันดึงเส้นทางสัมพันธ์จาก URI ของคำขอ, ค้นหารายการที่สอดคล้อง, และสร้างการตอบสนอง HTTP ที่สตรีมข้อมูลของรายการกลับไปยังไคลเอนต์.

**Definition anchor:** `invoke` คือจุดเริ่มต้นที่ Aspose.HTML เรียกใช้เมื่อมีคำขอสคีมที่กำหนดเองต้องการการประมวลผล.

หากรายการที่ร้องขอไม่มีอยู่, เมธอดจะคืนค่าการตอบสนอง 404 พร้อมข้อความข้อความธรรมดาที่เป็นประโยชน์. มิฉะนั้น, มันจะสร้างอ็อบเจ็กต์ `MessageResponse`, ตั้งค่า MIME type ที่เหมาะสม, และแนบสตรีมของรายการ.

```java
@Override
public void invoke(INetworkOperationContext context) {
    String pathInsideArchive = context.getRequest().getRequestUri().getPathname().substring(1).replaceAll("\\\\", "/");
    Stream stream = GetFile(pathInsideArchive);
    if (stream != null) {
        // If the file is found, return it as a response
        ResponseMessage response = new ResponseMessage(200);
        response.setContent(new StreamContent(stream));
        response.getHeaders().getContentType().setMediaType(MimeType.fromFileExtension(context.getRequest().getRequestUri().getPathname()));
        context.setResponse(response);
    } else {
        // If the file is not found, return a 404 error
        context.setResponse(new ResponseMessage(404));
    }
    // Invoke the next handler in the chain
    invoke(context);
}
```

## ขั้นตอนที่ 3: Implement เมธอด `GetFile`
`GetFile` ใช้ API มาตรฐาน `java.util.zip.ZipFile` เพื่อค้นหารายการภายในอาร์ไคฟ์และคืนค่าเป็น Aspose `Stream`. นี่คือจุดที่การทำงาน **read zip entry java** เกิดขึ้นจริง.

**Definition anchor:** `GetFile` เปิดไฟล์ ZIP, ค้นหา `ZipEntry` ที่ตรงกับเส้นทางของคำขอ, และห่อ `InputStream` ของมันใน Aspose `Stream`.

เมธอดนี้ยังกำหนด MIME type ที่ถูกต้องตามส่วนขยายของไฟล์, เพื่อให้เบราว์เซอร์แสดงภาพ, สคริปต์, หรือสไตล์อย่างถูกต้อง.

```java
Stream GetFile(String path) {
    try (ZipFile zipFile = new ZipFile(archive)) {
        ZipEntry entry = zipFile.getEntry(path);
        if (entry != null) {
            InputStream inputStream = zipFile.getInputStream(entry);
            return new Stream(inputStream);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    return null;
}
```

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | ทำไมจึงเกิด | วิธีแก้ |
|-------|----------------|-----|
| **`IOException` บนไฟล์ขนาดใหญ่** | บัฟเฟอร์เริ่มต้นอาจเล็กเกินไป. | เพิ่มขนาดบัฟเฟอร์หรือใช้ช่อง `java.nio` สำหรับสตรีมมิ่ง. |
| **MIME type ไม่ถูกต้อง** | `MimeType.fromFileExtension` อาจคืนค่า `application/octet-stream` สำหรับส่วนขยายที่ไม่รู้จัก. | ตั้งค่า MIME type ด้วยตนเองตามประเภทเนื้อหาที่คุณรู้. |
| **ข้อกังวลเรื่องความปลอดภัยต่อเธรด** | การแชร์อินสแตนซ์ `ZipFile` เดียวกันระหว่างเธรดอาจทำให้เกิด `ZipException`. | เปิด `ZipFile` ใหม่ภายใน `GetFile` (ตามที่แสดง) เพื่อให้แต่ละคำขอได้ฮา​นด์​เล​่ของตนเอง. |
| **รายการที่หายไปคืนค่า 404** | ปัญหาการทำให้เส้นทางเป็นมาตรฐาน (เช่น slash นำหน้า). | การเรียก `substring(1)` จะลบ slash นำหน้า; ตรวจสอบให้แน่ใจว่า URI ของคำขอตรงกับโครงสร้างภายในของอาร์ไคฟ์. |

### เคล็ดลับประสิทธิภาพ
- **Reuse buffers:** จัดสรร `byte[]` ขนาด 64 KB ที่สามารถใช้ซ้ำได้และส่งผ่านไปยังลูปคัดลอกสตรีมเพื่อ ลดภาระการทำงานของ GC.  
- **Enable lazy loading:** ตั้งค่า `useZip64` ของ `ZipFile` เป็น `true` เมื่อจัดการอาร์ไคฟ์ที่ใหญ่กว่า 4 GB.  
- **Cache MIME mappings:** สร้างแผนที่สถิตของส่วนขยายทั่วไปไปยัง MIME type เพื่อหลีกเลี่ยงการค้นหาแบบซ้ำ.

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้ตัวจัดการนี้กับรูปแบบอาร์ไคฟ์อื่นเช่น RAR หรือ TAR ได้หรือไม่?**  
A: การทำงานปัจจุบันมุ่งเป้าเฉพาะไฟล์ ZIP เท่านั้น. คุณสามารถปรับตรรกะโดยเปลี่ยน `java.util.zip.ZipFile` เป็นไลบรารีที่รองรับ RAR/TAR, แต่คุณจะต้องจัดการกับ API การค้นหารายการของพวกมันเอง.

**Q: จะเกิดอะไรขึ้นหากไฟล์ ZIP เสียหาย?**  
A: อาร์ไคฟ์ที่เสียหายจะทำให้เกิด `IOException` ระหว่าง `GetFile`. ให้จับข้อยกเว้นและคืนค่าการตอบสนอง 500 พร้อมข้อความวินิจฉัยเพื่อให้แอปพลิเคชันคงที่.

**Q: สามารถแก้ไขไฟล์ภายใน ZIP archive ด้วยตัวจัดการนี้ได้หรือไม่?**  
A: ไม่. ตัวจัดการนี้เป็นแบบอ่านอย่างเดียว; มันสตรีมรายการไปยังไคลเอนต์. สำหรับสถานการณ์ที่ต้องเขียนกลับคุณจะต้องมีคอมโพเนนต์เขียนแยกที่สร้างไฟล์ ZIP ใหม่.

**Q: ฉันจะปรับปรุงประสิทธิภาพเมื่อให้บริการไฟล์ขนาดใหญ่มากได้อย่างไร?**  
A: ดำเนินการรองรับ HTTP range requests โดยตรวจสอบ header `Range` และส่งสตรีมบางส่วน. วิธีนี้ทำให้เบราว์เซอร์สามารถขอส่วนของไฟล์, ลดความหน่วงที่รับรู้.

**Q: ตัวจัดการนี้สามารถใช้ได้อย่างปลอดภัยในสภาพแวดล้อมหลายเธรดหรือไม่?**  
A: ได้, โดยที่แต่ละคำขอสร้างอินสแตนซ์ `ZipFile` ของตนเอง (ตามที่แสดง). หลีกเลี่ยงการแชร์สถานะที่เปลี่ยนแปลงได้ระหว่างเธรด.

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง

- [ZIP Archive Message Handler in Aspose.HTML for Java](/html/java/handling-zip-files/zip-archive-message-handler/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/java/custom-schema-message-handling/custom-schema-message-handler/)
- [Custom Schema Filter and Message Handling in Aspose.HTML for Java](/html/java/custom-schema-message-handling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}