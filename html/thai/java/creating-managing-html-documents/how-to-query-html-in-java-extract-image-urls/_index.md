---
category: general
date: 2026-03-05
description: วิธีการ query HTML ใน Java เพื่ออ่านไฟล์ HTML และดึงรูปภาพออกมา เรียนรู้การอ่านไฟล์
  HTML ด้วย Java, การดึง URL ของรูปภาพใน Java, และการวนลูป NodeList ใน Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: th
og_description: วิธีค้นหา HTML ใน Java และดึง URL ของรูปภาพ คู่มือนี้แสดงวิธีอ่านไฟล์
  HTML ด้วย Java, ค้นหาภาพ, และวนลูป NodeList ใน Java.
og_title: วิธีดึงข้อมูล HTML ใน Java – แยก URL ของรูปภาพ
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: วิธีสืบค้น HTML ด้วย Java – ดึง URL ของรูปภาพ
url: /th/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการ Query HTML ใน Java – ดึง URL ของรูปภาพ

เคยสงสัย **how to query HTML** ใน Java เพื่อดึงรูปภาพทุกรูปบนหน้าเว็บหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต้องอ่านไฟล์ HTML, ดึงรูปภาพ, แล้วทำอะไรบางอย่างกับ URL เหล่านั้น ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างเชิงปฏิบัติที่แสดง **how to query HTML** อย่างชัดเจน, อ่านไฟล์ HTML แบบ Java, และรับ URL ของรูปภาพในรูปแบบ Java.

เราจะใช้ Aspose.HTML for Java, แต่แนวคิด—XPath, CSS selectors, และการ iterating over a `NodeList`—ใช้ได้กับไลบรารี DOM ใดก็ได้ เมื่อจบคู่มือคุณจะคุ้นเคยกับ **how to extract images**, รู้วิธี **iterate over NodeList Java**, และมีโค้ดสแนปเปตที่พร้อมใช้งานที่คุณสามารถใส่ลงในโปรเจกต์ของคุณได้.

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## สิ่งที่คุณจะได้เรียนรู้

- โหลดเอกสาร HTML จากดิสก์ (read HTML file Java)
- ค้นหาแท็ก `<img>` ด้วย XPath และ CSS selectors (how to extract images)
- วนลูปผ่าน `NodeList` ที่ได้ (iterate over NodeList Java)
- พิมพ์แอตทริบิวต์ `src` ของแต่ละรูปภาพ (get image URLs Java)

ไม่มีบริการภายนอก, ไม่มีเครื่องมือ build ที่ซับซ้อน—แค่ Java ธรรมดาและการพึ่งพา Maven เพียงหนึ่งรายการ.

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Java 8 หรือใหม่กว่า
- Maven หรือ Gradle สำหรับการจัดการ dependency
- ความคุ้นเคยพื้นฐานกับโครงสร้าง HTML
- ตัวเลือกแต่เป็นประโยชน์: ไฟล์ HTML ง่าย (`sample.html`) ที่มีบาง `<figure><img …></figure>`

ถ้าคุณมีทั้งหมดนี้ เราก็สามารถเริ่มได้เลย.

## ขั้นตอนที่ 1: Read HTML File Java – โหลดเอกสาร

สิ่งแรกที่ต้องทำคือ นำ HTML เข้าสู่หน่วยความจำ `HTMLDocument` ของ Aspose.HTML ทำหน้าที่หนักหน่วง คิดว่าเป็นการเปิดหนังสือเพื่อคุณจะได้เลื่อนไปยังหน้าใดก็ได้.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดไฟล์จะให้คุณได้ต้นไม้ DOM ที่สามารถ query ได้ หากเส้นทางผิดคุณจะได้รับ `FileNotFoundException` ดังนั้นตรวจสอบตำแหน่งไฟล์ให้แน่ใจก่อนรัน.

## ขั้นตอนที่ 2: Locate Images with XPath – How to Extract Images

XPath เป็นภาษาคำสั่ง query ที่ทรงพลังซึ่งช่วยให้คุณระบุตำแหน่ง node อย่างแม่นยำที่นี่เราขอทุก `<img>` ภายใน `<figure>` ที่มีแอตทริบิวต์ `alt` ด้วย

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**ทำไมต้องใช้ XPath?** มันสั้นและทำงานได้แม้ HTML จะยุ่งยาก นิพจน์ `//figure/img[@alt]` หมายถึง: “any `<img>` under a `<figure>` that carries an `alt` attribute.” หากต้องการกรองด้วยแอตทริบิวต์อื่น เพียงปรับวงเล็บ.

