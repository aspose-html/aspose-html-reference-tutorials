---
category: general
date: 2026-03-04
description: วิธีไฮไลท์ HTML โดยการค้นหาข้อความใน HTML และห่อหุ้มแต่ละผลลัพธ์ด้วยแท็ก
  <mark> คู่มือ Java ทีละขั้นตอนเพื่อแทนที่ข้อความด้วยองค์ประกอบ mark
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: th
og_description: วิธีไฮไลท์ HTML ด้วยการค้นหาข้อความใน HTML แล้วห่อหุ้มผลลัพธ์ที่ตรงกับแท็ก
  <mark> ตัวอย่าง Java ฉบับเต็มสำหรับการแทนที่ข้อความด้วยแท็ก mark.
og_title: วิธีไฮไลท์ HTML – ค้นหาข้อความและแทนที่ด้วย <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: วิธีไฮไลท์ HTML – ค้นหาข้อความและแทนที่ด้วย <mark>
url: /th/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการไฮไลท์ HTML – ค้นหาข้อความ & แทนที่ด้วย `<mark>`

เคยสงสัย **วิธีการไฮไลท์ HTML** เมื่อคำบางคำปรากฏหลายครั้งหรือไม่? บางทีคุณอาจกำลังสร้างเว็บไซต์เอกสาร, ระบบบล็อก, หรือแค่ต้องการเน้นชื่อแบรนด์ในหน้าเว็บแบบคงที่ ข่าวดีคือ? มันค่อนข้างง่ายเมื่อคุณรู้วิธีค้นหาข้อความใน HTML และห่อผลลัพธ์ด้วยแท็ก `<mark>`.

ในบทแนะนำนี้เราจะพาไปผ่านโซลูชัน Java ฉบับเต็มที่โหลดไฟล์ HTML, ค้นหาคำเป้าหมาย, แทนที่แต่ละครั้งด้วยแท็ก `<mark>` และสุดท้ายบันทึกเวอร์ชันที่ไฮไลท์แล้ว เมื่อจบคุณจะสามารถ **highlight word in HTML**, **highlight occurrences of word**, และแม้กระทั่ง **replace text with mark** ได้โดยไม่ทำลายมาร์กอัปโดยรอบ.

> **สิ่งที่คุณต้องการ**  
> • Java 17 หรือใหม่กว่า (โค้ดทำงานกับเวอร์ชันก่อนหน้าก็ได้)  
> • ไลบรารี Aspose.HTML for Java (เวอร์ชันทดลองฟรีหรือสำเนาที่มีลิขสิทธิ์)  
> • ไฟล์ HTML ง่าย ๆ ที่คุณต้องการประมวลผล  

![ภาพหน้าจอแสดงผลลัพธ์ HTML ที่ไฮไลท์ – วิธีการไฮไลท์ html](/images/highlight-html-example.png "ตัวอย่างวิธีการไฮไลท์ html")

## ขั้นตอนที่ 1 – โหลดเอกสาร HTML (วิธีการไฮไลท์ HTML)

ก่อนอื่นเราต้องนำไฟล์ต้นฉบับเข้าหน่วยความจำ คลาส `Document` ของ Aspose.HTML ทำงานหนักทั้งหมดโดยการแยกวิเคราะห์มาร์กอัปเป็นโครงสร้างคล้าย DOM ที่เราสามารถสอบถามได้

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดเอกสารทำให้เราได้โมเดลอ็อบเจกต์ที่สะอาด ทำให้เราสามารถจัดการโหนดข้อความได้อย่างปลอดภัยโดยไม่ต้องกังวลว่าจะทำลายแท็กหรือแอตทริบิวต์ นอกจากนี้ยังทำให้ช่องว่างเป็นมาตรฐาน ซึ่งทำให้ขั้นตอน **search text in html** ต่อไปมีความน่าเชื่อถือมากขึ้น.

## ขั้นตอนที่ 2 – ค้นหาข้อความใน HTML สำหรับคำเป้าหมาย

เมื่อเอกสารพร้อมแล้ว เราจะมองหาการปรากฏของคำที่ต้องการเน้น `searchText` method จะคืนรายการของอ็อบเจกต์ `TextMatch` ซึ่งแต่ละอันบรรยายตำแหน่งที่การจับคู่อยู่ใน DOM

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**เคล็ดลับ:** การค้นหาเป็นแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กตามค่าเริ่มต้น หากคุณต้องการการค้นหาแบบไม่แยกแยะตัวพิมพ์ ให้แปลงข้อความในเอกสารและ `searchTerm` ให้เป็นรูปแบบเดียวกันก่อนเรียก `searchText` หรือใช้วิธีการที่อิง regular‑expression ที่ไลบรารีให้มา

## ขั้นตอนที่ 3 – แทนที่ข้อความด้วย `<mark>` (ไฮไลท์คำใน HTML)

สำหรับแต่ละการจับคู่ เราจะสร้างข้อความของโหนดที่บรรจุใหม่โดยแทรกองค์ประกอบ `<mark>` รอบคำที่ตรงกันอย่างแม่นยำ สิ่งนี้ทำให้เรามีผลต่อข้อความเป้าหมายเท่านั้นและไม่กระทบส่วนอื่นของ HTML

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**คำอธิบาย:**  
- `getStartOffset`/`getEndOffset` ให้ตำแหน่งอักขระที่ตรงกันภายในโหนดพาเรนต์อย่างแม่นยำ  
- โดยการตัดข้อความต้นฉบับ (`textBefore` และ `textAfter`) เราจะเก็บทุกอย่างอื่นไว้เหมือนเดิม  
- การห่อการจับคู่ด้วย `<mark>` เป็นวิธีมาตรฐานในการ **replace text with mark** และทำให้ได้การไฮไลท์โดยเบราว์เซอร์โดยไม่ต้องใช้ CSS เพิ่มเติม

