---
title: DOM Mutation Observer พร้อม Aspose.HTML สำหรับ Java
linktitle: DOM Mutation Observer - การสังเกตการเพิ่มโหนด
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อนำ DOM Mutation Observer ไปใช้ในคู่มือทีละขั้นตอนนี้ ตรวจสอบและตอบสนองต่อการเปลี่ยนแปลง DOM ได้อย่างมีประสิทธิภาพ
weight: 11
url: /th/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DOM Mutation Observer พร้อม Aspose.HTML สำหรับ Java


คุณเป็นนักพัฒนา Java ที่ต้องการสังเกตและตอบสนองต่อการเปลี่ยนแปลงใน Document Object Model (DOM) ของเอกสาร HTML หรือไม่ Aspose.HTML สำหรับ Java นำเสนอโซลูชันอันทรงพลังสำหรับงานนี้ ในคู่มือทีละขั้นตอนนี้ เราจะมาสำรวจวิธีใช้ Aspose.HTML สำหรับ Java เพื่อสร้างเอกสาร HTML และสังเกตการเพิ่มโหนดด้วย Mutation Observer บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการ โดยแบ่งตัวอย่างแต่ละตัวอย่างออกเป็นหลายขั้นตอน เมื่อสิ้นสุด คุณจะสามารถนำ DOM Mutation Observers ไปใช้กับโปรเจ็กต์ Java ของคุณได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกการใช้ Aspose.HTML สำหรับ Java เรามาตรวจสอบก่อนว่าคุณได้เตรียมข้อกำหนดเบื้องต้นที่จำเป็นไว้แล้ว:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) ในระบบของคุณแล้ว

2.  Aspose.HTML สำหรับ Java: คุณจะต้องดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ Java คุณสามารถค้นหาลิงก์ดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment) - ใช้ Java IDE ที่คุณต้องการ เช่น IntelliJ IDEA หรือ Eclipse สำหรับการเขียนและรันโค้ด Java

## แพ็คเกจนำเข้า

หากต้องการเริ่มต้นใช้งาน Aspose.HTML สำหรับ Java คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นลงในโค้ด Java ของคุณ โดยคุณสามารถทำได้ดังนี้:

```java
// นำเข้าแพ็คเกจที่จำเป็น
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// สร้างเอกสาร HTML ที่ว่างเปล่า
HTMLDocument document = new HTMLDocument();
```

ตอนนี้ คุณได้นำเข้าแพ็คเกจที่จำเป็นแล้ว มาดูคำแนะนำทีละขั้นตอนในการใช้งาน DOM Mutation Observer ใน Java กัน

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ผู้สังเกตการณ์การกลายพันธุ์

ขั้นแรก คุณต้องสร้างอินสแตนซ์ Mutation Observer ตัวสังเกตการณ์นี้จะคอยตรวจสอบการเปลี่ยนแปลงใน DOM และดำเนินการฟังก์ชันเรียกกลับเมื่อเกิดการกลายพันธุ์

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

ในขั้นตอนนี้ เราจะสร้างผู้สังเกตการณ์พร้อมด้วยฟังก์ชันการโทรกลับที่พิมพ์ข้อความเมื่อมีการเพิ่มโหนดใน DOM

## ขั้นตอนที่ 2: กำหนดค่าผู้สังเกตการณ์

ตอนนี้เรามาตั้งค่าตัวสังเกตการณ์ด้วยตัวเลือกที่ต้องการกัน เราต้องการสังเกตการณ์การเปลี่ยนแปลงรายการย่อยและการเปลี่ยนแปลงซับทรี รวมถึงการเปลี่ยนแปลงข้อมูลอักขระด้วย

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// ส่งผ่านโหนดเป้าหมายเพื่อสังเกตด้วยการกำหนดค่าที่ระบุ
observer.observe(document.getBody(), config);
```

 ที่นี่เราตั้งค่า`config` วัตถุเพื่อเปิดใช้งานการสังเกตรายการย่อย ซับทรี และการเปลี่ยนแปลงข้อมูลอักขระ จากนั้นเราส่งโหนดเป้าหมาย (ในกรณีนี้คือเอกสาร)`<body>`) และการกำหนดค่าให้กับผู้สังเกตการณ์

## ขั้นตอนที่ 3: ปรับเปลี่ยน DOM

ตอนนี้เราจะทำการเปลี่ยนแปลงบางอย่างใน DOM เพื่อเรียกใช้ตัวสังเกตการณ์ เราจะสร้างองค์ประกอบย่อหน้าและผนวกเข้ากับเนื้อหาของเอกสาร

```java
// สร้างองค์ประกอบย่อหน้าและผนวกเข้ากับเนื้อหาของเอกสาร
Element p = document.createElement("p");
document.getBody().appendChild(p);

// สร้างข้อความและผนวกเข้ากับย่อหน้า
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

ในขั้นตอนนี้ เราจะสร้างองค์ประกอบย่อหน้า HTML และเพิ่มลงในเนื้อหาของเอกสาร จากนั้น เราจะสร้างโหนดข้อความที่มีเนื้อหาว่า "Hello World" และผนวกเข้ากับย่อหน้า

