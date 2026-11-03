---
category: general
date: 2026-05-28
description: Học cách sử dụng SaveOptions để cắt giảm các trang HTML trong Python.
  Hướng dẫn từng bước này cũng giải thích cách tải tài liệu HTML và loại bỏ hiệu quả
  các tài nguyên lồng nhau.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: vi
og_description: Cách sử dụng SaveOptions để cắt giảm các trang HTML trong Python.
  Hãy làm theo hướng dẫn này để tải tài liệu HTML, thiết lập giới hạn tài nguyên và
  lưu một tệp sạch, nhẹ.
og_title: Cách sử dụng SaveOptions trong Python – Cắt bớt các trang HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Cách sử dụng SaveOptions trong Python – Cắt bớt các trang HTML
url: /vi/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng SaveOptions trong Python – Cắt Bớt Trang HTML

Bạn đã bao giờ tự hỏi **cách sử dụng SaveOptions** để thu gọn một tệp HTML khổng lồ mà không làm hỏng gì không? Bạn không phải là người duy nhất. Khi bạn tải một trang có hàng chục tài nguyên lồng nhau—như CSS, JS, hoặc thậm chí các đoạn HTML khác—kết quả đầu ra có thể phình to không kiểm soát được.  

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, không chỉ cho thấy **cách sử dụng SaveOptions**, mà còn hướng dẫn **cách tải một tài liệu HTML** và cách **cắt bớt một trang HTML** bằng cách giới hạn độ sâu lồng nhau. Khi kết thúc, bạn sẽ có một tệp sạch, đã được cắt bớt, sẵn sàng để triển khai hoặc xử lý tiếp.

## Những Điều Bạn Sẽ Đạt Được

- Tải bất kỳ tệp HTML cục bộ nào chỉ với một dòng lệnh.  
- Cấu hình các tùy chọn xử lý tài nguyên để dừng lại ở một độ sâu bao gồm cụ thể.  
- Lưu kết quả đã cắt bớt bằng lớp mạnh mẽ `SaveOptions`.  

Không cần công cụ bên ngoài, không cần phép màu—chỉ cần Python thuần và một thư viện nhỏ thực hiện phần việc nặng.

---

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

1. **Python 3.9+** được cài đặt (cú pháp sử dụng hoạt động trên bất kỳ phiên bản gần đây nào).  
2. Gói giả định `htmlprocessor` cung cấp `HTMLDocument`, `SaveOptions`, và `ResourceHandlingOptions`. Cài đặt bằng cách:

