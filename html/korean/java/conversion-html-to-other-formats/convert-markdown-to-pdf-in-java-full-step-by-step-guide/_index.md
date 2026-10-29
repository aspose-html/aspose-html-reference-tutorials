---
category: general
date: 2026-06-03
description: Java를 사용하여 마크다운을 PDF로 변환합니다. 간단한 라이브러리로 마크다운에서 PDF를 생성하는 방법을 배우고, 몇 분
  안에 마크다운 파일로 PDF를 만들 수 있습니다.
draft: false
keywords:
- convert markdown to pdf
- generate pdf from markdown
- create pdf from markdown file
- how to convert markdown to pdf
- convert markdown file to pdf
language: ko
og_description: 마크다운을 PDF로 빠르게 변환하세요. 이 가이드는 마크다운에서 PDF를 생성하는 방법, 마크다운 파일로부터 PDF를
  만드는 방법을 보여주며, 마크다운을 PDF로 변환하는 방법에 대해 답변합니다.
og_title: Java에서 Markdown을 PDF로 변환하기 – 완전한 프로그래밍 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Convert markdown to PDF using Java. Learn how to generate PDF from
    markdown with a simple library and create PDF from markdown file in minutes.
  headline: Convert Markdown to PDF in Java – Full Step‑by‑Step Guide
  type: TechArticle
tags:
- Java
- Markdown
- PDF
- Document Conversion
title: Java에서 Markdown을 PDF로 변환하기 – 전체 단계별 가이드
url: /ko/java/conversion-html-to-other-formats/convert-markdown-to-pdf-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Markdown을 PDF로 변환 – 전체 단계별 가이드

IDE를 떠나지 않고 **markdown을 pdf로 변환하는 방법**이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 README 파일, 블로그 초안, 혹은 기술 사양서를 깔끔한 PDF로 만들어 공유해야 하는데, 이를 프로그래밍 방식으로 처리하면 수작업 복사‑붙여넣기 시간을 크게 절약할 수 있습니다.

이 튜토리얼에서는 Maven 의존성 몇 개만으로 **markdown에서 PDF를 생성**하는 깔끔하고 프로덕션 수준의 솔루션을 단계별로 살펴봅니다. 마지막에는 몇 줄의 Java 코드만으로 **markdown 파일을 pdf로 만들** 수 있게 되고, 이미지, 커스텀 CSS, 대용량 문서 처리 방법도 확인할 수 있습니다.  

> **Pro tip:** 같은 접근법으로 markdown 파일을 다른 포맷(HTML, DOCX)으로 변환할 수도 있습니다 – 최종 렌더러만 교체하면 됩니다.

## 배울 내용

- 필수 라이브러리(`flexmark-java`와 `openhtmltopdf`) 설정하기
- 디스크에서 markdown 파일 읽어오기
- markdown을 HTML로 변환하기 (markdown과 PDF 사이의 다리)
- HTML을 PDF 렌더러에 전달하고 출력 파일 쓰기
- 상대 이미지 경로와 유니코드 문자 같은 일반적인 엣지 케이스 처리하기

## 사전 요구 사항

- JDK 17 이상 (코드에서 `var` 키워드를 사용하지만, 필요하면 11로 다운그레이드 가능)
- Maven 또는 Gradle 빌드 도구 (예시는 Maven)
- 변환하고 싶은 markdown 파일 – 데모에서는 `YOUR_DIRECTORY` 폴더에 위치한 `readme.md`를 사용합니다.

---

## Step 1: 변환 라이브러리 추가

먼저, 유지 관리가 잘 되는 두 라이브러리를 가져옵니다:

| 라이브러리 | 필요 이유 | Maven 좌표 |
|-----------|-----------|------------|
| **flexmark‑java** | Markdown을 파싱하고 HTML로 렌더링합니다. | `com.vladsch.flexmark:flexmark-all:0.64.8` |
| **openhtmltopdf‑core** | HTML을 받아 PDF를 생성합니다. | `org.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` |

