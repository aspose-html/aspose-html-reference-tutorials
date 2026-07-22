---
category: general
date: 2026-07-21
description: Tạo các tùy chọn xử lý tài nguyên trong Python và học cách đặt độ sâu
  xử lý tối đa cho việc phân tích HTML. Hãy làm theo hướng dẫn từng bước này để quản
  lý tài nguyên một cách đáng tin cậy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: vi
lastmod: 2026-07-21
og_description: Tạo các tùy chọn xử lý tài nguyên trong Python và ngay lập tức xem
  cách thiết lập độ sâu xử lý tối đa để tải tài liệu HTML một cách an toàn. Nắm vững
  kỹ thuật này trong vài phút.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Tạo các tùy chọn xử lý tài nguyên trong Python – Hướng dẫn chi tiết từng
  bước
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Tạo các tùy chọn xử lý tài nguyên trong Python – Hướng dẫn đầy đủ
url: /vi/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tùy chọn xử lý tài nguyên trong Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **tạo các tùy chọn xử lý tài nguyên** cho một trang HTML khổng lồ mà không làm tràn bộ nhớ? Bạn không phải là người duy nhất. Khi bạn đưa một tài liệu khổng lồ vào bộ phân tích, các tài nguyên lồng nhau như frames, iframes, hoặc CSS liên kết có thể nhanh chóng mất kiểm soát.  

Tin tốt? Bạn có thể yêu cầu bộ phân tích dừng lại sau một số mức lồng nhau nhất định. Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn **cách đặt độ sâu xử lý tối đa** và giữ cho ứng dụng của bạn luôn phản hồi. Sẵn sàng chưa? Hãy cùng bắt đầu.

## Những gì bạn sẽ học

- Tại sao việc giới hạn độ sâu lồng nhau lại quan trọng đối với hiệu năng và bảo mật.  
- Đoạn mã chính xác bạn cần để **tạo các tùy chọn xử lý tài nguyên** bằng lớp `ResourceHandlingOptions`.  
- Cách cấu hình `max_handling_depth` để bộ phân tích dừng lại sau ba mức.  
- Mẹo xử lý các trường hợp đặc biệt, chẳng hạn như tài liệu có tham chiếu vòng hoặc tài nguyên bị thiếu.  

Không yêu cầu kinh nghiệm trước với thư viện — chỉ cần một cài đặt Python 3 hoạt động và hiểu cơ bản về I/O file.

## Yêu cầu trước

- Python 3.8+ (thư viện hoạt động trên mọi phiên bản gần đây).  
- Gói `htmlparser` cung cấp `HTMLDocument` và `ResourceHandlingOptions`.  
- Một file HTML mẫu (`big_page.html`) được đặt trong thư mục bạn có thể tham chiếu.  

Nếu bạn chưa cài đặt gói, chạy:

```bash
pip install htmlparser
```

Giờ mà phần chuẩn bị đã xong, chúng ta hãy đi vào phần cốt lõi.

## Tạo tùy chọn xử lý tài nguyên – Bước 1

Điều đầu tiên cần làm: bạn cần một thể hiện của `ResourceHandlingOptions`. Hãy nghĩ nó như một hộp công cụ nơi bạn có thể đặt các giới hạn và chính sách mà bộ phân tích phải tuân theo.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Tại sao điều này quan trọng:**  
Khi bộ phân tích gặp một `<iframe>` bên trong một `<iframe>` khác, nó thường sẽ theo chuỗi vô hạn. Bằng cách giới hạn độ sâu ở `3`, bạn ngăn chặn việc đệ quy không kiểm soát có thể làm cạn kiệt RAM hoặc gây tràn ngăn xếp.  

> **Mẹo chuyên nghiệp:** Nếu bạn đang phân tích nội dung không tin cậy (ví dụ: HTML do người dùng tải lên), hãy cân nhắc giảm độ sâu xuống `1` hoặc `2` để giảm thiểu các cuộc tấn công tiềm năng.

## Tải tài liệu HTML – Bước 2

Với đối tượng tùy chọn đã sẵn sàng, truyền nó vào `HTMLDocument`. Hàm khởi tạo sẽ tôn trọng `max_handling_depth` mà bạn vừa đặt.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Bên trong đang diễn ra gì?**  
`HTMLDocument` đọc file, xây dựng cây DOM, và sau đó duyệt qua mọi tài nguyên bên ngoài (stylesheet, script, hình ảnh). Mỗi khi gặp một tài nguyên lồng nhau, nó kiểm tra `resource_options.max_handling_depth`. Nếu đã đạt giới hạn, bộ phân tích sẽ ghi cảnh báo và bỏ qua các mức lồng sâu hơn.  

