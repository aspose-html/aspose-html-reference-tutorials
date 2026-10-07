---
category: general
date: 2026-02-16
description: CompletableFuture를 사용해 Java에서 JavaScript를 실행하고, JS를 지연시키며, 비동기 코드를 평가하는
  방법을 배워보세요. 비동기 JavaScript 평가를 위한 완전한 단계별 가이드.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: ko
og_description: 이 완전한 튜토리얼에서 Java에서 JavaScript를 실행하고, JS를 지연시키며, CompletableFuture를
  사용해 비동기 코드를 평가하는 방법을 마스터하세요.
og_title: CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 방법
tags:
- javascript
- java
- asynchronous
- completablefuture
title: CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 방법
url: /ko/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 방법

메인 스레드를 차단하지 않고 Java 애플리케이션 내부에서 **JavaScript를 실행하는 방법**을 궁금해 본 적 있나요? 데이터를 가져오는 작은 스크립트를 호출해야 할 수도 있지만 UI가 멈추길 원하지 않을 겁니다. 좋은 소식은 최신 Java 라이브러리를 사용하면 JavaScript를 **asynchronously** 평가할 수 있으며, 브라우저에서처럼 지연을 도입할 수도 있다는 점입니다. 이 가이드에서는 Aspose HTML의 `ScriptEngine`과 `CompletableFuture`를 함께 사용하여 **JavaScript를 실행하는 방법**을 수행하고 Java에서 결과를 얻는 완전한 실행 가능한 예제를 보여드립니다.

우리는 또한 **CompletableFuture 사용 방법**, **JS 지연 방법**, 그리고 **비동기 평가 방법** 코드를 다룰 것이며, 이를 통해 어떤 Java 프로젝트에서도 **JavaScript를 비동기적으로 평가**할 수 있습니다. 마지막까지 읽으면 복사‑붙여넣기하고, 수정하고, 더 큰 시스템에 삽입할 수 있는 견고한 템플릿을 얻게 됩니다.

Aspose HTML for Java JAR 외에 외부 빌드 도구는 필요하지 않으며, 이를 클래스패스에 넣기만 하면 됩니다. 이제 시작해 봅시다.

## 배우게 될 내용

- 현​대 ES2022 JavaScript를 실행할 수 있는 Java `ScriptEngine` 설정하기.
- `async` 함수 작성하기, 여기에는 지연(`how to delay js`)이 포함됩니다.
- `evaluateAsync` 호출하고 `CompletableFuture` 받기(`how to use completablefuture`).
- JavaScript 프로미스가 해결되면 결과를 가져오기(`how to evaluate async`).
- 오류 처리, 스레드 관리, 패턴 확장을 위한 팁.

Aspose HTML for Java JAR 외에 외부 빌드 도구는 필요하지 않으며, 이를 클래스패스에 넣기만 하면 됩니다. 이제 시작해 봅시다.

## Step 1: JavaScript 실행 방법 – 스크립팅 엔진 초기화

우선 가장 먼저 해야 할 일입니다. Aspose HTML 라이브러리는 JavaScript 코드를 실행할 수 있는 `ScriptEngine` 클래스를 제공합니다. 이를 JVM 내부에서 실행되는 작은 Chromium 엔진이라고 생각하면 됩니다.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **왜 중요한가:** `ScriptEngine`을 인스턴스화하면 최신 JavaScript(`async/await` 포함)가 바로 사용할 수 있는 샌드박스 환경을 얻습니다. 외부 Node 프로세스를 띄울 필요가 없습니다.

## Step 2: JS 지연 방법 – Promise 기반 타이머를 사용한 Async 함수 작성

JavaScript의 `setTimeout`은 실행을 일시 중지하는 고전적인 방법입니다. 최신 코드에서는 이를 `Promise`로 감싸 `await`할 수 있게 합니다. 바로 이것을 스크립트 문자열에서 수행할 것입니다.

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

> **JS 지연 방법:** `delay` 헬퍼는 `ms` 밀리초 후에 해결되는 프로미스를 생성합니다. 이를 `await`함으로써 함수는 Java 스레드를 차단하지 않고 일시 중지됩니다.

## Step 3: 비동기 평가 방법 – 스크립트를 실행하고 CompletableFuture 얻기

