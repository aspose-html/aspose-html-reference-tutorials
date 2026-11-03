---
category: general
date: 2026-05-28
description: Java에서 고정 스레드 풀을 사용한 Executor 활용 방법, HTML에서 텍스트 추출 및 처리 속도 향상 – 완전한 Java
  스레드 풀 예제.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: ko
og_description: Java에서 고정 스레드 풀을 사용해 Executor를 활용하는 방법. HTML 파일에서 텍스트를 효율적으로 추출하는
  완전한 Java 스레드 풀 예제를 배워보세요.
og_title: Java에서 Executor 사용 방법 – 고정 스레드 풀 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Java에서 Executor 사용 방법 – 고정 스레드 풀 가이드
url: /ko/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Executor 사용 방법 – 고정 스레드 풀 가이드

많은 작업을 한 번에 실행하면서 메모리를 초과하지 않게 **executor를 어떻게 사용하는지** 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 애플리케이션에서는 HTML 파일이 들어 있는 폴더를 크롤링하고, 본문 텍스트를 추출하며, 이를 빠르게 처리해야 하는 경우가 많습니다—바로 이 튜토리얼이 해결하는 시나리오입니다.

우리는 **fixed thread pool java** 구현을 단계별로 살펴볼 것입니다. 이 구현은 HTML에서 텍스트를 추출하고, 각 파일의 문자 수를 출력하며, 깔끔하게 종료합니다. 최종적으로 어떤 프로젝트에든 삽입할 수 있는 **java thread pool example**을 제공하고, 풀 크기 조정 및 엣지 케이스 처리에 대한 몇 가지 팁도 함께 제공합니다.

> **필요한 것**  
> * Java 17 (또는 최신 JDK)  
> * 작은 HTML 파싱 라이브러리 – 여기서는 검증된 *jsoup*을 사용합니다(설정 필요 없음).  
> * 원하는 디렉터리에 있는 몇 개의 샘플 *.html* 파일.

---

## 고정 스레드 풀로 Executor 사용하기

동시성 작업이 많은 Java 프로그램의 핵심은 `ExecutorService`입니다. **fixed thread pool**을 생성하면 JVM에 정확히 N개의 워커 스레드를 유지하도록 지시하게 되며, 이는 스레드 생성 오버헤드를 방지하고 자원 사용을 제한합니다.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*왜 중요한가:*  
HTML 파일마다 새로운 `Thread`를 시작한다면, OS는 보통 노트북에서 수십 개의 스레드를 스케줄링해야 하며, 그 결과 컨텍스트 스위치가 과도하게 발생합니다. 고정 풀은 동일한 네 개의 스레드를 재사용하므로 CPU 사용량을 예측 가능하게 합니다.

---

## 처리할 HTML 파일 정의 – Fixed Thread Pool Java

다음으로 풀에 전달할 파일 목록을 정의합니다. 실제 앱에서는 디렉터리 트리를 순회할 것이지만, 여기서는 간단히 처리합니다.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*팁:* `List.of`는 불변 리스트를 반환하므로 추가 동기화 없이 스레드 간에 안전하게 공유할 수 있습니다.

---

## 각 HTML 파일에 대해 별도 작업 제출하기

이제 각 경로를 executor에 전달합니다. 제출하는 람다식은 네 개의 워커 스레드 중 하나에서 **병렬**로 실행됩니다.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**왜 로직을 메서드** (`extractBodyText`) 로 감싸는지 다음 섹션에서 명확해집니다—람다식을 깔끔하게 유지하고 추출 코드를 다른 곳에서도 재사용할 수 있게 합니다.

---

## HTML에서 텍스트 추출 – 핵심 로직

다음은 Jsoup을 사용해 실제로 **html에서 텍스트를 추출**하는 재사용 가능한 헬퍼입니다. 파일을 열고, DOM을 파싱한 뒤, 순수 본문 텍스트를 반환합니다.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*왜 Jsoup인가?* 가볍고, 잘못된 마크업을 우아하게 처리하며, 전체 브라우저 엔진이 필요 없습니다. 메서드는 `IOException`을 throws 하므로 호출자가 로그를 남기거나 복구 방식을 결정할 수 있습니다—단일 파일 오류가 전체 executor를 종료시키지 않도록 하는 스레드 풀 시나리오에 적합합니다.

