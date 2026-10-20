---
category: general
date: 2026-04-23
description: Cara menggunakan querySelectorAll di Java untuk menyaring elemen berdasarkan
  kelas, membaca nilai atribut, dan mengiterasi NodeList untuk mengekstrak data produk.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: id
og_description: Cara menggunakan querySelectorAll di Java untuk memfilter elemen berdasarkan
  kelas, membaca nilai atribut, dan mengiterasi NodeList untuk mengekstrak data produk.
og_title: Cara Menggunakan querySelectorAll di Java – Memfilter Berdasarkan Kelas
tags:
- Java
- HTML parsing
- DOM manipulation
title: Cara Menggunakan querySelectorAll di Java – Memfilter Berdasarkan Kelas
url: /id/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan querySelectorAll di Java – Filter berdasarkan Kelas

Cara menggunakan querySelectorAll di Java adalah kunci ketika Anda perlu mengambil elemen tertentu dari dokumen HTML. Dalam tutorial ini kami akan memfilter elemen berdasarkan kelas, membaca nilai atribut, dan mengiterasi NodeList untuk mengambil harga produk dari halaman katalog.  

Pernahkah Anda menatap file HTML yang sangat besar, bertanya-tanya bagaimana cara mengambil hanya kartu “on‑sale” tanpa menulis parser khusus? Itulah masalah yang akan kami selesaikan di sini—tanpa pustaka tambahan selain Aspose.HTML, dan hanya beberapa langkah sederhana.

Anda akan mendapatkan program lengkap yang dapat dijalankan dan dapat:

* **Selects elements** using a CSS selector (`select elements css selector`),
* **Filters by class** (`filter elements by class`),
* **Reads a custom attribute** (`how to read attribute`),
* **Iterates the resulting NodeList** (`iterate nodelist java`).

Tidak diperlukan pengalaman sebelumnya dengan Aspose.HTML—hanya setup Java dasar dan file HTML untuk diuji.

![contoh cara menggunakan querySelectorAll di Java](https://example.com/images/queryselectorall-java.png "contoh cara menggunakan querySelectorAll di Java")

---

## Apa yang Anda Butuhkan

| Persyaratan | Mengapa penting |
|-------------|----------------|
| **Java 17+** | Fitur bahasa modern dan penanganan modul yang lebih baik. |
| **Aspose.HTML for Java** (latest version) | Menyediakan kelas `Document` dan mesin CSS‑selector. |
| **catalog.html** (sample HTML) | Sumber yang akan kami query. |
| **IDE or plain `javac`** | Untuk mengompilasi dan menjalankan demo. |

Jika Anda belum menambahkan Aspose.HTML ke proyek Anda, letakkan JAR ke folder `libs` Anda dan tambahkan ke classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Langkah 1 – Muat Dokumen HTML

Sebelum Anda dapat melakukan query apa pun, Anda memerlukan objek `Document` yang mewakili file HTML. Anggaplah seperti memuat spreadsheet sebelum Anda dapat membaca sel apa pun.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Mengapa ini penting:** Kelas `Document` mengurai markup menjadi pohon DOM, memungkinkan mesin CSS‑selector bekerja. Melewatkan langkah ini akan meninggalkan Anda dengan string biasa dan tidak ada cara untuk menggunakan `querySelectorAll`.

---

## Langkah 2 – Pilih Elemen dengan CSS Selector

Sekarang masuk ke inti masalah: **cara menggunakan querySelectorAll**. Metode ini menerima selector CSS yang valid apa pun, sehingga Anda dapat menjadi sangat tepat—atau sangat luas—sesuai kebutuhan. Untuk skenario kami, kami menginginkan kartu produk yang:

* memiliki kelas `product-card`,
* juga ditandai dengan kelas `sale`,
* dan memiliki atribut `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Penjelasan:**  
> * `.product-card.sale` → memfilter elemen yang mengandung **kedua** kelas.  
> * `[data-price]` → memastikan atribut ada, secara efektif **memfilter elemen berdasarkan kelas** **dan** atribut dalam satu panggilan.  
> * Hasilnya adalah `NodeList`, yang merupakan koleksi berurutan yang dapat Anda iterasi.  

Jika Anda pernah perlu **select elements css selector** untuk pola yang berbeda, cukup ubah string—tidak perlu menulis ulang kode.

---

## Langkah 3 – Iterasi NodeList di Java

`NodeList` berperilaku mirip array, tetapi tidak mengimplementasikan `Iterable`. Itulah mengapa kami menggunakan loop `for` klasik—sempurna untuk skenario **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Mengapa menggunakan loop `for`?**  
> Loop ini memberi Anda akses langsung ke indeks, yang berguna untuk pencatatan atau percabangan kondisi. Jika Anda lebih suka loop `while`, logikanya tetap sama—hanya ubah konstruksi loopnya.

---

## Langkah 4 – Baca Atribut `data-price`

Sekarang kami akhirnya menjawab **cara membaca attribute** nilai dari sebuah elemen. Dalam API DOM, `getAttribute` mengembalikan string mentah, persis seperti yang muncul dalam markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tip:** Jika atribut mungkin tidak ada, `getAttribute` mengembalikan `null`. Anda dapat melindungi diri dengan pemeriksaan sederhana:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Langkah 5 – Output Hasil

Terakhir, kami mencetak setiap harga ke konsol. Ini mencerminkan skenario dunia nyata di mana Anda mungkin akan mengirim nilai ke basis data atau payload API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Output Konsol yang Diharapkan

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Jika selector tidak menemukan node yang cocok, loop tidak pernah dijalankan—tidak ada pengecualian yang dilempar. Ini merupakan jaring pengaman yang bagus untuk **edge cases** di mana katalog mungkin kosong.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut file lengkap yang dapat Anda salin‑tempel ke `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Simpan file, kompilasi, dan jalankan—saksikan harga mengalir keluar. 🎉

---

## Pertanyaan Umum & Tips Pro

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika saya perlu memilih berdasarkan nama tag juga?* | Cukup tambahkan tag di depan: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Bisakah saya menggabungkan beberapa filter atribut?* | Tentu saja. Contoh: `[data-price][data-stock]` akan mempertahankan hanya elemen yang memiliki **kedua** atribut. |
| *Apakah `querySelectorAll` sensitif huruf besar/kecil?* | Ya—CSS selector memperlakukan nama kelas dan atribut sebagai sensitif huruf besar/kecil dalam HTML5. |
| *Bagaimana cara menangani file HTML yang sangat besar?* | Aspose.HTML melakukan streaming dokumen, tetapi Anda juga dapat membatasi selector ke subtree (`someElement.querySelectorAll(...)`). |
| *Apa | 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}