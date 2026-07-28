---
category: general
date: 2026-07-27
description: Cara menggunakan SaveOptions di Aspose.HTML (Python) untuk mengonversi
  halaman HTML besar dan menerapkan penanganan sumber daya secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: id
lastmod: 2026-07-27
og_description: Cara menggunakan SaveOptions di Aspose.HTML (Python) memungkinkan
  Anda mengonversi halaman HTML besar sambil menerapkan penanganan sumber daya untuk
  hasil yang bersih dan cepat.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Cara Menggunakan SaveOptions di Aspose.HTML – Panduan Python
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
title: Cara Menggunakan SaveOptions di Aspose.HTML (Python)
url: /id/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan SaveOptions di Aspose.HTML (Python)

Cara menggunakan SaveOptions di Aspose.HTML untuk Python adalah pertanyaan yang sering diajukan oleh banyak pengembang ketika menangani file HTML yang sangat besar. Jika Anda perlu **mengonversi halaman HTML besar** sambil tetap mengontrol **apply resource handling**, Anda berada di tempat yang tepat.  

Dalam tutorial ini kami akan membahas skenario dunia nyata: mengambil halaman HTML yang berat, membatasi seberapa dalam sumber daya bersarang diambil, dan akhirnya menyimpan (atau mengonversi) hasilnya dengan kontrol yang sangat jelas. Tanpa referensi yang samar, hanya contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke proyek Anda hari ini.

> **Pro tip:** `SaveOptions` milik Aspose.HTML tidak hanya berfungsi untuk menyimpan kembali ke HTML tetapi juga untuk mengonversi ke PDF, PNG, atau bahkan DOCX. Pola yang kami bahas di bawah ini berlaku untuk semua format tersebut.

---

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode menggunakan type hints tetapi dapat dijalankan pada versi terbaru apa pun)  
- **Aspose.HTML untuk Python via .NET** – instal dengan `pip install aspose-html`  
- Sebuah **file HTML besar** yang ingin Anda perkecil atau ubah (contoh menggunakan `big_page.html`)  
- Ruang disk yang cukup untuk file output  

Itu saja—tanpa pustaka tambahan, tanpa alat build yang berat.

---

## Cara Menggunakan SaveOptions dengan Opsi Resource Handling

Inilah inti permasalahannya. Kami akan membuat instance `SaveOptions`, melampirkan objek `ResourceHandlingOptions` yang memberi tahu Aspose.HTML seberapa dalam ia harus menelusuri aset yang ditautkan, lalu menyerahkan semuanya ke metode `save` dokumen.

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

**Mengapa ini berhasil:**  
- `HTMLDocument` memuat file asli, mengurai setiap `<img>`, `<link>`, `<script>`, dll.  
- `ResourceHandlingOptions.max_handling_depth` memberi tahu mesin untuk berhenti menelusuri sumber daya setelah tiga tingkat bersarang—sempurna untuk menghindari loop tak berujung pada halaman yang menyematkan halaman lain.  
- `SaveOptions` adalah wadah yang membawa baik format output (HTML secara default) maupun aturan resource handling.  
- Akhirnya, `doc.save` menulis file baru, menerapkan aturan yang baru saja kami tetapkan.

Saat Anda menjalankan skrip, Anda akan melihat file baru di `big_page_processed.html`. Buka di browser; Anda akan memperhatikan bahwa semua gambar, gaya, dan skrip hingga tiga tingkat kedalaman masih ada, sementara referensi yang lebih dalam telah dihapus. Ini secara dramatis mengurangi ukuran file tanpa merusak tata letak inti halaman—tepat apa yang Anda butuhkan ketika **mengonversi halaman HTML besar** untuk penggunaan offline atau pengiriman email.

---

## Mengonversi Halaman HTML Besar Secara Efisien

