---
date: 2026-01-09
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อกำหนดตัวเลือกการบันทึก XPS
  และแปลง EPUB เป็น XPS อย่างมีประสิทธิภาพ
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: การระบุตัวเลือกการบันทึก Aspose HTML สำหรับการแปลง EPUB เป็น XPS
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ระบุ Aspose HTML Save Options สำหรับ EPUB ไปยัง XPS

การแปลงเอกสาร EPUB เป็น XPS สามารถเป็นส่วนที่มีประโยชน์ในกระบวนการทำงานของการเผยแพร่, และ **Aspose HTML Save Options** ให้คุณควบคุมผลลัพธ์ได้อย่างละเอียด ในบทเรียนนี้เราจะอธิบายขั้นตอนที่จำเป็นเพื่อกำหนดค่า save options เหล่านี้ด้วย Aspose.HTML for Java และสร้างไฟล์ XPS คุณภาพสูง

## คำตอบอย่างรวดเร็ว
- **Aspose HTML Save Options ทำอะไร?** มันทำให้คุณสามารถปรับขนาดหน้า, สีพื้นหลัง, และการตั้งค่าเรนเดอร์อื่น ๆ เมื่อบันทึกเป็นรูปแบบเช่น XPS.  
- **ต้องใช้ไลบรารีใด?** Aspose.HTML for Java (รุ่นล่าสุด).  
- **ต้องการไลเซนส์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **สามารถเปลี่ยนขนาดหน้ากระดาษได้หรือไม่?** ได้ – คุณสามารถตั้งค่าความกว้างและความสูงใด ๆ ผ่าน `PageSetup`.  
- **การแปลงเร็วหรือไม่?** สำหรับไฟล์ EPUB ปกติ การแปลงจะเสร็จในไม่กี่วินาทีบน JVM สมัยใหม่.

## Aspose HTML Save Options คืออะไร?
Aspose HTML Save Options คือชุดของคุณสมบัติที่ควบคุมวิธีการเรนเดอร์และบันทึกเอกสาร HTML, EPUB หรือเอกสารเว็บอื่น ๆ ไปยังรูปแบบเป้าหมายเช่น XPS, PDF หรือไฟล์ภาพ พวกมันให้คุณกำหนดการจัดหน้า, สีพื้นหลัง, ระยะขอบ, และอื่น ๆ เพื่อให้ไฟล์ที่ได้ตรงตามข้อกำหนดการออกแบบของคุณ

## ทำไมต้องใช้ Aspose.HTML for Java เพื่อแปลง EPUB เป็น XPS?
- **ความแม่นยำสูง** – รักษาการจัดเลย์เอาต์ที่ซับซ้อน, ฟอนต์, และกราฟิกเวกเตอร์.  
- **การควบคุมแบบโปรแกรม** – ทำการแปลงเป็นชุดอัตโนมัติภายในแอปพลิเคชัน Java.  
- **ไม่มีการพึ่งพาภายนอก** – ไลบรารี Java แท้, ไม่มีคอมโพเนนต์เนทีฟ.  
- **ผลลัพธ์ที่ปรับแต่งได้** – ด้วย save options คุณสามารถปรับ XPS ให้ตรงตามความต้องการของคุณได้

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะลงลึกในโค้ด, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

