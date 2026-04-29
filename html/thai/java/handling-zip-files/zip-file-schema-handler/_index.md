---
date: 2026-02-15
description: เรียนรู้วิธีอ่านรายการ zip ใน Java ด้วย Aspose.HTML for Java คู่มือนี้แสดงการสตรีมไฟล์
  zip archive ใน Java และการตอบสนองไฟล์ zip ใน Java ด้วยตัวจัดการสคีมาที่กำหนดเอง.
linktitle: ZIP File Schema Handler in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: อ่านรายการ ZIP ใน Java – ตัวจัดการ ZIP ใน Aspose.HTML
url: /th/java/handling-zip-files/zip-file-schema-handler/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# อ่าน ZIP Entry Java – ZIP Handler ใน Aspose.HTML

## คำแนะนำ
เมื่อทำงานกับเอกสาร HTML ที่ซับซ้อนหรือแอปพลิเคชันเว็บ คุณอาจต้อง **read zip entry java** เพื่อให้บริการทรัพยากรที่อยู่ภายในไฟล์ ZIP ลองนึกภาพการโหลดรูปภาพ, สคริปต์ หรือสไตล์ชีตโดยตรงจากไฟล์ ZIP ที่บรรจุไว้และส่งกลับเป็นส่วนหนึ่งของการตอบสนองเว็บปกติ—โดยไม่ต้องทำขั้นตอนการแตกไฟล์เพิ่มเติม นั่นคือสิ่งที่ `ZIPFileSchemaMessageHandler` ใน Aspose.HTML for Java ทำให้เป็นไปได้ ในบทแนะนำนี้เราจะอธิบายการสร้างตัวจัดการสคีมาที่กำหนดเองซึ่งให้ **java zip archive streaming** และคืน **java zip file response** ที่เหมาะสมสำหรับคำขอใด ๆ ที่ใช้สคีม่า `zip-file:`

## คำตอบอย่างรวดเร็ว
- **What does the handler do?** ให้บริการไฟล์โดยตรงจากไฟล์ ZIP โดยไม่ต้องแตกออกไปยังดิสก์  
- **Which scheme is used?** `zip-file:` – สคีม่า URI ที่กำหนดเองและลงทะเบียนกับ Aspose.HTML  
- **Do I need a license?** รุ่นทดลองฟรีใช้ได้สำหรับการพัฒนา; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **Can it handle large files?** ใช่, มันสตรีมเนื้อหา entry ทำให้ใช้หน่วยความจำน้อยที่สุด  
- **Is it thread‑safe?** ตัวจัดการไม่มีสถานะ; เพียงตรวจสอบให้แน่ใจว่าไฟล์ ZIP พื้นฐานไม่ได้ถูกแก้ไขพร้อมกัน  

## **read zip entry java** คืออะไร?
การอ่าน ZIP entry ใน Java หมายถึงการค้นหาไฟล์เฉพาะภายในคอนเทนเนอร์ `.zip` และดึงข้อมูลของมันเป็นสตรีม คลาสมาตรฐาน `java.util.zip.ZipFile` ทำให้ขั้นตอนนี้ง่ายขึ้น และ Aspose.HTML ให้คุณเชื่อมตรรกะนี้เข้ากับ pipeline ของ HTTP ผ่านตัวจัดการสคีมาที่กำหนดเอง

## ทำไมต้องใช้ **java zip archive streaming**?
การสตรีม ZIP entry ช่วยหลีกเลี่ยงการโหลดทั้งไฟล์ ZIP เข้าไปในหน่วยความจำ ซึ่งสำคัญสำหรับเว็บแอปที่มีการเข้าชมสูงหรือเมื่อให้บริการสินทรัพย์ขนาดใหญ่ (เช่น รูปภาพความละเอียดสูงหรือส่วนของวิดีโอ) วิธีนี้ยังลดภาระ I/O เนื่องจากรูปแบบ ZIP รองรับการเข้าถึงแบบสุ่มต่อ entry แต่ละรายการ

