---
category: general
date: 2026-09-13
description: Học cách phân tích HTML và tải tài liệu HTML đồng thời giới hạn độ sâu
  để ngăn chặn đệ quy vô hạn trong Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- load html document
- how to limit depth
- prevent infinite recursion
language: vi
lastmod: 2026-09-13
og_description: Cách phân tích HTML và tải tài liệu HTML một cách an toàn. Hướng dẫn
  này chỉ ra cách giới hạn độ sâu và ngăn chặn vòng lặp vô hạn.
og_image_alt: Diagram showing HTML parsing flow with depth‑limit control
og_title: Cách phân tích HTML với giới hạn độ sâu – Hướng dẫn Python
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  headline: How to parse HTML with depth limiting using Python
  type: TechArticle
- description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  name: How to parse HTML with depth limiting using Python
  steps:
  - name: Create resource handling options
    text: The `ResourceHandlingOptions` object tells the parser when to stop following
      nested resources such as `<iframe>` tags or linked CSS files.
  - name: Load HTML document with the configured options
    text: Now you load the file while supplying the options you just defined. This
      is the **load html document** step that respects the depth limit.
  - name: Parse the document safely
    text: With the document loaded, you can now traverse the DOM. The example below
      extracts all headings (`<h1>`‑`<h3>`) without exceeding the depth limit.
  type: HowTo
tags:
- html parsing
- python
- recursion
- resource handling
title: Cách phân tích HTML với giới hạn độ sâu bằng Python
url: /vi/python/general/how-to-parse-html-with-depth-limiting-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách phân tích HTML với giới hạn độ sâu bằng Python

Nếu bạn cần **how to parse html** từ một báo cáo lớn, bước đầu tiên là tải tài liệu HTML với một lớp bảo vệ ngăn chặn việc lồng sâu quá mức. Hướng dẫn này sẽ chỉ cho bạn cách tải một tài liệu HTML, đặt độ sâu xử lý tối đa, và **prevent infinite recursion** khi các tài nguyên tham chiếu lẫn nhau.

Bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được sử dụng `ResourceHandlingOptions` và `HTMLDocument`. Khi kết thúc hướng dẫn, bạn có thể an toàn phân tích bất kỳ tệp HTML nào mà không làm cạn kiệt bộ nhớ hay gây tràn ngăn xếp.

## Yêu cầu trước

* Python 3.9 hoặc mới hơn đã được cài đặt.
* Thư viện xử lý HTML cung cấp `ResourceHandlingOptions` và `HTMLDocument`. (Trong hướng dẫn này chúng tôi giả định thư viện có tên `htmlhandler`; cài đặt nó bằng `pip install htmlhandler`.)
* Kiến thức cơ bản về đệ quy và cấu trúc HTML.

Không cần cấu hình hệ thống bổ sung.

## Cách phân tích HTML với giới hạn độ sâu

Cốt lõi của giải pháp là tạo một thể hiện `ResourceHandlingOptions`, cấu hình `max_handling_depth` của nó, và truyền vào `HTMLDocument`. Các bước sau sẽ hướng dẫn bạn qua quá trình này.

### Bước 1: Tạo tùy chọn xử lý tài nguyên

Đối tượng `ResourceHandlingOptions` cho trình phân tích biết khi nào nên dừng việc theo dõi các tài nguyên lồng nhau như thẻ `<iframe>` hoặc các tệp CSS được liên kết.

```python
# Step 1: Create resource handling options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources
```

*__Tại sao điều này quan trọng__*: Nếu không có giới hạn độ sâu, một tài liệu độc hại hoặc sai cấu trúc có thể nhúng các tài nguyên tham chiếu lẫn nhau vô hạn. Đặt `max_handling_depth` thành 3 đảm bảo trình phân tích dừng lại sau ba cấp độ, đủ cho hầu hết các tài liệu hợp lệ đồng thời bảo vệ thời gian chạy.

### Bước 2: Tải tài liệu HTML với các tùy chọn đã cấu hình

Bây giờ bạn tải tệp trong khi cung cấp các tùy chọn vừa định nghĩa. Đây là bước **load html document** tôn trọng giới hạn độ sâu.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/big_report.html",
    resource_handling_options=resource_options
)
```

*__Tại sao điều này quan trọng__*: Việc truyền `resource_handling_options` vào `HTMLDocument` tích hợp giới hạn độ sâu trực tiếp vào động cơ phân tích. Trình phân tích sẽ tự động dừng việc duyệt khi đạt tới giới hạn, điều này **prevents infinite recursion**.

### Bước 3: Phân tích tài liệu một cách an toàn

Khi tài liệu đã được tải, bạn có thể duyệt DOM. Ví dụ dưới đây trích xuất tất cả các tiêu đề (`<h1>`‑`<h3>`) mà không vượt quá giới hạn độ sâu.

```python
def extract_headings(node, current_depth=0):
    """
    Recursively collect heading text while respecting the max handling depth.
    """
    if current_depth > resource_options.max_handling_depth:
        return []  # Prevent infinite recursion by aborting deeper calls

    headings = []
    if node.tag_name in ("h1", "h2", "h3"):
        headings.append(node.text_content.strip())

    for child in node.children:
        headings.extend(extract_headings(child, current_depth + 1))
    return headings

