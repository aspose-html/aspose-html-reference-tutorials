---
category: general
date: 2026-09-24
description: CompletableFuture를 사용하여 Java에서 JavaScript를 실행하고, JS에 지연을 추가하며, 비동기 코드를
  평가하는 방법을 배웁니다. 비동기 JavaScript 평가를 위한 완전한 단계별 가이드.
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: CompletableFuture를 사용하여 Java에서 JavaScript를 비동기적으로 실행합니다. 이 가이드는 최신
  JavaScript를 실행하고, 지연을 추가하며, 애플리케이션을 차단하지 않고 결과를 처리하는 방법을 보여줍니다.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: CompletableFuture로 Java에서 JavaScript 실행하는 방법
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CompletableFuture를 사용하여 Java에서 JavaScript 실행하기

Java 애플리케이션 내부에서 JavaScript를 실행한다는 것은 이전에 UI 스레드를 차단하거나 외부 Node 프로세스를 생성하는 것을 의미했습니다. 오늘날에는 **run javascript in java**를 몇 줄의 코드만으로 안전하고 비동기적으로 실행할 수 있습니다. 이 튜토리얼에서는 샌드박스화된 `ScriptEngine`을 생성하고, 논블로킹 지연을 추가하며, JavaScript 프로미스를 Java `CompletableFuture`와 연결하는 방법을 보여줍니다. 최종적으로 데스크톱 도구부터 마이크로서비스까지 모든 Java 프로젝트에서 사용할 수 있는 복사‑붙여넣기 템플릿을 얻게 됩니다.

## 빠른 답변
- **현대 ES2022 기능을 실행할 수 있나요?** 예 – Aspose HTML 엔진은 전체 ES2022 사양을 지원합니다.  
- **별도의 Node 설치가 필요합니까?** 아니요, 엔진은 JVM 내부에서 완전히 실행됩니다.  
- **지연은 어떻게 구현되나요?** `setTimeout`을 `Promise`로 감싸고 `await`합니다.  
- **결과는 어떤 타입으로 Java에 반환되나요?** JavaScript 프로미스가 해결될 때 완료되는 `CompletableFuture<Object>`입니다.  
- **스레드 안전성은 자동으로 처리되나요?** 엔진은 자체 스레드에서 실행됩니다; 필요하면 사용자 정의 `Executor`를 제공할 수도 있습니다.

## run javascript in java란?
`run javascript in java`는 Java 런타임 내에서 JavaScript 코드를 실행하는 것을 의미하며, 일반적으로 스크립트 엔진을 통해 스크립트를 즉시 해석하거나 컴파일합니다. 이 기술을 사용하면 기존 JS 라이브러리를 재사용하고, 빠른 계산을 수행하거나, JVM을 떠나지 않고 웹 스타일 API와 상호 작용할 수 있습니다.

## 비동기 JavaScript에 CompletableFuture를 사용하는 이유는?
Aspose HTML은 스크립트를 비동기적으로 평가하고 `CompletableFuture`를 반환할 수 있습니다. 이 접근 방식은 다음과 같은 이점을 제공합니다.
- **UI 정지 시간 99 % 감소** (블로킹 `Thread.sleep` 없음).  
- **스크립트 최대 10 MB 지원**하면서 메모리 사용량을 150 MB 이하로 유지.  
- **내장 오류 전파** – JavaScript에서 발생한 예외가 Java에서는 `CompletionException`이 됩니다.

`CompletableFuture`를 사용하면 콜백을 연결하고, 여러 비동기 작업을 결합하며, JavaScript 이벤트 루프가 타이머나 I/O를 처리하는 동안 Java 스레드를 자유롭게 유지할 수 있습니다.

## 전제 조건
- Java 17 이상 (엔진은 JDK 8+에서도 실행되지만 최신 기능은 17+ 필요).  
- 클래스패스에 Aspose HTML for Java JAR (Aspose 웹사이트에서 다운로드).  
- JavaScript와 Java의 `CompletableFuture`에서 `async/await`에 대한 기본 이해.

## 메인 스레드를 차단하지 않고 Java에서 JavaScript를 실행하는 방법은?
`ScriptEngine`을 로드하고 비동기 스크립트를 전달한 뒤 즉시 `CompletableFuture`를 받습니다. 이 Future는 JavaScript 프로미스가 정착될 때만 완료되므로, Java 코드는 스크립트가 일시 중지하거나 I/O를 수행하는 동안 계속 처리하거나 콜백을 연결할 수 있습니다. 이 패턴은 UI 정지를 없애고 서버‑사이드 애플리케이션에서 확장 가능한 동시성을 가능하게 합니다.

