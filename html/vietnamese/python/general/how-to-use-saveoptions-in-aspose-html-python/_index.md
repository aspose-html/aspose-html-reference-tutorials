---
category: general
date: 2026-07-27
description: Cách sử dụng SaveOptions trong Aspose.HTML (Python) để chuyển đổi trang
  HTML lớn và áp dụng xử lý tài nguyên một cách hiệu quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: vi
lastmod: 2026-07-27
og_description: Cách sử dụng SaveOptions trong Aspose.HTML (Python) cho phép bạn chuyển
  đổi trang HTML lớn đồng thời áp dụng xử lý tài nguyên để đạt kết quả sạch sẽ và
  nhanh chóng.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Cách sử dụng SaveOptions trong Aspose.HTML – Hướng dẫn Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Cách sử dụng SaveOptions trong Aspose.HTML (Python)
url: /vi/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng SaveOptions trong Aspose.HTML (Python)

Cách sử dụng SaveOptions trong Aspose.HTML cho Python là câu hỏi mà nhiều nhà phát triển đặt ra khi làm việc với các tệp HTML khổng lồ. Nếu bạn cần **convert large HTML page** trong khi vẫn kiểm soát chặt chẽ **apply resource handling**, bạn đang ở đúng nơi.  

Trong hướng dẫn này, chúng ta sẽ đi qua một kịch bản thực tế: lấy một trang HTML cồng kềnh, giới hạn độ sâu mà các tài nguyên lồng nhau được kéo vào, và cuối cùng lưu (hoặc chuyển đổi) kết quả với kiểm soát rõ ràng. Không có các tham chiếu mơ hồ, chỉ có một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể sao chép‑dán vào dự án của mình ngay hôm nay.

> **Mẹo chuyên nghiệp:** `SaveOptions` của Aspose.HTML không chỉ hoạt động để lưu lại thành HTML mà còn để chuyển đổi sang PDF, PNG, hoặc thậm chí DOCX. Mẫu tương tự mà chúng tôi trình bày bên dưới áp dụng cho tất cả các định dạng đó.

---

## Những gì bạn cần

- **Python 3.8+** (mã sử dụng type hints nhưng chạy trên bất kỳ phiên bản mới nào)  
- **Aspose.HTML for Python via .NET** – cài đặt bằng `pip install aspose-html`  
- Một **large HTML file** mà bạn muốn thu nhỏ hoặc chuyển đổi (ví dụ sử dụng `big_page.html`)  
- Một lượng không gian đĩa vừa đủ cho tệp đầu ra  

Đó là tất cả—không cần thư viện bổ sung, không cần công cụ xây dựng nặng.

## Cách sử dụng SaveOptions với tùy chọn Resource Handling Options

Đây là phần cốt lõi của vấn đề. Chúng ta sẽ tạo một thể hiện `SaveOptions`, gắn một đối tượng `ResourceHandlingOptions` để chỉ cho Aspose.HTML độ sâu mà nó nên truy tìm các tài nguyên liên kết, và sau đó truyền tất cả cho phương thức `save` của tài liệu.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Tại sao cách này hoạt động:**
- `HTMLDocument` tải tệp gốc, phân tích mọi `<img>`, `<link>`, `<script>`, v.v.  
- `ResourceHandlingOptions.max_handling_depth` chỉ cho engine dừng truy tìm tài nguyên sau ba mức lồng nhau—hoàn hảo để tránh vòng lặp vô hạn trên các trang nhúng các trang khác.  
- `SaveOptions` là phương tiện mang cả định dạng đầu ra (HTML mặc định) và các quy tắc resource handling.  
- Cuối cùng, `doc.save` ghi tệp mới, áp dụng các quy tắc chúng ta vừa thiết lập.  

Khi bạn chạy script, bạn sẽ thấy một tệp mới tại `big_page_processed.html`. Mở nó trong trình duyệt; bạn sẽ nhận thấy rằng tất cả hình ảnh, kiểu dáng và script lên tới ba mức độ sâu vẫn còn, trong khi các tham chiếu sâu hơn đã bị loại bỏ. Điều này giảm đáng kể kích thước tệp mà không phá vỡ bố cục chính của trang—đúng những gì bạn cần khi **convert large HTML page** để sử dụng offline hoặc gửi email.

## Chuyển đổi Large HTML Page một cách hiệu quả

