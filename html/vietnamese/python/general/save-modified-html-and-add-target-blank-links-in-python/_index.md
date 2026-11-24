---
category: general
date: 2026-11-24
description: Lưu HTML đã chỉnh sửa và thêm liên kết target="_blank" trong Python bằng
  Aspose.HTML. Tìm hiểu cách thay đổi thuộc tính href target cho tất cả các thẻ <a>
  và mở mọi liên kết trong tab mới.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified html
- add target blank links
- change href target
- open all links newtab
language: vi
lastmod: 2026-11-24
og_description: Lưu HTML đã chỉnh sửa và thêm liên kết target blank trong Python với
  Aspose.HTML. Thực hiện theo hướng dẫn từng bước này để thay đổi mục tiêu href và
  mở tất cả các liên kết trong tab mới.
og_image_alt: Screenshot of a Python script that saves modified HTML with target='_blank'
  on every link
og_title: Lưu HTML đã chỉnh sửa và thêm liên kết target="_blank" trong Python – hướng
  dẫn chi tiết
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Save modified HTML and add target blank links in Python using Aspose.HTML.
    Learn how to change href target for all <a> tags and open all links newtab.
  headline: Save modified HTML and add target blank links in Python
  type: TechArticle
tags:
- Aspose.HTML
- Python
- HTML manipulation
- Web automation
title: Lưu HTML đã chỉnh sửa và thêm liên kết target="_blank" trong Python
url: /vi/python/general/save-modified-html-and-add-target-blank-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu HTML đã chỉnh sửa và thêm liên kết target blank trong Python

Nếu bạn cần **lưu HTML đã chỉnh sửa** sau khi cập nhật mọi liên kết, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Aspose.HTML cho Python. Bạn sẽ học cách **thêm liên kết target blank**, thay đổi mục tiêu href, và làm cho tất cả các liên kết mở trong một tab mới.

Bài tutorial bao gồm mọi thứ từ việc tải tệp HTML đến việc xác minh rằng các thay đổi đã được ghi đúng. Không cần công cụ bên ngoài nào ngoài thư viện Aspose.HTML.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.8 trở lên đã được cài đặt  
* Giấy phép Aspose.HTML cho Python đang hoạt động (hoặc khóa dùng thử miễn phí)  
* Một tệp HTML cục bộ mà bạn muốn chỉnh sửa (ví dụ, `index.html`)  

Bạn có thể cài đặt thư viện bằng pip:

```bash
pip install aspose-html
```

## Bước 1: Tải tài liệu HTML

Bước đầu tiên là tạo một thể hiện `HTMLDocument` trỏ tới tệp nguồn của bạn. Đối tượng này đại diện cho toàn bộ cây DOM, cho phép bạn truy vấn và chỉnh sửa các phần tử.

```python
from aspose.html import HTMLDocument

# Load the original HTML file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")
```

*Lý do quan trọng*: Việc tải tài liệu cung cấp cho bạn quyền truy cập lập trình vào mọi nút, điều cần thiết cho các cập nhật hàng loạt như thay đổi thuộc tính `target` trên tất cả các thẻ `<a>`.

## Bước 2: Thêm liên kết target blank vào mọi anchor

Để làm cho mọi siêu liên kết mở trong một tab mới, bạn đặt thuộc tính `target` thành `_blank`. Phương thức `query_selector_all` trả về một bộ sưu tập sống của tất cả các phần tử `<a>`, bất kể độ sâu lồng nhau.

```python
# Update all <a> tags to open links in a new tab
for link in doc.query_selector_all("a"):
    link.set_attribute("target", "_blank")
```

**Các điểm chính**

* Vòng lặp tiếp cận mỗi anchor đúng một lần, đảm bảo **add target blank links** được áp dụng đồng đều.  
* Nếu một liên kết đã có thuộc tính `target`, lời gọi sẽ ghi đè lên, bảo đảm hành vi nhất quán.  

### Xử lý các giá trị `target` đã tồn tại (tùy chọn)

Nếu bạn muốn giữ lại các target hiện có và chỉ đặt `_blank` khi thuộc tính còn thiếu, hãy thêm một kiểm tra điều kiện:

```python
for link in doc.query_selector_all("a"):
    if not link.has_attribute("target"):
        link.set_attribute("target", "_blank")
```

## Bước 3: Thay đổi href target và mở tất cả liên kết trong tab mới

Đôi khi bạn cần viết lại thuộc tính `href`—có thể để thêm tiền tố URL cơ sở hoặc chuyển các đường dẫn tương đối thành URL tuyệt đối. Kỹ thuật duyệt DOM tương tự cũng áp dụng cho việc thay đổi `href`.

```python
base_url = "https://example.com/"

for link in doc.query_selector_all("a"):
    href = link.get_attribute("href")
    # Skip empty or already absolute URLs
    if href and not href.startswith("http"):
        new_href = base_url + href.lstrip("/")
        link.set_attribute("href", new_href)
    # Ensure the link opens in a new tab
    link.set_attribute("target", "_blank")
```

