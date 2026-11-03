---
category: general
date: 2026-02-10
description: Java 고정 스레드 풀을 사용하여 HTML 파일에서 이미지 수를 세고, 작업을 동시에 실행하며, Executor Service를
  올바르게 종료하는 방법을 배웁니다.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: ko
og_description: Java 고정 스레드 풀 사용을 마스터하여 이미지 수를 세고, 파일을 병렬 처리하며, Executor 서비스를 안전하게
  종료합니다.
og_title: 'Java 고정 스레드 풀: 병렬 파일에서 이미지 개수 세기'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java 고정 스레드 풀: 병렬 파일에서 이미지 개수 세기'
url: /ko/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – 병렬 이미지 카운팅 튜토리얼

수십 개의 HTML 파일을 **java fixed thread pool** 으로 빠르게 이미지 개수를 세고 싶었던 적 있나요? 디렉터리에 있는 페이지들을 보면서 “각 파일에 `<img>` 태그가 몇 개 있는지 알아야 해” 라고 생각했지만, 단일 스레드 루프는 영원히 걸릴 것이라는 걸 깨달은 적이 있나요?  

좋은 소식은 커스텀 스레드 매니저를 직접 구현하거나 저수준 `Thread` 객체와 씨름할 필요가 없다는 것입니다. 이 가이드에서는 *java fixed thread pool* 을 사용해 **이미지를 카운트하는 방법**, 작업을 동시에 실행하는 java, 그리고 작업이 끝났을 때 **shutdown executor service** 를 우아하게 수행하는 방법을 정확히 보여드립니다.  

풀 설정, 파일 목록 준비, 병렬 작업 제출, 에지 케이스 처리, 출력 검증까지 모든 과정을 다룹니다. 끝까지 읽으면 **java parallel file processing** 을 깔끔하고 유지보수하기 쉬운 방식으로 구현한 실행 가능한 프로그램을 얻게 됩니다.  

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Java 17 이상 (코드에서 간결성을 위해 `var` 키워드를 사용하지만, 필요하면 다운그레이드 가능)
- 클래스패스에 Aspose.HTML for Java – Maven Central에서 가져올 수 있습니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- 분석하고 싶은 HTML 파일 몇 개 (`YOUR_DIRECTORY/` 에 존재한다고 가정)
- 익숙한 IDE 또는 빌드 도구 – IntelliJ IDEA, VS Code, 혹은 순수 `javac` 도 괜찮습니다.

이것만 있으면 됩니다. 별도 서버, Docker 없이 순수 Java와 작은 서드파티 라이브러리만 있으면 됩니다.

## Step 1: Create a java fixed thread pool

*java fixed thread pool* 은 제출된 각 작업에 대해 재사용되는 제한된 수의 워커 스레드를 제공합니다. 이는 새 스레드를 계속 생성하는 오버헤드를 방지하고 동시성 수준을 제한해 디스크에서 파일을 읽을 때 매우 중요합니다.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**왜 4인가요?** Quad‑core 노트북이라면 네 개의 스레드가 각 코어를 과도하게 할당하지 않으면서 바쁘게 유지합니다. 코어가 더 많은 서버라면 숫자를 늘릴 수 있지만, 각 스레드가 파일 핸들을 열게 되므로 너무 많이 만들면 OS 제한에 걸릴 수 있습니다.

## Step 2: List the HTML files you want to analyse

다음 단계인 **java parallel file processing** 은 파일 경로 배열(또는 `List`)을 만드는 것입니다. 실제 프로젝트에서는 디렉터리를 재귀적으로 탐색하고 확장자로 필터링하거나 데이터베이스에서 경로를 읽어올 수 있습니다. 여기서는 가장 직관적인 방법을 보여줍니다:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

동적으로 파일 집합을 다뤄야 한다면 정적 배열을 다음과 같이 교체하면 됩니다:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

이 스니펫은 파일 개수에 관계없이 **java parallel file processing** 을 가능하게 해 주며, 나머지 코드는 그대로 사용할 수 있습니다.

## Step 3: Submit tasks to **run tasks concurrently java**

이제 튜토리얼의 핵심 단계 – 각 파일에 대해 람다식을 제출해 **run tasks concurrently java** 합니다. 각 작업은 Aspose.HTML 로 HTML 문서를 로드하고 모든 `<img>` 요소를 조회한 뒤 개수를 출력합니다.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**왜 람다를 사용하나요?** 코드가 간결해지고 별도의 `Runnable` 클래스를 만들 필요가 없습니다. 람다는 `filePath` 를 자동으로 캡처하므로 각 작업이 자신의 파일에만 작동합니다.

