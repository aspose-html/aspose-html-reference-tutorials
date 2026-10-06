---
category: general
date: 2026-10-05
description: Pelajari cara membatasi sumber daya bersarang di Aspose.HTML untuk Python
  guna mencegah rekursi tak terbatas dan mengendalikan kedalaman sumber daya.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resources
- prevent infinite recursion
language: id
lastmod: 2026-10-05
og_description: Batasi sumber daya bersarang di Aspose.HTML untuk Python untuk mencegah
  rekursi tak terbatas. Ikuti panduan langkah demi langkah ini untuk mengontrol kedalaman
  sumber daya dengan aman.
og_image_alt: Diagram illustrating limit nested resources setting in Aspose.HTML
og_title: Batasi sumber daya bersarang di Aspose.HTML – hentikan rekursi tak terbatas
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Learn how to limit nested resources in Aspose.HTML for Python to prevent
    infinite recursion and control resource depth.
  headline: How to limit nested resources in Aspose.HTML for Python
  type: TechArticle
- description: Learn how to limit nested resources in Aspose.HTML for Python to prevent
    infinite recursion and control resource depth.
  name: How to limit nested resources in Aspose.HTML for Python
  steps:
  - name: Prerequisites
    text: '* Python 3.8 or newer. * Aspose.HTML for Python installed (`pip install
      aspose-html`). * A local HTML file that includes multiple levels of linked resources
      (e.g., CSS → @import → more CSS).'
  - name: Common patterns that trigger recursion
    text: '| Pattern | Why it recurses | How the depth limit helps | |---------|----------------|---------------------------|
      | CSS `@import` chain that loops back to the original file | Each import creates
      a new resource request | The parser stops after `max_handling_depth` levels
      | | JavaScript that dynamica'
  - name: Tips for fine‑tuning the limit
    text: '* **Start with `3`** – most sites need at most two levels (page → CSS →
      imported CSS). * **Increase to `5`** only if you know the page legitimately
      uses deeper nesting. * **Set to `1`** when you only need the main document and
      want to skip all external resources (great for quick text extraction).'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- resource handling
title: Cara membatasi sumber daya bersarang di Aspose.HTML untuk Python
url: /id/python/general/how-to-limit-nested-resources-in-aspose-html-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi sumber daya bersarang di Aspose.HTML untuk Python

Jika Anda perlu **membatasi sumber daya bersarang** saat memuat dokumen HTML dengan Aspose.HTML, panduan ini menunjukkan secara tepat cara melakukannya. Mengontrol kedalaman penanganan sumber daya juga **mencegah rekursi tak terbatas** ketika sebuah halaman merujuk dirinya sendiri melalui CSS, skrip, atau gambar.

Di bagian berikut Anda akan mempelajari mengapa membatasi sumber daya bersarang penting, cara mengonfigurasi `ResourceHandlingOptions`, dan cara memverifikasi bahwa dokumen dimuat tanpa menghabiskan memori atau menyebabkan stack overflow.

## Apa yang akan Anda pelajari

* Mengapa sumber daya bersarang dapat menyebabkan loop rekursi tak terbatas.
* Cara menetapkan kedalaman penanganan maksimum dengan `ResourceHandlingOptions`.
* Contoh Python lengkap yang dapat dijalankan yang mendemonstrasikan teknik ini.
* Tips untuk memecahkan masalah kasus tepi umum seperti impor CSS melingkar.

### Prasyarat

* Python 3.8 atau lebih baru.
* Aspose.HTML untuk Python terpasang (`pip install aspose-html`).
* File HTML lokal yang mencakup beberapa tingkat sumber daya tertaut (misalnya, CSS → @import → CSS lainnya).

---

## Langkah 1: Impor kelas Aspose.HTML yang diperlukan

Langkah pertama adalah membawa kelas yang diperlukan ke dalam ruang lingkup. `HTMLDocument` mengurai file, sementara `ResourceHandlingOptions` memungkinkan Anda mengontrol seberapa dalam pengurai mengikuti sumber daya yang ditautkan.

```python
# Import required classes from the Aspose.HTML package
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

*Mengapa ini penting*: Tanpa mengimpor `ResourceHandlingOptions` Anda tidak dapat menetapkan batas kedalaman, yang berarti pengurai akan mengikuti setiap sumber daya yang ditautkan tanpa henti.

---

## Langkah 2: Konfigurasikan kedalaman penanganan sumber daya

Buat sebuah instance `ResourceHandlingOptions` dan tetapkan `max_handling_depth`. Kedalaman **3** menghentikan pengurai setelah tiga tingkat sumber daya bersarang, yang biasanya cukup untuk halaman web tipikal sekaligus melindungi dari rekursi yang tidak terkendali.

```python
# Create a ResourceHandlingOptions object
resource_options = ResourceHandlingOptions()

# Limit nested resources to three levels
resource_options.max_handling_depth = 3  # This value prevents infinite recursion
```

*Mengapa ini penting*: Jika sebuah halaman merujuk file CSS yang pada gilirannya mengimpor file CSS lain yang kembali merujuk file asli, pengurai dapat berulang selamanya. Properti `max_handling_depth` memberi tahu Aspose.HTML untuk berhenti setelah jumlah tingkat yang ditentukan, secara efektif **mencegah rekursi tak terbatas**.

---

## Langkah 3: Muat dokumen HTML dengan opsi yang telah dikonfigurasi

Berikan objek `resource_options` ke konstruktor `HTMLDocument`. Pengurai kini menghormati batas kedalaman yang Anda definisikan.