## ขั้นตอนที่ 4: รอการสังเกต (แบบอะซิงโครนัส)

เนื่องจากการกลายพันธุ์ถูกสังเกตแบบอะซิงโครนัส เราจึงต้องรอสักครู่เพื่อให้ผู้สังเกตจับภาพการเปลี่ยนแปลง เราจะใช้`synchronized` และ`wait` เพื่อจุดประสงค์นี้ ดังแสดงด้านล่างนี้

```java
// เนื่องจากการกลายพันธุ์กำลังทำงานในโหมดอะซิงค์ โปรดรอสักสองสามวินาที
synchronized (this) {
    wait(5000);
}
```

เราจะรอ 5 วินาทีเพื่อให้แน่ใจว่าผู้สังเกตการณ์มีโอกาสจับภาพการกลายพันธุ์ใดๆ

## ขั้นตอนที่ 5: หยุดสังเกต

ในที่สุด เมื่อคุณสังเกตเสร็จสิ้น สิ่งสำคัญคือต้องตัดการเชื่อมต่อจากผู้สังเกตเพื่อปลดปล่อยทรัพยากร

```java
// หยุดสังเกต
observer.disconnect();
```

ด้วยขั้นตอนนี้ คุณได้ทำการสังเกตเสร็จสิ้นและสามารถล้างทรัพยากรได้

## บทสรุป

ในบทช่วยสอนนี้ เราได้อธิบายขั้นตอนการใช้ Aspose.HTML สำหรับ Java เพื่อนำ DOM Mutation Observer ไปใช้ คุณได้เรียนรู้วิธีสร้าง Observer กำหนดค่า Observer ทำการเปลี่ยนแปลง DOM รอการสังเกต และหยุดการสังเกตแล้ว ตอนนี้ คุณมีทักษะในการใช้ DOM Mutation Observer ในโปรเจ็กต์ Java ของคุณเพื่อตรวจสอบและตอบสนองต่อการเปลี่ยนแปลงใน DOM ของเอกสาร HTML ได้อย่างมีประสิทธิภาพ

หากคุณมีคำถามหรือพบปัญหา โปรดอย่าลังเลที่จะขอความช่วยเหลือ[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/) นอกจากนี้ คุณยังสามารถเข้าถึง[เอกสารประกอบ](https://reference.aspose.com/html/java/) สำหรับข้อมูลโดยละเอียดเกี่ยวกับ Aspose.HTML สำหรับ Java

## คำถามที่พบบ่อย

### คำถามที่ 1: DOM Mutation Observer คืออะไร

A1: DOM Mutation Observer คือฟีเจอร์ JavaScript ที่ช่วยให้คุณเฝ้าดูการเปลี่ยนแปลงใน Document Object Model (DOM) ของเอกสาร HTML ได้ โดยฟีเจอร์นี้ให้วิธีการตอบสนองต่อการเพิ่ม การลบ หรือการปรับเปลี่ยนโหนด DOM แบบเรียลไทม์

### คำถามที่ 2: ฉันสามารถใช้ Aspose.HTML สำหรับ Java ในโครงการเชิงพาณิชย์ของฉันได้หรือไม่

 A2: ใช่ คุณสามารถใช้ Aspose.HTML สำหรับ Java ในโปรเจ็กต์เชิงพาณิชย์ได้ คุณสามารถค้นหาข้อมูลเกี่ยวกับการออกใบอนุญาตและการซื้อได้[ที่นี่](https://purchase.aspose.com/buy).

### คำถามที่ 3: มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.HTML สำหรับ Java หรือไม่

 A3: ใช่ คุณสามารถทดลองใช้ Aspose.HTML สำหรับ Java ได้ฟรี[ที่นี่](https://releases.aspose.com/). ซึ่งช่วยให้คุณสามารถสำรวจคุณสมบัติและความสามารถต่างๆ ได้ก่อนตัดสินใจซื้อ

### คำถามที่ 4: ประโยชน์จากการสังเกตการเปลี่ยนแปลงข้อมูลตัวละครด้วย Mutation Observer คืออะไร

A4: การสังเกตการเปลี่ยนแปลงข้อมูลอักขระนั้นมีประโยชน์สำหรับสถานการณ์ที่คุณต้องการตรวจสอบและตอบสนองต่อการเปลี่ยนแปลงในเนื้อหาข้อความขององค์ประกอบ HTML ตัวอย่างเช่น คุณสามารถใช้เพื่อติดตามและตอบสนองต่ออินพุตของผู้ใช้ในแบบฟอร์มบนเว็บ

### คำถามที่ 5: ฉันจะกำจัดทรัพยากรอย่างไรเมื่อใช้ Aspose.HTML สำหรับ Java?

 A5: การปล่อยทรัพยากรเมื่อเสร็จสิ้นนั้นเป็นสิ่งสำคัญ ในตัวอย่างของเรา เราใช้`document.dispose()` เพื่อทำความสะอาดทรัพยากรที่เชื่อมโยงกับเอกสาร HTML ตรวจสอบให้แน่ใจว่าคุณได้กำจัดวัตถุและทรัพยากรที่คุณสร้างขึ้นเพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
