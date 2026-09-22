---
category: general
date: 2026-02-10
description: Установите коэффициент пикселей устройства в Java с использованием песочницы
  Aspose.HTML. Узнайте, как задать ширину и высоту экрана и получить заголовок страницы
  в Java с полным, исполняемым примером.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: ru
og_description: Установите коэффициент пикселей устройства в Java с помощью песочницы
  Aspose.HTML. Это руководство покажет, как задать ширину и высоту экрана и получить
  заголовок страницы в Java за несколько простых шагов.
og_title: Установка device pixel ratio в Java – Руководство Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Установка коэффициента пикселей устройства в Java – учебник Mobile Sandbox
url: /ru/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

alt text? It's part of markdown image. The instruction: translate all text content. Alt text is text, so translate it. But the URL remains same. Also title attribute "set device pixel ratio diagram" should be translated? Title attribute is inside quotes after URL. That's text, should translate. So alt and title become Russian.

Ok.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# установить коэффициент пикселей устройства в Java – Руководство по мобильному песочному окружению

Когда‑нибудь нужно было **установить коэффициент пикселей устройства** при тестировании адаптивного сайта на Java? Вы не одиноки. Многие разработчики сталкиваются с тем, что страница выглядит идеально на десктопе, но ломается на телефонах с высоким DPI. Хорошая новость? С помощью песочницы Aspose.HTML вы можете эмулировать iPhone X (или любое другое устройство) прямо из вашего Java‑кода — без браузера.

В этом руководстве мы пройдёмся по **установке ширины и высоты экрана**, настройке **коэффициента пикселей устройства**, а затем **получим заголовок страницы java**, чтобы убедиться, что всё отрисовано корректно. К концу вы получите автономную программу, которую можно вставить в любой проект и сразу начать тестировать мобильные макеты.

## Требования

- Java 8 или новее (код также компилируется с JDK 11)  
- Библиотека Aspose.HTML for Java (версия 23.7 или новее) — её можно получить из Maven Central  
- IDE или простая настройка командной строки `javac`  
- Доступ в Интернет для демонстрационного URL (`https://responsive.example.com`)

Никаких дополнительных фреймворков, без Selenium, только чистый Java и Aspose.HTML.

---

## Шаг 1: Установить ширину и высоту экрана и коэффициент пикселей устройства

Первое, что нам нужно, — объект `SandboxOptions`, который сообщает песочнице, каким «устройством» мы будем себя выдавать. Здесь мы используем размеры iPhone X (375 × 812 CSS‑пикселей) и **коэффициент пикселей устройства** = 3.0, что соответствует дисплею Retina с высоким DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Почему это важно:**  
> Вызов `setDevicePixelRatio` масштабирует всё — от изображений до рендеринга шрифтов — поэтому страница «думает», что находится на реальном телефоне. Если пропустить этот шаг, макет может вернуться к CSS‑медиа‑запросам для десктопа, что сводит тестирование мобильных устройств на нет.

---

## Шаг 2: Создать экземпляр песочницы

Теперь превратим эти параметры в работающую песочницу. Думайте о песочнице как о небольшом безголовом браузере, который учитывает заданные размеры и коэффициент пикселей.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Совет:** Один и тот же объект `Sandbox` можно переиспользовать для нескольких загрузок страниц; просто меняйте URL, а песочница сохранит те же характеристики устройства.

---

## Шаг 3: Загрузить страницу в песочнице

С готовой песочницей загрузка страницы сводится к созданию `HTMLDocument` и передаче песочницы в качестве второго аргумента. Это заставит документ отрисоваться с использованием виртуального устройства, которое мы задали ранее.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Если URL недоступен или страница содержит ошибки, Aspose.HTML бросит исключение. В продакшн‑коде, скорее всего, обернёте это в `try‑catch` и залогируете ошибку, но для учебного примера оставим всё просто.

---

## Шаг 4: Проверить с помощью get page title java

Самая быстрая проверка — прочитать заголовок документа. Если песочница правильно применила **коэффициент пикселей устройства**, заголовок будет идентичен тому, что вы увидите на реальном iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Ожидаемый вывод (пример):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Если заголовок напечатан, вы успешно **установили коэффициент пикселей устройства**, **задали ширину и высоту экрана** и **получили заголовок страницы** с помощью Java.

---

## Полный, готовый к запуску пример

Ниже полная программа, которую можно скопировать в файл `SandboxDemo.java`. Убедитесь, что JAR‑файлы Aspose.HTML находятся в classpath (`-cp`), прежде чем компилировать.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Скомпилировать и запустить:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Вы должны увидеть заголовок, выведенный в консоль, что подтверждает отрисовку страницы с нужным **коэффициентом пикселей устройства**.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Можно ли изменить коэффициент пикселей во время выполнения?** | Да — просто создайте новый `SandboxOptions` с другим значением `setDevicePixelRatio` и инстанцируйте новую `Sandbox`. Переиспользовать одну и ту же песочницу после изменения её параметров не поддерживается. |
| **Как тестировать несколько устройств?** | Пройдите в цикле список `SandboxOptions` (например, iPhone 8, Pixel 4) и выполните ту же логику загрузки и получения заголовка для каждого. |
| **Работает ли это с HTTPS‑сайтами, имеющими самоподписанные сертификаты?** | Aspose.HTML использует стандартное хранилище доверенных сертификатов Java. Добавьте сертификат в keystore JVM или отключите проверку только для тестов (не рекомендуется в продакшене). |
| **Как сделать скриншот вместо простого заголовка?** | API `HTMLDocument` предоставляет методы `save`, позволяющие экспортировать отрисованную страницу в PNG или JPEG. Используйте `htmlDoc.save("output.png", SaveFormat.PNG);` после загрузки. |
| **Песочница потокобезопасна?** | Каждый экземпляр `Sandbox` изолирован, но не рекомендуется делить один объект между несколькими потоками без синхронизации. |

---

## Визуальный обзор

![Диаграмма, показывающая установку коэффициента пикселей устройства в мобильной песочнице](https://example.com/images/sandbox-diagram.png "диаграмма установки коэффициента пикселей устройства")

*Иллюстрация выше отображает поток от настройки `SandboxOptions` (включая **установку ширины и высоты экрана** и **коэффициент пикселей устройства**) до загрузки URL и извлечения заголовка.*

---

## Заключение

Теперь вы знаете, **как установить коэффициент пикселей устройства** в Java, **как задать ширину и высоту экрана** для точной эмуляции мобильных устройств и **как получить заголовок страницы java**, чтобы подтвердить успешную отрисовку. Этот компактный рабочий процесс устраняет необходимость в тяжёлых браузерах при автоматическом UI‑тестировании и легко интегрируется в CI‑конвейеры.

Готовы к следующему шагу? Попробуйте экспортировать отрисованную страницу как изображение или поиграйте с отладкой CSS‑медиа‑запросов, переключая `devicePixelRatio` между 1.0 и 3.0. Вы также можете изучить возможности Aspose.HTML по конвертации в PDF, чтобы получить печатную версию мобильного представления.

Счастливого кодинга, и пусть ваши мобильные макеты всегда выглядят чётко — независимо от плотности пикселей!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}