Điều này có nghĩa là bạn sẽ có một DOM hoàn chỉnh cho ba lớp đầu tiên, phần còn lại sẽ được bỏ qua một cách an toàn.

## Xác minh cấu hình – Bước 3

Luôn luôn là ý tưởng tốt để xác nhận rằng các thiết lập của bạn đã có hiệu lực. Đối tượng `resource_options` cung cấp trạng thái hiện tại, vì vậy bạn có thể in ra hoặc kiểm tra trong một test.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Nếu phép kiểm tra (assertion) thành công, bạn có thể yên tâm rằng bộ phân tích sẽ tuân thủ giới hạn trong suốt quá trình chạy.

## Xử lý các trường hợp đặc biệt

### Tham chiếu vòng

Một số trang cũ nhúng iframe trỏ lại chính trang gốc, tạo ra vòng lặp. Với `max_handling_depth` đã được đặt, vòng lặp sẽ tự động bị ngắt sau lần lặp thứ ba. Tuy nhiên, bạn vẫn có thể thấy cảnh báo trong log. Để tắt các log ồn ào, điều chỉnh mức logger:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Tài nguyên bị thiếu

Nếu một tài nguyên lồng nhau không tải được (404 hoặc timeout mạng), bộ phân tích sẽ ném ngoại lệ theo mặc định. Bao bọc lời gọi tải trong khối `try/except` để giữ cho ứng dụng của bạn không bị sập:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Điều chỉnh độ sâu một cách động

Đôi khi bạn cần các độ sâu khác nhau cho các phần khác nhau của pipeline. Vì `resource_options` là một đối tượng có thể thay đổi, bạn có thể sửa `max_handling_depth` ngay trong lúc chạy:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Chỉ cần nhớ đặt lại giá trị trước khi tái sử dụng cùng một thể hiện tùy chọn trong một luồng khác.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là một script đầy đủ mà bạn có thể sao chép‑dán, chỉnh sửa đường dẫn file, và chạy ngay lập tức.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Kết quả mong đợi (khi các file tồn tại và hợp lệ):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Nếu không đọc được file, bạn sẽ thấy thông báo lỗi thay vì chương trình bị sập.

![Create resource handling options in Python](/images/resource-options.png){alt="Tạo tùy chọn xử lý tài nguyên trong Python"}

## Tóm tắt – Tại sao cách tiếp cận này tuyệt vời

- **An toàn trước hết:** Giới hạn độ sâu lồng nhau ngăn chặn đệ quy không kiểm soát và bùng nổ bộ nhớ.  
- **Linh hoạt:** Bạn có thể thay đổi `max_handling_depth` tại thời gian chạy để phù hợp với các kịch bản khác nhau.  
- **Đơn giản:** Vài dòng mã cho phép bạn **tạo các tùy chọn xử lý tài nguyên** và áp dụng ngay lập tức.  

Nói tóm lại, bạn đã có một mẫu mạnh mẽ để kiểm soát mức độ sâu mà bộ phân tích của bạn theo dõi các tài nguyên bên ngoài.

## Tiếp theo là gì?

- Khám phá thêm lớp `ResourceHandlingOptions` — có các cờ cho việc cache, xử lý timeout, và lọc MIME‑type.  
- Kết hợp việc giới hạn độ sâu với một chuỗi `UserAgent` tùy chỉnh để tránh bị chặn bởi các máy chủ nghiêm ngặt.  
- Nếu bạn làm việc với I/O bất đồng bộ, hãy xem phiên bản `aiohtmlparser` mà cũng tôn trọng các tùy chọn tương tự nhưng hoạt động với `asyncio`.  

Hãy thoải mái thử nghiệm: đặt độ sâu thành `0` và quan sát bộ phân tích bỏ qua mọi tham chiếu bên ngoài. Đây là một cách tắt nhanh khi bạn chỉ cần HTML thô.

Có câu hỏi hoặc trang khó nào vẫn gây rắc rối? Để lại bình luận bên dưới, tôi sẽ sẵn sàng giúp bạn tinh chỉnh các thiết lập. Chúc bạn parsing vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoạt động đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create sandbox for HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}