## ข้อกำหนดเบื้องต้น
1. **Java Development Kit (JDK) 8+** ติดตั้ง  
2. IDE เช่น **IntelliJ IDEA**, **Eclipse**, หรือ **NetBeans**  
3. **Aspose.HTML for Java** library – ดาวน์โหลดได้จาก **[here](https://releases.aspose.com/html/java/)** และเพิ่ม JAR(s) ไปยัง classpath ของโปรเจคของคุณ  
4. ความคุ้นเคยพื้นฐานกับคอลเลกชันของ Java และการจัดการข้อยกเว้น  

## นำเข้าแพ็กเกจ
การนำเข้าต่อไปนี้ให้คุณเข้าถึงยูทิลิตี้เครือข่ายของ Aspose.HTML, การจัดการ MIME, และคลาส I/O มาตรฐานของ Java  

```java
import com.aspose.html.MimeType;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.StreamContent;
import com.aspose.html.utils.Stream;
```

## ขั้นตอนที่ 1: สร้างคลาส ZIP File Schema Handler
เราเริ่มโดยการสืบทอด `CustomSchemaMessageHandler` คอนสตรัคเตอร์จะลงทะเบียนสคีม่า `zip-file` ที่กำหนดเองและเก็บเส้นทางไปยังไฟล์ ZIP ที่ต้องการให้บริการ  

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
เมธอด `invoke` จะดักจับทุกคำขอที่ใช้สคีม่า `zip-file:` มันจะดึงเส้นทางที่ร้องขอ, ดึง entry ที่สอดคล้องเป็นสตรีม, และสร้าง **java zip file response** หากไม่พบ entry จะคืนค่าการตอบสนอง 404  

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
`GetFile` ใช้ API มาตรฐาน `java.util.zip.ZipFile` เพื่อค้นหา entry ภายใน archive และคืนค่าเป็น Aspose `Stream` นี่คือจุดที่การทำงาน **read zip entry java** เกิดขึ้นจริง  

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
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **`IOException` on large files** | บัฟเฟอร์เริ่มต้นอาจเล็กเกินไป | เพิ่มขนาดบัฟเฟอร์หรือใช้ช่อง `java.nio` สำหรับสตรีม |
| **Incorrect MIME type** | `MimeType.fromFileExtension` อาจคืนค่า `application/octet-stream` สำหรับส่วนขยายที่ไม่รู้จัก | ตั้งค่า MIME type ด้วยตนเองตามประเภทเนื้อหาที่คุณทราบ |
| **Thread‑safety concerns** | การแชร์อินสแตนซ์ `ZipFile` เดียวกันระหว่างหลายเธรดอาจทำให้เกิด `ZipException` | เปิด `ZipFile` ใหม่ภายใน `GetFile` (ตามตัวอย่าง) เพื่อให้แต่ละคำขอได้รับแฮนด์เดิลของตนเอง |
| **Missing entry returns 404** | ปัญหาการทำให้เส้นทางเป็นมาตรฐาน (เช่น มีสแลชนำหน้า) | คำสั่ง `substring(1)` จะลบสแลชนำหน้า; ตรวจสอบให้แน่ใจว่า URI ของคำขอตรงกับโครงสร้างภายในของ archive |

## คำถามที่พบบ่อย

### ฉันสามารถใช้ตัวจัดการนี้กับรูปแบบ archive อื่นเช่น RAR หรือ TAR ได้หรือไม่?
ขณะนี้ตัวจัดการออกแบบมาสำหรับไฟล์ ZIP เท่านั้น อย่างไรก็ตาม ด้วยการปรับแต่งบางอย่างอาจทำให้สามารถรองรับรูปแบบ archive อื่นได้

### จะเกิดอะไรขึ้นหากไฟล์ ZIP เสียหาย?
หากไฟล์ ZIP เสียหาย ตัวจัดการจะไม่สามารถดึงไฟล์ได้และคุณอาจเจอ `IOException` ควรจัดการกับข้อยกเว้นเหล่านี้เพื่อให้แอปพลิเคชันของคุณคงที่

### สามารถแก้ไขไฟล์ภายใน ZIP archive ด้วยตัวจัดการนี้ได้หรือไม่?
ไม่ได้, ตัวจัดการนี้ออกแบบมาเพื่ออ่านไฟล์จาก ZIP archive เท่านั้น ไม่ได้สำหรับการแก้ไขไฟล์

### ฉันจะปรับปรุงประสิทธิภาพของการให้บริการไฟล์ขนาดใหญ่ได้อย่างไร?
สำหรับไฟล์ขนาดใหญ่ ควรพิจารณาใช้เทคนิคการแบ่งไฟล์เป็นชั้นหรือการสตรีมเพื่อลดการใช้หน่วยความจำและเพิ่มประสิทธิภาพ

### ตัวจัดการนี้สามารถใช้ในสภาพแวดล้อมหลายเธรดได้หรือไม่?
ได้, แต่คุณต้องรับประกันความปลอดภัยของเธรด โดยเฉพาะเมื่อจัดการกับทรัพยากรที่ใช้ร่วมกันเช่นไฟล์ ZIP  

---

**Last Updated:** 2026-02-15  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}