Jika tujuan Anda adalah *mengonversi halaman HTML besar* ke versi yang lebih ramping, potongan kode di atas sudah melakukan sebagian besar pekerjaan berat. Namun, Anda mungkin ingin mengubah format output sepenuhnya. Aspose.HTML membuatnya menjadi satu baris:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Cukup ganti properti `format` dengan `"PNG"`, `"JPEG"`, atau `"DOCX"` dan Anda sudah memiliki pipeline konversi lengkap. Aturan **apply resource handling** tetap berlaku, sehingga PDF yang dihasilkan tidak akan menyematkan setiap file CSS eksternal dari situs asli—hanya yang berada dalam kedalaman tiga tingkat yang Anda definisikan.

---

## Menerapkan Resource Handling pada Sumber Daya Bersarang

Mari selami lebih dalam tentang **apply resource handling** secara efektif. Misalkan HTML Anda berisi stylesheet yang sendiri mengimpor stylesheet lain, masing‑masing menarik gambar. Tanpa batas kedalaman, Aspose.HTML dapat menelusuri rantai tersebut selamanya, membebani memori dan CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – Tidak ada sumber daya eksternal yang diambil; Anda mendapatkan kerangka HTML yang sangat sederhana.  
- **Depth 1** – Hanya sumber daya tingkat pertama (tag `<img>` langsung, file CSS segera) yang disertakan.  
- **Depth 2+** – Penelusuran bersarang yang lebih dalam dihormati, berguna untuk situs kompleks di mana gaya bergantung pada gaya lain.

Pilih kedalaman yang sesuai dengan skenario **mengonversi halaman HTML besar** Anda. Untuk buletin email, depth 1 biasanya sudah cukup. Untuk arsip lokal, depth 3 (seperti pada contoh utama) memberikan keseimbangan yang baik.

---

## Contoh Lengkap yang Dapat Dijalankan – Dari Awal hingga Selesai

Berikut adalah skrip mandiri yang dapat Anda letakkan dalam file bernama `process_html.py`. Skrip ini mencakup penanganan error, logging, dan helper kecil yang mencetak pengurangan ukuran yang Anda capai.

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

**Output yang diharapkan (console):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Buka file yang telah diproses; Anda akan melihat halaman yang lebih ringan namun tetap tampak seperti aslinya. Jika Anda mengubah `fmt` menjadi `"PDF"`, console akan melaporkan ukuran file PDF dan Anda dapat membukanya dengan penampil PDF apa pun.

---

## Pertanyaan Umum & Kasus Edge

- **Bagaimana jika halaman tersebut merujuk sumber daya melalui HTTPS yang memerlukan autentikasi?**  
  Aspose.HTML mengikuti redirect tetapi tidak mengirim kredensial secara otomatis. Anda dapat mengunduh aset tersebut terlebih dahulu atau menggunakan handler `WebRequest` khusus (di luar cakupan panduan ini).

- **Apakah saya dapat mempertahankan CSS inline sambil menghapus file eksternal?**  
  Ya—atur `resource_options.max_handling_depth = 0`. Ini melewatkan file eksternal tetapi tetap menyimpan blok `<style>` apa pun.

- **Bagaimana dengan gambar sangat besar yang masih membuat output menjadi berat?**  
  Setelah menyimpan, Anda dapat menjalankan proses sekunder dengan Pillow untuk memperkecil gambar, atau biarkan opsi kompresi gambar bawaan Aspose.HTML yang menangani hal ini (gunakan `save_options.image_quality`).

- **Apakah batas kedalaman diterapkan per tipe sumber daya?**  
  Batasnya bersifat global untuk semua tipe sumber daya (gambar, skrip, gaya). Jika Anda memerlukan kontrol yang lebih granular, Anda harus memfilter sumber daya secara manual setelah memuat dokumen.

---

## Kesimpulan

Anda kini memiliki pemahaman yang kuat tentang **cara menggunakan SaveOptions** di Aspose.HTML


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}