---
category: general
date: 2026-10-28
description: Cách đọc HTML trong Java và trích xuất văn bản từ các tệp HTML. Học cách
  chuyển đổi HTML sang văn bản bằng Jsoup, bao gồm các kỹ thuật đọc HTML từ tệp và
  chuyển HTML sang văn bản trong Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: vi
lastmod: 2026-10-28
og_description: Cách đọc HTML trong Java và trích xuất văn bản từ các tệp HTML. Hướng
  dẫn này trình bày giải pháp hoàn chỉnh để chuyển đổi HTML sang văn bản bằng Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Cách đọc HTML và trích xuất văn bản trong Java – hướng dẫn nhanh
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Cách đọc HTML và trích xuất văn bản trong Java – hướng dẫn từng bước
url: /vi/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đọc HTML và trích xuất văn bản trong Java – hướng dẫn từng bước

Nếu bạn cần **how to read html** từ một tệp cục bộ, hướng dẫn này cung cấp giải pháp đầy đủ. Bạn sẽ học cách tải một tài liệu HTML, trích xuất văn bản thuần, và tùy chọn chuyển đổi HTML sang văn bản với kiểm soát chi tiết. Khi kết thúc tutorial, bạn có thể chạy mã ví dụ và thấy văn bản đã trích xuất được in ra console.

Đọc các tệp HTML là một nhiệm vụ phổ biến khi xử lý dữ liệu thu thập từ web, tạo báo cáo, hoặc làm sạch nội dung do người dùng tạo. Các bước dưới đây bao gồm mọi thứ bạn cần, từ việc thêm thư viện cần thiết đến xử lý các trường hợp đặc biệt như markup bị hỏng hoặc vấn đề mã hoá ký tự.

## Những gì bạn cần

- Java 17 hoặc mới hơn (mã vẫn biên dịch được với các phiên bản cũ hơn)
- Maven hoặc Gradle để quản lý phụ thuộc, hoặc JAR Jsoup được thêm thủ công
- Một tệp HTML có tên `input.html` đặt trong thư mục `src/main/resources` của dự án (bạn có thể thay đổi đường dẫn sau này)

## Cài đặt thư viện Jsoup

Jsoup là một thư viện nhẹ, được tài liệu hoá tốt, cho phép phân tích HTML thành cấu trúc giống DOM. Nó xử lý HTML bị hỏng một cách mềm dẻo, khiến nó lý tưởng cho các nhiệm vụ **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Nếu bạn muốn tải xuống thủ công, đặt JAR vào classpath và import `org.jsoup.*` trong file nguồn của bạn.

## Tải HTML từ tệp

Bước lập trình đầu tiên là đọc tệp vào một đối tượng `Document`. Jsoup cung cấp phương thức tĩnh `parse` nhận vào một `File` và tên charset.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Why this matters:** `Jsoup.parse(File, String)` đọc các byte thô, giải mã chúng theo charset được cung cấp, và xây dựng một DOM sạch sẽ. Cách tiếp cận này an toàn hơn việc tự đọc tệp thành chuỗi vì Jsoup chuẩn hoá dấu xuống dòng và tự động sửa các lỗi markup phổ biến.

## Trích xuất văn bản thuần từ HTML

Khi bạn đã có một `Document`, việc lấy văn bản hiển thị chỉ cần một lời gọi phương thức. Phương thức `text()` nối nội dung văn bản của tất cả các phần tử trong khi loại bỏ thẻ, script và style.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Lời gọi `body()` giới hạn việc trích xuất chỉ trong phần tử `<body>`, đây là mục tiêu thường gặp khi bạn **read html from file** để phân tích nội dung. Chuỗi kết quả có khoảng trắng được gộp thành một dấu cách duy nhất, mô phỏng cách trình duyệt hiển thị văn bản.

### Kết quả mong đợi

Giả sử `input.html` chứa:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Chạy chương trình sẽ in:

```
Extracted text:
Hello World This is a demo page.
```

## Chuyển đổi HTML sang văn bản với các tùy chọn bổ sung

Đôi khi bạn cần kiểm soát nhiều hơn so với `text()` cung cấp—ví dụ, giữ lại các ngắt dòng, giữ số thứ tự danh sách, hoặc bỏ qua một số thẻ nhất định. `NodeTraversor` của Jsoup kết hợp với một `NodeVisitor` tùy chỉnh cho phép bạn làm được điều đó.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Thay thế lời gọi đơn giản `doc.body().text()` bằng:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** Visitor duyệt DOM theo chiều sâu, chèn một ký tự xuống dòng trước mỗi phần tử cấp khối (ví dụ, `<p>`, `<div>`, `<h1>`). Điều này giữ lại khoảng cách giữa các đoạn, hữu ích khi bạn **convert html to text** để tăng khả năng đọc hoặc cho các pipeline NLP sau này.

## Những cạm bẫy thường gặp và thực hành tốt

| Vấn đề | Nguyên nhân | Cách khắc phục đề xuất |
|-------|-------------|------------------------|
| Sai charset | Các tệp được lưu ở ISO‑8859‑1 nhưng được phân tích như UTF‑8 gây ra ký tự bị rối. | Phát hiện charset từ thẻ meta của tệp (`<meta charset="...">`) hoặc truyền tên đúng vào `Jsoup.parse`. |
| Tệp lớn | Việc tải một tệp HTML rất lớn vào bộ nhớ có thể gây `OutOfMemoryError`. | Dòng dữ liệu tệp bằng `Jsoup.parse(File, String, String baseUri)` và xử lý các nút một cách tuần tự, hoặc tăng kích thước heap của JVM. |
| Văn bản script/style không mong muốn | `text()` loại bỏ nội dung script và style, nhưng các visitor tùy chỉnh có thể vô tình bao gồm chúng. | Bỏ qua các nút có tên thẻ là `script` hoặc `style` trong phương thức `head` của visitor. |
| Giữ lại khoảng trắng | Việc gộp các khoảng trắng có thể mất định dạng cần thiết cho việc chuyển đổi markdown. | Sử dụng `Element.wholeText()` cho các nút văn bản thô, sau đó xử lý khoảng trắng thủ công. |

Việc giải quyết những vấn đề này đảm bảo giải pháp **html to text java** của bạn hoạt động đáng tin cậy trên nhiều đầu vào đa dạng.

## Ví dụ đầy đủ có thể chạy

Dưới đây là một chương trình tự chứa minh hoạ toàn bộ quy trình—từ cài đặt phụ thuộc đến xác minh đầu ra. Sao chép mã vào một file tên `HtmlToTextDemo.java`, đặt một tệp `input.html` bên cạnh nó, và chạy `javac && java` như minh hoạ.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Running the program

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Console hiển thị cả việc trích xuất đơn giản và chi tiết

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}