## ขั้นตอนที่ 3: Locate Images with CSS Selector – วิธีทางเลือกเพื่อ Extract Images

บางครั้งคุณอาจชอบไวยากรณ์ CSS เพราะมันสะท้อนสิ่งที่คุณเขียนใน stylesheet `querySelectorAll` ยอมรับ selector เดียวกับที่คุณใช้ในเบราว์เซอร์.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**ทำไมต้องมีทั้งสอง?** การสาธิตทั้งสองแสดงให้คุณเลือกเครื่องมือที่คุณถนัดได้ ในการใช้งานจริงคุณอาจเลือกใช้หนึ่งอย่าง แต่การมีตัวอย่างทั้งสองทำให้บทแนะนำสมบูรณ์ยิ่งขึ้น.

## ขั้นตอนที่ 4: Iterate Over NodeList Java – รับ URL ของรูปภาพใน Java

ตอนนี้เรามีคอลเลกชันแล้ว เราต้องเดินผ่านมัน นี่คือจุดที่ **iterate over NodeList Java** เข้ามามีบทบาท เราจะดึงแอตทริบิวต์ `src` ของแต่ละรูปภาพและพิมพ์ออก.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**ทำไมต้องใช้ `for` loop แบบคลาสสิก?** `NodeList` ของ Aspose ไม่ได้ implement `Iterable` ดังนั้น syntax `for‑each` ที่พัฒนาแล้วจะไม่คอมไพล์ การใช้ลูปด้วยดัชนีเป็นวิธีที่เชื่อถือได้ในการ **iterate over NodeList Java**.

## ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมกับ HTML ตัวอย่างเช่น:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

จะให้ผลลัพธ์คล้ายกับ:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

หากไฟล์ของคุณมี `<img>` แท็กเพิ่มเติมที่ตรงตามเงื่อนไข ตัวเลขจะเพิ่มตาม.

## ข้อผิดพลาดทั่วไป & เคล็ดลับมืออาชีพ

- **ปัญหาเส้นทางไฟล์:** ใช้เส้นทางแบบ absolute หรือวาง `sample.html` ให้สัมพันธ์กับไดเรกทอรีทำงานของโปรเจกต์
- **ขาดแอตทริบิวต์ `alt`:** คำสั่ง XPath/CSS ของเรากรองด้วย `[@alt]` หากต้องการ *ทั้งหมด* ให้ลบตัวกรองแอตทริบิวต์ (`//figure/img` หรือ `figure img`).
- **ประสิทธิภาพ:** สำหรับเอกสารขนาดใหญ่ พิจารณาใช้ streaming parser แต่สำหรับงาน web‑scraping ส่วนใหญ่วิธี DOM เพียงพอ.
- **ปัญหา encoding:** Aspose.HTML เคารพ charset ที่ระบุใน HTML หากเห็นอักขระแปลก ให้แน่ใจว่าไฟล์บันทึกเป็น UTF‑8.

## การขยายตัวอย่าง

ตอนนี้คุณสามารถ **get image URLs Java** แล้ว คุณอาจต้องการ:

1. **ดาวน์โหลดรูปภาพ** ด้วย `java.net.URL` และ `Files.copy`.
2. **เก็บ URL ลงฐานข้อมูล** เพื่อประมวลผลต่อในภายหลัง.
3. **กรองตามนามสกุลไฟล์** (`src.endsWith(".png")`).

ทั้งหมดนี้เป็นการขยายที่ง่ายของลูปที่แสดงในขั้นตอน 4.

## สรุป

ในคู่มือนี้เราได้ครอบคลุม **how to query HTML** ใน Java ตั้งแต่ต้นจนจบ: การโหลดไฟล์, การค้นหารูปภาพด้วย XPath และ CSS selectors, และ **iterating over NodeList Java** เพื่อพิมพ์ `src` ของแต่ละรูป คุณมีพื้นฐานที่มั่นคงสำหรับ **how to extract images** และคุณรู้วิธี **read HTML file Java** อย่างแม่นยำด้วย Aspose.HTML.

คุณสามารถปรับโค้ดให้ตรงกับความต้องการสครัปของคุณ—ไม่ว่าจะเป็นการดึงแอตทริบิวต์อื่น, จัดการแท็ก `<a>`, หรือส่ง URL ไปยังตัวดาวน์โหลด รูปแบบยังคงเหมือนเดิม: โหลด, query, iterate, และทำงาน.

มีคำถามหรืออยากแชร์กรณีการใช้งานที่เจ๋ง? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}