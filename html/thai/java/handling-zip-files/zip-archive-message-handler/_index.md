---
title: ตัวจัดการข้อความเก็บถาวร ZIP ใน Aspose.HTML สำหรับ Java
linktitle: ตัวจัดการข้อความเก็บถาวร ZIP ใน Aspose.HTML สำหรับ Java
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีสร้าง ZIP Archive Message Handler โดยใช้ Aspose.HTML สำหรับ Java คู่มือนี้จะอธิบายแต่ละขั้นตอนเพื่อช่วยให้คุณจัดการและให้บริการไฟล์จากไฟล์ ZIP ได้อย่างมีประสิทธิภาพ
weight: 10
url: /th/java/handling-zip-files/zip-archive-message-handler/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวจัดการข้อความเก็บถาวร ZIP ใน Aspose.HTML สำหรับ Java

## การแนะนำ
การทำงานกับไฟล์ ZIP อาจเป็นส่วนสำคัญในการจัดการข้อมูลในรูปแบบต่างๆ โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการทรัพยากรบนเว็บอย่างมีประสิทธิภาพ ในคู่มือนี้ เราจะแนะนำคุณเกี่ยวกับการสร้าง ZIP Archive Message Handler โดยใช้ Aspose.HTML สำหรับ Java ตัวจัดการนี้จะช่วยให้คุณอ่านไฟล์ได้โดยตรงจากไฟล์ ZIP และทำหน้าที่เป็นการตอบสนองต่อคำขอเครือข่าย ถือเป็นวิธีที่มีประสิทธิภาพในการปรับปรุงการจัดการไฟล์ โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับชุดข้อมูลขนาดใหญ่ที่บีบอัดไว้ในไฟล์เดียว
## ข้อกำหนดเบื้องต้น
ก่อนจะเจาะลึกโค้ด เรามาตรวจสอบกันก่อนว่าคุณมีทุกสิ่งที่จำเป็นในการปฏิบัติตามบทช่วยสอนนี้:
-  Aspose.HTML สำหรับ Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.HTML สำหรับ Java แล้ว คุณสามารถ[ดาวน์โหลดได้ที่นี่](https://releases.aspose.com/html/java/).
- Java Development Kit (JDK): ตรวจสอบให้แน่ใจว่าคุณติดตั้ง JDK 8 ขึ้นไป
- สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE): IDE เช่น IntelliJ IDEA หรือ Eclipse สามารถทำให้กระบวนการพัฒนาราบรื่นยิ่งขึ้น
- ความเข้าใจพื้นฐานเกี่ยวกับ Java: คุณควรจะคุ้นเคยกับการเขียนโปรแกรม Java โดยเฉพาะอย่างยิ่งการจัดการไฟล์และการทำงานของเครือข่าย

## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็น การนำเข้าเหล่านี้จะช่วยให้คุณจัดการการทำงานของเครือข่าย การอ่านไฟล์ และการจัดการเนื้อหาภายใน ZIP Archive Message Handler
```java
import com.aspose.html.IDisposable;
import com.aspose.html.MimeType;
import com.aspose.html.net.ByteArrayContent;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.MessageHandler;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.messagefilters.ProtocolMessageFilter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
```
## ขั้นตอนที่ 1: เริ่มต้นตัวจัดการข้อความไฟล์ ZIP
 ขั้นตอนแรกคือการสร้างคลาสที่ขยาย`MessageHandler` ชั้นเรียนและดำเนินการ`IDisposable` อินเทอร์เฟซ คลาสนี้จะจัดการการดำเนินการที่เกี่ยวข้องกับไฟล์เก็บถาวร ZIP