*Lý do quan trọng*: Bằng cách **changing href target** và đảm bảo **open all links newtab**, bạn bảo đảm người dùng được dẫn tới vị trí đúng và việc điều hướng diễn ra mà không rời khỏi trang hiện tại.

## Bước 4: Lưu tài liệu đã chỉnh sửa

Sau khi hoàn tất mọi chỉnh sửa, gọi `save` để ghi các thay đổi vào một tệp mới. Đây là thời điểm **save modified html** thực sự diễn ra.

```python
# Save the updated HTML to a new file
doc.save("YOUR_DIRECTORY/index_modified.html")
```

Tệp `index_modified.html` kết quả sẽ chứa mọi thẻ `<a>` với `target="_blank"` và bất kỳ giá trị `href` nào đã được cập nhật. Bạn có thể mở tệp trong trình duyệt để xác minh rằng việc nhấp vào bất kỳ liên kết nào đều mở trong một tab mới.

## Bước 5: Xác minh kết quả (tùy chọn)

Một kiểm tra nhanh giúp xác nhận rằng thao tác đã thành công:

```python
# Reload the saved file to verify changes
verify_doc = HTMLDocument("YOUR_DIRECTORY/index_modified.html")
for link in verify_doc.query_selector_all("a"):
    assert link.get_attribute("target") == "_blank", "Target attribute not set correctly"
print("All links have target='_blank' and the file was saved successfully.")
```

Nếu câu lệnh assert thất bại, script sẽ ném lỗi, chỉ ra phần tử gây vấn đề.

## Mẹo chuyên nghiệp: Xử lý hàng loạt nhiều tệp

Khi bạn có một thư mục chứa nhiều tệp HTML, hãy gói logic vào một hàm và lặp qua từng tệp:

```python
import os
from aspose.html import HTMLDocument

def process_file(input_path: str, output_path: str, base_url: str = None):
    doc = HTMLDocument(input_path)
    for link in doc.query_selector_all("a"):
        if base_url:
            href = link.get_attribute("href")
            if href and not href.startswith("http"):
                link.set_attribute("href", base_url + href.lstrip("/"))
        link.set_attribute("target", "_blank")
    doc.save(output_path)

source_dir = "YOUR_DIRECTORY"
for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src = os.path.join(source_dir, filename)
        dst = os.path.join(source_dir, f"{os.path.splitext(filename)[0]}_modified.html")
        process_file(src, dst, base_url="https://example.com/")
```

Mẫu này mở rộng quy trình **save modified html** cho bất kỳ số lượng trang nào đồng thời duy trì **add target blank links** và **change href target** một cách nhất quán.

## Kết quả mong đợi

Mở `index_modified.html` trong trình duyệt sẽ hiển thị cùng bố cục hình ảnh như trang gốc, nhưng mọi siêu liên kết giờ đã bao gồm:

```html
<a href="https://example.com/about.html" target="_blank">About Us</a>
```

Nhấp vào liên kết sẽ mở đích đến trong một tab trình duyệt mới, giữ nguyên trang hiện tại của người dùng.

## Những lỗi thường gặp và cách tránh chúng

| Vấn đề | Giải thích | Cách khắc phục |
|--------|------------|----------------|
| Thiếu giấy phép Aspose.HTML | Thư viện sẽ ném lỗi giấy phép khi chạy. | Lấy tệp giấy phép và gọi `aspose.html.License().set_license("license_path")` trước khi tải tài liệu. |
| URL tương đối bắt đầu bằng `//` | Được coi là URL phụ thuộc giao thức và có thể không được thay đổi. | Thêm kiểm tra `href.startswith("//")` và thêm tiền tố `https:` nếu cần. |
| Tệp HTML rất lớn | Việc tải các tệp khổng lồ có thể tiêu tốn nhiều bộ nhớ. | Sử dụng API streaming hoặc chia tệp thành các phần nhỏ hơn nếu bộ nhớ trở thành nút thắt. |

## Kết luận

Bạn đã biết cách **save modified HTML** sau khi áp dụng **add target blank links**, **change href target**, và đảm bảo **open all links newtab** bằng Aspose.HTML cho Python. Giải pháp hoàn chỉnh tải một tệp HTML, cập nhật mọi phần tử `<a>`, và ghi kết quả vào một tệp mới, đồng thời xử lý các trường hợp đặc biệt như thuộc tính `target` đã tồn tại và URL tương đối.

Tiếp theo, bạn có thể khám phá:

* Sử dụng bộ chọn CSS để chỉ nhắm mục tiêu các liên kết ngoài (`a[href^="http"]`)  
* Chèn JavaScript thêm `rel="noopener"` để tăng bảo mật khi mở tab mới  
* Chuyển đổi HTML đã chỉnh sửa sang PDF bằng Aspose.PDF cho Python  

Hãy tự do điều chỉnh mã cho cấu trúc dự án của mình và thử nghiệm các thao tác DOM bổ sung. Chúc bạn lập trình vui vẻ!


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to save HTML as PDF with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-pdf-with-aspose-html-for-python/)
- [How to save HTML as Markdown with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-markdown-with-aspose-html-for-python/)
- [How to Use Aspose – Convert HTML to Markdown and Extract Links](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}