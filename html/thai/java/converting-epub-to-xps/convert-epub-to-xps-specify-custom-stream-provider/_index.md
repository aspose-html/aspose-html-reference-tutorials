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

## Quick Answers
- **ผลลัพธ์ของการแปลงคืออะไร?** เอกสาร XPS ที่คงรูปแบบและฟอนต์ไว้  
- **ต้องใช้ไลเซนส์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการทดสอบ; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **สามารถรันในคอนเทนเนอร์ได้หรือไม่?** ได้—ไม่จำเป็นต้องเขียนไฟล์ลงระบบหากเก็บทั้งหมดในหน่วยความจำ  
- **รองรับเวอร์ชัน Java ใด?** Java 8 หรือสูงกว่า  
- **จำเป็นต้องใช้ custom stream provider หรือไม่?** ไม่จำเป็น แต่จะให้การควบคุมเต็มรูปแบบต่อการใช้หน่วยความจำและการจัดการผลลัพธ์

## What is “convert EPUB to XPS”?
การแปลงไฟล์ EPUB เป็น XPS คือการเปลี่ยนรูปแบบ e‑book ที่สามารถรีฟลว์ได้ให้เป็นเอกสารที่มีการจัดวางแบบ fixed‑layout และอิสระต่ออุปกรณ์ XPS (XML Paper Specification) เป็นมาตรฐานของ Microsoft ที่เทียบเคียงกับ PDF เหมาะสำหรับสถานการณ์ที่ต้องการการแสดงผลที่คงที่และไม่เปลี่ยนแปลงระหว่างแพลตฟอร์มต่าง ๆ

## Why use a custom stream provider?
`MemoryStreamProvider` แบบกำหนดเองทำให้คุณเก็บผลลัพธ์การแปลงไว้ใน RAM แทนการเขียนไฟล์ชั่วคราวลงดิสก์ วิธีนี้:
- ลดภาระ I/O  
- ปรับปรุงประสิทธิภาพในสถาปัตยกรรม server‑less หรือ micro‑service  
- ให้ความยืดหยุ่นในการสตรีมผลลัพธ์โดยตรงไปยังไคลเอนต์, ที่เก็บข้อมูลคลาวด์ หรือ API อื่น ๆ

## Prerequisites

เพื่อให้ **convert EPUB to XPS** สำเร็จ ให้ตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

### 1. Aspose.HTML for Java Library  

คุณต้องติดตั้งและกำหนดค่าไลบรารี Aspose.HTML for Java ในสภาพแวดล้อม Java ของคุณ หากยังไม่ได้ทำ สามารถดาวน์โหลดไลบรารีได้จาก [download link](https://releases.aspose.com/html/java/)

### 2. Input EPUB File  

คุณต้องมีไฟล์ EPUB ที่ต้องการแปลงเป็น XPS พร้อมใช้งานสำหรับกระบวนการแปลง

เมื่อคุณเตรียมข้อกำหนดทั้งหมดแล้ว เราจะเดินผ่านขั้นตอนการแปลงทีละขั้นตอน

## Import Packages

ก่อนเริ่มทำงาน ให้แน่ใจว่าได้ import แพ็กเกจที่จำเป็นสำหรับ Aspose.HTML for Java เพื่อใช้ฟังก์ชันต่าง ๆ

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## Open the EPUB File

ขั้นแรกคุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน โดยใช้ `FileInputStream` เข้าถึงไฟล์ EPUB

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## Create MemoryStreamProvider

ต่อไปสร้างอินสแตนซ์ของ `MemoryStreamProvider` ซึ่งอ็อบเจ็กต์นี้จะเก็บผลลัพธ์การแปลงไว้ในหน่วยความจำ

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## Convert EPUB to XPS

จากนั้นใช้เมธอด `Converter.convertEPUB` เพื่อแปลงไฟล์ EPUB เป็น XPS โดยMemoryStreamProvider` จะเป็นแหล่งที่มาของสตรีมปลายทาง

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Get Resulted Data

เมื่อการแปลงเสร็จสิ้น ให้ดึง memory stream ที่บรรจุข้อมูล XPS ออกมา

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Save the Output (Optional)

หากต้องการไฟล์จริง—เช่นเพื่อการดีบักหรือตรวจสอบแบบออฟไลน์—ให้เขียน memory stream ลงดิสก์ ในหลายกรณีการผลิตคุณสามารถข้ามขั้นตอนนี้และสตรีมข้อมูลโดยตรงไปยังไคลเอนต์ได้

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Complete Source Code

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

## Common Issues and Solutions

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **`java.lang.OutOfMemoryError`** | ไฟล์ EPUB ขนาดใหญ่เกินขนาด heap เริ่มต้นเมื่อเก็บไว้ในหน่วยความจำทั้งหมด | เพิ่มขนาด heap ของ JVM (`-Xmx`) หรือประมวลผล EPUB เป็นชิ้นส่วนถ้าเป็นไปได้ |
| **Missing fonts in XPS** | ฟอนต์ที่ไม่ได้ฝังใน EPUB ไม่พร้อมใช้งานบนเครื่องแปลง | ตรวจสอบให้ฟอนต์ที่จำเป็นติดตั้งบนเซิร์ฟเวอร์หรือฝังฟอนต์ใน EPUB |
| **`UnsupportedOperationException` from `MemoryStreamProvider`** | ใช้เวอร์ชัน Aspose.HTML ที่ล้าสมัย | อัปเดตเป็นรุ่นล่าสุดของ Aspose.HTML for Java |

## Frequently Asked Questions

### 1. What is EPUB?

EPUB (Electronic Publication) เป็นรูปแบบไฟล์ที่ใช้กันอย่างแพร่หลายสำหรับ eBooks ออกแบบให้อ่านได้ง่ายบนอุปกรณ์หลากหลาย เช่น eReader, แท็บเล็ต, และสมาร์ทโฟน

### 2. What is XPS?

XPS (XML Paper Specification) เป็นรูปแบบเอกสารที่พัฒนาโดย Microsoft ใช้สำหรับการแชร์และเก็บเอกสารโดยคงลักษณะการแสดงผลและการจัดวางอย่างสม่ำเสมอ

### 3. Why use Aspose.HTML for Java?

Aspose.HTML for Java เป็นไลบรารีที่ทรงพลัง ช่วยให้การจัดการเอกสาร, การแปลง, และการเรนเดอร์ทำได้ง่ายขึ้น มีฟีเจอร์ครบครันและรองรับหลายรูปแบบไฟล์ ทำให้เป็นเครื่องมือที่มีคุณค่าสำหรับนักพัฒนา

### 4. Can I convert other document formats using Aspose.HTML for Java?

ได้, Aspose.HTML for Java รองรับการแปลงหลายรูปแบบรวมถึง HTML, EPUB, XPS และอื่น ๆ อีกมากมาย เป็นเครื่องมืออเนกประสงค์สำหรับการจัดการเอกสาร

### 5. Where can I find additional resources and support?

สำหรับเอกสารและการสนับสนุน ให้เยี่ยมชม [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) และ [support forum](https://forum.aspose.com/)

---

**Last Updated:** 2026-01-07  
**Tested With:** Aspose.HTML for Java 24.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}