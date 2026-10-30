---
category: general
date: 2026-06-19
description: 재사용 가능한 Runnable을 사용하여 Java에서 스레드를 시작하고, 여러 스레드를 시작하며, 스레드 이름을 출력하고,
  Java로 HTML을 파싱하는 방법. 단계별 예제.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: ko
og_description: Runnable을 사용해 Java에서 스레드를 시작하고, 여러 스레드를 실행하며, 스레드 이름을 출력하고, Java로
  HTML을 파싱하는 단일 실행 가능한 예제.
og_title: Java에서 스레드 시작하는 방법 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Java에서 스레드 시작하는 방법 – 완전 가이드
url: /ko/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 스레드 시작하기 – 완전 가이드

보일러플레이트 코드에 빠지지 않고 **how to start thread** 하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 웹 크롤러를 만들든, UI 업데이트를 하든, 무거운 계산을 오프로드하든, 스레드 생성 마스터는 모든 Java 개발자에게 필수 스킬입니다.

이 튜토리얼에서는 실용적인 시나리오를 따라갑니다: **Java로 HTML 파싱**, 현재 스레드 이름 출력, 그리고 동일한 로직을 공유하는 **여러 스레드 시작**. 끝까지 보면 **Runnable 사용 방법**, 여러 워커를 띄우는 방법, 기대한 출력 결과를 확인하는 방법을 모두 복사‑붙여넣기 할 수 있는 예제로 익히게 됩니다.

## What You’ll Learn

- `Thread` 클래스와 `Runnable`을 사용해 **how to start thread** 하는 정확한 단계
- 코드를 중복하지 않고 **여러 스레드 시작** 하는 방법
- 처리 결과와 함께 **스레드 이름 출력** 하는 가장 간단한 방법
- 가벼운 `HTMLDocument` 헬퍼(또는 원하는 파서)를 이용한 **Java로 HTML 파싱** 방법
- 재사용 가능하고 테스트 가능한 코드를 위해 **how to use runnable** 이 왜 중요한지

핵심 예제에는 외부 라이브러리가 필요하지 않지만, 더 강력한 파서가 필요할 경우 Jsoup 등으로 교체할 수 있는 부분을 언급합니다.

---

## Step 1: Define a reusable task – **how to use runnable**

첫 번째로 알아야 할 **how to use runnable** 은 각 스레드가 수행할 작업을 캡슐화하는 것입니다. `Runnable` 은 단일 `run()` 메서드를 가진 함수형 인터페이스로, 람다식에 최적입니다.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**왜 중요한가:** 로직을 `Runnable` 안에 두면 언제든 `Thread` 객체, 스레드 풀, 혹은 executor service에 넘길 수 있습니다. 이렇게 하면 코드가 DRY하고 테스트하기 쉬워집니다.

---

## Step 2: **How to start thread** – create the first worker

이제 `Runnable` 이 준비됐으니, 스레드를 시작하는 것은 `Thread` 생성자를 호출하는 것만큼 쉽습니다. **how to start thread** 질문은 한 줄로 해결됩니다:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

두 번째 인수인 `"Worker-1"`을 주목하세요. 이 이름은 나중에 **print thread name** 할 때 표시되어 디버깅을 훨씬 간단하게 만들어 줍니다.

---

## Step 3: **Start multiple threads** – reuse the same Runnable

여러 HTML 파일을 동시에 처리하고 싶나요? 같은 `Runnable` 로 또 다른 `Thread` 를 만들면 됩니다. 이렇게 하면 **start multiple threads** 하면서 작업 코드를 복사할 필요가 없습니다:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

`Worker-1` 과 `Worker-2` 모두 `extractTextLength` 에 정의된 블록을 동시에 실행합니다. 작업이 상태를 갖지 않기 때문에(파일을 읽기만 함) 레이스 컨디션을 신경 쓸 필요가 없습니다.

---

## Step 4: **Print thread name** while parsing HTML

