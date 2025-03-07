---
title: ปรับแต่งระยะขอบหน้า HTML ด้วย Aspose.HTML
linktitle: ส่วนขยาย CSS - การเพิ่มชื่อเรื่องและหมายเลขหน้า
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีปรับแต่งระยะขอบหน้า เพิ่มหมายเลขหน้าและชื่อเรื่องให้กับเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java
weight: 10
url: /th/java/advanced-usage/css-extensions-adding-title-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปรับแต่งระยะขอบหน้า HTML ด้วย Aspose.HTML

Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพสำหรับการประมวลผลเอกสาร HTML ในแอปพลิเคชัน Java ในบทช่วยสอนนี้ เราจะสำรวจวิธีการสร้างระยะขอบหน้าแบบกำหนดเองและเพิ่มหมายเลขหน้าและชื่อเรื่องลงในเอกสาร HTML ของคุณโดยใช้ Aspose.HTML สำหรับ Java คำแนะนำทีละขั้นตอนนี้จะแบ่งกระบวนการออกเป็นขั้นตอนที่จัดการได้เพื่อช่วยให้คุณรวมคุณลักษณะเหล่านี้เข้ากับเอกสาร HTML ของคุณได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา Java บนคอมพิวเตอร์ของคุณแล้ว

2.  Aspose.HTML สำหรับ Java: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ Java จาก[ที่นี่](https://releases.aspose.com/html/java/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็นจาก Aspose.HTML สำหรับ Java เพิ่มคำสั่งนำเข้าต่อไปนี้ลงในโค้ด Java ของคุณ:

```java
// นำเข้าแพ็กเกจ Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

ตอนนี้ มาแบ่งกระบวนการการเพิ่มระยะขอบหน้าแบบกำหนดเอง หมายเลขหน้า และชื่อเรื่องให้เป็นขั้นตอนที่จัดการได้:

## ขั้นตอนที่ 1: เริ่มต้นการกำหนดค่าและระยะขอบหน้า

```java
// เริ่มต้นวัตถุการกำหนดค่าและตั้งค่าระยะขอบหน้าสำหรับเอกสาร
Configuration configuration = new Configuration();
try {
    // รับบริการตัวแทนผู้ใช้
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // ตั้งค่ารูปแบบของระยะขอบที่กำหนดเองและสร้างเครื่องหมายบนนั้น
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

ในขั้นตอนนี้ เราจะเริ่มต้นวัตถุการกำหนดค่าและตั้งค่าระยะขอบหน้าแบบกำหนดเอง รวมถึงตำแหน่งของตัวนับหน้าและชื่อหน้า

## ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```java
// เริ่มต้นเอกสาร HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ที่นี่ เราจะสร้างเอกสาร HTML พร้อมเนื้อหาตัวอย่าง (ในกรณีนี้คือข้อความ "Hello World") และใช้การกำหนดค่าจากขั้นตอนที่ 1

## ขั้นตอนที่ 3: เริ่มต้นอุปกรณ์เอาต์พุตและเรนเดอร์เอกสาร

```java
// เริ่มต้นอุปกรณ์ส่งออก
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //ส่งเอกสารไปยังอุปกรณ์ส่งออก
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

ในขั้นตอนนี้ เราจะตั้งค่าอุปกรณ์เอาต์พุตและเรนเดอร์เอกสาร HTML เอกสารจะถูกประมวลผลและบันทึกเป็นไฟล์ XPS พร้อมระยะขอบหน้า หมายเลขหน้า และชื่อเรื่องที่ระบุไว้

## บทสรุป

ขอแสดงความยินดี! คุณได้เรียนรู้วิธีการสร้างระยะขอบหน้าแบบกำหนดเองและเพิ่มหมายเลขหน้าและชื่อเรื่องลงในเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว การปรับแต่งนี้ช่วยให้คุณสร้างเอกสารที่ดูเป็นมืออาชีพและดึงดูดสายตามากขึ้น

 หากคุณมีคำถามหรือประสบปัญหาใดๆ โปรดเยี่ยมชม[เอกสาร Aspose.HTML สำหรับ Java](https://reference.aspose.com/html/java/) หรือขอความช่วยเหลือได้ที่[ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร?

A1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ให้เครื่องมืออันทรงพลังสำหรับการทำงานกับเอกสาร HTML ในแอปพลิเคชัน Java

### คำถามที่ 2: ฉันสามารถปรับแต่งระยะขอบหน้าเพิ่มเติมได้หรือไม่

A2: ใช่ คุณสามารถปรับเปลี่ยนรูปแบบ CSS ในขั้นตอนที่ 1 เพื่อกำหนดระยะขอบหน้าตามความต้องการของคุณได้

### คำถามที่ 3: ฉันจะเพิ่มเนื้อหาเพิ่มเติมลงในเอกสาร HTML ได้อย่างไร

A3: คุณสามารถปรับเปลี่ยนเนื้อหา HTML ในขั้นตอนที่ 2 ได้โดยการแทนที่เนื้อหาตัวอย่างด้วยเนื้อหาของคุณเอง

### คำถามที่ 4: Aspose.HTML สำหรับ Java สามารถใช้งานร่วมกับรูปแบบเอกสารอื่นได้หรือไม่

A4: ใช่ Aspose.HTML สำหรับ Java สามารถใช้แปลงเอกสาร HTML เป็นรูปแบบต่างๆ รวมถึง PDF, XPS และรูปภาพ

### คำถามที่ 5: ฉันต้องมีใบอนุญาตในการใช้ Aspose.HTML สำหรับ Java หรือไม่?

 A5: ใช่ คุณสามารถขอรับใบอนุญาตหรือทดลองใช้งานฟรีได้จาก[ที่นี่](https://purchase.aspose.com/buy) หรือ[ที่นี่](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
