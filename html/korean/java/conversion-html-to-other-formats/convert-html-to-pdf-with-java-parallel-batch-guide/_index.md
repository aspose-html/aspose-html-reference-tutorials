---
category: general
date: 2026-06-07
description: Java의 ExecutorService를 사용해 HTML을 PDF로 변환합니다. HTML 파일을 일괄 변환하는 방법, HTML
  문서를 PDF로 저장하는 방법, 그리고 ExecutorService를 정상적으로 종료하는 방법을 배워보세요.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: ko
og_description: Java의 ExecutorService를 사용하여 HTML을 PDF로 변환합니다. 배치 변환을 마스터하고 HTML 문서를
  PDF로 저장하며, ExecutorService를 정상적으로 종료합니다.
og_title: Java로 HTML을 PDF로 변환하기 – 병렬 배치 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Java로 HTML을 PDF로 변환 – 병렬 배치 가이드
url: /ko/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java로 HTML을 PDF로 변환 – 병렬 배치 가이드

Ever needed to **convert HTML to PDF** but felt stuck juggling dozens of files? You're not the only one—many devs hit that wall when building report generators or invoice exporters. The good news? With a few lines of Java and a smart thread pool, you can **batch convert HTML to PDF** in a snap, **save HTML document as PDF**, and even **shutdown ExecutorService gracefully** when the work’s done.

이 튜토리얼에서는 완전하고 바로 실행 가능한 예제를 단계별로 살펴봅니다. 고정 크기 스레드 풀이 병렬 변환에 왜 최적의 선택인지, 변환 코드는 어떻게 생겼는지, 그리고 Executor를 깔끔하게 종료하는 정확한 단계들을 확인할 수 있습니다. 끝까지 따라오면 프로젝트에 바로 넣을 수 있는 독립 실행형 프로그램을 얻게 됩니다—빠진 부분 없이, 애매한 “문서 참고” 링크 없이.

---

## 만들게 될 것

- 로컬 HTML 파일 목록을 읽는 Java 콘솔 앱.  
- 각 파일을 PDF 버전으로 만드는 워커 스레드에 전달.  
- 앱은 **ExecutorService**를 사용해 변환을 병렬로 실행.  
- 모든 작업이 큐에 들어가면 풀을 **shutdown gracefully**하여 스레드가 남지 않도록 보장.

**Prerequisites**  
- Java 17 (또는 최신 JDK).  
- **OpenHTMLtoPDF**, **iText**, 또는 **Flying Saucer**와 같이 HTML을 렌더링할 수 있는 PDF 라이브러리. 코드에서는 자리표시자 `HTMLDocument` 클래스를 참조합니다; 이를 라이브러리 API로 교체하세요.  
- Java 동시성에 대한 기본 지식 (특별한 사전 지식은 필요 없음).

![ExecutorService를 사용한 HTML 파일을 PDF로 배치 변환하는 다이어그램](batch-convert-diagram.png "ExecutorService를 사용한 병렬 HTML을 PDF로 변환")

*Alt text: 스레드 풀을 이용해 HTML을 PDF로 배치 처리하는 방법을 보여주는 다이어그램.*

## 병렬로 HTML을 PDF로 변환 (HTML을 PDF로 배치 변환)

수십 개—심지어 수천 개—의 HTML 파일을 다룰 때 메인 스레드에서 하나씩 변환하면 병목이 됩니다. 고정 크기 스레드 풀을 사용하면 JVM이 일정 수의 워커 스레드를 재사용해 CPU 사용량을 높게 유지하면서 시스템을 과부하시키지 않을 수 있습니다.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### 왜 이렇게 동작할까

- **Parallelism**: 각 `submit` 호출이 변환 작업을 워커 스레드에 넘겨주므로, 쿼드코어 머신에서는 네 개의 파일을 동시에 처리할 수 있습니다.  
- **Isolation**: `convertAndSave` 메서드에 **save HTML document as PDF**에 필요한 모든 로직이 들어 있어, 나중에 기반 라이브러리를 쉽게 교체할 수 있습니다.  
- **Graceful termination**: 먼저 `shutdown()`을 호출해 “더 이상 작업이 없으니 현재 작업을 마무리해 주세요”라고 풀에 알립니다. `awaitTermination` 루프가 스레드에게 마무리할 시간을 주고, 그래도 끝나지 않으면 `shutdownNow()`를 호출합니다. 이 패턴이 **shutdown ExecutorService gracefully**하는 권장 방법입니다.

---

## HTML 문서를 PDF로 저장 – 핵심 변환 로직

어떤 **convert HTML to PDF** 워크플로든 변환 라이브러리가 핵심입니다. 예제에서는 더미 `HTMLDocument`를 사용하지만, **OpenHTMLtoPDF**를 이용한 간단한 예시는 다음과 같습니다:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**무슨 일이 일어나고 있나요?**  
1. HTML 파일을 문자열로 읽어들입니다.  
2. `PdfRendererBuilder`가 마크업을 파싱하고 CSS를 적용한 뒤, 결과를 PDF 파일로 스트리밍합니다.  
3. `IOException`이 발생하면 `convertAndSave`로 전파되어 성공 또는 실패를 로그에 남깁니다.

iText의 `HtmlConverter.convertToPdf`나 Flying Saucer의 `ITextRenderer`로 이 코드를 교체해도 됩니다. 주변의 스레드 풀 코드는 그대로 유지되므로, **save HTML document as PDF**를 별도의 관심사로 강조한 이유가 여기 있습니다.

---

## ExecutorService를 정상적으로 종료 – 모범 사례

일반적인 실수는 작업을 제출한 직후 `shutdownNow()`를 호출하는 것입니다. 이렇게 하면 스레드가 즉시 중단되어 디스크에 반쯤 작성된 PDF 파일이 남을 수 있습니다. 우리가 사용한 패턴—`shutdown()` → `awaitTermination()` → 선택적 `shutdownNow()`—은 다음을 보장합니다:

- **No new tasks**가 모든 작업을 큐에 넣은 뒤에는 받아들여지지 않습니다.  
- **Running tasks**는 깔끔하게 마무리할 기회를 얻습니다.  
- **Blocked threads**는 합리적인 제한 시간(여기서는 60초)을 초과할 경우에만 중단됩니다.  

PDF가 매우 크거나 렌더링 엔진이 느릴 경우, 제한 시간을 늘리거나 `executor.invokeAll(tasks, timeout, unit)`을 사용해 더 엄격히 제어할 수 있습니다.

---

## 전체 작동 예제 (모든 조각을 합친 것)

아래는 `HtmlToPdfBatch.java` 파일 하나에 복사·붙여넣기 할 수 있는 전체 프로그램입니다. OpenHTMLtoPDF 의존성을 `pom.xml` 또는 Gradle 빌드에 추가하고 바로 실행하세요.



## 다음에 배울 내용은?

이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제들을 다루는 튜토리얼입니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}