Nếu mục tiêu của bạn là *convert large HTML page* thành một phiên bản gọn hơn, đoạn mã trên đã thực hiện hầu hết công việc nặng. Tuy nhiên, bạn có thể muốn thay đổi hoàn toàn định dạng đầu ra. Aspose.HTML làm điều đó chỉ trong một dòng:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Chỉ cần thay thế thuộc tính `format` bằng `"PNG"`, `"JPEG"` hoặc `"DOCX"` và bạn sẽ có một quy trình chuyển đổi đầy đủ. Các quy tắc **apply resource handling** vẫn giữ nguyên, vì vậy PDF kết quả sẽ không nhúng mọi tệp CSS bên ngoài từ trang gốc—chỉ những tệp nằm trong độ sâu ba mức mà bạn đã định nghĩa.

## Áp dụng Resource Handling cho các tài nguyên lồng nhau

Hãy đi sâu hơn một chút vào **apply resource handling** một cách hiệu quả. Giả sử HTML của bạn chứa một stylesheet mà tự nó nhập các stylesheet khác, mỗi cái lại kéo các hình ảnh. Nếu không có giới hạn độ sâu, Aspose.HTML có thể truy tìm chuỗi này mãi mãi, làm tăng bộ nhớ và sử dụng CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – Không có tài nguyên bên ngoài nào được lấy; bạn nhận được một khung HTML tối giản.  
- **Depth 1** – Chỉ các tài nguyên cấp một (các thẻ `<img>` trực tiếp, các tệp CSS ngay lập tức) được bao gồm.  
- **Depth 2+** – Độ lồng sâu hơn được tôn trọng, hữu ích cho các trang phức tạp nơi các style phụ thuộc vào các style khác.  

Chọn độ sâu phù hợp với kịch bản **convert large HTML page** của bạn. Đối với bản tin email, depth 1 thường là đủ. Đối với lưu trữ cục bộ, depth 3 (như trong ví dụ chính) mang lại sự cân bằng tốt.

## Ví dụ Hoạt động đầy đủ – Từ đầu đến cuối

Dưới đây là một script tự chứa mà bạn có thể đặt vào tệp có tên `process_html.py`. Nó bao gồm xử lý lỗi, ghi log, và một trợ giúp nhỏ in ra mức giảm kích thước mà bạn đạt được.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Kết quả mong đợi (console):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Mở tệp đã xử lý; bạn sẽ thấy một trang gọn hơn nhưng vẫn giống như bản gốc. Nếu bạn chuyển `fmt` sang `"PDF"`, console sẽ báo kích thước tệp PDF và bạn có thể mở nó bằng bất kỳ trình xem PDF nào.

## Câu hỏi thường gặp & Trường hợp đặc biệt

- **Nếu trang tham chiếu các tài nguyên qua HTTPS yêu cầu xác thực thì sao?**  
  Aspose.HTML theo dõi các chuyển hướng nhưng sẽ không tự động gửi thông tin xác thực. Bạn có thể tải trước các tài nguyên đó hoặc sử dụng một trình xử lý `WebRequest` tùy chỉnh (ngoài phạm vi của hướng dẫn này).

- **Có thể giữ lại CSS nội tuyến trong khi loại bỏ các tệp bên ngoài không?**  
  Có—đặt `resource_options.max_handling_depth = 0`. Điều này bỏ qua các tệp bên ngoài nhưng để lại bất kỳ khối `<style>` nào.

- **Còn các hình ảnh rất lớn vẫn làm tăng kích thước đầu ra thì sao?**  
  Sau khi lưu, bạn có thể thực hiện một lần xử lý phụ bằng Pillow để giảm kích thước hình ảnh, hoặc để các tùy chọn nén ảnh tích hợp sẵn của Aspose.HTML xử lý (sử dụng `save_options.image_quality`).

- **Giới hạn độ sâu có được áp dụng cho từng loại tài nguyên không?**  
  Giới hạn này là toàn cục cho tất cả các loại tài nguyên (hình ảnh, script, style). Nếu bạn cần kiểm soát chi tiết, bạn sẽ phải lọc tài nguyên thủ công sau khi tải tài liệu.

## Kết luận

Bạn giờ đã nắm vững **how to use SaveOptions** trong Aspose.HTML


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, có thể chạy được cùng với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}