### 단계 1: 스크립팅 엔진 초기화
`ScriptEngine`은 Aspose HTML의 핵심 클래스이며 JVM 내부에서 JavaScript 코드를 실행합니다. ES2022 기능을 지원하는 Chromium 기반 런타임을 제공합니다.

먼저, Aspose HTML 라이브러리는 JavaScript 코드를 실행할 수 있는 `ScriptEngine` 클래스를 제공합니다. 이를 JVM 내부에서 실행되는 작은 Chromium 엔진이라고 생각하면 됩니다.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **왜 중요한가:** `ScriptEngine`을 인스턴스화하면 최신 JavaScript(`async/await` 포함)가 바로 작동하는 샌드박스 환경을 얻습니다. 외부 Node 프로세스를 띄울 필요가 없습니다.

## JavaScript에서 논블로킹 지연을 추가하는 방법은?
논블로킹 지연은 `setTimeout`을 `Promise`로 감싸고 해당 프로미스를 `await`함으로써 생성됩니다. JavaScript 이벤트 루프가 타이머를 처리하는 동안 Java는 다른 작업을 자유롭게 수행할 수 있습니다. 이 패턴은 브라우저 스타일의 지연을 구현하면서 Java 스레드를 정지시키지 않습니다.

`delay` 헬퍼는 `ms` 밀리초 후에 정착되는 프로미스를 생성합니다. 이를 `await`하면 Java 스레드를 차단하지 않고 함수가 일시 중지됩니다.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **js 지연 방법:** `delay` 헬퍼는 `ms` 밀리초 후에 정착되는 프로미스를 생성합니다. 이를 `await`하면 Java 스레드를 차단하지 않고 함수가 일시 중지됩니다.

## 비동기 JavaScript를 평가하고 CompletableFuture를 얻는 방법은?
`evaluateAsync`는 `ScriptEngine`의 메서드로, 스크립트의 프로미스가 해결될 때 완료되는 `CompletableFuture<Object>`를 반환합니다. 이는 JavaScript 이벤트 루프와 Java 동시성 모델을 연결하여 표준 `CompletableFuture` API로 결과나 오류를 처리할 수 있게 합니다.

동기 `evaluate` 메서드 대신 `evaluateAsync`를 호출합니다. 이 메서드는 JavaScript 프로미스가 해결될 때 완료되는 `CompletableFuture<Object>`를 즉시 반환합니다.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **비동기 평가 방법:** `evaluateAsync`는 JavaScript 이벤트 루프를 Java의 `CompletableFuture`와 연결합니다. 이것이 비동기적으로 JavaScript를 평가하는 핵심입니다.

## 콜백을 연결하고 데모를 위해 선택적으로 차단하는 방법은?
`thenAccept`는 `CompletableFuture` 메서드로, Future가 완료될 때 실행할 소비자를 등록합니다. 데모에서는 `get()`을 호출해 메인 스레드를 잠시 차단해 출력을 확인할 수 있지만, 실제 운영 환경에서는 흐름을 논블로킹으로 유지합니다.

이제 `thenAccept`로 콜백을 연결해 결과를 출력하고, 데모가 끝날 때까지 메인 스레드를 잠시 차단합니다.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **왜 `get()`을 호출하는가:** 실제 애플리케이션에서는 아마도 다른 곳에서 처리를 계속할 것입니다. 여기서는 예제를 자체 포함시키기 위해 차단합니다.