# Start traversal from the root element
all_headings = extract_headings(html_doc.root)
print("Collected headings:", all_headings)
```

**Kết quả mong đợi (ví dụ)**:

```
Collected headings: ['Executive Summary', 'Methodology', 'Results', 'Conclusion']
```

Điều kiện `if current_depth > resource_options.max_handling_depth` là cơ chế **how to limit depth** ngăn chặn đệ quy tiếp tục. Mẫu này hoạt động cho bất kỳ dữ liệu dạng cây nào, không chỉ HTML.

## Cách tải tài liệu HTML với tùy chọn tùy chỉnh

Nếu bạn cần điều chỉnh độ sâu cho một tệp cụ thể, chỉ cần thay đổi `max_handling_depth` trước khi tạo `HTMLDocument`.

```python
resource_options.max_handling_depth = 5   # Allow deeper nesting for this file
html_doc = HTMLDocument("another_report.html", resource_handling_options=resource_options)
```

Thay đổi giới hạn hữu ích khi bạn biết tài liệu chứa cấu trúc lồng nhau hợp lệ (ví dụ: bảng lồng nhau). Mã giống vẫn **prevent infinite recursion** vì giới hạn được áp dụng trong thời gian chạy.

## Những lỗi thường gặp và cách tránh

| Rủi ro | Nguyên nhân | Cách khắc phục |
|--------|-------------|----------------|
| **Thiếu `resource_handling_options`** | Trình phân tích theo dõi mọi tài nguyên, dẫn đến đệ quy không giới hạn. | Luôn truyền thể hiện `ResourceHandlingOptions` khi khởi tạo `HTMLDocument`. |
| **Đặt `max_handling_depth` quá thấp** | Nội dung quan trọng có thể bị bỏ qua vì trình phân tích dừng quá sớm. | Kiểm tra với mẫu đại diện và chọn độ sâu cân bằng giữa an toàn và đầy đủ. |
| **Hàm đệ quy không kiểm tra độ sâu** | Các phép duyệt tùy chỉnh vẫn có thể đệ quy vô hạn ngay cả khi trình phân tích dừng. | Bao gồm cùng logic kiểm tra độ sâu (`if current_depth > max_depth: return`) trong mọi hàm trợ giúp đệ quy. |
| **Giả định mọi nút đều có `children`** | Các nút văn bản có thể không có thuộc tính `children`, gây lỗi thuộc tính. | Kiểm tra bằng `hasattr(node, "children")` hoặc sử dụng khối try/except. |

Việc giải quyết những vấn đề này đảm bảo giải pháp **how to parse html** của bạn vẫn vững chắc trên nhiều đầu vào đa dạng.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là toàn bộ script bạn có thể sao chép‑dán vào tệp có tên `parse_report.py`. Nó minh họa toàn bộ quy trình từ tạo tùy chọn đến trích xuất tiêu đề.

```python
# parse_report.py
from htmlhandler import ResourceHandlingOptions, HTMLDocument

def main():
    # ---- Step 1: configure depth limit ----
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3   # adjust as needed

    # ---- Step 2: load the HTML document ----
    html_path = "YOUR_DIRECTORY/big_report.html"
    html_doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # ---- Step 3: recursive extraction with safety guard ----
    def extract_headings(node, current_depth=0):
        if current_depth > resource_options.max_handling_depth:
            return []  # stop deeper recursion

        headings = []
        if node.tag_name in ("h1", "h2", "h3"):
            headings.append(node.text_content.strip())

        # Safely iterate over children if they exist
        if hasattr(node, "children"):
            for child in node.children:
                headings.extend(extract_headings(child, current_depth + 1))
        return headings

    # Run extraction starting from the document root
    headings = extract_headings(html_doc.root)
    print("Collected headings:", headings)

if __name__ == "__main__":
    main()
```

Chạy script:

```bash
python parse_report.py
```

Bạn sẽ thấy danh sách các tiêu đề được in ra console, xác nhận rằng trình phân tích đã tôn trọng giới hạn độ sâu và **prevented infinite recursion**.

## Các bước tiếp theo

* **Parse other elements** – điều chỉnh `extract_headings` để thu thập bảng, liên kết hoặc hình ảnh.
* **Stream large files** – sử dụng phân tích tăng dần (`HTMLDocument.stream`) khi xử lý các báo cáo đa gigabyte.
* **Integrate with asyncio** – bọc bước tải trong một hàm async nếu bạn cần I/O không chặn.

Khám phá các chủ đề này sẽ nâng cao khả năng của bạn trong việc **load html document** các đối tượng một cách hiệu quả đồng thời duy trì kiểm soát đầy đủ độ sâu đệ quy.

Bằng cách làm theo hướng dẫn này, bạn giờ đã biết cách **how to parse html** một cách an toàn, cách **load html document** với giới hạn độ sâu tùy chỉnh, và cách **prevent infinite recursion** trong bất kỳ phép duyệt đệ quy nào. Áp dụng mẫu này vào dự án của bạn và điều chỉnh cài đặt độ sâu cho phù hợp với độ phức tạp của các tệp nguồn. Chúc lập trình vui!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được minh họa trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)
- [how to query html in Java – load HTML, CSS selector, and extract headings](/html/english/java/css-html-form-editing/how-to-query-html-in-java-load-html-css-selector-and-extract/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}