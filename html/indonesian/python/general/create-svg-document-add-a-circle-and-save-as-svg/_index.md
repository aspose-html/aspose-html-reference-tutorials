---
category: general
date: 2026-07-31
description: Pelajari cara membuat dokumen SVG, menambahkan lingkaran, dan menyimpan
  file SVG dengan cepat. Ekspor grafik sebagai SVG dengan beberapa baris kode Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: id
lastmod: 2026-07-31
og_description: Buat dokumen SVG, tambahkan lingkaran, dan simpan file SVG dalam hitungan
  detik. Panduan ini menunjukkan cara mengekspor grafik sebagai SVG dengan kode yang
  jelas dan dapat dijalankan.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Buat Dokumen SVG – Tambahkan Lingkaran dan Simpan sebagai SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Buat Dokumen SVG – Tambahkan Lingkaran dan Simpan sebagai SVG
url: /id/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen SVG – Tambahkan Lingkaran dan Simpan sebagai SVG

Pernah perlu **membuat dokumen SVG** dari kode tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami kebingungan saat pertama kali mencoba grafis vektor. Dalam tutorial ini kita akan menelusuri contoh kecil yang berdiri sendiri yang menunjukkan cara **menambahkan lingkaran ke SVG**, lalu **menyimpan file SVG** sehingga Anda dapat **mengekspor grafik sebagai SVG** untuk digunakan di web atau alat desain.

Kita akan tetap ringan: hanya beberapa baris Python, sebuah pustaka bantu SVG yang populer, dan sedikit penjelasan. Pada akhir tutorial Anda akan memiliki `circle.svg` yang siap pakai di folder Anda, dan Anda akan mengerti mengapa setiap langkah penting—tanpa jalan pintas “lihat dokumen”.

## Apa yang Anda Butuhkan

- Python 3.8+ (versi terbaru apa saja)
- Paket `svgwrite` – instal dengan `pip install svgwrite`
- Editor teks atau IDE (VS Code, PyCharm, atau bahkan Notepad sudah cukup)
- Izin menulis ke direktori tempat Anda ingin menyimpan file

Itu saja. Tanpa dependensi berat, tanpa layanan eksternal.

## Langkah 1: Siapkan Dokumen SVG

Membuat dokumen SVG semudah menginstansiasi objek `Drawing` dari `svgwrite`. Anggap objek ini sebagai kanvas kosong tempat semua bentuk berada.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Mengapa ini penting:** Kelas `Drawing` menangani semua boilerplate XML untuk Anda—namespace, header, dan elemen akar `<svg>`. Dengan menentukan nama file di awal, kita sudah tahu ke mana file akan disimpan, sehingga langkah **save svg file** berikutnya menjadi sangat sederhana.

### Pro tip
Jika Anda berencana menghasilkan banyak file dalam sebuah loop, berikan setiap `Drawing` nama yang unik atau gunakan `io.BytesIO` untuk menyimpan semuanya di memori sampai siap menulis.

## Langkah 2: Tambahkan Lingkaran ke SVG

Setelah dokumen ada, mari **menambahkan lingkaran ke SVG**. Metode `add()` menerima objek bentuk apa pun; `Circle` cocok untuk titik merah sederhana di tengah.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Mengapa kita menggunakan variabel `center` dan `radius`:** Menuliskan angka secara langsung membuat kode lebih sulit dibaca dan dipelihara. Dengan memberi nama pada nilai‑nilai tersebut, maksudnya menjadi jelas—lingkaran ini berada tepat di tengah kanvas 200 × 200 dan cukup besar untuk terlihat.

### Kasus tepi – Latar belakang transparan
Jika Anda memerlukan latar belakang transparan (default untuk SVG), Anda dapat melewatkan pengaturan `fill` pada elemen akar. Untuk latar belakang putih, tambahkan:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Letakkan ini sebelum menambahkan lingkaran sehingga persegi panjang berada di bawahnya.

## Langkah 3: Simpan File SVG

Dengan bentuk sudah ditempatkan, aksi terakhir adalah **menyimpan file SVG**. Metode `save()` menulis XML ke disk, dan karena kita sudah memberi `Drawing` nama file, satu panggilan saja cukup.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Apa yang terjadi di balik layar?** `svgwrite` men-serialize pohon elemen menjadi string, menambahkan deklarasi XML, dan menulisnya dengan encoding UTF‑8. Jika direktori target tidak ada, Python akan mengeluarkan `FileNotFoundError`; pastikan path valid atau buat dengan `os.makedirs()`.

### Bonus: Mengekspor grafik sebagai SVG secara programatis

Jika Anda memerlukan konten SVG sebagai string—misalnya, untuk disisipkan dalam email HTML—Anda dapat memanggil `dwg.tostring()` alih‑alih `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip lengkap yang siap dijalankan:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Output yang diharapkan:** Setelah menjalankan skrip, Anda akan melihat file `circle.svg` di folder yang sama. Membukanya di browser atau editor vektor apa pun menampilkan lingkaran merah yang terpusat pada kotak putih—tepat seperti yang diprogram.

## Pertanyaan Umum & Gotchas

- **Bagaimana jika saya ingin bentuk lain?** Ganti `dwg.circle` dengan `dwg.rect`, `dwg.ellipse`, atau bahkan string `<path>` khusus. API konsisten di semua bentuk.
- **Bisakah saya menyematkan SVG langsung di HTML?** Tentu saja. File yang baru saja Anda buat dapat direferensikan dengan `<img src="circle.svg" alt="Red circle">` atau di‑inline dengan tag `<svg>`.
- **Mengapa tidak menulis XML mentah?** Anda bisa, tetapi pustaka seperti `svgwrite` menangani keanehan namespace dan membuat kode jauh lebih mudah dipelihara—terutama saat Anda mulai menambahkan gradien atau animasi.

## Kesimpulan

Sekarang Anda tahu cara **membuat dokumen SVG**, **menambahkan lingkaran ke SVG**, dan **menyimpan file SVG** sehingga Anda dapat **mengekspor grafik sebagai SVG** hanya dengan beberapa baris Python. Pola ini dapat diperluas: ganti lingkaran dengan bentuk vektor apa pun, lakukan loop atas data untuk menghasilkan diagram, atau proses batch aset untuk sistem desain.

Langkah selanjutnya? Coba tambahkan label teks, bereksperimen dengan gradien, atau menghasilkan galeri ikon lengkap dalam satu skrip. Jika Anda penasaran dengan fitur yang lebih maju, lihat dokumentasi `svgwrite` tentang grup (`<g>`), transformasi, dan dukungan animasi.

Selamat coding, semoga vektor Anda selalu tajam!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}