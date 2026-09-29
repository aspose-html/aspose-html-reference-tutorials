---
category: general
date: 2026-09-29
description: Cách lưu SVG bằng Python và xuất SVG sang PNG. Học cách chuyển đổi SVG
  sang PNG với các tùy chọn tinh chỉnh trong vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: vi
lastmod: 2026-09-29
og_description: Cách lưu SVG bằng Python và xuất SVG sang PNG. Hãy làm theo hướng
  dẫn này để chuyển đổi SVG sang PNG với khả năng kiểm soát đầy đủ các tùy chọn.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Cách lưu SVG thành PNG bằng Python – từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Cách lưu SVG thành PNG bằng Python – hướng dẫn đầy đủ
url: /vi/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu SVG thành PNG bằng Python – hướng dẫn đầy đủ

Nếu bạn cần **cách lưu SVG** thành hình ảnh raster, hướng dẫn này sẽ cho bạn một giải pháp sẵn sàng chạy. Bạn sẽ học cách tải tệp SVG vector, tùy chọn điều chỉnh các cài đặt lưu ảnh, và xuất kết quả ra PNG chỉ trong ba dòng mã.

Lưu tệp SVG thành PNG thường được sử dụng khi bạn muốn nhúng đồ họa vào trang web, tạo ảnh thu nhỏ, hoặc cung cấp hình ảnh raster cho các pipeline học máy. Cách tiếp cận được mô tả ở đây hoạt động trên Windows, macOS và Linux mà không cần phụ thuộc gốc bổ sung.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.9 hoặc mới hơn đã được cài đặt
* Gói `aspose.svg` (Aspose SVG chính thức cho Python qua .NET). Cài đặt bằng:

```bash
pip install aspose-svg
```

* Một tệp SVG hợp lệ trên đĩa (ví dụ, `vector.svg`)

Các yêu cầu này giúp ví dụ tự chứa và tránh các công cụ bên ngoài như CairoSVG.

## Cách lưu SVG bằng Python

Cốt lõi của quá trình gồm ba bước: tải, cấu hình và lưu. Các phần sau sẽ phân tích từng bước.

### Bước 1: Tải tài liệu SVG

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` phân tích XML SVG và xây dựng một biểu diễn trong bộ nhớ. Việc tải tệp trước là bắt buộc; nếu không, thao tác lưu sẽ không có dữ liệu nguồn.

### Bước 2: (Tùy chọn) Tạo tùy chọn lưu ảnh

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` cho phép bạn tinh chỉnh đầu ra PNG. Điều chỉnh chiều rộng và chiều cao giữ tỷ lệ khung hình trừ khi bạn đặt cả hai một cách rõ ràng. Đặt màu nền hữu ích khi SVG gốc có độ trong suốt nhưng bạn cần PNG không trong suốt.

### Bước 3: Lưu SVG thành PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

Phương thức `save` ghi một tệp PNG vào đường dẫn đích. Nếu bạn bỏ qua đối số `options`, thư viện sẽ sử dụng kích thước mặc định lấy từ viewBox của SVG.

### Toàn bộ script

Kết hợp các phần lại sẽ cho ra một chương trình hoàn chỉnh, có thể chạy được:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Chạy script sẽ in **“SVG successfully saved as PNG.”** và tạo `vector.png` trong cùng thư mục.

## Chuyển đổi SVG sang PNG – xử lý các vấn đề thường gặp

### Tệp không tồn tại hoặc đường dẫn không hợp lệ

Nếu `src_path` không tồn tại, `SVGDocument` sẽ ném ra `FileNotFoundError`. Bao quanh lời gọi bằng khối `try/except` để cung cấp thông báo lỗi thân thiện:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Giữ tỷ lệ khung hình

Khi chỉ một kích thước (chiều rộng **hoặc** chiều cao) được đặt, thư viện sẽ tự động điều chỉnh kích thước còn lại để duy trì tỷ lệ khung hình gốc. Nếu bạn đặt cả hai kích thước, hình ảnh có thể bị kéo dài. Chọn cách tiếp cận phù hợp với yêu cầu UI của bạn.

### Nền trong suốt

Nếu SVG gốc dựa vào độ trong suốt (ví dụ, biểu tượng), bạn có thể giữ PNG trong suốt bằng cách bỏ qua `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Biến thể này hữu ích khi PNG sẽ được xếp lớp lên các đồ họa khác.

## Xuất SVG sang PNG – mẹo hiệu năng

* **Tái sử dụng `ImageSaveOptions`** khi chuyển đổi nhiều tệp trong một lô. Tạo một đối tượng tùy chọn mới cho mỗi tệp chỉ gây thêm tải nhẹ, nhưng việc tái sử dụng tránh việc cấp phát bộ nhớ lặp lại.
* **Xử lý hàng loạt**: Duyệt qua một thư mục chứa các tệp SVG và gọi `convert_svg_to_png` cho mỗi tệp. Thư viện xử lý mỗi tệp độc lập, vì vậy bạn có thể song song hoá vòng lặp bằng `concurrent.futures.ThreadPoolExecutor` để chuyển đổi nhanh hơn trên máy đa lõi.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Lưu SVG thành PNG – xác minh

Sau khi chuyển đổi, bạn có thể xác minh đầu ra bằng chương trình:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Kết quả điển hình:

```
PNG size: (1024, 768), mode: RGBA
```

`mode` `RGBA` xác nhận rằng hình ảnh có kênh alpha (độ trong suốt). Nếu bạn đặt màu nền, chế độ sẽ là `RGB`.

## Kết luận

Bây giờ bạn đã biết **cách lưu SVG** thành PNG bằng Python, cách **chuyển đổi SVG sang PNG**, và cách **xuất SVG sang PNG** với kích thước tùy chỉnh và xử lý nền. Script hoàn chỉnh minh họa toàn bộ quy trình từ tải tệp SVG vector đến tạo ra hình ảnh PNG raster.

Tiếp theo, khám phá các chủ đề liên quan như **lưu SVG thành PNG** ở chế độ hàng loạt, sử dụng các thư viện thay thế như **CairoSVG**, hoặc tạo PDF đa trang từ nguồn SVG. Thử nghiệm các cài đặt `ImageSaveOptions` khác nhau để tinh chỉnh chất lượng, DPI và nén cho trường hợp sử dụng cụ thể của bạn.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [svg sang png java – Chuyển đổi SVG thành hình ảnh với Aspose.HTML cho Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Hiển thị tài liệu SVG dưới dạng PNG trong .NET với Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Cách đặt DPI khi chuyển đổi SVG sang PNG bằng Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}