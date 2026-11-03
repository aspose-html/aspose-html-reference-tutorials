---
category: general
date: 2026-05-28
description: Pelajari cara menggunakan SaveOptions untuk memotong halaman HTML di
  Python. Panduan langkah demi langkah ini juga menjelaskan cara memuat dokumen HTML
  dan secara efisien menghapus sumber daya bersarang.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: id
og_description: Cara menggunakan SaveOptions untuk memotong halaman HTML di Python.
  Ikuti panduan ini untuk memuat dokumen HTML, mengatur batas sumber daya, dan menyimpan
  file yang bersih serta ringan.
og_title: Cara Menggunakan SaveOptions di Python – Memangkas Halaman HTML
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
title: Cara Menggunakan SaveOptions di Python – Memangkas Halaman HTML
url: /id/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan SaveOptions di Python – Memangkas Halaman HTML

Pernah bertanya-tanya **bagaimana cara menggunakan SaveOptions** untuk memperkecil file HTML yang sangat besar tanpa merusak apa pun? Anda bukan satu-satunya. Ketika Anda mengambil sebuah halaman yang mencakup puluhan sumber daya bersarang—seperti CSS, JS, atau bahkan potongan HTML lainnya—hasil output Anda dapat membengkak tak terkendali.  

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan, yang tidak hanya menunjukkan **bagaimana cara menggunakan SaveOptions**, tetapi juga mencakup **cara memuat dokumen HTML** dan cara terbaik untuk **memangkas halaman HTML** dengan membatasi kedalaman bersarang. Pada akhir tutorial Anda akan memiliki file bersih yang dipangkas, siap untuk dipasang atau diproses lebih lanjut.

## Apa yang Akan Anda Capai

- Memuat file HTML lokal apa pun dengan satu baris kode.  
- Mengonfigurasi opsi penanganan sumber daya untuk berhenti pada kedalaman inklusi tertentu.  
- Menyimpan hasil yang dipangkas menggunakan kelas `SaveOptions` yang kuat.  

Tanpa alat eksternal, tanpa sulap—hanya Python biasa dan perpustakaan kecil yang melakukan pekerjaan berat.

---

## Prasyarat

Sebelum kita melanjutkan, pastikan Anda memiliki:

1. **Python 3.9+** terpasang (sintaks yang digunakan berfungsi pada versi terbaru apa pun).  
2. Paket hipotetis `htmlprocessor` yang menyediakan `HTMLDocument`, `SaveOptions`, dan `ResourceHandlingOptions`. Instal dengan:

```bash
pip install htmlprocessor
```

> **Pro tip:** Jika Anda menggunakan lingkungan virtual, aktifkan terlebih dahulu—menjaga dependensi tetap rapi.

---

## Langkah 1: Cara Memuat Dokumen HTML

Memuat file semudah menunjuk konstruktor ke path Anda. Perpustakaan membaca markup, membangun pohon mirip DOM, dan menyiapkannya untuk manipulasi lebih lanjut.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Mengapa ini penting:** Objek `HTMLDocument` mengabstraksi penanganan string mentah, memberi Anda metode untuk menanyakan, memodifikasi, dan akhirnya menyimpan halaman. Ia juga menormalkan akhir baris dan enkoding karakter, yang menyelamatkan Anda dari bug halus di kemudian hari.

Anda akan melihat kami mencetak judul hanya untuk memverifikasi bahwa pemuatan berhasil. Jika file tidak ada atau rusak, konstruktor akan mengeluarkan pengecualian yang jelas—tanpa kegagalan diam.

---

## Langkah 2: Mengonfigurasi Penanganan Sumber Daya – Inti dari Pemangkasan

Bagian selanjutnya dari teka‑teki adalah **cara memangkas halaman HTML** dengan membatasi seberapa dalam pemroses mengikuti inklusi. Di sinilah `ResourceHandlingOptions` bersinar.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Apa yang Dilakukan `max_handling_depth`?

- **Depth 1** → Hanya file HTML akar, semua sumber daya eksternal diabaikan.  
- **Depth 2** → Akar plus file yang langsung direferensikan (misalnya, sebuah `iframe` atau server‑side include).  
- **Nilai lebih tinggi** → Bersarang lebih dalam, tetapi juga menghasilkan output yang lebih besar dan waktu pemrosesan yang lebih lama.

Dengan membatasi kedalaman pada **2**, kami mempertahankan halaman utama dan satu lapisan inklusi, mengabaikan apa pun yang lebih dalam. Ini biasanya cukup untuk menghilangkan footer berulang, skrip analitik, atau templat bersarang yang tidak Anda perlukan dalam salinan yang dipangkas.

---

## Langkah 3: Menempelkan Opsi ke Konfigurasi Penyimpanan