`pom.xml`에 추가하세요:

```xml
<dependencies>
    <!-- Flexmark – Markdown → HTML -->
    <dependency>
        <groupId>com.vladsch.flexmark</groupId>
        <artifactId>flexmark-all</artifactId>
        <version>0.64.8</version>
    </dependency>

    <!-- OpenHTMLtoPDF – HTML → PDF -->
    <dependency>
        <groupId>org.openhtmltopdf</groupId>
        <artifactId>openhtmltopdf-pdfbox</artifactId>
        <version>1.0.10</version>
    </dependency>
</dependencies>
```

> **왜 이 두 개인가?** Flexmark는 표, 코드 블록, 각주 등 모든 Markdown 요소를 충실히 HTML로 변환해 줍니다. OpenHTMLtoPDF는 PDFBox 엔진을 사용해 HTML을 렌더링하므로 폰트와 이미지 처리가 기본 제공됩니다. 두 라이브러리를 함께 쓰면 **markdown 파일을 pdf로 변환**하는 작업을 최소한의 보일러플레이트 코드만으로 구현할 수 있습니다.

---

## Step 2: Markdown 소스 읽기

파일을 `String`으로 읽어옵니다. `java.nio.file.Files`를 사용하면 코드가 간결하고 유니코드도 자동으로 처리됩니다.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;
import java.io.IOException;

/**
 * Loads the markdown content from the given path.
 *
 * @param markdownPath absolute or relative path to the .md file
 * @return the file content as a UTF‑8 string
 * @throws IOException if the file cannot be read
 */
static String loadMarkdown(String markdownPath) throws IOException {
    Path path = Path.of(markdownPath);
    return Files.readString(path, StandardCharsets.UTF_8);
}
```

> **엣지 케이스:** markdown에 Windows 줄바꿈(`\r\n`)이 포함돼 있어도 `readString`이 이를 `\n`으로 정규화해 주므로 Flexmark가 정상적으로 동작합니다.

---

## Step 3: Markdown을 HTML로 변환

Flexmark가 무거운 작업을 담당합니다. 파서 커스터마이징도 가능하지만(예: GitHub‑flavored 테이블, 각주 활성화) 기본 설정만으로도 대부분의 문서에 충분합니다.

```java
import com.vladsch.flexmark.html.HtmlRenderer;
import com.vladsch.flexmark.parser.Parser;
import com.vladsch.flexmark.util.ast.Node;

/**
 * Turns raw markdown into HTML.
 *
 * @param markdown the markdown source
 * @return HTML string ready for PDF rendering
 */
static String markdownToHtml(String markdown) {
    Parser parser = Parser.builder().build();
    HtmlRenderer renderer = HtmlRenderer.builder().build();
    Node document = parser.parse(markdown);
    return renderer.render(document);
}
```

**HTML을 거치는 이유:** PDF 생성기는 레이아웃, CSS, 폰트를 원시 markdown보다 훨씬 잘 이해합니다. 먼저 HTML로 변환하면 커스텀 헤더, 페이지 번호, 워터마크 등 스타일을 완벽히 제어할 수 있습니다.

---

## Step 4: HTML을 PDF로 렌더링

OpenHTMLtoPDF는 HTML `String`을 받아 `OutputStream`에 PDF를 씁니다. 아래 예시는 기본 CSS 스타일시트를 추가하는 작은 래퍼이며(`style.css`를 원하는 파일로 교체 가능) 동작합니다.

```java
import org.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.OutputStream;
import java.io.FileOutputStream;

/**
 * Generates a PDF file from HTML.
 *
 * @param html   the HTML content produced by Flexmark
 * @param pdfPath path where the resulting PDF should be saved
 * @throws IOException if writing the PDF fails
 */