### How to **count images** efficiently

Aspose.HTML 은 파일을 한 번 파싱해 DOM을 구축하고, `querySelectorAll("img")` 은 노드 수 *n* 에 대해 O(n) 시간에 실행됩니다. 대부분의 HTML 페이지에서는 무시할 수준입니다. 만약 기가바이트 규모의 파일을 스트리밍 방식으로 더 빠르게 처리해야 한다면 SAX 파서를 사용할 수 있지만, 그 경우 여기서 목표로 하는 단순함을 포기하게 됩니다.

## Step 4: Properly **shutdown executor service**

풀을 종료하지 않으면 JVM 이 영원히 실행됩니다. 아래 패턴은 모든 작업이 끝날 때까지 기다리면서 **shutdown executor service** 를 수행하는 권장 방법입니다:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**작업이 멈추면 어떻게 하나요?** `shutdownNow()` 호출은 실행 중인 스레드에 인터럽트를 시도합니다. 이미지 카운팅 로직이 인터럽트를 잘 처리한다면( Aspose.HTML 은 I/O 블로킹을 하지 않음) 풀은 깔끔히 종료됩니다. 이 패턴은 모든 **java fixed thread pool** 사용 시 금본위 표준입니다.

## Step 5: Verify the output

IDE 혹은 커맨드 라인에서 프로그램을 실행하세요:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

예시 출력은 다음과 같습니다:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

출력 순서가 섞여 있어도 정상입니다 – 스레드마다 종료 시점이 다르기 때문입니다. 중요한 것은 모든 파일이 처리되고, 종료 절차 후 프로그램이 정상적으로 종료된다는 점입니다.

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Expected Result

스니펫을 실행하면 각 파일 경로와 해당 파일에 포함된 `<img>` 태그 수가 출력되고, 그 뒤에 JVM 이 종료됩니다. 남아 있는 스레드나 메모리 누수가 없습니다.

## Common Pitfalls & Pro Tips

- **Pitfall:** `newCachedThreadPool()` 을 사용하고 *fixed* 풀을 쓰지 않는 경우. 이는 무제한 스레드를 생성해 대량 배치 시 파일 디스크립터를 고갈시킬 수 있습니다. 반드시 `newFixedThreadPool` 을 사용하세요.
- **Pro tip:** HTML 파일이 매우 크다면 힙 크기(`-Xmx2g`)를 늘리거나 스트리밍 파서로 전환을 고려하세요. 대부분의 마케팅 페이지는 기본 힙으로 충분합니다.
- **Pitfall:** `shutdown()` 호출을 잊는 경우 – 결과를 출력한 뒤 애플리케이션이 멈춥니다. 위의 `shutdownAndAwaitTermination` 메서드가 이를 견고하게 처리합니다.
- **Pro tip:** 성능 지표가 필요하면 각 작업의 시작·종료 시간을 로그에 남기세요. `HTMLDocument` 생성 전후에 `System.nanoTime()` 을 호출하면 파싱에 걸린 시간을 알 수 있습니다.
- **Pitfall:** 스레드 수를 하드코딩하는 경우. 합리적인 기본값으로 `Runtime.getRuntime().availableProcessors()` 를 사용하세요:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Related Topics You Might Explore Next

- `CompletableFuture` 로 **run tasks concurrently java** 를 구현해 보다 표현력 있는 파이프라인 만들기
- 이미지 카운트를 데이터베이스에 저장해 분석 대시보드 구축
- `java.nio.file.Files.walk` API 와 스트림을 결합한 **java parallel file processing** 활용
- 디버깅에 도움이 되는 의미 있는 스레드 이름을 부여하는 커스텀 `ThreadFactory` 구현

## Conclusion

우리는 **java fixed thread pool** 을 활용해 여러 HTML 파일에서 **how to count images** 를 수행하고, **shutdown executor service** 를 올바르게 처리하는 완전한 예제를 살펴보았습니다. 이 패턴은 파일 배열을 동적 리스트로 교체하고 풀 크기를 조정하면 어떤 **java parallel file processing** 워크로드에도 쉽게 확장됩니다.  

한 번 실행해 보고, 스레드 수를 조정하거나 결과를 CSV 로 내보내는 기능을 추가해 보세요. 견고한 동시성 기반과 Aspose.HTML 같은 편리한 라이브러리를 결합하면 가능성은 무한합니다. Happy coding!  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}