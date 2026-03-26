---
category: general
date: 2026-03-26
description: 실시간 데모에서 await delay JavaScript, 카운터 증가 클래스, 그리고 public class fields
  JavaScript를 보여주는 최상위 await 예제.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: ko
og_description: 간결한 튜토리얼에서 await delay JavaScript, 카운터 증가 클래스, 그리고 public class fields
  JavaScript를 보여주는 최상위 await 예제.
og_title: 최상위 await 예제 – JavaScript에서 await delay 사용
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: 최상위 await 예제 – JavaScript에서 await delay 사용
url: /ko/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await example – Using await delay in JavaScript

모듈 실행을 async IIFE 로 감싸지 않고도 일시 중지할 수 있는 방법이 궁금하셨나요? 바로 **top level await example**이 해답입니다. 이 튜토리얼에서는 `await delay javascript` 를 사용해 작업을 연기하고, **public class fields javascript** 를 활용하는 `increment counter class` 를 만드는 작은 웹 페이지를 단계별로 살펴봅니다. 끝까지 따라오시면 최신 브라우저 어디서든 바로 복사‑붙여넣기 할 수 있는 완전한 코드 스니펫을 얻으실 수 있습니다.

클래스에 public 필드를 정의하는 방법부터 간단한 promise 기반 딜레이 헬퍼를 연결하는 과정까지 모두 다룹니다. 외부 라이브러리나 빌드 단계 없이 순수 HTML, `<script type="module">` 그리고 최신 ECMAScript 기능만 사용합니다. async 함수에 익숙하시다면 top‑level await 이 자연스럽게 확장된 느낌임을 알 수 있을 것이고, **javascript class public field** 문법이 처음이라면 각 라인 뒤에 있는 이유를 자세히 설명합니다.

## What You’ll Learn

- **top level await example** 가 모듈 스크립트 안에서 어떻게 동작하는지
- `await delay javascript` 헬퍼가 `setTimeout` 을 promise 로 흉내 내는 패턴
- public 필드(`count`)와 static 초기화 블록을 사용하는 **increment counter class** 작성 방법
- 예상되는 콘솔 출력과 static 블록이 스크립트 나머지 부분보다 먼저 실행되는지 확인하는 방법
- top‑level await 을 지원하지 않는 구형 브라우저 등 흔히 마주치는 문제 해결 팁

> **Pro tip:** 최신 브라우저(Chrome 106+, Firefox 102+, Edge 106+)는 이미 top‑level await 을 지원합니다. 구형 환경을 지원해야 한다면 Vite 나 Babel 같은 도구로 번들링을 고려하세요.

## Step 1 – Define a Class with a Public Field and a Static Block

데모 첫 번째 파트는 숫자 카운터를 저장하는 클래스입니다. `count = 0;` 라인을 주목하세요—이것이 ES2022 에 도입된 **public class fields javascript** 문법이며, 생성자 없이 인스턴스 속성을 만들 수 있습니다.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**왜 static 블록을 사용할까요?** 모듈이 파싱되는 순간, *top‑level await 이 실행되기 전*에 한 번만 실행되는 초기화 로직(예: 로깅)을 수행할 수 있게 해줍니다. 이를 통해 메시지가 콘솔에 가장 먼저 표시되어 **클래스가 일찍 평가되었음**을 증명합니다.

## Step 2 – Create an `await delay javascript` Helper

다음으로는 아주 작은 promise 기반 딜레이 함수를 만들 차례입니다. 본질적으로 `setTimeout` 을 감싸지만, promise 를 반환하므로 `await` 할 수 있습니다.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**엣지 케이스:** `ms` 가 음수이거나 숫자가 아니면 `setTimeout` 은 이를 `0` 으로 처리합니다. 검증 로직을 추가할 수도 있지만, 데모에서는 한 줄 구현이 가독성을 높입니다.

## Step 3 – Use Top‑Level Await to Pause Execution

이제 쇼의 주인공, top‑level await 을 사용합니다. 스크립트가 모듈(`type="module"`)이기 때문에 `await` 을 최상위 스코프에 바로 배치할 수 있습니다. 이렇게 하면 promise 가 해결될 때까지 모듈이 일시 중지되어 부수 효과의 순서를 제어할 수 있습니다.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**자주 묻는 질문:** “일반 `<script>` 태그에서도 top‑level await 을 쓸 수 있나요?” 아니요—모듈 스크립트에서만 지원됩니다. `type="module"` 을 빼면 구문 오류가 발생합니다.

## Step 4 – Instantiate the Class, Increment, and Log the Result

마지막으로 모든 것을 합칩니다: 인스턴스를 생성하고 `increment()` 를 호출한 뒤 최종 카운트를 출력합니다. 이를 통해 **increment counter class** 가 실제로 동작하는 모습을 확인할 수 있습니다.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Expected Console Output

```
Counter class initialized
Final count: 1
```

DevTools 로 페이지를 열면 static‑block 메시지가 딜레이가 끝나기 **앞에** 표시되어 클래스가 먼저 평가됐음을 확인할 수 있습니다.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

다음과 같이 작성하지 않은 이유가 궁금할 수 있습니다:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

두 방식 모두 동작하지만 **public class fields javascript** 를 사용하면 더 깔끔하고 선언적인 문법을 얻을 수 있습니다. 필드가 한 번만 정의되므로 매번 생성자 호출 시마다 중복 정의하지 않아도 되며, 클래스가 커질수록 가독성이 향상됩니다. 또한 static 블록은 생성자 안에 넣을 수 없으므로 초기화 로직을 분리하기에 자연스럽습니다.

## Step 6 – Adapting the Example for Real‑World Apps

실제 애플리케이션에서는 하나의 카운터보다 더 많은 로직이 필요합니다. 몇 가지 아이디어를 제시합니다:

- **다중 카운터:** 식별자를 키로 하는 `Map` 에 저장
- **영속 상태:** `console.log` 대신 `localStorage` 에 기록
- **비동기 초기화:** static 블록에서 서버로부터 설정을 받아 인스턴스 생성 전에 사용

이러한 패턴도 모두 top‑level await 의 혜택을 받습니다. 모듈 로드 시 한 번만 데이터를 가져와 모든 소비자가 사용할 수 있게 보장하기 때문입니다.

## Frequently Asked Questions

**Q: Does top‑level await block other modules?**  
A: No. Each module runs independently. Only the module that contains the await is paused; other modules continue loading in parallel.

**Q: What if the delay promise rejects?**  
A: An unhandled rejection will abort the module evaluation and surface as an error in the console. Wrap the await in a `try…catch` if you need graceful fallback.

**Q: Is the `static` keyword required?**  
A: Not for the counter itself, but the static block is a handy way to demonstrate that code runs *once* at load time—great for logging or feature‑detection.

## Conclusion

You’ve just built a **top level await example** that showcases `await delay javascript`, an **increment counter class**, and the power of **public class fields javascript**. The complete, runnable snippet lives above, and the console output proves that the static block fires before the delayed code runs.  

From here you can experiment with more complex async flows, swap the delay for a real API call, or expand the class with additional methods. Remember, modern JavaScript lets you treat modules as first‑class async entities—no extra wrappers needed.

Happy coding, and feel free to drop your variations in the comments. If you found this guide useful, share it with a teammate who’s still wrestling with async patterns!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}