1. **สภาพแวดล้อมการพัฒนา Java** – ติดตั้ง JDK 8 หรือสูงกว่า.  
2. **ไลบรารี Aspose.HTML for Java** – ดาวน์โหลดจาก [download link](https://releases.aspose.com/html/java/).  
3. **ไฟล์ EPUB** – ไฟล์ EPUB ต้นฉบับที่คุณต้องการแปลง.  

การมีสิ่งเหล่านี้พร้อมจะทำให้คุณสามารถทำตามขั้นตอนได้โดยไม่มีการขัดจังหวะ

## นำเข้าแพ็กเกจ
แรกสุด, นำเข้าคลาสที่จำเป็น. วางคำสั่ง import ที่ส่วนบนของไฟล์ซอร์ส Java ของคุณ:

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

การนำเข้าดังกล่าวจะทำให้คุณเข้าถึงเอนจินการแปลงและ **Aspose HTML Save Options** ที่จำเป็นสำหรับการปรับแต่งละเอียด

## เปิดไฟล์ EPUB
ต่อไป, เปิดไฟล์ EPUB ที่คุณต้องการแปลง. ตัวช่วย `Resources.input` จะโหลดไฟล์จากโฟลเดอร์ resources ของตัวอย่าง:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

การใช้บล็อก try‑with‑resources จะทำให้สตรีมถูกปิดโดยอัตโนมัติ

## สร้าง XPS Save Options (กำหนดขนาดหน้าและพื้นหลัง)
ตอนนี้เราจะสร้างอินสแตนซ์ของ `XpsSaveOptions` และปรับแต่งมัน. ที่นี่คือจุดที่ **save options** แสดงศักยภาพจริง ๆ:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **ขนาดหน้า** – ตั้งเป็น 3000 × 1000 พิกเซลในตัวอย่างนี้; ปรับให้ตรงกับขนาดกระดาษเป้าหมายของคุณ.  
- **สีพื้นหลัง** – `AliceBlue` แสดงวิธีการเปลี่ยนพื้นหลังของแคนวาส; คุณสามารถเลือก `Color` ใดก็ได้.  

การตั้งค่าเหล่านี้เป็นส่วนหนึ่งของ **Aspose HTML Save Options** ที่มีผลต่อเอกสาร XPS สุดท้าย

## แปลง EPUB เป็น XPS
สุดท้าย, เรียกใช้ตัวแปลงพร้อมสตรีม, ตัวเลือกที่กำหนดค่า, และเส้นทางเอาต์พุต:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

เมื่อบรรทัดนี้ทำงาน, Aspose.HTML จะอ่านไฟล์ EPUB, ใช้การตั้งค่าหน้าและสีพื้นหลังที่คุณกำหนด, และเขียนไฟล์ XPS ที่สอดคล้องอย่างเต็มรูปแบบ

## ปัญหาทั่วไปและเคล็ดลับ
- **ขนาดหน้าที่ไม่ถูกต้อง** – ตรวจสอบให้แน่ใจว่าขนาดระบุเป็นพิกเซล (หรือใช้ `Length.fromInches`).  
- **ฟอนต์หาย** – ฝังฟอนต์ที่จำเป็นใน EPUB หรือทำการติดตั้งบนโฮสต์ JVM เพื่อหลีกเลี่ยงการใช้ฟอนต์สำรอง.  
- **ไฟล์ขนาดใหญ่** – สำหรับ EPUB ขนาดใหญ่มาก, เพิ่มขนาด heap ของ JVM (`-Xmx`) เพื่อป้องกัน `OutOfMemoryError`.  

## สรุป
โดยการใช้ **Aspose HTML Save Options**, คุณจะได้การควบคุมที่แม่นยำว่าการเรนเดอร์ EPUB ไปเป็น XPS ทำอย่างไร ขั้นตอนข้างต้นแสดงวิธีตั้งค่าขนาดหน้า, สีพื้นหลัง, และทำการแปลงด้วยเพียงไม่กี่บรรทัดของโค้ด Java. นำรูปแบบนี้ไปผสานในกระบวนการประมวลผลแบบชุดของคุณเพื่อทำงานการเผยแพร่อัตโนมัติอย่างมีประสิทธิภาพ

## คำถามที่พบบ่อย

**Q: Aspose.HTML for Java คืออะไร?**  
A: เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถสร้าง, แก้ไข, เรนเดอร์, และแปลงเอกสาร HTML, EPUB, และเอกสารเว็บอื่น ๆ ได้โดยไม่ต้องใช้เบราว์เซอร์.

**Q: สามารถใช้ในโครงการเชิงพาณิชย์ได้หรือไม่?**  
A: ได้. สำหรับการใช้งานในผลิตภัณฑ์จริงคุณต้องมีไลเซนส์ที่ถูกต้อง. คุณสามารถซื้อได้ที่ [purchase page](https://purchase.aspose.com/buy).

**Q: มีรุ่นทดลองฟรีหรือไม่?**  
A: มีแน่นอน. ดาวน์โหลดรุ่นทดลองจาก [here](https://releases.aspose.com/).

**Q: จะได้รับการสนับสนุนจากที่ไหน?**  
A: มีการสนับสนุนจากชุมชนและความช่วยเหลืออย่างเป็นทางการผ่านฟอรั่ม Aspose ที่ [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: ข้อกำหนดของระบบคืออะไร?**  
A: ต้องมี Java Development Kit (JDK) 8+ และระบบปฏิบัติการที่รองรับโดย runtime ของ Aspose. ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมของคุณตรงตามข้อกำหนดเบื้องต้นที่ระบุไว้ก่อนหน้า.

---

**อัปเดตล่าสุด:** 2026-01-09  
**ทดสอบด้วย:** Aspose.HTML for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}