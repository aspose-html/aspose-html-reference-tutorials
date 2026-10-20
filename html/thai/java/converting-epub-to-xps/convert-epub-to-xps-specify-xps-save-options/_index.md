---
date: 2026-03-29
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อกำหนดตัวเลือกการบันทึก XPS,
  แปลง EPUB เป็น XPS, และจัดการการให้สิทธิ์ใช้งาน
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: วิธีใช้ตัวเลือกการบันทึก HTML ของ Aspose สำหรับแปลง EPUB เป็น XPS
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose HTML Save Options สำหรับการแปลง EPUB เป็น XPS

ในคู่มือนี้เราจะแสดง **วิธีใช้ Aspose** HTML Save Options เพื่อแปลงเอกสาร EPUB เป็น XPS พร้อมการควบคุมเต็มที่ของขนาดหน้า, สีพื้นหลัง, และข้อพิจารณาด้านลิขสิทธิ์ ไม่ว่าคุณจะสร้างระบบประมวลผลแบบชุดหรือเครื่องมือแปลงแบบครั้งเดียว ขั้นตอนเหล่านี้จะช่วยให้คุณได้ผลลัพธ์ที่เชื่อถือได้อย่างรวดเร็ว.

## คำตอบสั้น
- **Aspose HTML Save Options ทำอะไร?** มันให้คุณปรับขนาดหน้า, สีพื้นหลัง, และการตั้งค่าเรนเดอร์อื่น ๆ เมื่อบันทึกเป็นรูปแบบเช่น XPS.  
- **ต้องใช้ไลบรารีอะไร?** Aspose.HTML for Java (เวอร์ชันล่าสุด).  
- **ต้องมีลิขสิทธิ์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการประเมิน; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **สามารถเปลี่ยนขนาดหน้าได้หรือไม่?** ได้ – คุณสามารถกำหนดความกว้างและความสูงใด ๆ ผ่าน `PageSetup`.  
- **การแปลงเร็วหรือไม่?** สำหรับไฟล์ EPUB ปกติ การแปลงจะเสร็จในไม่กี่วินาทีบน JVM สมัยใหม่.

## “how to use aspose” คืออะไรในบริบทนี้?
วลี **วิธีใช้ Aspose** หมายถึงขั้นตอนปฏิบัติเพื่อใช้ประโยชน์จากไลบรารี Aspose.HTML ในการจัดการและแปลงเอกสารบนเว็บ ในบทเรียนนี้เราจะเน้นที่ **aspose html save options** ที่ให้คุณปรับแต่งผลลัพธ์เมื่อคุณ **แปลง EPUB เป็น XPS**.

## ทำไมต้องใช้ Aspose.HTML สำหรับ Java เพื่อแปลง EPUB เป็น XPS?
- **ความแม่นยำสูง** – รักษาการจัดวางที่ซับซ้อน, ฟอนต์, และกราฟิกเวกเตอร์.  
- **การควบคุมผ่านโปรแกรม** – ทำการแปลงเป็นชุดอัตโนมัติภายในแอปพลิเคชัน Java.  
- **ไม่มีการพึ่งพาภายนอก** – ไลบรารี Java แท้, ไม่มีส่วนประกอบเนทีฟ.  
- **ผลลัพธ์ที่ปรับแต่งได้** – ด้วย save options คุณสามารถปรับ XPS ให้ตรงตามความต้องการของคุณ เช่น **ระบุขนาดหน้า** หรือกำหนดพื้นหลังแบบกำหนดเอง.  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกในโค้ด โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

