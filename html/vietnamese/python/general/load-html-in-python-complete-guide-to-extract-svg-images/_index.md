---
category: general
date: 2026-06-10
description: Tải HTML trong Python để trích xuất hình ảnh SVG từ các trang của bạn
  — mã từng bước, mẹo và xử lý các trường hợp đặc biệt.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: vi
og_description: Tải HTML trong Python và trích xuất hình ảnh SVG với ví dụ rõ ràng,
  có thể chạy được. Tìm hiểu cách tìm kiếm các phần tử SVG trong HTML và xử lý các
  trường hợp đặc biệt.
og_title: Tải HTML trong Python – Trích xuất hình ảnh SVG một cách hiệu quả
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Tải HTML trong Python – Hướng dẫn toàn diện để trích xuất hình ảnh SVG
url: /vi/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tải HTML trong Python – Hướng Dẫn Toàn Diện để Trích Xuất Hình Ảnh SVG

Bạn đã bao giờ cần **load HTML in Python** chỉ để lấy mọi đồ họa SVG từ một trang chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một web‑scraper, tạo báo cáo tài sản, hoặc chỉ tò mò về các biểu tượng mà một trang web sử dụng, việc biết cách **extract SVG images** sẽ giúp bạn tiết kiệm rất nhiều công việc tìm kiếm thủ công.

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp thực tế, từ đầu tới cuối mà **loads HTML in Python**, sau đó **searches HTML SVG** các phần tử, **finds inline SVG**, và thậm chí lấy các tệp SVG bên ngoài được tham chiếu bởi thẻ `<img>`. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng, một vài mẹo cho những phần khó, và một hình ảnh rõ ràng về cách đầu ra trông như thế nào.

## Những Điều Bạn Sẽ Nhận Được

* Một script Python có thể chạy hoàn chỉnh, phân tích một tệp HTML cục bộ (hoặc một trang đã lấy) và liệt kê mọi SVG mà nó có thể tìm thấy.  
* Hiểu sự khác biệt giữa **inline SVG** (`<svg>…</svg>`) và **external SVG** (`<img src="… .svg">`).  
* Chiến lược để xử lý markup bị hỏng, tệp thiếu, và các quirks của namespace.  
* Ý tưởng mở rộng mã—lưu các SVG, chuyển chúng sang PNG, hoặc đưa chúng vào cơ sở dữ liệu.  

### Yêu Cầu Trước

* Đã cài đặt Python 3.8+.  
* Hiểu biết cơ bản về các thư viện `requests` và `BeautifulSoup` của Python (chúng tôi sẽ import chúng, không cần đào sâu).  
* Một tệp HTML cục bộ hoặc một URL bạn muốn quét.  

Bây giờ, hãy bắt đầu.

## Tải HTML trong Python – Cài Đặt Trình Phân Tích

Bước đầu tiên là **load HTML in Python**. Bạn có thể đọc một tệp từ đĩa hoặc lấy một trang từ xa. Dưới đây là một helper tối thiểu nhưng mạnh mẽ thực hiện cả hai:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Tại sao điều này quan trọng:** Sử dụng `BeautifulSoup` trừu tượng hoá các quirks của việc phân tích chuỗi thô, và hàm này xử lý một cách nhẹ nhàng cả tệp cục bộ và URL từ xa. Nó cũng ném ra một ngoại lệ nếu yêu cầu mạng thất bại—do đó bạn sẽ ngay lập tức biết khi có gì sai.

## Trích Xuất Hình Ảnh SVG – Tìm Các Phần Tử Inline SVG

Khi tài liệu đã được tải, phần tiếp theo hợp lý là **find inline SVG** các thẻ. Inline SVG được nhúng trực tiếp trong markup HTML, có nghĩa là bạn có thể lấy nó ngay từ DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Pro tip:* Nếu trang sử dụng namespace SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` vẫn tìm thấy thẻ vì nó mặc định bỏ qua namespace. Đó là một tiện ích khi bạn chỉ **searching HTML SVG**.

## Tìm Kiếm HTML SVG – Xử Lý Tham Chiếu `<img>` Bên Ngoài

Nhiều trang không nhúng SVG trực tiếp; chúng tham chiếu các tệp bên ngoài qua `<img src="icon.svg">`. Để lấy chúng, chúng ta cần lặp qua mọi thẻ `<img>`, kiểm tra `src` của chúng, và xem liệu nó có kết thúc bằng `.svg` không.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Cảnh báo trường hợp đặc biệt:** Một số trang sử dụng query string (`icon.svg?v=2`) hoặc fragment (`icon.svg#layer`). Kiểm tra `endswith(".svg")` vẫn hoạt động vì chúng ta chỉ nhìn vào phần cuối đã chuyển sang chữ thường của chuỗi. Nếu bạn cần xác thực chặt chẽ hơn, hãy cân nhắc sử dụng `urllib.parse` để loại bỏ các tham số trước.

## Tìm Inline SVG – Báo Cáo Kết Quả

Bây giờ chúng ta có hai danh sách—một cho markup SVG inline và một cho các tham chiếu tệp bên ngoài—chúng ta có thể kết hợp chúng và báo cáo tổng số. Điều này phản ánh đoạn mã gốc bạn đã đăng, nhưng thêm một chút ngữ cảnh.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Kết Hợp Tất Cả — Script Hoàn Chỉnh

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu nó dưới tên `extract_svg.py` và chỉ định tới một tệp HTML cục bộ hoặc một URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Đầu Ra Dự Kiến

Chạy script với một mẫu `sample.html` có thể tạo ra:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Nếu bạn bỏ comment khối tải xuống, SVG bên ngoài

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [svg to png java – Chuyển Đổi SVG sang Hình Ảnh với Aspose.HTML cho Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Chuyển Đổi SVG sang Hình Ảnh trong .NET với Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Cách Chuyển Đổi SVG sang XPS với Aspose.HTML cho Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}