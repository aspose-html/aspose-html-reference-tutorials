---
date: 2026-01-07
description: แปลง EPUB เป็น XPS อย่างง่ายดายด้วย Aspose.HTML สำหรับ Java. ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อกระบวนการแปลงที่ราบรื่น.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: วิธีแปลง EPUB เป็น XPS ด้วยผู้ให้บริการสตรีมแบบกำหนดเอง
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง EPUB เป็น XPS ด้วย Custom Stream Provider

ในโลกการเผยแพร่ดิจิทัลในปัจจุบัน **convert EPUB to XPS** เป็นความต้องการที่พบบ่อย—ไม่ว่าจะต้องการการแสดงผลแบบ fixed‑layout เพื่อการพิมพ์, การเก็บถาวร, หรือการแชร์ระหว่างอุปกรณ์ Windows Aspose.HTML for Java ทำให้การแปลงนี้ง่ายดาย และโดยการใช้ custom memory stream provider คุณสามารถเก็บกระบวนการทั้งหมดไว้ในหน่วยความจำ ซึ่งเหมาะอย่างยิ่งสำหรับสภาพแวดล้อมคลาวด์หรือการทำงานที่ต้องการประสิทธิภาพสูง ด้านล่างนี้คุณจะพบทุกอย่างที่ต้องการเพื่อเริ่มต้น ตั้งแต่ข้อกำหนดเบื้องต้นจนถึงตัวอย่างที่พร้อมรันเต็มรูปแบบ

## คำตอบด่วน
- **ผลลัพธ์ของคำถามคืออะไร?** เอกสาร XPS ที่คงรูปแบบและฟอนต์ไว้
- **ต้องใช้พื้นที่เซนส์หรือไม่?** การทดลองทดลองฟรีสำหรับการทดสอบสามารถใช้ได้; จะต้องมีเซนส์เป็นศูนย์กลางอย่างแท้จริง
- **สามารถรันได้ในนานแค่ไหน?** ไม่จำเป็นต้องเขียนไฟล์ลงระบบหากเก็บบันทึกข้อมูล
- ** รองรับรองรับ Java ใด ๆ ?** Java8 หรือรองรับ
- ** ต้องการผู้ให้บริการสตรีมแบบกำหนดเองหรือไม่** ไม่จำเป็นต้องอาศัยการควบคุมโดยตรงและการจัดการผลลัพธ์

## “แปลง EPUB เป็น XPS” คืออะไร?
ไดร์เวอร์ไฟล์ EPUB เป็น XPS นั่นคือในรูปแบบในรูปแบบ e-book ที่เป็นรีฟลอว์ได้ให้เป็นเอกสารที่มีการวางรูปแบบคงที่-layout และความอิสระต่ออุปกรณ์ XPS (XML Paper Specification) เป็นมาตรฐานของ Microsoft ที่เทียบเคียงกับ PDF ในสถานการณ์ที่ต้องการความสำคัญที่จะไม่ปรับปรุงระหว่างแพลตฟอร์มต่างๆ

## เหตุใดจึงต้องใช้ผู้ให้บริการสตรีมแบบกำหนดเอง
`MemoryStreamProvider` ไม่จำเป็นต้องเก็บผลลัพธ์ที่กล่าวถึง RAM แทนเนื้อหาไฟล์ชั่วคราวลงวิธีการวิธีการ:
- ลดความเครียด I/O
- ปรับปรุงประสิทธิภาพในการติดตาม Server-less หรือ Micro-service
- ไม่ต้องพูดถึงในการสตรีมผลลัพธ์โดยตรงไปยังสถานที่ต่างๆ, ที่การประชุมหรือ API อื่นๆ

## ข้อกำหนดเบื้องต้น

หากต้องการ **แปลง EPUB เป็น XPS** ดำเนินการเพื่อให้คุณสามารถปฏิบัติตามคำสั่งได้ทันที:

### 1. Aspose.HTML สำหรับไลบรารี Java