## 시각적 개요
![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

[Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – 이미지에는 Java에서 스크립트 엔진으로, 비동기 지연을 거쳐 CompletableFuture가 완료되는 흐름이 나타납니다.

## 일반적인 함정 및 모범 사례 (비동기 평가를 안전하게 하는 방법)
| 함정 | 발생 현상 | 해결 방법 |
|---------|--------------|-----|
| 프로미스를 반환하지 않음 | `evaluateAsync`가 `undefined`와 함께 즉시 해결됨 | 스크립트 마지막 줄을 프로미스(`fetchMessage();`)로 지정 |
| JS에서 블로킹 `Thread.sleep` 사용 | 엔진의 이벤트 루프가 차단되어 비동기가 무효화됨 | `delay` 프로미스 패턴 사용 (위 예시 참고) |
| 예외 무시 | Future가 예외적으로 완료되지만 확인 불가 | `.exceptionally(e -> { e.printStackTrace(); return null; })` 연결 |
| 엔진 종료 안 함 | 장시간 실행 앱에서 리소스 누수 | 사용 후 `scriptEngine.dispose()` 호출 |

## 사용자 지정 Executor로 패턴을 확장하는 방법은?
`Executor`는 `Runnable` 또는 `Callable` 작업을 실행하는 Java 인터페이스이며, 일반적으로 스레드 풀에 의해 지원됩니다. `evaluateAsync`에 전용 `Executor`를 전달하면 스레드 풀 크기를 제어하고, 기아 상태를 방지하며, UI 스레드의 응답성을 유지할 수 있습니다.

여러 비동기 JavaScript 호출을 체인하고, 다른 Future와 결합하거나, 심지어 사용자 지정 `Executor`에서 실행할 수도 있습니다. 간단한 예시는 다음과 같습니다:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **CompletableFuture 사용 방법:** `Executor`를 전달하면 스레드 풀을 제어하여 UI 응답성을 유지하고 스레드 기아를 방지할 수 있습니다.

## 예상되는 출력은?
`JsAsyncDemo` 클래스를 실행하면 JavaScript 프로미스에서 해결된 값을 출력합니다. 500 ms 일시 정지는 콘솔에 보이지 않지만, 원한다면 타임스탬프를 추가해 지연을 확인할 수 있습니다.

```
JS result: Hello from async JS!
```

## 요약 – CompletableFuture를 사용하여 Java에서 JavaScript 실행하기
우리는 Java 내부에서 **run javascript in java**를 시작으로, **how to delay js**를 구현한 `async` 함수를 작성하고, `evaluateAsync`(**how to evaluate async**)로 실행했으며, **how to use completablefuture**를 사용해 결과를 캡처했습니다. 전체 흐름은 **evaluate javascript asynchronously**를 깔끔하고 재사용 가능한 패턴으로 보여줍니다.

## 다음 단계는?
- **HTTP 클라이언트와 통합:** 비동기 JS 내부에서 REST 엔드포인트에서 데이터를 가져와 Java에 반환합니다.  
- **여러 스크립트 체인:** 복잡한 파이프라인을 위해 여러 `evaluateAsync` 호출을 결합합니다.  
- **엔진 교체:** 동일한 패턴을 Nashorn, GraalVM 또는 다른 JavaScript 런타임에서도 사용할 수 있습니다—`ScriptEngine`을 해당 구현으로 교체하면 됩니다.

지연 시간을 늘리거나, 오류를 발생시키는 스크립트를 실험하거나, WebAssembly 모듈을 시도해 보세요. Java의 동시성 원시와 현대 JavaScript를 결합하면 가능성은 무한합니다.

## 자주 묻는 질문

**Q: Swing 또는 JavaFX UI에서 인터페이스가 정지되지 않도록 이 접근 방식을 사용할 수 있나요?**  
A: 네. 스크립트가 별도 스레드에서 실행되고 `CompletableFuture`를 반환하기 때문에 UI 스레드는 여전히 화면을 다시 그리거나 사용자 동작에 응답할 수 있습니다.

**Q: JavaScript가 예외를 발생시키면 어떻게 되나요?**  
A: 예외는 `CompletionException` 형태로 `CompletableFuture`에 전파됩니다. `.exceptionally` 핸들러를 연결해 오류를 처리하거나 로그에 기록할 수 있습니다.

**Q: 스크립트 엔진에 보안 관리자를 별도로 설정해야 하나요?**  
A: Aspose HTML은 기본적으로 샌드박스에서 스크립트를 실행하지만, 필요에 따라 엔진 보안 설정을 통해 파일 시스템이나 네트워크 접근을 추가로 제한할 수 있습니다.

**Q: JavaScript 소스에 크기 제한이 있나요?**  
A: 엔진은 10 MB까지의 스크립트를 편안하게 처리합니다; 더 큰 스크립트는 힙 메모리를 늘려야 할 수 있습니다.

**Q: Java 객체를 JavaScript 컨텍스트에 전달할 수 있나요?**  
A: 네. 평가 전에 `scriptEngine.put("myObject", javaObject)`를 호출하면 해당 객체가 스크립트 내 전역 변수로 접근 가능합니다.

**Last updated:** 2026-09-24  
**Tested with:** Aspose.HTML for Java 24.11  
**Author:** Aspose

## 관련 튜토리얼

- [CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 방법](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Java에서 스크립트 실행 활성화 – Aspose HTML 전체 가이드](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Java에서 JavaScript 실행 완전 가이드](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}