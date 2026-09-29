---
category: general
date: 2026-09-29
description: 클래스로 요소를 선택하고, 파일에서 HTML을 읽으며, Java에서 외부 링크를 찾는 방법을 배웁니다. 이 단계별 가이드는
  NodeList를 효율적으로 반복하는 방법을 다룹니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: ko
lastmod: 2026-09-29
og_description: Java에서 클래스로 요소를 선택하고, 파일에서 HTML을 읽으며, querySelectorAll을 사용해 외부 링크를
  찾습니다. NodeList를 순회하는 전체 예제를 따라보세요.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Java에서 클래스별 요소 선택 – querySelectorAll을 이용한 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Java에서 querySelectorAll을 사용하여 클래스별 요소 선택하는 방법
url: /ko/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 querySelectorAll을 사용하여 클래스별 요소 선택하기

Java에서 HTML 파일을 처리하면서 **클래스별 요소를 선택**해야 한다면, 이 가이드는 정확한 방법을 보여줍니다. 파일에서 HTML을 읽고, `querySelectorAll`을 사용해 외부 링크를 찾으며, 결과 `NodeList`를 안전하게 반복하는 방법을 배울 수 있습니다.

Java에서 HTML을 다루는 것은 종종 무겁게 느껴지지만, 최신 라이브러리들은 간결한 CSS‑selector 기반 API를 제공합니다. 아래 예시는 **jsoup**(버전 1.17.2)를 사용합니다. 이 라이브러리는 `querySelectorAll`‑스타일 선택자를 구현하고 `NodeList`처럼 동작하는 `Elements` 컬렉션을 반환합니다. 필요에 따라 동일한 로직을 다른 DOM 구현에도 적용할 수 있습니다.

## 사전 요구 사항

* JDK 17 이상이 설치되어 있어야 합니다.
* 의존성 관리를 위한 Maven 또는 Gradle.
* Java 스트림 및 DOM 모델에 대한 기본적인 이해.

프로젝트에 jsoup을 추가하세요:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## 단계 1: 파일에서 HTML 읽기

첫 번째 작업은 디스크에서 HTML 문서를 로드하는 것입니다. `Jsoup.parse(Path, Charset)`는 파일을 읽고 쿼리할 수 있는 DOM 트리를 구축합니다.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*왜 중요한가*: 파일을 한 번만 로드하면 이후 요소를 반복할 때 반복적인 I/O를 피할 수 있습니다. `Document` 객체는 전체 DOM을 보유하므로 빠른 선택자 쿼리가 가능합니다.

## 단계 2: `querySelectorAll`을 사용해 클래스별 요소 선택

문서가 메모리에 로드되었으므로 CSS 선택자를 사용해 **클래스별 요소를 선택**할 수 있습니다. 선택자 `"a.external"`은 `external` 클래스를 가진 `<a>` 태그와 일치합니다—즉, **외부 링크를 찾는** 데 정확히 필요합니다.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*왜 중요한가*: 클래스 선택자는 표현력이 뛰어나면서도 성능이 좋습니다. 라이브러리는 선택자를 최적화된 순회로 변환하므로 모든 노드에 대해 수동 루프를 작성할 필요가 없습니다.

## 단계 3: Java에서 NodeList (Elements) 반복

`Elements`는 `Iterable<Element>`를 구현하므로 표준 `for‑each` 루프를 사용해 **NodeList Java** 객체를 **반복**할 수 있습니다. 아래 루프는 각 링크의 `href` 속성을 출력합니다.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*왜 중요한가*: 직접 반복하면 코드가 가독성이 높아지고, 단순 출력만 필요할 때 컬렉션을 스트림으로 변환하는 오버헤드를 피할 수 있습니다.

## 전체 작동 예제

세 단계를 결합하면 명령줄에서 실행할 수 있는 독립적인 프로그램이 완성됩니다.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### 예상 출력

`input.html`에 다음과 같은 내용이 있다고 가정하면:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

프로그램을 실행하면 다음과 같이 출력됩니다:

```
External link: https://example.com
External link: https://openai.com
```

## 전문가 팁 및 흔히 겪는 함정

* **인코딩 중요** – 파일은 항상 UTF‑8(또는 소스와 일치하는 문자셋)으로 읽어야 합니다. 잘못된 인코딩은 속성 값의 문자를 손상시킬 수 있습니다.
* **다중 클래스** – 요소에 여러 클래스가 있는 경우(예: `class="btn external"`), 선택자 `"a.external"`은 여전히 일치합니다. CSS 클래스 선택자는 토큰이 존재하는지를 확인하기 때문이며, 정확한 문자열을 요구하지 않습니다.
* **성능 팁** – `href` 속성만 필요하다면 `doc.select("a.external[href]").eachAttr("href")`와 같이 직접 요청할 수 있습니다. 이렇게 하면 각 매치에 대해 전체 `Element` 객체를 생성하는 것을 피할 수 있습니다.
* **null 안전성** – `link.attr("href")`는 속성이 없을 경우 빈 문자열을 반환하므로, 출력 전에 null 검사를 할 필요가 없습니다.

## 자주 묻는 질문

**Q: `<html>` 루트가 없는 HTML 조각에서도 작동하나요?**  
A: 예. `Jsoup.parse`는 입력을 조각으로 간주하고 누락된 루트 요소를 자동으로 추가하여 선택자가 조각의 body에서도 동작하도록 합니다.

**Q: jsoup 없이 `querySelectorAll`을 사용할 수 있나요?**  
A: 표준 Java DOM API(`org.w3c.dom`)에는 `querySelectorAll`이 포함되어 있지 않습니다. **HTMLUnit**이나 **jodd-lagarto**와 같은 라이브러리가 유사한 메서드를 제공합니다. 여기서 보여준 패턴—로드, CSS로 선택, 반복—은 동일합니다.

**Q: 링크를 단순히 출력하는 대신 수정해야 한다면 어떻게 하나요?**  
A: 각 `Element`를 얻은 후 `link.attr("href", "newUrl")`를 호출하고, `Files.writeString`을 사용해 문서를 디스크에 다시 쓸 수 있습니다.

## 결론

이제 **클래스별 요소를 선택**하고, **파일에서 HTML을 읽으며**, **외부 링크를 찾고**, `querySelectorAll`‑스타일 선택자를 사용해 **Java에서 NodeList를 반복**하는 방법을 알게 되었습니다. 전체 예제는 깔끔하고 프로덕션에 적합한 워크플로우를 보여주며, 이를 더 큰 스크래핑이나 변환 파이프라인에 삽입할 수 있습니다.

다음으로 **HTMLUnit으로 동적 콘텐츠 파싱**, **수정된 HTML을 디스크에 다시 쓰기**, 혹은 **Java 스트림을 사용해 링크 URL을 리스트로 수집**과 같은 관련 주제를 살펴보세요. 이들 각각은 여기서 시연한 클래스 기반 선택 핵심 기술을 기반으로 합니다. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Java에서 HTML 쿼리하기 – 요소 선택, 속성으로 필터링 및 텍스트 가져오기](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList Java 반복 – HTML 읽기 및 이미지 src 가져오기](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Aspose.HTML for Java에서 파일로부터 HTML 문서 로드하기](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}