```java
public class ZIPArchiveMessageHandler extends MessageHandler implements IDisposable {
    private String filePath;
    // เริ่มต้นอินสแตนซ์ของคลาส ZipArchiveMessageHandler
    public ZIPArchiveMessageHandler(String path) {
        this.filePath = path;
        getFilters().addItem(new ProtocolMessageFilter("zip"));
    }
}
```

 ในขั้นตอนนี้ เราจะกำหนดโครงสร้างพื้นฐานของตัวจัดการ เราจะกำหนด`ZIPArchiveMessageHandler` คลาสและเริ่มต้นด้วยเส้นทางไฟล์ซึ่งเป็นที่ที่ไฟล์ ZIP ของคุณอยู่`ProtocolMessageFilter` รับประกันว่าตัวจัดการนี้จัดการกับไฟล์ ZIP เท่านั้น
## ขั้นตอนที่ 2: นำวิธีการกำจัดไปใช้
ในการจัดการทรัพยากรอย่างมีประสิทธิผล โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับไฟล์ สิ่งสำคัญคือต้องดำเนินการดังต่อไปนี้`dispose` วิธีการนี้จะช่วยให้แน่ใจว่าทรัพยากรใดๆ ที่ใช้โดยตัวจัดการจะได้รับการปลดปล่อยอย่างถูกต้อง

```java
@Override
public void dispose() {
    // รหัสการทำความสะอาดหากมีให้ไปที่นี่
}
```

 แม้ว่า`dispose` ในตัวอย่างนี้ วิธีการนี้ว่างเปล่า คุณสามารถเพิ่มรหัสการทำความสะอาดที่จำเป็นใดๆ ลงไปที่นี่ได้ ถือเป็นแนวทางปฏิบัติที่ดีในการใช้วิธีการนี้เพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ โดยเฉพาะอย่างยิ่งในแอปพลิเคชันที่ซับซ้อนมากขึ้น
## ขั้นตอนที่ 3: จัดการคำขอเครือข่าย
 ฟังก์ชันหลักของตัวจัดการข้อความเก็บถาวร ZIP ถูกกำหนดไว้ใน`invoke` วิธีการนี้ประมวลผลคำขอเครือข่ายขาเข้า อ่านไฟล์ที่ร้องขอจากไฟล์เก็บถาวร ZIP และส่งกลับเป็นการตอบสนอง

```java
@Override
public void invoke(INetworkOperationContext context) {
    byte[] buff = new byte[0];
    try {
        buff = Files.readAllBytes(Paths.get(context.getRequest().getRequestUri().getPathname().trim()));
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
    if (buff != null) {
        ResponseMessage msg = new ResponseMessage(200);
        msg.setContent(new ByteArrayContent(buff));
        context.getResponse().getHeaders().getContentType().setMediaType(MimeType.fromFileExtension(context.getRequest().getRequestUri().getPathname()));
    } else {
        context.setResponse(new ResponseMessage(404));
    }
    invoke(context);
}
```

 ในขั้นตอนนี้ เราจะกำหนดตรรกะในการจัดการคำขอเครือข่าย`invoke` วิธีการอ่านไฟล์ที่ร้องขอจากไฟล์ ZIP โดยใช้`Files.readAllBytes`วิธีการ หากพบไฟล์ ระบบจะส่งกลับเป็นการตอบสนองพร้อมชนิดเนื้อหาที่เหมาะสม หากไม่พบ ระบบจะส่งการตอบสนอง 404 เพื่อระบุว่าไม่พบไฟล์
## ขั้นตอนที่ 4: ตั้งค่าประเภทเนื้อหา
การตั้งค่าประเภทเนื้อหาที่ถูกต้องสำหรับการตอบกลับเป็นสิ่งสำคัญเพื่อให้แน่ใจว่าไคลเอนต์จะตีความไฟล์ได้อย่างถูกต้อง ประเภทเนื้อหาจะถูกกำหนดขึ้นตามนามสกุลไฟล์

```java
context.getResponse().getHeaders().getContentType().setMediaType(MimeType.fromFileExtension(context.getRequest().getRequestUri().getPathname()));
```

 ที่นี่เราจะตั้งค่า`ContentType` ส่วนหัวของการตอบสนองให้ตรงกับประเภท MIME ของไฟล์ที่ร้องขอ ขั้นตอนนี้จะช่วยให้มั่นใจว่าเมื่อไคลเอนต์ได้รับไฟล์แล้ว ไคลเอนต์จะทราบวิธีจัดการไฟล์อย่างถูกต้อง ไม่ว่าจะเป็นรูปภาพ เอกสาร หรือไฟล์ประเภทอื่นใดก็ตาม
