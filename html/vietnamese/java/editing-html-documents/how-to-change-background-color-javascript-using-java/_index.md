---
category: general
date: 2026-09-29
description: Thay đổi màu nền bằng JavaScript trong một tệp HTML sử dụng Java. Học
  cách tải HTML trong Java, chạy JavaScript trong HTML và chỉnh sửa HTML bằng Java
  để tạo nền trang mới.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: vi
lastmod: 2026-09-29
og_description: Thay đổi màu nền bằng JavaScript trong một trang HTML sử dụng Java.
  Hướng dẫn này cho bạn biết cách tải HTML trong Java, chạy JavaScript trong HTML
  và thiết lập màu nền của trang một cách lập trình.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Thay đổi màu nền bằng JavaScript với Java – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Cách thay đổi màu nền JavaScript bằng Java
url: /vi/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi màu nền javascript bằng Java

Nếu bạn cần **change background color javascript** trong một tệp HTML hiện có, bạn có thể thực hiện hoàn toàn bằng Java mà không cần mở trình duyệt. Hướng dẫn này cho bạn cách **load html in java**, thực thi một đoạn JavaScript nhỏ, và sau đó **modify html with java** để nền của trang được cập nhật.  

Giải pháp này hoạt động với thư viện mã nguồn mở **HTMLUnit**, cung cấp một trình duyệt không giao diện (headless) có thể đánh giá JavaScript chính xác như một trình duyệt thực. Khi kết thúc hướng dẫn này, bạn sẽ có một phương thức có thể tái sử dụng để **sets page background** thành bất kỳ màu nào bạn chọn.

## Yêu cầu trước

| Bạn cần gì | Tại sao quan trọng |
|---------------|----------------|
| Java 8 hoặc mới hơn | HTMLUnit yêu cầu ít nhất Java 8. |
| Công cụ xây dựng Maven hoặc Gradle | Để tự động tải phụ thuộc HTMLUnit. |
| Một tệp HTML bạn muốn chỉnh sửa (ví dụ, `input.html`) | Tài liệu nguồn sẽ được tải và thay đổi. |

Thêm HTMLUnit vào dự án của bạn:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** Sử dụng phiên bản ổn định mới nhất của HTMLUnit để có engine JavaScript chính xác nhất.

## Thay đổi màu nền javascript – tải HTML trong Java

Bước đầu tiên là tải tài liệu HTML vào một đối tượng `HTMLPage`. Điều này cung cấp cho bạn một API kiểu DOM và một ngữ cảnh thực thi JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Why this matters*: `WebClient` tạo ra một môi trường sandbox nơi JavaScript có thể chạy, vì vậy bạn có thể **run js in html** chính xác như trình duyệt của người dùng.

## Run js in html to set page background

Khi trang đã được tải, bạn có thể đánh giá bất kỳ biểu thức JavaScript nào. Đoạn mã dưới đây thay đổi thuộc tính `backgroundColor` của phần tử `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Explanation*:  
- `document.body.style.backgroundColor` là thuộc tính DOM chuẩn cho nền của trang.  
- Bằng cách gọi `eval`, chúng ta **run js in html** mà không cần cửa sổ trình duyệt thực.  
- Phương thức này có thể tái sử dụng cho bất kỳ màu nào, đáp ứng yêu cầu **set page background**.

## Modify html with java and save the result

Sau khi đoạn script chạy, DOM phản ánh kiểu mới. Bạn có thể ghi lại HTML đã cập nhật trở lại đĩa.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Kết hợp tất cả lại với nhau sẽ cho bạn một chương trình duy nhất, có thể chạy được:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in ra:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Mở `js_modified.html` trong bất kỳ trình duyệt nào sẽ hiển thị trang với nền màu xanh nhạt, xác nhận rằng thao tác **change background color javascript** đã thành công.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách xử lý |
|-----------|------------------|
| **Định dạng màu khác nhau** | Chuyển bất kỳ giá trị CSS‑compatible nào (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Thiếu thẻ `<body>`** | Script sẽ thất bại một cách im lặng; bạn có thể trước tiên đảm bảo `<body>` tồn tại bằng `page.getFirstByXPath("//body")`. |
| **Tệp HTML lớn** | Tắt CSS (`setCssEnabled(false)`) và chỉ bật các tính năng JavaScript bạn cần để giảm sử dụng bộ nhớ. |
| **Chạy nhiều script** | Gọi `changeBackground` nhiều lần hoặc tạo một phương thức tiện ích nhận danh sách các lệnh JavaScript. |

## Kết luận

Bây giờ bạn đã biết cách **change background color javascript** bằng cách tải một tệp HTML trong Java, **run js in html**, và **modify html with java** để **set page background** thành bất kỳ màu nào bạn chọn. Ví dụ hoàn chỉnh ở trên hoạt động với thư viện HTMLUnit mới nhất và có thể được tích hợp vào các pipeline tự động hoá lớn hơn, chẳng hạn như xử lý hàng loạt báo cáo HTML hoặc chuẩn bị mẫu email.

**Các bước tiếp theo**  
- Khám phá các thao tác DOM khác (ví dụ, chèn phần tử, xóa script).  
- Kết hợp cách tiếp cận này với trình render PDF để tạo PDF của các trang đã được định dạng.  
- Thử sử dụng một engine headless khác như Selenium WebDriver nếu bạn cần độ chính xác đầy đủ của trình duyệt.

Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Lấy Computed Style Java – Trích xuất màu nền từ HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [Cách tải HTML, đặt DPI thiết bị & đọc màu nền](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Tạo HTML từ JavaScript trong Java – Hướng dẫn chi tiết từng bước](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}