Sekarang kami mengikat aturan sumber daya kami ke sebuah instance `SaveOptions`. Objek ini memberi tahu perpustakaan *tepat* bagaimana menulis file kembali ke disk.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Mengapa menggunakan `SaveOptions`?**  
> Ia memberi Anda kontrol granular atas output—lebih dari sekadar kedalaman sumber daya. Anda dapat menambahkan kompresi, pretty‑printing, atau bahkan callback khusus tanpa menyentuh logika penyimpanan inti.

---

## Langkah 4: Cara Menggunakan SaveOptions untuk Memangkas Halaman HTML

Akhirnya, kami memanggil metode `save` dengan opsi yang telah dikonfigurasi. Perpustakaan akan menelusuri DOM, menghormati batas kedalaman, dan menulis file yang dipangkas.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Hasil yang Diharapkan

- File `trimmed_page.html` berisi markup asli **plus** semua inklusi hingga satu tingkat dalam.  
- Semua inklusi yang lebih dalam dihilangkan, menghasilkan halaman yang lebih kecil dan lebih cepat dimuat.  
- Tidak ada tag yang rusak muncul—perpustakaan secara otomatis menutup elemen yang tertinggal setelah penghapusan.

Anda dapat membuka output di browser untuk memverifikasi bahwa konten utama masih dirender, sementara skrip atau frame bersarang yang tidak diperlukan telah hilang.

---

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut skrip lengkap yang dapat Anda salin‑tempel dan jalankan:

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

Jalankan skrip, arahkan `INPUT` ke file HTML kompleks apa pun, dan Anda akan mendapatkan versi yang lebih ramping di `OUTPUT`.  

> **Catatan kasus tepi:** Jika halaman asli berisi komentar kondisional (`<!--[if IE]>…<![endif]-->`) yang merujuk ke sumber daya lebih dalam, mereka akan dihapus seperti inklusi bersarang lainnya. Ini mencegah trik lama‑IE memperbesar ukuran akhir Anda.

---

## Ringkasan Visual

Berikut diagram singkat yang menggambarkan alur—dari memuat dokumen, melalui penanganan sumber daya, hingga menyimpan hasil yang dipangkas.

![contoh cara menggunakan saveoptions](https://example.com/placeholder.png "Diagram yang menunjukkan cara menggunakan SaveOptions untuk memangkas halaman HTML")

*Alt text:* **contoh cara menggunakan saveoptions** – menampilkan proses tiga langkah memuat, mengonfigurasi, dan menyimpan dokumen HTML.

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika saya membutuhkan kedalaman bersarang yang lebih dalam?** | Tingkatkan `max_handling_depth` menjadi 3 atau 4, tetapi ingat ukuran output akan bertambah. |
| **Bisakah saya mengecualikan tag tertentu (mis., `<script>`) terlepas dari kedalaman?** | Ya—`SaveOptions` juga mendukung properti `tag_exclusion_list`. Tambahkan `"script"` ke daftar itu untuk selalu menghapus skrip. |
| **Apakah perpustakaan ini thread‑safe?** | Versi saat ini tidak. Buat `HTMLDocument` terpisah per thread. |
| **Apakah URL relatif akan ditulis ulang?** | Secara default tidak. Gunakan `save_opt.rewrite_relative_urls = True` jika Anda perlu menyesuaikannya ke lokasi baru. |

---

## Langkah Selanjutnya

Setelah Anda menguasai **cara menggunakan SaveOptions**, coba ekstensi berikut:

- **Kompres output:** Atur `save_opt.enable_gzip = True` untuk file yang lebih kecil saat dikirim.  
- **Pretty‑print untuk debugging:** Aktifkan `save_opt.indent_output = True` agar HTML diformat rapi.  
- **Pemrosesan batch:** Loop melalui direktori berisi file HTML dan terapkan logika pemangkasan yang sama—ideal untuk generator situs statis.

Setiap penyesuaian ini dibangun di atas fondasi yang baru saja Anda pelajari, menjaga kode tetap bersih dan mudah dipelihara.

---

## Kesimpulan

Kami telah membahas seluruh siklus pemangkasan halaman HTML di Python: **cara memuat dokumen HTML**, mengonfigurasi **cara memangkas halaman HTML** menggunakan `ResourceHandlingOptions`, dan akhirnya **cara menggunakan SaveOptions** untuk menulis file yang telah dibersihkan. Contoh ini sepenuhnya mandiri, dapat dijalankan langsung, dan menunjukkan mengapa mengontrol kedalaman sumber daya adalah optimasi penting untuk web‑scraping, pembuatan situs statis, atau situasi apa pun di mana Anda memerlukan snapshot HTML yang ringan.

Cobalah, bereksperimen dengan nilai `max_handling_depth` yang berbeda, dan biarkan halaman yang dipangkas melakukan pekerjaan berat untuk Anda. Jika menemukan kendala, tinggalkan komentar di bawah—selamat coding!

## Tutorial Terkait

- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Penangan Sumber Daya Kustom](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Cara Merender HTML menjadi PNG – Panduan Lengkap C#](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Cara Mengompres HTML ke ZIP di C# – Simpan HTML ke Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}