1. **สภาพแวดล้อมการพัฒนา Java** – ติดตั้ง JDK 8 หรือสูงกว่า.  
2. **ไลบรารี Aspose.HTML for Java** – ดาวน์โหลดจาก [download link](https://releases.aspose.com/html/java/).  
3. **ไฟล์ EPUB** – EPUB ต้นฉบับที่คุณต้องการ **แปลง EPUB เป็น XPS**.  

เมื่อคุณเตรียมสิ่งเหล่านี้ไว้แล้ว คุณจะสามารถทำตามขั้นตอนได้โดยไม่มีการขัดจังหวะ.

## นำเข้าแพ็กเกจ

แรกสุด ให้นำเข้าคลาสที่จำเป็น วางการนำเข้าเหล่านี้ที่ส่วนบนของไฟล์ซอร์ส Java ของคุณ:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

การนำเข้าดังกล่าวทำให้คุณเข้าถึงเอนจินการแปลงและ **Aspose HTML Save Options** ที่จำเป็นสำหรับการปรับแต่งอย่างละเอียด.

## เปิดไฟล์ EPUB

ต่อไป เปิดไฟล์ EPUB ที่ต้องการแปลง ตัวช่วย `Resources.input` จะโหลดไฟล์จากโฟลเดอร์ resources ของตัวอย่าง:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

การใช้บล็อก try‑with‑resources จะทำให้สตรีมถูกปิดโดยอัตโนมัติ.

## สร้าง XPS Save Options (กำหนดขนาดหน้าและพื้นหลัง)

ตอนนี้เราจะสร้างอินสแตนซ์ `XpsSaveOptions` และปรับแต่งมัน นี่คือจุดที่ **save options** ทำให้เด่นจริง ๆ:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **ขนาดหน้า** – ตั้งเป็น 3000 × 1000 พิกเซลในตัวอย่างนี้; ปรับให้ตรงกับขนาดกระดาษเป้าหมายของคุณหรือใช้ `Length.fromInches` เพื่อ **ระบุขนาดหน้า** เป็นนิ้ว.  
- **สีพื้นหลัง** – `AliceBlue` แสดงวิธีการเปลี่ยนสีพื้นหลังของแคนวาส; คุณสามารถเลือก `Color` ใดก็ได้.  

การตั้งค่าเหล่านี้เป็นส่วนหนึ่งของ **aspose html save options** ที่มีผลต่อเอกสาร XPS สุดท้าย.

## แปลง EPUB เป็น XPS

สุดท้าย เรียกใช้คอนเวอร์เตอร์ด้วยสตรีม, ตัวเลือกที่กำหนดค่าแล้ว, และเส้นทางเอาต์พุต:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

เมื่อบรรทัดนี้ทำงาน Aspose.HTML จะอ่านไฟล์ EPUB, ใช้การตั้งค่าหน้าและสีพื้นหลังที่คุณกำหนด, และเขียนไฟล์ XPS ที่สอดคล้องอย่างสมบูรณ์.

## ปัญหาและเคล็ดลับทั่วไป

- **ขนาดหน้าผิด** – ตรวจสอบให้แน่ใจว่าขนาดถูกระบุเป็นพิกเซล (หรือใช้ `Length.fromInches`).  
- **ฟอนต์หาย** – ฝังฟอนต์ที่จำเป็นใน EPUB หรือติดตั้งบนโฮสต์ JVM เพื่อหลีกเลี่ยงการใช้ฟอนต์สำรอง.  
- **ไฟล์ขนาดใหญ่** – สำหรับ EPUB ขนาดใหญ่มาก ให้เพิ่ม heap ของ JVM (`-Xmx`) เพื่อป้องกัน `OutOfMemoryError`.  
- **การลิขสิทธิ์ Aspose HTML** – ตรวจสอบว่าคุณได้โหลดลิขสิทธิ์ที่ถูกต้องก่อนการแปลง; มิฉะนั้นจะมีลายน้ำเวอร์ชันทดลองปรากฏ.

## สรุป

โดยใช้ **Aspose HTML Save Options** คุณจะได้การควบคุมที่แม่นยำว่าการแปลง EPUB ไปเป็น XPS ทำอย่างไร ขั้นตอนข้างต้นแสดงให้คุณเห็นวิธี **แปลง EPUB**, ตั้ง **ขนาดหน้า**, เปลี่ยนพื้นหลัง, และทำการแปลงด้วยเพียงไม่กี่บรรทัดของโค้ด Java ผสานรูปแบบนี้เข้ากับกระบวนการประมวลผลแบบชุดของคุณเพื่อทำงานการเผยแพร่โดยอัตโนมัติอย่างมีประสิทธิภาพ.

## คำถามที่พบบ่อย

**Q: Aspose.HTML for Java คืออะไร?**  
A: เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถสร้าง, แก้ไข, เรนเดอร์, และแปลง HTML, EPUB, และเอกสารเว็บอื่น ๆ ได้โดยไม่ต้องใช้เบราว์เซอร์.

**Q: สามารถใช้ในโครงการเชิงพาณิชย์ได้หรือไม่?**  
A: ได้. สำหรับการใช้งานในผลิตภัณฑ์จริง คุณต้องมีลิขสิทธิ์ที่ถูกต้อง คุณสามารถซื้อได้ที่ [purchase page](https://purchase.aspose.com/buy).

**Q: มีรุ่นทดลองฟรีหรือไม่?**  
A: แน่นอน. ดาวน์โหลดรุ่นทดลองจาก [here](https://releases.aspose.com/).

**Q: จะหาได้รับการสนับสนุนได้จากที่ไหน?**  
A: การสนับสนุนจากชุมชนและความช่วยเหลืออย่างเป็นทางการมีให้ผ่านฟอรั่มของ Aspose ที่ [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: ข้อกำหนดระบบคืออะไร?**  
A: ต้องมี Java Development Kit (JDK) 8+ และระบบปฏิบัติการที่รองรับโดย Aspose runtime. ตรวจสอบให้แน่ใจว่าระบบของคุณตรงตามข้อกำหนดเบื้องต้นที่ระบุไว้ก่อนหน้า.

---

**Last Updated:** 2026-03-29  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}