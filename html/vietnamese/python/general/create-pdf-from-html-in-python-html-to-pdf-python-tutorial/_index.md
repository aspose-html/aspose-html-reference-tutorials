---
category: general
date: 2026-07-15
description: Tạo PDF từ HTML bằng Python. Tìm hiểu cách chuyển đổi HTML sang PDF nhanh
  chóng với một script đơn giản và các bước rõ ràng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: vi
lastmod: 2026-07-15
og_description: Tạo PDF từ HTML bằng Python. Hướng dẫn này cho bạn biết cách chuyển
  đổi HTML sang PDF, lưu HTML dưới dạng PDF và xử lý tài nguyên một cách hiệu quả.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Tạo PDF từ HTML trong Python – Hướng dẫn thực hành
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Tạo PDF từ HTML trong Python – Hướng dẫn Python chuyển HTML sang PDF
url: /vi/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF từ HTML trong Python – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ cần **tạo PDF từ HTML** nhưng không chắc thư viện Python nào nên chọn? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn khi họ cố gắng chuyển một báo cáo web, hoá đơn, hoặc trang marketing thành PDF có thể in được.  

Tin tốt là chỉ với vài dòng mã, bạn có thể **chuyển đổi HTML sang PDF** một cách đáng tin cậy, và script hoạt động trên Windows, macOS và Linux. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, giải thích lý do mỗi bước quan trọng, và chỉ cho bạn cách **lưu HTML dưới dạng PDF** mà không để lại bất kỳ lỗ hổng nào.

---

## Những Điều Bạn Sẽ Học

- Cài đặt gói Python phù hợp cho việc chuyển đổi HTML‑to‑PDF.  
- Tải một tệp HTML với các tùy chọn xử lý tài nguyên tùy chỉnh (để tránh việc nhập CSS vô tận).  
- Tạo một tệp PDF sạch sẽ trên đĩa.  
- Xử lý các trường hợp đặc biệt phổ biến như hình ảnh bên ngoài, đường dẫn tương đối và tài liệu lớn.  

Khi hoàn thành **hướng dẫn HTML sang PDF** này, bạn sẽ có một hàm tái sử dụng có thể chèn vào bất kỳ dự án nào.

---

## Yêu Cầu Trước

- Python 3.9+ (mã cũng chạy được với 3.8, nhưng 3.9+ cung cấp các tính năng mới nhất của `pathlib`).  
- Kiến thức cơ bản về dòng lệnh và môi trường ảo.  
- Một tệp HTML bạn muốn chuyển thành PDF—bất kỳ trang tĩnh nào cũng được.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng môi trường ảo, hãy kích hoạt nó trước khi cài đặt thư viện; điều này giúp Python toàn cục của bạn gọn gàng hơn.

---

## Bước 1 – Cài đặt WeasyPrint (động cơ phía sau quá trình chuyển đổi)

WeasyPrint là một thư viện thuần Python, chuyển đổi HTML và CSS sang PDF. Nó hỗ trợ hầu hết các tính năng web hiện đại và cho phép bạn kiểm soát chi tiết quá trình tải tài nguyên.

```bash
pip install weasyprint
```