### กรณีขอบและเคล็ดลับ

- **หลายการจับคู่ในโหนดเดียว:** ลูปจะประมวลผลแต่ละ `TextMatch` ตามลำดับ เนื่องจากเราจะแทนที่เนื้อหาโหนดทั้งหมดทุกครั้ง การออฟเซ็ตภายหลังจะเปลี่ยนแปลง Aspose.HTML คืนค่าการจับคู่ตามลำดับเอกสาร ดังนั้นการแทนที่แบบง่ายทำงานได้ในกรณีส่วนใหญ่ หากพบการจับคู่ที่ทับซ้อน ให้พิจารณารวบรวมการจับคู่ทั้งหมดก่อนแล้วสร้างโหนดใหม่ในหนึ่งรอบ  
- **องค์ประกอบที่ไม่สามารถบรรจุ HTML ดิบได้:** หากโหนดพาเรนต์เป็นบล็อก `<script>` หรือ `<style>` การแทรก `<mark>` จะทำให้หน้าเว็บเสีย คุณสามารถข้ามโหนดเหล่านั้นได้โดยตรวจสอบ `parentNode.getNodeName()` ก่อนทำการแทนที่  

## ขั้นตอนที่ 4 – บันทึกเอกสารที่ไฮไลท์ (ไฮไลท์การปรากฏของคำ)

หลังจากทำการแทนที่ทั้งหมดเสร็จ เราจะบันทึก DOM ที่แก้ไขกลับไปยังดิสก์ ไฟล์ผลลัพธ์จะมีมาร์กอัปเดิมบวกกับแท็ก `<mark>` ใหม่ ทำให้ **highlighting occurrences of word** “Aspose” อย่างมีประสิทธิภาพ

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

เปิด `highlighted.html` ในเบราว์เซอร์ใดก็ได้ คุณจะเห็นทุกคำว่า “Aspose” ถูกห่อด้วยพื้นหลังสีเหลืองอ่อน (สไตล์เริ่มต้นของ `<mark>`). หากคุณต้องการลุคแบบกำหนดเอง ให้เพิ่มกฎ CSS เล็ก ๆ นี้:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## คำถามที่พบบ่อย (Search Text in HTML – FAQs)

**Q: ถ้าคำปรากฏอยู่ในค่าแอตทริบิวต์ล่ะ?**  
A: `searchText` ตรวจสอบเฉพาะเนื้อหาข้อความของโหนด ไม่รวมสตริงแอตทริบิวต์ หากต้องการไฮไลท์ค่าแอตทริบิวต์ คุณต้องวนลูปผ่านองค์ประกอบและตรวจสอบแอตทริบิวต์ด้วยตนเอง

**Q: ฉันสามารถไฮไลท์หลายคำที่แตกต่างกันในครั้งเดียวได้หรือไม่?**  
A: แน่นอน สร้างรายการของคำ, วนลูปผ่านแต่ละคำ, และใช้ตรรกะการแทนที่เดียวกัน เพียงระวังการจับคู่ที่ทับซ้อนกัน

**Q: วิธีนี้ทำงานกับแท็ก HTML5‑only เช่น `<section>` หรือ `<article>` หรือไม่?**  
A: ใช่ Aspose.HTML รองรับองค์ประกอบ HTML5 สมัยใหม่อย่างเต็มที่ ดังนั้นการเดินทางผ่าน DOM ทำงานได้ไม่ว่าประเภทแท็กจะเป็นอะไร

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นโปรแกรม Java ที่สมบูรณ์พร้อมรันที่แสดงกระบวนการทำงานทั้งหมด – ตั้งแต่การโหลดไฟล์จนถึงการบันทึกผลลัพธ์ที่ไฮไลท์

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `highlighted.html` แล้วคุณจะเห็นทุกการปรากฏของ “Aspose” ถูกไฮไลท์ ส่วนอื่นของหน้าไม่ถูกเปลี่ยนแปลงและไฟล์ยังคงเป็นเอกสาร HTML ที่ถูกต้อง

## สรุป

เราได้อธิบาย **วิธีการไฮไลท์ HTML** โดยการ **ค้นหาข้อความใน HTML** อย่างโปรแกรมมิ่ง, ห่อการจับคู่แต่ละรายการด้วยแท็ก `<mark>` และสุดท้ายบันทึกการเปลี่ยนแปลง วิธีนี้ทำให้คุณสามารถ **highlight word in HTML**, **highlight occurrences of word**, และ **replace text with mark** ได้โดยไม่ต้องเขียนโค้ดการจัดการสตริงที่เปราะบาง

ขั้นตอนต่อไป? ลองขยายสคริปต์ให้:

- รับคำค้นหาเป็นอาร์กิวเมนต์บรรทัดคำสั่ง  
- สร้างไฟล์ CSS ที่กำหนดสีไฮไลท์แบบกำหนดเอง  
- ประมวลผลโฟลเดอร์เต็มของไฟล์ HTML ในหนึ่งชุด  

การเปลี่ยนแปลงเหล่านี้จะทำให้คุณเข้าใจลึกซึ้งยิ่งขึ้นเกี่ยวกับ Aspose.HTML API และรูปแบบการประมวลผลข้อความทั่วไป

หากคุณเจอปัญหาใดหรือมีไอเดียสำหรับการปรับปรุงเพิ่มเติม ฝากคอมเมนต์ด้านล่างได้เลย ขอให้สนุกกับการไฮไลท์!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}