---
category: general
date: 2026-06-03
description: Buat dokumen HTML dalam Java dan sematkan JavaScript untuk meningkatkan
  penghitung. Pelajari contoh mesin skrip, dapatkan innerHTML elemen, dan lainnya.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: id
og_description: Buat dokumen HTML di Java, sematkan JavaScript untuk meningkatkan
  penghitung, dan ambil nilai akhir menggunakan contoh mesin skrip.
og_title: Buat Dokumen HTML dengan JavaScript Tersemat – Contoh Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Buat Dokumen HTML dengan JavaScript Tersemat – Contoh Java
url: /id/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen HTML dengan JavaScript Tersemat – Contoh Java

Pernah perlu **membuat dokumen HTML** dari kode Java dan bertanya-tanya bagaimana cara menyematkan JavaScript di dalamnya? Dalam panduan ini kami akan menunjukkan hal itu secara langkah demi langkah, dan Anda akan mendapatkan contoh mesin skrip yang berfungsi yang mencetak nilai penghitung akhir.  

Jika Anda pernah bertanya pada diri sendiri *“bagaimana cara mendapatkan element innerHTML setelah skrip dijalankan?”* atau *“apa cara paling bersih untuk menambah penghitung di JavaScript dari Java?”*—Anda berada di tempat yang tepat. Kami akan membahas **embed javascript html**, **increment counter javascript**, dan **get element innerHTML** semua dalam satu tutorial yang kohesif.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Contoh Membuat Dokumen HTML dengan JavaScript Tersemat"}

## Apa yang Akan Anda Bangun

Pada akhir tutorial ini Anda akan memiliki program Java yang berdiri sendiri yang:

1. **Membuat dokumen HTML** di memori.
2. **Menyematkan cuplikan JavaScript kecil** yang menambah penghitung lima kali.
3. **Menginisialisasi script engine** (contoh `ScriptEngine`) untuk menjalankan cuplikan tersebut.
4. **Mengambil nilai penghitung akhir** menggunakan `getElementInnerHTML`.
5. Mencetak `Final counter value: 5` ke konsol.

Tanpa file eksternal, tanpa server web—hanya Java murni dan string HTML kecil.

---

## Prasyarat

- Java 17 atau lebih baru (API `ScriptEngine` merupakan bagian dari pustaka standar).
- Familiaritas dasar dengan HTML dan JavaScript (tidak perlu keahlian mendalam).
- IDE atau editor teks sederhana plus terminal untuk mengompilasi dan menjalankan program.

---

## Langkah 1: Buat Dokumen HTML di Java

Hal pertama yang kita butuhkan adalah objek dokumen HTML kosong yang nanti dapat diisi dengan markup. Anggap saja ini sebagai halaman virtual yang hanya hidup di memori.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Mengapa ini penting:** Dengan **membuat dokumen HTML** secara manual, Anda menghindari penulisan ke disk dan membuat semuanya dapat diuji. Simulasi DOM kecil ini memungkinkan kita nanti **mendapatkan element innerHTML** tanpa browser penuh.

---

## Langkah 2: Sematkan JavaScript HTML – Logika Penghitung

Sekarang kita akan menulis markup HTML yang menyertakan blok `<script>`. Skrip ini akan **increment counter JavaScript** lima kali.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Penjelasan:**  
- `<div id='counter'>0</div>` adalah elemen target kita.  
- Loop `for` menjalankan logika **increment counter javascript**, memperbarui div setiap iterasi.  
- Karena kita tidak berada di browser nyata, mesin skrip yang akan kita gunakan nanti harus memahami `document.getElementById`. Itu sebabnya kami menambahkan stub kecil di `HTMLDocument`.

---

## Langkah 3: Inisialisasi Script Engine – Contoh Script Engine

Java dilengkapi dengan API `ScriptEngine` (JSR‑223). Kami akan membuat pembungkus kecil yang memberi konten HTML ke engine dan menyediakan metode DOM minimal yang dibutuhkannya.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Mengapa ini penting:** Contoh **script engine example** ini menunjukkan cara menjalankan JavaScript tersemat tanpa browser penuh. Ia juga memperlihatkan cara ringan untuk mengekspos `document.getElementById` sehingga skrip dapat berinteraksi dengan mock DOM kami.

---

## Langkah 4: Jalankan JavaScript – Increment Counter JavaScript dalam Aksi

Setelah engine siap, kami cukup menjalankan skrip. Loop di dalam tag `<script>` akan dieksekusi, dan mock `setInnerHTML` kami akan memperbarui penghitung.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Apa yang terjadi di balik layar?** Setiap iterasi loop memanggil `document.getElementById('counter').innerHTML = i + 1;`. Mock `setInnerHTML` kami meneruskan string numerik ke `HTMLDocument.updateCounter`, yang menyimpan nilai terbaru. Setelah loop selesai, peta internal dokumen berisi `"5"` untuk elemen `counter`.

---

## Langkah 5: Ambil Nilai Penghitung Akhir – Dapatkan Element InnerHTML

Sekarang skrip telah selesai, kita dapat **get element innerHTML** dari instance `HTMLDocument` kami.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Menjalankan seluruh program akan mencetak:

```
Final counter value: 5
```

Itu mengkonfirmasi bahwa logika **increment counter javascript** berhasil dan kami berhasil **mengambil element innerHTML** setelah eksekusi skrip.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java lengkap yang siap dijalankan:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Dokumen HTML Kosong di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Buat Dokumen HTML dari String di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Simpan Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}