Chạy lệnh trên sẽ tải về `cairocffi`, `tinycss2` và một vài phụ thuộc khác. Nếu bạn gặp lỗi liên quan đến `cairo` trên Windows, hãy tải các bánh xe đã biên dịch sẵn từ [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Bước 2 – Chuẩn bị một helper nhỏ cho việc xử lý tài nguyên

Khi bạn tải một tài liệu HTML tham chiếu tới các stylesheet hoặc hình ảnh bên ngoài, thư viện sẽ theo các liên kết đó. Trong một số trường hợp, điều này dẫn đến việc lồng sâu hoặc thậm chí vòng lặp vô hạn (ví dụ một file CSS `@import` chính nó). Để giữ mọi thứ gọn gàng, chúng ta giới hạn độ sâu của việc xử lý tài nguyên.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Lớp trên không bắt buộc đối với WeasyPrint, nhưng nó phản ánh mẫu bạn đã thấy trong đoạn mã gốc và cung cấp một điểm hook để ngăn chặn các import chạy quá mức. Bạn sẽ thấy nó được sử dụng trong bước tiếp theo.

---

## Bước 3 – Tải tài liệu HTML bằng các tùy chọn tùy chỉnh

Bây giờ chúng ta thực sự đọc tệp HTML. Lớp `HTML` chấp nhận một đối số `base_url`, chúng ta đặt nó thành thư mục chứa tệp nguồn—điều này giúp các liên kết tương đối hoạt động mà không cần máy chủ web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Tại sao điều này quan trọng:** Nếu HTML của bạn kéo vào một chuỗi các file CSS, mỗi `@import` sẽ kích hoạt một lần tải khác. Bộ bảo vệ độ sâu ngăn script bị chạy ra ngoài tầm kiểm soát.

---

## Bước 4 – Lưu tài liệu đã xử lý dưới dạng PDF

Với đối tượng `HTML` trong tay, việc tạo PDF chỉ cần một dòng lệnh. Chúng ta cũng truyền vào một đoạn CSS đơn giản để ép kích thước trang sạch sẽ (A4) và thêm một lề nhỏ—có thể tùy chỉnh theo nhu cầu.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Gọi `write_pdf` sẽ ghi PDF ra đĩa, vì vậy bạn sẽ có một tệp sẵn sàng chia sẻ.

---

## Bước 5 – Kết Hợp Tất Cả

Dưới đây là một script ngắn gọn mà bạn có thể sao chép‑dán vào `convert.py`. Thay thế các đường dẫn placeholder bằng thư mục thực tế của bạn.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Kết quả mong đợi** – sau khi chạy `python convert.py` bạn sẽ thấy:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Mở tệp đã tạo bằng bất kỳ trình xem PDF nào; bạn sẽ thấy bố cục trang gốc, kiểu CSS và hình ảnh (miễn là chúng có thể truy cập được từ tệp HTML).  

Nếu bạn nhận thấy thiếu hình ảnh, hãy kiểm tra lại thuộc tính `src` của chúng, chúng phải là URL tuyệt đối hoặc đường dẫn tương đối tồn tại dưới `YOUR_DIRECTORY`.

---

## Các Câu Hỏi Thường Gặp & Xử Lý Trường Hợp Đặc Biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu HTML của tôi tham chiếu tới các phông chữ bên ngoài thì sao?* | WeasyPrint sẽ tự động tải các file phông chữ, nhưng bạn có thể muốn whitelist các domain để tránh thời gian tải lâu. |
| *Tôi có thể chuyển đổi một chuỗi HTML thay vì một tệp không?* | Có—sử dụng `HTML(string=my_html_string)` và bỏ qua `base_url` hoặc đặt nó thành một thư mục tạm. |
| *Làm sao tôi kiểm soát siêu dữ liệu PDF (tiêu đề, tác giả)?* | Truyền một dict `metadata` vào `write_pdf`, ví dụ: `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Tôi gặp lỗi “cairo‑cffi error” trên Linux.* | Cài đặt gói hệ thống `libcairo2-dev` (`apt-get install libcairo2-dev` trên Debian/Ubuntu) trước khi pip cài WeasyPrint. |

---

## Tổng Kết

Chúng ta vừa **tạo PDF từ HTML** bằng một quy trình Python sạch sẽ, đã khám phá cơ chế **chuyển đổi HTML sang PDF**, và chỉ cho bạn cách **lưu HTML dưới dạng PDF** với việc xử lý tài nguyên mạnh mẽ. Script đủ nhỏ để chèn vào các pipeline CI, nhưng cũng đủ linh hoạt để mở rộng với header, footer hoặc watermark tùy chỉnh.

Các bước tiếp theo bạn có thể khám phá:

- Sử dụng thư viện **html to pdf python** `pdfkit` cho cách tiếp cận dựa trên wkhtmltopdf (tốt cho CSS legacy).  
- Thêm giao diện CLI với `argparse` để script chấp nhận các đối số đầu vào/đầu ra.  
- Tạo PDF ngay trong một endpoint Flask hoặc FastAPI để cung cấp báo cáo theo yêu cầu.  

Hãy thoải mái thử nghiệm, phá vỡ và sau đó quay lại hướng dẫn này để ôn lại nhanh. Nếu gặp khó khăn, tài liệu và diễn đàn cộng đồng của WeasyPrint là những nguồn tài nguyên tuyệt vời.

Chúc lập trình vui vẻ, và tận hưởng việc biến những trang web thành PDF mượt mà!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}