```python
# Load the HTML document using the configured resource handling options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    resource_handling_options=resource_options
)

# Optional: verify that the document loaded successfully
print("Document loaded. Number of pages:", doc.pages.count)
```

*Mengapa ini penting*: Dengan menyediakan `resource_handling_options`, Anda memastikan bahwa gambar, stylesheet, atau skrip bersarang diproses hanya hingga kedalaman yang diizinkan. Pernyataan `print` mengonfirmasi bahwa dokumen berhasil dimuat tanpa menimbulkan kesalahan rekursi.

---

## Cara **mencegah rekursi tak terbatas** dalam skenario dunia nyata

### Pola umum yang memicu rekursi

| Pola | Mengapa terjadi rekursi | Bagaimana batas kedalaman membantu |
|------|------------------------|------------------------------------|
| Rantai CSS `@import` yang kembali ke file asli | Setiap impor membuat permintaan sumber daya baru | Pengurai berhenti setelah tingkat `max_handling_depth` |
| JavaScript yang secara dinamis memuat skrip tambahan yang merujuk skrip asli | Skrip dapat memicu panggilan jaringan lebih lanjut tanpa batas | Batas kedalaman membatasi jumlah pemuatan skrip |
| Gambar yang dihasilkan melalui data URL yang merujuk sumber daya lain | Pengurai memperlakukan setiap data URL sebagai sumber daya terpisah | Setelah batas tercapai, data URL selanjutnya diabaikan |

### Tips untuk menyempurnakan batas

* **Mulai dengan `3`** – kebanyakan situs memerlukan paling banyak dua tingkat (halaman → CSS → CSS yang diimpor).  
* **Tingkatkan ke `5`** hanya jika Anda yakin halaman memang menggunakan penumpukan yang lebih dalam.  
* **Setel ke `1`** ketika Anda hanya membutuhkan dokumen utama dan ingin melewatkan semua sumber daya eksternal (bagus untuk ekstraksi teks cepat).

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah skrip mandiri yang dapat Anda salin, sesuaikan jalur file, dan jalankan langsung.

```python
# limit_nested_resources_example.py
# -------------------------------------------------
# Demonstrates how to limit nested resources in Aspose.HTML
# to prevent infinite recursion when loading large pages.
# -------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions

def load_html_with_limit(html_path: str, max_depth: int = 3):
    """
    Loads an HTML file while limiting the depth of nested resources.

    Args:
        html_path: Path to the local HTML file.
        max_depth: Maximum number of nested resource levels.

    Returns:
        An HTMLDocument instance if loading succeeds.
    """
    # Configure the depth limit
    options = ResourceHandlingOptions()
    options.max_handling_depth = max_depth

    # Load the document using the configured options
    document = HTMLDocument(html_path, resource_handling_options=options)

    # Simple verification output
    print(f"Loaded '{html_path}' with max depth {max_depth}.")
    print(f"Total pages: {document.pages.count}")

    return document

if __name__ == "__main__":
    # Replace with the path to your HTML file
    html_file = "YOUR_DIRECTORY/big_page.html"
    load_html_with_limit(html_file, max_depth=3)
```

**Output yang diharapkan**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Total pages: 1
```

Jika pengurai menemukan rekursi yang lebih dalam dari tiga tingkat, ia menghentikan pemrosesan sumber daya lebih lanjut dan skrip selesai tanpa menimbulkan pengecualian—tepat apa yang Anda butuhkan untuk **mencegah rekursi tak terbatas**.

---

## Pro tip: mencatat peristiwa penanganan sumber daya

Aspose.HTML dapat memancarkan peristiwa ketika ia melewatkan sebuah sumber daya karena batas kedalaman. Mengaktifkan pencatatan membantu Anda memahami aset mana yang diabaikan.

```python
import logging
logging.basicConfig(level=logging.INFO)

# Inside load_html_with_limit, after creating `options`:
options.resource_handling_event_handler = lambda sender, args: \
    logging.info(f"Skipped resource: {args.resource_uri} (depth {args.current_depth})")
```

Potongan kode ini mencetak satu baris untuk setiap sumber daya yang melebihi batas, memberi Anda visibilitas tentang apa yang diabaikan.

---

## Kesimpulan

Anda kini tahu cara **membatasi sumber daya bersarang** di Aspose.HTML untuk Python dan mengapa hal itu penting untuk **mencegah rekursi tak terbatas**. Dengan mengonfigurasi `ResourceHandlingOptions.max_handling_depth`, Anda melindungi aplikasi dari pemuatan sumber daya yang tidak terkendali, mengurangi konsumsi memori, dan membuat proses HTML Anda lebih dapat diprediksi.

Siap melangkah lebih jauh? Jelajahi topik terkait berikut:

* **Mengurai HTML tanpa sumber daya eksternal** – setel `max_handling_depth` ke 1.  
* **Mengekstrak teks dari halaman HTML besar** – gabungkan batas kedalaman dengan `HTMLDocument.text`.  
* **Mengonversi HTML ke PDF sambil mengontrol kedalaman sumber daya** – berikan `ResourceHandlingOptions` yang sama ke API konversi PDF.

Silakan bereksperimen dengan nilai kedalaman yang berbeda dan bagikan temuan Anda di kolom komentar. Selamat coding!  

![Diagram yang menggambarkan pengaturan limit nested resources di Aspose.HTML](limit_nested_resources.png "diagram limit nested resources")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Custom Resource Handler in Aspose HTML – Save to Stream Guide](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [How to Sandbox JavaScript – Complete Aspose.HTML Guide](/html/english/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)
- [Render HTML to PDF with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/render-html-to-pdf-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}