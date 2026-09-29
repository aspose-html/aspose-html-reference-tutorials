---
category: general
date: 2026-09-29
description: Học cách chọn các phần tử theo lớp, đọc HTML từ tệp và tìm các liên kết
  ngoài trong Java. Hướng dẫn từng bước này bao gồm việc lặp qua NodeList một cách
  hiệu quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: vi
lastmod: 2026-09-29
og_description: Chọn các phần tử theo lớp trong Java, đọc HTML từ tệp và tìm các liên
  kết ngoài bằng querySelectorAll. Tham khảo ví dụ đầy đủ để lặp qua NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Chọn các phần tử theo lớp trong Java – hướng dẫn đầy đủ với querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Cách chọn các phần tử theo lớp trong Java bằng querySelectorAll
url: /vi/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chọn phần tử theo lớp trong Java bằng querySelectorAll

Nếu bạn cần **chọn phần tử theo lớp** khi xử lý một tệp HTML trong Java, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn sẽ học cách đọc HTML từ tệp, sử dụng `querySelectorAll` để tìm các liên kết ngoài, và duyệt `NodeList` kết quả một cách an toàn.

Làm việc với HTML trong Java thường cảm thấy nặng nề, nhưng các thư viện hiện đại cung cấp cho bạn một API ngắn gọn, dựa trên bộ chọn CSS. Ví dụ dưới đây sử dụng **jsoup** (phiên bản 1.17.2) vì nó triển khai các bộ chọn kiểu `querySelectorAll` và trả về một collection `Elements` hoạt động giống như một `NodeList`. Bạn có thể điều chỉnh cùng logic này cho các triển khai DOM khác nếu cần.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* JDK 17 hoặc mới hơn đã được cài đặt.
* Maven hoặc Gradle để quản lý phụ thuộc.
* Kiến thức cơ bản về Java streams và mô hình DOM.

Thêm jsoup vào dự án của bạn:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Bước 1: Đọc HTML từ tệp

Nhiệm vụ đầu tiên là tải tài liệu HTML từ đĩa. `Jsoup.parse(Path, Charset)` đọc tệp và xây dựng một cây DOM mà bạn có thể truy vấn.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Why this matters*: *Tại sao điều này quan trọng*: Tải tệp một lần tránh việc I/O lặp lại khi bạn duyệt các phần tử sau này. Đối tượng `Document` giữ toàn bộ DOM, cho phép truy vấn bộ chọn nhanh chóng.

## Bước 2: Sử dụng `querySelectorAll` để chọn phần tử theo lớp

Bây giờ tài liệu đã có trong bộ nhớ, bạn có thể **chọn phần tử theo lớp** bằng một bộ chọn CSS. Bộ chọn `"a.external"` khớp với các thẻ `<a>` có lớp `external` — chính xác những gì bạn cần để **tìm các liên kết ngoài**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Why this matters*: *Tại sao điều này quan trọng*: Sử dụng bộ chọn lớp vừa biểu đạt vừa hiệu quả. Thư viện chuyển bộ chọn thành một phép duyệt tối ưu, vì vậy bạn không cần viết vòng lặp thủ công cho mỗi nút.

## Bước 3: Duyệt NodeList (Elements) trong Java

`Elements` triển khai `Iterable<Element>`, có nghĩa là bạn có thể dùng vòng lặp `for‑each` tiêu chuẩn để **duyệt NodeList Java**. Vòng lặp dưới đây in ra thuộc tính `href` của mỗi liên kết.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Why this matters*: *Tại sao điều này quan trọng*: Duyệt trực tiếp giữ cho mã dễ đọc và tránh chi phí chuyển collection sang stream khi bạn chỉ cần xuất đơn giản.

## Ví dụ đầy đủ hoạt động

Kết hợp ba bước lại với nhau tạo ra một chương trình tự chứa mà bạn có thể chạy từ dòng lệnh.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Kết quả mong đợi

Giả sử `input.html` chứa:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Chạy chương trình sẽ in ra:

```
External link: https://example.com
External link: https://openai.com
```

## Mẹo chuyên nghiệp và những lỗi thường gặp

* **Mã hoá quan trọng** – Luôn đọc tệp bằng UTF‑8 (hoặc charset phù hợp với nguồn của bạn). Mã hoá sai có thể làm hỏng ký tự trong giá trị thuộc tính.
* **Nhiều lớp** – Nếu một phần tử có nhiều lớp (ví dụ, `class="btn external"`), bộ chọn `"a.external"` vẫn khớp vì bộ chọn lớp CSS kiểm tra sự tồn tại của token, không phải chuỗi chính xác.
* **Mẹo hiệu năng** – Nếu bạn chỉ cần thuộc tính `href`, có thể yêu cầu trực tiếp bằng `doc.select("a.external[href]").eachAttr("href")`. Điều này tránh việc tạo đối tượng `Element` đầy đủ cho mỗi kết quả.
* **An toàn null** – `link.attr("href")` trả về chuỗi rỗng nếu thuộc tính thiếu, vì vậy bạn không cần kiểm tra null trước khi in.

## Câu hỏi thường gặp

**Q: Điều này có hoạt động với các đoạn HTML thiếu thẻ gốc `<html>` không?**  
A: Có. `Jsoup.parse` coi đầu vào như một đoạn và tự động thêm các phần tử gốc còn thiếu, cho phép các bộ chọn hoạt động trên phần body của đoạn.

**Q: Tôi có thể sử dụng `querySelectorAll` mà không cần jsoup không?**  
A: API DOM chuẩn của Java (`org.w3c.dom`) không có `querySelectorAll`. Các thư viện như **HTMLUnit** hoặc **jodd-lagarto** cung cấp các phương pháp tương tự. Mô hình được trình bày ở đây—tải, chọn bằng CSS, duyệt—vẫn giống nhau.

**Q: Nếu tôi cần sửa đổi các liên kết thay vì chỉ in ra thì sao?**  
A: Sau khi lấy được mỗi `Element`, bạn có thể gọi `link.attr("href", "newUrl")` và sau đó ghi tài liệu trở lại đĩa bằng `Files.writeString`.

## Kết luận

Bây giờ bạn đã biết cách **chọn phần tử theo lớp**, **đọc HTML từ tệp**, **tìm các liên kết ngoài**, và **duyệt NodeList trong Java** bằng các bộ chọn kiểu `querySelectorAll`. Ví dụ hoàn chỉnh minh họa một quy trình làm việc sạch sẽ, sẵn sàng cho sản xuất mà bạn có thể nhúng vào các pipeline thu thập dữ liệu hoặc chuyển đổi lớn hơn.

Tiếp theo, khám phá các chủ đề liên quan như **phân tích nội dung động với HTMLUnit**, **ghi HTML đã sửa đổi trở lại đĩa**, hoặc **sử dụng Java streams để thu thập URL liên kết vào danh sách**. Mỗi chủ đề này dựa trên kỹ thuật chọn dựa trên lớp được trình bày ở đây. Chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách truy vấn HTML trong Java – Chọn phần tử, lọc theo thuộc tính và lấy văn bản](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Duyệt NodeList Java – Đọc HTML & Lấy src ảnh](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Tải tài liệu HTML từ tệp trong Aspose.HTML cho Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}