ติดตั้งและรับฟังไลบรารี Aspose.HTML for Java สำหรับ Java ของคุณหากคุณยังไม่ได้ทำสารคดีจาก [ลิงก์ดาวน์โหลด](https://releases.aspose.com/html/java/)

### 2. ใส่ไฟล์ EPUB

มีไฟล์ EPUB ที่ต้องการแปลงเป็น XPS ที่พร้อมใช้งานสำหรับการแปลง

ไม่ต้องเตรียมข้อกำหนดทั้งหมดแล้วเป็นส่วนขั้นตอนการควบคุมทีละขั้นตอน

## แพคเกจนำเข้า

ก่อนเริ่มทำงาน ให้แน่ใจว่าได้ import แพ็กเกจที่จำเป็นสำหรับ Aspose.HTML for Java เพื่อใช้ฟังก์ชันต่าง ๆ

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## เปิดไฟล์ EPUB

ขั้นแรกคุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน โดยใช้ `FileInputStream` เข้าถึงไฟล์ EPUB

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## สร้าง MemoryStreamProvider

ต่อไปสร้างอินสแตนซ์ของ `MemoryStreamProvider` ซึ่งอ็อบเจ็กต์นี้จะเก็บผลลัพธ์การแปลงไว้ในหน่วยความจำ

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## แปลง EPUB เป็น XPS

จากนั้นใช้เมธอด `Converter.convertEPUB` เพื่อแปลงไฟล์ EPUB เป็น XPS โดยMemoryStreamProvider` จะเป็นแหล่งที่มาของสตรีมปลายทาง

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## รับข้อมูลที่ได้

เมื่อการแปลงเสร็จสิ้น ให้ดึง memory stream ที่บรรจุข้อมูล XPS ออกมา

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## บันทึกผลลัพธ์ (ไม่บังคับ)

หากต้องการไฟล์จริง—เช่นเพื่อการดีบักหรือตรวจสอบแบบออฟไลน์—ให้เขียน memory stream ลงดิสก์ ในหลายกรณีการผลิตคุณสามารถข้ามขั้นตอนนี้และสตรีมข้อมูลโดยตรงไปยังไคลเอนต์ได้

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## โค้ดต้นฉบับทั้งหมด

ด้านล่างเป็นตัวอย่างโค้ดเต็มรูปแบบที่พร้อมรัน คุณสามารถคัดลอก, วางและปรับใช้ในโปรเจกต์ของคุณได้เลย

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## ปัญหาทั่วไปและแนวทางแก้ไข

| ปัญหา | ทำไมมันถึงเกิดขึ้น | แก้ไข |
|----------------------|----------------|-----|
| **`java.lang.OutOfMemoryError`** | ใน EPUB ขนาดใหญ่เกินขนาดฮีปเกิดขึ้นเมื่อเห็นได้ชัดว่าทั้งหมด | ขนาดฮีปของ JVM (`-Xmx`) หรือ EPUB อาจจะเป็นถ้าเป็นไปได้ |
| **แบบอักษรหายไปใน XPS** | ฟอนต์ไม่ต้องฝังใน EPUB ไม่สามารถใช้บนเครื่องแปลง | ตัดต่อให้ฟอนต์ติดตั้งบนเซิร์ฟเวอร์หรือฝังฟอนต์ใน EPUB |
| **`UnsupportedOperationException` จาก `MemoryStreamProvider`** | ใช้ Aspose.HTML ได้ที่ | อัปเดตเป็นปัจจุบันของ Aspose.HTML สำหรับ Java |

## คำถามที่พบบ่อย

### 1. EPUB คืออะไร?

EPUB (Electronic Publication) ประเภทของไฟล์ที่ใช้สำหรับ eBooks ออกแบบให้อ่านได้หลากหลาย เช่น eReader, สมาร์ทโฟน, และสมาร์ทโฟน

### 2. XPS คืออะไร?

XPS (XML Paper Specification) ในรูปแบบเอกสารที่ใช้งานได้ Microsoft ใช้สำหรับแชร์และเก็บเอกสารโดยคงลักษณะการทำงานและเสียงที่เข้ากันได้

### 3. เหตุใดจึงต้องใช้ Aspose.HTML สำหรับ Java?

Aspose.HTML สำหรับ Java เป็นไลบรารีที่สามารถพบได้ในการดูแลเอกสาร, ร้อง, รีโมทคอนโทรลทำคำสั่งมีระบบปฏิบัติการที่รองรับและรองรับหลายรูปแบบไฟล์ที่รองรับที่มีคุณค่าสำหรับการตรวจสอบ

### 4. ฉันสามารถแปลงรูปแบบเอกสารอื่นโดยใช้ Aspose.HTML สำหรับ Java ได้หรือไม่

ได้, Aspose.HTML สำหรับ Java รองรับหลายรูปแบบ ได้แก่ HTML, EPUB, XPS ระบบควบคุมการจัดเก็บข้อมูลสำหรับการจัดการเอกสาร

### 5. ฉันจะหาแหล่งข้อมูลเพิ่มเติมและการสนับสนุนได้จากที่ไหน?

สำหรับเอกสารและความสำเร็จอย่างต่อเนื่อง [Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/) และ [support forum](https://forum.aspose.com/)

---

**อัปเดตล่าสุด:** 2026-01-07
**ทดสอบด้วย:** Aspose.HTML สำหรับ Java 24.12 (ล่าสุด ณ เวลาที่เขียน)
**ผู้เขียน:** สมมติ 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}