`Runnable` 내부에서 이미 `Thread.currentThread().getName()` 을 호출했습니다. 이것이 **print thread name** 하는 정석적인 방법입니다. 출력 예시는 다음과 같습니다(HTML 본문에 1 234자가 있다고 가정):

```
Worker-1: 1234
Worker-2: 1234
```

큰 파일로 실행하면 두 스레드가 같은 파일을 읽기 때문에 각 라인은 동일한 길이를 보여줍니다. 경로를 바꾸거나 파일 이름을 매개변수로 전달하면 다른 결과를 확인할 수 있습니다.

---

## Step 5: Full, runnable example – from import to execution

아래는 `HtmlThreadDemo.java` 라는 파일에 바로 넣어 실행할 수 있는 **self‑contained** 프로그램 전체입니다. 실제 파서가 없을 경우에도 컴파일이 되도록 아주 간단한 `HTMLDocument` 스텁을 포함했습니다. 실제 운영 환경에서는 Jsoup 등으로 교체하세요.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Expected output

`page.html` 의 `<body>` 태그 안에 2 567자가 들어 있다고 가정하면 다음과 같은 출력이 나타납니다:

```
Worker-1: 2567
Worker-2: 2567
```

파일을 읽지 못하면 `catch` 블록 덕분에 스택 트레이스가 출력됩니다.

---

## Common Pitfalls & Pro Tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **File not found** | `"YOUR_DIRECTORY/page.html"` 경로가 JVM을 실행하는 위치에 상대적이기 때문 | 절대 경로를 사용하거나 `Paths.get("").toAbsolutePath()` 로 디버그 |
| **Race conditions** | `Runnable` 이 공유 상태를 변경하면 스레드 간 충돌 발생 | 작업을 상태 없이 유지하거나 공유 객체 접근을 동기화 |
| **Too many threads** | 수십 개의 `Thread` 를 생성하면 OS 자원이 고갈될 수 있음 | 기본을 익힌 뒤 `ExecutorService` 로 제한된 풀 전환 |
| **Incorrect HTML parsing** | 스텁 `HTMLDocument` 가 단순해서 복잡한 페이지 파싱에 실패 | Jsoup 사용 예: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Extending the Example

이제 **how to start thread** 를 알았으니 다음과 같이 확장해 볼 수 있습니다:

- **다른 파일 파싱** – 파일명을 `Runnable` 에 전달(생성자 또는 변수 캡처 람다 사용)
- **결과 수집** – 단순 출력 대신 `ConcurrentLinkedQueue<Integer>` 로 결과 저장
- **스레드 풀 활용** – `Executors.newFixedThreadPool(4)` 로 확장성 향상
- **파서 교체** – 프로젝트에 맞는 Jsoup, HtmlUnit 등으로 교체

이 모든 단계는 핵심 아이디어, 즉 재사용 가능한 작업 정의 → 하나 혹은 여러 스레드에 전달 → **print thread name** 으로 어느 스레드가 작업 중인지 확인하는 흐름에 기반합니다.

---

## Conclusion

Java에서 **how to start thread** 하는 방법을 다루고, 재사용 가능한 작업을 위해 **how to use runnable** 을 활용했으며, **여러 스레드 시작** 과 **HTML 파싱** 예시를 통해 **print thread name** 하는 방법을 보여드렸습니다. 위의 완전한 코드 스니펫은 바로 실행할 수 있으며, 개념은 더 복잡한 프로덕션 수준 애플리케이션에도 그대로 적용됩니다.

파일 경로를 바꾸거나 워커 수를 늘리거나 실제 HTML 파서를 연결해 보세요. 기본은 변하지 않으며, 이제 멀티스레드 Java 프로젝트의 탄탄한 기반을 갖추게 되었습니다.

스레드 안전성, executor 서비스, HTML 파싱 라이브러리 등에 궁금한 점이 있으면 아래에 댓글을 남겨 주세요. Happy coding!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 다양한 구현 방식을 탐구할 수 있도록 완전한 코드 예제와 단계별 설명을 제공합니다.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}