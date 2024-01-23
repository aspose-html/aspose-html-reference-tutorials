---
title: ปรับแต่งระยะขอบหน้า HTML ด้วย Aspose.HTML
linktitle: ส่วนขยาย CSS - การเพิ่มชื่อและหมายเลขหน้า
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีปรับแต่งระยะขอบหน้า เพิ่มหมายเลขหน้า และชื่อเรื่องให้กับเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java
type: docs
weight: 10
url: /th/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพสำหรับการประมวลผลเอกสาร HTML ในแอปพลิเคชัน Java ในบทช่วยสอนนี้ เราจะสำรวจวิธีสร้างระยะขอบหน้าแบบกำหนดเอง และเพิ่มหมายเลขหน้าและชื่อเรื่องให้กับเอกสาร HTML ของคุณโดยใช้ Aspose.HTML สำหรับ Java คำแนะนำทีละขั้นตอนนี้จะแบ่งกระบวนการออกเป็นขั้นตอนที่สามารถจัดการได้ เพื่อช่วยให้คุณรวมคุณลักษณะเหล่านี้เข้ากับเอกสาร HTML ของคุณได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา Java บนคอมพิวเตอร์ของคุณ

2.  Aspose.HTML สำหรับ Java: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ Java จาก[ที่นี่](https://releases.aspose.com/html/java/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็นจาก Aspose.HTML สำหรับ Java เพิ่มคำสั่งการนำเข้าต่อไปนี้ลงในโค้ด Java ของคุณ:

```java
// นำเข้าแพ็คเกจ Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

ตอนนี้ เรามาแจกแจงขั้นตอนการเพิ่มระยะขอบหน้า หมายเลขหน้า และชื่อแบบกำหนดเองลงในขั้นตอนที่สามารถจัดการได้:

## ขั้นตอนที่ 1: เริ่มต้นการกำหนดค่าและระยะขอบหน้า

```java
// เตรียมใช้งานออบเจ็กต์การกำหนดค่าและตั้งค่าระยะขอบหน้าสำหรับเอกสาร
Configuration configuration = new Configuration();
try {
    // รับบริการตัวแทนผู้ใช้
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // กำหนดรูปแบบของระยะขอบแบบกำหนดเองและสร้างเครื่องหมายบนนั้น
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

ในขั้นตอนนี้ เราจะเริ่มต้นออบเจ็กต์การกำหนดค่าและตั้งค่าระยะขอบของหน้าแบบกำหนดเอง รวมถึงตำแหน่งของตัวนับหน้าและชื่อหน้า

## ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```java
// เริ่มต้นเอกสาร HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ที่นี่ เราสร้างเอกสาร HTML พร้อมเนื้อหาตัวอย่าง (ในกรณีนี้คือข้อความ "Hello World") และใช้การกำหนดค่าจากขั้นตอนที่ 1

## ขั้นตอนที่ 3: เริ่มต้นอุปกรณ์เอาท์พุตและเรนเดอร์เอกสาร

```java
// เตรียมใช้งานอุปกรณ์เอาท์พุต
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

ในขั้นตอนนี้ เราตั้งค่าอุปกรณ์เอาท์พุตและเรนเดอร์เอกสาร HTML เอกสารจะได้รับการประมวลผลและบันทึกเป็นไฟล์ XPS โดยมีระยะขอบหน้า หมายเลขหน้า และชื่อเรื่องที่ระบุ

## บทสรุป

ยินดีด้วย! คุณได้เรียนรู้วิธีสร้างระยะขอบหน้าแบบกำหนดเองและเพิ่มหมายเลขหน้าและชื่อเรื่องให้กับเอกสาร HTML ของคุณโดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว การปรับแต่งนี้ช่วยให้คุณสร้างเอกสารที่เป็นมืออาชีพและดึงดูดสายตามากขึ้น

 หากคุณมีคำถามหรือประสบปัญหาใด ๆ โปรดเยี่ยมชมที่[Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/) หรือขอความช่วยเหลือได้ที่[กำหนดฟอรั่มการสนับสนุน](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร

คำตอบ 1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่มีเครื่องมืออันทรงพลังสำหรับการทำงานกับเอกสาร HTML ในแอปพลิเคชัน Java

### คำถามที่ 2: ฉันสามารถปรับแต่งระยะขอบของหน้าเพิ่มเติมได้หรือไม่

A2: ได้ คุณสามารถแก้ไขสไตล์ CSS ได้ในขั้นตอนที่ 1 เพื่อปรับแต่งระยะขอบของหน้าตามความต้องการของคุณ

### คำถามที่ 3: ฉันจะเพิ่มเนื้อหาเพิ่มเติมลงในเอกสาร HTML ได้อย่างไร

A3: คุณสามารถปรับเปลี่ยนเนื้อหา HTML ในขั้นตอนที่ 2 ได้โดยการแทนที่เนื้อหาตัวอย่างด้วยเนื้อหาของคุณเอง

### คำถามที่ 4: Aspose.HTML สำหรับ Java เข้ากันได้กับรูปแบบเอกสารอื่นๆ หรือไม่

ตอบ 4: ได้ Aspose.HTML สำหรับ Java สามารถใช้แปลงเอกสาร HTML เป็นรูปแบบต่างๆ ได้ รวมถึง PDF, XPS และรูปภาพ

### คำถามที่ 5: ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.HTML สำหรับ Java หรือไม่

 A5: ได้ คุณสามารถขอรับใบอนุญาตหรือทดลองใช้ฟรีได้จาก[ที่นี่](https://purchase.aspose.com/buy) หรือ[ที่นี่](https://releases.aspose.com/).