## ขั้นตอนที่ 5: เรียกใช้ตัวจัดการถัดไป
ในที่สุด หลังจากจัดการคำขอปัจจุบันแล้ว สิ่งสำคัญคือต้องส่งการควบคุมไปยังตัวจัดการข้อความตัวถัดไปในไปป์ไลน์ ซึ่งถือเป็นสิ่งสำคัญในรูปแบบห่วงโซ่ความรับผิดชอบที่ตัวจัดการหลายตัวอาจประมวลผลคำขอเดียวกัน

```java
invoke(context);
```

บรรทัดนี้จะช่วยให้แน่ใจว่าเมื่อตัวจัดการปัจจุบันทำงานเสร็จแล้ว คำขอจะถูกส่งต่อไปยังตัวจัดการถัดไปในห่วงโซ่ แนวทางนี้ช่วยให้สามารถจัดการคำขอได้อย่างยืดหยุ่นและแยกส่วน โดยที่ตัวจัดการที่แตกต่างกันสามารถจัดการด้านต่างๆ ของคำขอได้

## บทสรุป
ในบทช่วยสอนนี้ เราได้แนะนำวิธีสร้าง ZIP Archive Message Handler โดยใช้ Aspose.HTML สำหรับ Java ตัวจัดการนี้ช่วยให้คุณจัดการไฟล์ภายในไฟล์ ZIP ได้อย่างมีประสิทธิภาพ โดยให้บริการไฟล์โดยตรงตามคำขอของเครือข่าย ด้วยการแบ่งกระบวนการออกเป็นขั้นตอนง่ายๆ เราหวังว่าตอนนี้คุณคงเข้าใจชัดเจนแล้วว่าจะนำฟังก์ชันนี้ไปใช้ในโครงการของคุณเองอย่างไร
## คำถามที่พบบ่อย
### การใช้งานหลักของตัวจัดการข้อความ ZIP Archive คืออะไร  
ช่วยให้คุณสามารถอ่านไฟล์ได้โดยตรงจากไฟล์ ZIP และทำหน้าที่เป็นการตอบกลับของเครือข่าย ทำให้การจัดการไฟล์มีประสิทธิภาพมากยิ่งขึ้น
### ฉันสามารถจัดการประเภทไฟล์อื่น ๆ ด้วยตัวจัดการนี้ได้หรือไม่  
ใช่ แม้ว่าตัวอย่างนี้เน้นที่ไฟล์เก็บถาวร ZIP แต่ตัวจัดการก็สามารถปรับให้จัดการประเภทไฟล์อื่นได้ด้วยการปรับแต่งเล็กน้อย
### จะเกิดอะไรขึ้นหากไม่พบไฟล์ที่ร้องขอในไฟล์ ZIP?  
หากไม่พบไฟล์ ตัวจัดการจะส่งกลับการตอบสนอง 404 ซึ่งระบุว่าไม่สามารถค้นหาทรัพยากรได้
###  ฉันจำเป็นต้องดำเนินการตาม`dispose` method?  
 แม้ว่าอาจไม่จำเป็นในทุกกรณี แต่การนำไปปฏิบัติ`dispose` ถือเป็นแนวทางปฏิบัติที่ดีในการทำให้แน่ใจว่าทรัพยากรใดๆ ที่ใช้โดยตัวจัดการจะได้รับการปล่อยออกอย่างถูกต้อง
### ตัวจัดการนี้สามารถใช้ในเว็บเซิร์ฟเวอร์ได้หรือไม่?  
แน่นอน! ตัวจัดการนี้ได้รับการออกแบบมาเพื่อใช้ในแอปพลิเคชันเว็บที่คุณต้องให้บริการไฟล์จากไฟล์เก็บถาวร ZIP เพื่อตอบสนองต่อคำขอ HTTP

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