---

## Executor를 우아하게 종료하기 – Fixed Thread Pool 생성

모든 작업을 제출한 후, 풀에 새로운 작업을 받지 않도록 하고 이미 대기 중인 작업을 완료하도록 알려야 합니다.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*설명:* `shutdown()`은 새로운 제출을 방지하고, `awaitTermination`은 모든 파싱 작업이 끝날 때까지(또는 타임아웃이 만료될 때까지) 차단합니다. 무언가가 멈추면 `shutdownNow()`가 실행 중인 작업을 취소하려 시도합니다. 이 패턴은 **fixed thread pool**을 안전하게 **생성**하는 권장 방법입니다.

---

## 전체 실행 가능한 예제

모든 내용을 합쳐서, 컴파일하고 실행할 수 있는 단일 파일을 제공합니다. 필요한 import와 `main` 메서드, 위에서 설명한 헬퍼가 포함되어 있습니다.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**예상 출력** (각 파일에 약 1 200자의 본문 텍스트가 들어 있다고 가정할 때):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

파일이 없거나 형식이 잘못된 경우 `stderr`에 스택 트레이스가 출력되지만, 다른 작업은 영향을 받지 않고 계속 실행됩니다—바로 이것이 정상적인 **java thread pool example**이 해야 할 일입니다.

---

## 일반적인 질문 및 엣지 케이스

| Question | Answer |
|----------|--------|
| *파일이 네 개 이상이면 어떻게 되나요?* | 풀은 추가 작업을 대기열에 넣고, 스레드가 비게 되는 즉시 실행합니다. 별도의 코드는 필요하지 않습니다. |
| *대신 `newCachedThreadPool`을 사용해야 할까요?* | `newCachedThreadPool`은 필요에 따라 스레드를 생성하고 무한히 늘어날 수 있어 I/O‑중심 작업에 위험합니다. **fixed thread pool**은 메모리와 CPU 사용량을 예측 가능하게 합니다. |
| *CPU 코어 수에 따라 풀 크기를 어떻게 조정하나요?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` 와 같이 사용하는 것이 일반적인 패턴입니다. |
| *하나의 파일 파싱에 실패하면 어떻게 되나요?* | 람다식 내부의 `catch (IOException e)`가 실패를 격리하고 로그를 남기며, 풀의 나머지 작업은 계속 진행됩니다. |
| *추출한 텍스트를 호출자에게 반환할 수 있나요?* | 예—`submit(Runnable)` 대신 `Future<String>`을 사용합니다. 코드는 `Future<String> f = executor.submit(() -> extractBodyText(path));`와 같이 작성하고, 이후 `String result = f.get();` 로 결과를 얻을 수 있습니다. |

---

## 결론

우리는 **executor를 어떻게 사용하는지**와 **fixed thread pool java**를 사용해 HTML 파일 컬렉션을 병렬로 처리하고, 본문 텍스트를 추출하며, 문자 수를 보고하는 방법을 다루었습니다. 완전한 **java thread pool example**은 적절한 자원 관리, 오류 처리, 재사용 가능한 추출 메서드를 보여줍니다.

다음 단계는? `extractBodyText` 구현을 더 정교한 스크래퍼로 교체해 보거나, 더 큰 풀 크기로 실험하거나, 결과를 데이터베이스에 저장해 보세요. 파일 크기가 크게 다를 때는 `CompletionService`를 사용해 결과가 준비되는 즉시 가져오는 방법도 유용합니다.

디렉터리 경로를 조정하고, 파일을 추가하거나, 이 코드를 더 큰 크롤링 프레임워크에 통합해도 좋습니다. 핵심 패턴인—풀 생성, 독립 작업 제출, 우아한 종료—은 워크로드가 얼마나 복잡해도 변하지 않습니다.

코딩을 즐기세요, 그리고 여러분의 스레드가 언제나 살아 있기를 바랍니다(물론 종료할 때는 제외하지만요)!

## 관련 튜토리얼

- [Fixed thread pool java – ExecutorService를 이용한 병렬 HTML 정리](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Java에서 HTML 쿼리하기 – 완전 튜토리얼](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Java용 Aspose.HTML 사용법 - HTML5 Canvas 렌더링 마스터](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}