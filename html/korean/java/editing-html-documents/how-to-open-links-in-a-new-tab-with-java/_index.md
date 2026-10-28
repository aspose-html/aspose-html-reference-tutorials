---
category: general
date: 2026-10-28
description: Java에서 HTML을 파싱하고 외부 링크를 찾아 `target="_blank"`을 추가하여 새 탭에서 링크를 여는 방법을
  배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: ko
lastmod: 2026-10-28
og_description: 'Java를 사용해 링크를 새 탭에서 열기: HTML을 파싱하고 외부 링크를 찾아 target="_blank"을 추가한
  뒤 수정된 HTML을 저장합니다.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Java로 새 탭에서 링크 열기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Java로 새 탭에서 링크 열기
url: /ko/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java로 새 탭에서 링크 열기

정적 HTML 파일에서 **링크를 새 탭에서 열어야** 할 때, 이 가이드는 정확한 방법을 보여줍니다. **Java에서 HTML 파싱**, **외부 링크 찾기**, **target="_blank" 추가**, **수정된 HTML 저장**을 IDE를 떠나지 않고 배울 수 있습니다.

외부 링크를 새 브라우저 탭에서 열면 사용자 경험이 향상되고 방문자를 원래 페이지에 머무르게 할 수 있습니다. 아래 솔루션은 모든 HTML 문서에서 동작하며, 인기 있는 jsoup 라이브러리만 필요하고 Java 8 이상에서 실행됩니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* JDK 8 이상 설치  
* **jsoup** 의존성을 가져올 빌드 도구 (Maven 또는 Gradle)  
* `external` 클래스를 가진 앵커 태그가 포함된 HTML 파일

웹 서버나 추가 프레임워크가 필요하지 않습니다—jsoup가 로컬에서 모든 작업을 처리합니다.

## Step 1: 프로젝트에 jsoup 설정하기

jsoup을 의존성으로 추가합니다. Maven을 사용한다면 `pom.xml`에 다음을 넣으세요:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Gradle을 사용한다면 `build.gradle`에 다음 라인을 추가하세요:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

위 좌표는 2026년 10월 현재 최신 안정 버전을 가져옵니다. 동기화 후 Java 소스 파일에서 `org.jsoup` 클래스를 임포트할 수 있습니다.

## Step 2: HTML 문서 파싱하기

파일을 파싱하는 것이 **새 탭에서 링크 열기**의 첫 단계입니다. `Jsoup.parse` 메서드는 파일을 가변적인 DOM‑유사 구조로 읽어들입니다.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*왜 중요한가*: `Document`는 CSS‑스타일 선택자를 제공하므로 필요한 요소를 손쉽게 찾을 수 있습니다.

## Step 3: 외부 링크 찾기

이제 `external` 클래스를 가진 모든 `<a>` 요소를 찾아보세요. 이는 **외부 링크 찾기** 요구 사항에 부합합니다.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements`는 일치하는 노드들의 컬렉션입니다. 선택자가 빈 집합을 반환한다면 HTML에 해당 클래스가 없거나 다른 명명 규칙을 사용하고 있는 것이므로 선택자를 조정하세요.

## Step 4: 각 링크에 `target="_blank"` 추가하기

**외부 링크 찾기**에서 반환된 각 노드에 대해 `target` 속성을 `_blank`로 설정합니다. 이는 **target blank 추가** 단계를 만족시키며 브라우저가 새 탭에서 링크를 열도록 합니다.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` 메서드는 기존 `target` 값을 덮어써서 모든 외부 앵커에 일관된 동작을 보장합니다.

## Step 5: 수정된 HTML 저장하기

DOM을 업데이트한 후 변경 내용을 파일에 다시 씁니다. 이렇게 하면 튜토리얼의 **수정된 HTML 저장** 부분이 완료됩니다.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()`은 전체 문서를 직렬화하여 jsoup이 원래 파싱한 들여쓰기와 포맷을 유지합니다.

## 전체 작업 예제

모든 단계를 합치면 복사·붙여넣기·실행이 가능한 독립 프로그램이 완성됩니다.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### 예상 출력

`sample.html` 파일 내용이 다음과 같다고 가정합니다:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

프로그램을 실행하면 `updated.html` 파일은 다음과 같이 됩니다:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

외부 링크에만 `target="_blank"` 속성이 추가되어 브라우저가 이제 새 탭에서 열게 됩니다.

## Pro 팁 및 흔히 발생하는 실수

* **Pro 팁:** CSS 클래스가 없더라도 `http://` 또는 `https://` 로 시작하는 링크를 외부 링크로 처리하려면 선택자를 확장하세요: `doc.select("a[href^=http]")`.
* **Edge case:** 일부 페이지는 이미 `target="_self"` 를 지정할 수 있습니다; `attr` 호출이 이를 덮어써 일관된 동작을 보장합니다.
* **Performance:** 매우 큰 HTML 파일의 경우 메모리 사용량을 줄이기 위해 스트리밍 파싱(`Jsoup.parse(File, String, String, Parser.htmlParser())`)을 고려하세요.
* **Testing:** `updated.html` 을 브라우저에서 열고 개발자 도구로 링크를 검사해 `target` 속성이 있는지 확인하세요.

## 결론

이제 Java를 사용해 **새 탭에서 링크 열기**를 구현하는 완전하고 실행 가능한 솔루션을 갖추었습니다. 튜토리얼에서는 **Java에서 HTML 파싱**, **외부 링크 찾기**, **target blank 추가**, **수정된 HTML 저장**을 가벼운 jsoup 라이브러리와 함께 다루었습니다.

다음 단계로 할 수 있는 일:

* `rel="external"` 등 다른 링크 패턴을 처리하도록 선택자를 확장하기.  
* 프로젝트 내 모든 HTML 파일을 처리하는 빌드 단계와 이 로직을 결합하기.  
* 코드를 더 큰 콘텐츠 관리 파이프라인에 통합하기.

다양한 선택자나 출력 포맷을 실험해 보고, 결과를 커뮤니티와 공유하세요!


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}