동기식 `evaluate` 메서드 대신 `evaluateAsync`를 호출합니다. 이 메서드는 JavaScript 프로미스가 해결될 때 완료되는 `CompletableFuture<Object>`를 즉시 반환합니다.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **비동기 평가 방법:** `evaluateAsync`는 JavaScript 이벤트 루프와 Java의 `CompletableFuture`를 연결합니다. 이것이 **JavaScript를 비동기적으로 평가**하는 핵심입니다.

## Step 4: CompletableFuture 사용 방법 – 콜백을 연결하고 데모를 위해 블록하기

이제 `thenAccept`로 콜백을 연결해 결과를 출력하고, 데모가 끝날 때까지 메인 스레드를 잠시 블록합니다.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **`get()`을 호출하는 이유:** 실제 애플리케이션에서는 아마도 다른 곳에서 처리를 계속할 것입니다. 여기서는 예제를 자체적으로 유지하기 위해 블록합니다.

## 시각적 개요

![CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 흐름을 보여주는 다이어그램](https://example.com/diagram.png "JavaScript 실행 방법 – 비동기 흐름")

*Alt text:* **CompletableFuture를 사용하여 JavaScript를 비동기적으로 실행하는 흐름을 보여주는 다이어그램** – 이 이미지는 Java에서 스크립트 엔진으로, 비동기 지연, 그리고 CompletableFuture 완료까지의 흐름을 보여줍니다.

## 일반적인 함정 및 모범 사례 (비동기 안전 평가 방법)

| 함정 | 발생 현상 | 해결 방법 |
|------|----------|-----------|
| 프로미스를 반환하지 않음 | `evaluateAsync`가 즉시 `undefined`와 함께 해결됩니다 | 스크립트의 마지막 줄이 프로미스(`fetchMessage();`)인지 확인하세요 |
| JS에서 차단하는 `Thread.sleep` 사용 | 엔진의 이벤트 루프를 차단해 비동기를 무력화합니다 | `delay` 프로미스 패턴 사용(위 예시처럼) |
| 예외 무시 | Future가 예외적으로 완료되지만 확인할 수 없습니다 | `.exceptionally(e -> { e.printStackTrace(); return null; })`를 연결하세요 |
| 엔진을 종료하지 않음 | 장기 실행 앱에서 리소스 누수 발생 | 사용이 끝나면 `scriptEngine.dispose()`를 호출하세요 |

## 패턴 확장 (실제 프로젝트에서 CompletableFuture 사용 방법)

여러 비동기 JavaScript 호출을 체인으로 연결하고, 다른 Future와 결합하거나, 맞춤형 `Executor`에서 실행할 수도 있습니다. 아래는 간단한 예시입니다:

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

> **CompletableFuture 사용 방법:** `Executor`를 전달함으로써 스레드 풀을 제어하고 UI를 반응형으로 유지하며 스레드 고갈을 방지합니다.

## 예상 출력

`JsAsyncDemo` 클래스를 실행하면 다음과 같은 출력이 나타납니다:

```
JS result: Hello from async JS!
```

500 ms 지연은 콘솔에 표시되지 않지만, 원한다면 타임스탬프를 추가해 지연을 확인할 수 있습니다.

## 요약 – CompletableFuture로 JavaScript 실행하기

우리는 Java 내부에서 **JavaScript를 실행하는 방법**으로 시작하고, **JS를 지연하는 방법**인 `async` 함수를 작성했으며, `evaluateAsync`(**비동기 평가 방법**)로 실행하고 **CompletableFuture 사용 방법**으로 결과를 캡처했습니다. 전체 흐름은 **JavaScript를 비동기적으로 평가**하는 깔끔하고 재사용 가능한 패턴을 보여줍니다.

## 다음 단계

- **HTTP 클라이언트와 통합:** 비동기 JS 내부에서 REST 엔드포인트에서 데이터를 가져와 Java에 반환합니다.
- **여러 스크립트 사용:** 복잡한 파이프라인을 위해 여러 `evaluateAsync` 호출을 체인합니다.
- **엔진 교체:** 동일한 패턴이 Nashorn, GraalVM 또는 다른 JavaScript 런타임에서도 작동합니다—`ScriptEngine`만 교체하면 됩니다.

더 긴 지연, 오류를 발생시키는 스크립트, 혹은 WebAssembly 모듈을 실험해 보세요. Java의 동시성 원시와 최신 JavaScript를 결합하면 가능성은 무한합니다.

### 질문이 있나요?

내용이 명확하지 않다면—예를 들어 거부된 프로미스를 처리하는 방법이나 Java에서 스크립트로 변수를 전달하는 방법이 궁금하다면—아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}