```bash
pip install htmlprocessor
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng môi trường ảo, hãy kích hoạt nó trước—giúp các phụ thuộc của bạn gọn gàng hơn.

---

## Bước 1: Cách Tải Tài Liệu HTML

Việc tải một tệp đơn giản như việc chỉ định đường dẫn cho constructor. Thư viện sẽ đọc markup, xây dựng cây dạng DOM và chuẩn bị cho các thao tác tiếp theo.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Tại sao điều này quan trọng:** Đối tượng `HTMLDocument` trừu tượng hoá việc xử lý chuỗi thô, cung cấp cho bạn các phương thức để truy vấn, sửa đổi và cuối cùng là lưu trang. Nó cũng chuẩn hoá ký tự xuống dòng và mã hoá ký tự, giúp bạn tránh các lỗi tiềm ẩn sau này.

Bạn sẽ thấy chúng tôi in tiêu đề chỉ để xác nhận việc tải thành công. Nếu tệp bị thiếu hoặc sai định dạng, constructor sẽ ném ra một ngoại lệ rõ ràng—không có lỗi im lặng.

---

## Bước 2: Cấu Hình Xử Lý Tài Nguyên – Cốt Lõi của Việc Cắt Bớt

Phần tiếp theo của câu đố là **cách cắt bớt nội dung trang HTML** bằng cách giới hạn độ sâu mà bộ xử lý theo dõi các include. Đây là nơi `ResourceHandlingOptions` tỏa sáng.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### `max_handling_depth` Là Gì?

- **Depth 1** → Chỉ tệp HTML gốc, mọi tài nguyên bên ngoài đều bị bỏ qua.  
- **Depth 2** → Gốc cộng với bất kỳ tệp nào được tham chiếu trực tiếp (ví dụ: một `iframe` hoặc include phía server).  
- **Giá trị cao hơn** → Lồng sâu hơn, nhưng cũng làm tăng kích thước đầu ra và thời gian xử lý.

Bằng cách giới hạn độ sâu ở **2**, chúng ta giữ lại trang chính và một lớp include, loại bỏ mọi thứ sâu hơn. Thông thường, điều này đủ để xóa các footer dư thừa, script phân tích, hoặc các mẫu lồng nhau mà bạn không cần trong bản sao đã cắt bớt.

---

## Bước 3: Gắn Các Tùy Chọn Vào Cấu Hình Lưu

Bây giờ chúng ta gắn các quy tắc tài nguyên vào một thể hiện `SaveOptions`. Đối tượng này nói cho thư viện *chính xác* cách ghi tệp trở lại đĩa.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Tại sao nên dùng `SaveOptions`?**  
> Nó cho bạn kiểm soát chi tiết đầu ra—không chỉ dừng ở độ sâu tài nguyên. Bạn có thể sau này thêm nén, định dạng đẹp, hoặc thậm chí callback tùy chỉnh mà không cần chạm vào logic lưu cơ bản.

---

## Bước 4: Cách Sử Dụng SaveOptions Để Cắt Bớt Trang HTML

Cuối cùng, chúng ta gọi phương thức `save` với các tùy chọn đã cấu hình. Thư viện sẽ duyệt DOM, tôn trọng giới hạn độ sâu, và ghi ra một tệp đã cắt bớt.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Kết Quả Mong Đợi

- Tệp `trimmed_page.html` chứa markup gốc **cộng** bất kỳ include nào tới một mức độ sâu.  
- Tất cả các include sâu hơn đều bị bỏ qua, dẫn đến một trang nhỏ hơn, tải nhanh hơn.  
- Không có thẻ bị hỏng—thư viện tự động đóng bất kỳ phần tử nào còn lơ lửng sau khi loại bỏ.

Bạn có thể mở kết quả trong trình duyệt để xác nhận nội dung chính vẫn hiển thị, trong khi các script thừa hoặc frame lồng nhau đã biến mất.

---

## Ví Dụ Hoàn Chỉnh

Kết hợp tất cả lại, đây là script hoàn chỉnh mà bạn có thể sao chép‑dán và chạy:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Chạy script, chỉ định `INPUT` tới bất kỳ tệp HTML phức tạp nào, và bạn sẽ nhận được phiên bản gọn hơn trong `OUTPUT`.  

> **Lưu ý trường hợp đặc biệt:** Nếu trang gốc chứa các comment có điều kiện (`<!--[if IE]>…<![endif]-->`) tham chiếu tới tài nguyên sâu hơn, chúng sẽ bị loại bỏ giống như bất kỳ include lồng nào khác. Điều này ngăn các thủ thuật IE cũ làm tăng kích thước cuối cùng của bạn.

---

## Tóm Tắt Hình Ảnh

Dưới đây là một sơ đồ nhanh minh họa luồng—từ việc tải tài liệu, qua xử lý tài nguyên, đến lưu kết quả đã cắt bớt.

![ví dụ cách sử dụng saveoptions](https://example.com/placeholder.png "Sơ đồ minh họa cách sử dụng SaveOptions để cắt bớt các trang HTML")

*Văn bản thay thế:* **ví dụ cách sử dụng saveoptions** – hiển thị quy trình ba bước: tải, cấu hình và lưu tài liệu HTML.

---

## Câu Hỏi Thường Gặp & Những Cạm Bẫy

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu tôi cần độ sâu lồng sâu hơn thì sao?** | Tăng `max_handling_depth` lên 3 hoặc 4, nhưng nhớ rằng kích thước đầu ra sẽ tăng. |
| **Có thể loại trừ các thẻ cụ thể (ví dụ `<script>`) bất kể độ sâu không?** | Có—`SaveOptions` cũng hỗ trợ thuộc tính `tag_exclusion_list`. Thêm `"script"` vào danh sách này để luôn loại bỏ các script. |
| **Thư viện có an toàn với đa luồng không?** | Phiên bản hiện tại không. Hãy tạo một `HTMLDocument` riêng cho mỗi luồng. |
| **Các URL tương đối có được viết lại không?** | Mặc định là không. Dùng `save_opt.rewrite_relative_urls = True` nếu bạn cần chúng được điều chỉnh theo vị trí mới. |

---

## Bước Tiếp Theo

Giờ bạn đã thành thạo **cách sử dụng SaveOptions**, hãy thử các mở rộng sau:

- **Nén đầu ra:** Đặt `save_opt.enable_gzip = True` để giảm kích thước tệp khi truyền.  
- **Định dạng đẹp để gỡ lỗi:** Bật `save_opt.indent_output = True` để có HTML được căn chỉnh hợp lý.  
- **Xử lý hàng loạt:** Lặp qua một thư mục các tệp HTML và áp dụng cùng một logic cắt bớt—rất hữu ích cho các trình tạo site tĩnh.

Mỗi tùy chỉnh này dựa trên nền tảng bạn vừa học, giúp mã của bạn luôn sạch sẽ và dễ bảo trì.

---

## Kết Luận

Chúng ta đã đi qua toàn bộ vòng đời cắt bớt một trang HTML trong Python: **cách tải tài liệu HTML**, cấu hình **cách cắt bớt trang HTML** bằng `ResourceHandlingOptions`, và cuối cùng **cách sử dụng SaveOptions** để ghi tệp đã làm sạch. Ví dụ hoàn toàn tự chứa, chạy ngay mà không cần cấu hình thêm, và chứng minh tại sao kiểm soát độ sâu tài nguyên là một tối ưu quan trọng cho việc web‑scraping, tạo site tĩnh, hoặc bất kỳ tình huống nào bạn cần một bản sao HTML nhẹ.

Hãy thử nghiệm, thay đổi giá trị `max_handling_depth` và để các trang đã cắt bớt làm việc cho bạn. Nếu gặp khó khăn, hãy để lại bình luận bên dưới—chúc bạn lập trình vui vẻ!

## Các Tutorial Liên Quan

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [How to Zip HTML in C# – Save HTML to Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}