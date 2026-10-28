---
category: general
date: 2026-10-28
description: Học cách mở liên kết trong tab mới bằng cách phân tích HTML trong Java,
  tìm các liên kết ngoài và thêm thuộc tính target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: vi
lastmod: 2026-10-28
og_description: 'Mở liên kết trong tab mới bằng Java: phân tích HTML, tìm các liên
  kết ngoài, thêm target=''_blank'', và lưu HTML đã chỉnh sửa.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Mở liên kết trong tab mới bằng Java – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Cách mở liên kết trong tab mới bằng Java
url: /vi/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách mở liên kết trong tab mới bằng Java

Nếu bạn cần **mở liên kết trong tab mới** từ một tệp HTML tĩnh, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách **phân tích HTML trong Java**, **tìm các liên kết bên ngoài**, **thêm target blank**, và **lưu HTML đã chỉnh sửa** mà không rời khỏi IDE.

Mở các liên kết bên ngoài trong một tab trình duyệt mới cải thiện trải nghiệm người dùng và giữ khách truy cập ở trang gốc. Giải pháp dưới đây hoạt động với bất kỳ tài liệu HTML nào, chỉ yêu cầu thư viện jsoup phổ biến, và chạy trên Java 8 hoặc mới hơn.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* JDK 8 + đã được cài đặt  
* Công cụ xây dựng (Maven hoặc Gradle) để kéo **jsoup** vào dự án  
* Một tệp HTML chứa các thẻ anchor có lớp `external`

Bạn không cần máy chủ web hay các framework bổ sung—jsoup xử lý mọi thứ cục bộ.

## Bước 1: Cài đặt jsoup trong dự án

Thêm jsoup làm phụ thuộc. Nếu bạn dùng Maven, đặt đoạn này vào `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Đối với Gradle, thêm dòng sau vào `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Các tọa độ này sẽ kéo phiên bản ổn định mới nhất (tính đến tháng 10 2026). Sau khi đồng bộ, bạn có thể import các lớp `org.jsoup` trong các tệp nguồn Java của mình.

## Bước 2: Phân tích tài liệu HTML

Phân tích tệp là bước đầu tiên để **open links new tab**. Phương thức `Jsoup.parse` đọc tệp vào một cấu trúc giống DOM có thể thay đổi.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Lý do quan trọng*: `Document` cung cấp các bộ chọn kiểu CSS, giúp bạn dễ dàng định vị các phần tử cần thiết.

## Bước 3: Tìm các liên kết bên ngoài

Bây giờ hãy xác định mọi phần tử `<a>` có lớp `external`. Điều này đáp ứng yêu cầu **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` là một tập hợp các nút khớp. Nếu bộ chọn trả về một tập rỗng, HTML của bạn có thể thiếu lớp này hoặc sử dụng quy ước đặt tên khác—hãy điều chỉnh bộ chọn cho phù hợp.

## Bước 4: Thêm `target="_blank"` vào mỗi liên kết

Đối với mỗi nút được trả về bởi **find external links**, đặt thuộc tính `target` thành `_blank`. Điều này thực hiện bước **add target blank** và đảm bảo trình duyệt mở liên kết trong tab mới.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Phương thức `attr` ghi đè bất kỳ giá trị `target` hiện có nào, đảm bảo hành vi nhất quán trên tất cả các anchor bên ngoài.

## Bước 5: Lưu HTML đã chỉnh sửa

Sau khi cập nhật DOM, ghi các thay đổi trở lại tệp. Điều này hoàn thành phần **save modified html** của hướng dẫn.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` tuần tự hoá toàn bộ tài liệu, giữ nguyên thụt lề và định dạng như khi jsoup phân tích ban đầu.

## Ví dụ hoàn chỉnh

Kết hợp tất cả các bước lại sẽ tạo ra một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Kết quả mong đợi

Giả sử `sample.html` chứa:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Sau khi chạy chương trình, `updated.html` sẽ chứa:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Chỉ liên kết bên ngoài được thêm thuộc tính `target="_blank"`, nghĩa là trình duyệt sẽ mở nó trong một tab mới.

## Mẹo chuyên nghiệp và những lỗi thường gặp

* **Mẹo:** Nếu bạn muốn xử lý các liên kết bắt đầu bằng `http://` hoặc `https://` như là bên ngoài ngay cả khi không có lớp CSS, mở rộng bộ chọn: `doc.select("a[href^=http]")`.
* **Trường hợp đặc biệt:** Một số trang đã chỉ định `target="_self"`; lời gọi `attr` sẽ ghi đè, đảm bảo hành vi nhất quán.
* **Hiệu năng:** Đối với các tệp HTML rất lớn, cân nhắc phân tích theo luồng (`Jsoup.parse(File, String, String, Parser.htmlParser())`) để giảm mức tiêu thụ bộ nhớ.
* **Kiểm thử:** Xác minh kết quả bằng cách mở `updated.html` trong trình duyệt và kiểm tra liên kết bằng công cụ developer—tìm thuộc tính `target`.

## Kết luận

Bây giờ bạn đã có một giải pháp hoàn chỉnh, có thể chạy được để **open links in a new tab** bằng Java. Hướng dẫn đã bao gồm cách **parse html in java**, **find external links**, **add target blank**, và **save modified html**, tất cả với thư viện nhẹ jsoup.

Từ đây bạn có thể:

* Mở rộng bộ chọn để xử lý các mẫu liên kết khác (ví dụ: `rel="external"`).  
* Kết hợp logic này với một bước xây dựng xử lý tất cả các tệp HTML trong dự án.  
* Tích hợp mã vào một pipeline quản lý nội dung lớn hơn.

Hãy tự do thử nghiệm với các bộ chọn hoặc định dạng đầu ra khác nhau, và chia sẻ kết quả của bạn với cộng đồng!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}