static void htmlToPdf(String html, String pdfPath) throws IOException {
    try (OutputStream os = new FileOutputStream(pdfPath)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.useFastMode();                     // speeds up rendering for large docs
        builder.withHtmlContent(html, null);       // base URI null → relative URLs resolved against working dir
        builder.toStream(os);
        // Optional: add a custom stylesheet
        // builder.withCssFile(new File("style.css"));
        builder.run();
    }
}
```

> **이미지 참고:** markdown에 상대 경로 이미지가 포함돼 있다면 작업 디렉터리에서 해당 파일에 접근할 수 있도록 하거나 `withHtmlContent(html, baseUri)`에 올바른 base URI를 지정해야 합니다.

---

## Step 5: 전체 흐름 – 원‑라인 컨버터 구현

이제 원본 스니펫과 동일한 3줄 변환 로직을 오류 처리와 로깅을 포함해 구현합니다.

```java
public class MarkdownPdfConverter {

    /**
     * Convert a markdown file directly to a PDF file.
     *
     * @param markdownPath path to the source .md file
     * @param pdfPath      desired output .pdf file
     */
    public static void convert(String markdownPath, String pdfPath) {
        try {
            // Step 1: Load markdown
            String markdown = loadMarkdown(markdownPath);

            // Step 2: Transform to HTML
            String html = markdownToHtml(markdown);

            // Step 3: Render PDF
            htmlToPdf(html, pdfPath);

            System.out.println("✅ Successfully created PDF at " + pdfPath);
        } catch (IOException e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps (loadMarkdown, markdownToHtml, htmlToPdf) -----
    // (Copy‑paste the static methods defined earlier here)
}
```

### 컨버터 실행하기

```java
public class Main {
    public static void main(String[] args) {
        // Step 1: Define the path to the source Markdown file
        String markdownPath = "YOUR_DIRECTORY/readme.md";

        // Step 2: Define the desired output PDF file path
        String pdfPath = "YOUR_DIRECTORY/readme.pdf";

        // Step 3: Convert the Markdown document directly to PDF
        MarkdownPdfConverter.convert(markdownPath, pdfPath);
    }
}
```

**콘솔에 기대되는 출력**

```
✅ Successfully created PDF at YOUR_DIRECTORY/readme.pdf
```

`readme.pdf`를 열어보세요 – 원본 markdown 구조를 그대로 반영한 깔끔한 문서가 보이며, 헤딩, 글머리표 리스트, 코드 블록 등이 모두 올바르게 렌더링됩니다.

---

## 흔히 발생하는 문제 처리

| 이슈 | 발생 원인 | 해결 방법 |
|------|-----------|-----------|
| **이미지 누락** | 상대 이미지 경로가 JVM 작업 디렉터리를 기준으로 해석됩니다. | markdown 폴더를 base URI로 전달: `builder.withHtmlContent(html, new File(markdownPath).getParentFile().toURI().toString());` |
| **Unicode 깨짐** | PDF 렌더러가 기본 폰트 세트가 제한적입니다. | `builder.useFont(new File("fonts/DejaVuSans.ttf"), "DejaVu Sans", 400, PdfRendererBuilder.FontStyle.NORMAL, true);` 로 Unicode 지원 폰트 삽입 |
| **대용량 파일 정지** | 큰 HTML을 렌더링하면 메모리 사용량이 급증합니다. | `builder.useFastMode()` 활성화(예시 참고)하거나 markdown을 섹션별로 나눠 별도 PDF를 생성 |
| **표 스타일링 오류** | Flexmark 기본 HTML에 표용 CSS가 없습니다. | 작은 CSS 조각 추가: `builder.withCssContent("table { width: 100%; border-collapse: collapse; } th, td { border: 1px solid #ddd; padding: 8px; }");` |

---

## 보너스: 간단한 헤더/푸터 추가

페이지 번호나 타이틀을 모든 페이지에 넣고 싶다면 약간의 CSS와 HTML `<header>`/`<footer>` 블록을 삽입하면 됩니다.



## 다음에 배워야 할 내용

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 설명과 완전한 코드 예제를 제공합니다. 이를 통해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용해 보세요.

- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}