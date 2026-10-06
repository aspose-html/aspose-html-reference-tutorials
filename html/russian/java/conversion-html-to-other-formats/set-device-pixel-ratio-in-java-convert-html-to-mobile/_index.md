---
category: general
date: 2026-03-04
description: Установите коэффициент пикселей устройства в Java, чтобы отобразить мобильный
  вид вашего HTML. Узнайте, как преобразовать HTML в мобильный, протестировать адаптивный
  HTML и легко сохранить отрендеренный HTML‑файл.
draft: false
keywords:
- set device pixel ratio
- convert html to mobile
- test responsive html
- save rendered html file
- render html file java
language: ru
og_description: Установите коэффициент пикселей устройства в Java, чтобы отобразить
  мобильный вид вашего HTML. Это руководство показывает, как преобразовать HTML в
  мобильный, протестировать адаптивный HTML и сохранить отрендеренный HTML‑файл.
og_title: Установить соотношение пикселей устройства в Java — Преобразовать HTML для
  мобильных
tags:
- Aspose.HTML
- Java
- Responsive Design
title: Установить коэффициент пикселей устройства в Java – Преобразовать HTML для
  мобильных.
url: /ru/java/conversion-html-to-other-formats/set-device-pixel-ratio-in-java-convert-html-to-mobile/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить Device Pixel Ratio в Java – Преобразовать HTML в мобильный

Задумывались ли вы когда‑нибудь, как **set device pixel ratio** в Java, чтобы ваш HTML действительно выглядел так, как на телефоне? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда пытаются **convert HTML to mobile** без реального устройства, и в итоге гадуют, действительно ли их макет работает.  

В этом руководстве мы пройдемся по полному, готовому к запуску примеру, который **sets device pixel ratio**, загружает адаптивную страницу, **renders HTML file Java**‑style и, наконец, **save rendered HTML file** для последующего осмотра. К концу вы сможете **test responsive HTML** локально, без эмулятора.

## Что понадобится

- **Java 17** или новее (API работает с любой современной JDK).  
- Библиотека **Aspose.HTML for Java** – рекомендуется версия 22.12 или новее.  
- Простая адаптивная HTML‑страница (например, `responsive.html`).  
- IDE или обычный текстовый редактор и терминал – что вам удобнее.

Это всё. Никаких дополнительных инструментов сборки, Docker‑контейнеров, только чистый Java и один JAR.

---

## Шаг 1: Создать песочницу, которая **Set Device Pixel Ratio**

Сердце решения – класс `DocumentSandbox`. Настраивая его размеры экрана и **device pixel ratio**, вы имитируете дисплей высокой плотности (например, iPhone 6/7/8).  

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // high‑density display

        // The sandbox now **sets device pixel ratio** to 2.0, which tells the renderer
        // to treat each CSS pixel as two physical pixels – exactly what modern phones do.
```

**Почему это важно:**  
Если пропустить вызов `setDevicePixelRatio`, отрендеренный результат будет выглядеть размыто на ретина‑экранах, а ваши медиазапросы, зависящие от `devicePixelRatio`, никогда не сработают. Явно **setting device pixel ratio** гарантирует, что макет будет вести себя точно так же, как на реальном устройстве.

## Шаг 2: Загрузить страницу и **Convert HTML to Mobile**

Теперь указываем песочнице HTML‑файл, который нужно проанализировать. Тот же класс `Document`, который вы используете для рендера на десктопе, работает и здесь, но мы передаём песочницу вторым аргументом.

```java
        // 2️⃣ Load the responsive HTML document inside the sandbox
        // This is where we **convert HTML to mobile** by feeding it the mobileSandbox.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);
```

**Что происходит «под капотом»?**  
Aspose.HTML читает файл, применяет настройки viewport из песочницы и пересчитывает CSS‑единицы на основе **device pixel ratio**, установленного ранее. Это значит, что любые правила `@media (min-device-pixel-ratio: 2)` будут соблюдены, позволяя вам **test responsive HTML** без физического телефона.

## Шаг 3: **Render HTML File Java**‑Style и **Save Rendered HTML File**

Наконец, просим `Document` записать обработанную разметку. На выходе получаем обычный файл `.html`, отражающий то, как страница выглядит на симулированном устройстве.

```java
        // 3️⃣ Render and save the mobile view of the document
        // The save call creates a new HTML file that you can open in any browser.
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");
    }
}
```

Откройте `mobile_view.html` в Chrome, нажмите **Ctrl + Shift + I** и переключите панель устройств – вы увидите тот же макет, который только что отрендерили. Другими словами, вы успешно **render html file java** и **save rendered html file** для последующего QA.

## Полный, исполняемый пример

Ниже полностью готовая программа, которую можно скопировать в `MobileSandbox.java`. Не забудьте заменить `YOUR_DIRECTORY` на реальный путь к папке, где находится `responsive.html`.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1 – create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels (iPhone 6/7/8)
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // ★ set device pixel ratio ★

        // Step 2 – load the responsive HTML document inside the sandbox
        // This effectively **convert html to mobile** for testing.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);

        // Step 3 – render and **save rendered html file** for inspection
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");

        // Optional: print a friendly confirmation
        System.out.println("Mobile view saved to mobile_view.html – you can now open it in any browser.");
    }
}
```

### Ожидаемый результат

- `mobile_view.html` содержит точную разметку, которую браузер использовал бы на экране с плотностью 2×.  
- Все медиазапросы, зависящие от `device-pixel-ratio`, срабатывают корректно.  
- Файл можно открыть в любом настольном браузере и увидеть мобильный макет, что идеально подходит для **test responsive HTML** в CI‑конвейерах.

## Pro Tips & Edge Cases

| Ситуация | Что сделать | Почему |
|-----------|------------|-----|
| **Different screen sizes** | Отрегулируйте `setScreenWidth` / `setScreenHeight` под целевое устройство (например, 414 × 896 для iPhone XR). | Гарантирует корректную работу макета на разных брейкпоинтах. |
| **Testing landscape mode** | Поменяйте местами ширину и высоту, затем сохраните заново. | В ландшафтной ориентации часто срабатывают другие CSS‑правила. |
| **High‑resolution images** | Оставьте `setDevicePixelRatio` равным 3.0 для устройств типа iPhone X. | Принудительно заставит рендерер выбирать `@2x` или `@3x` ресурсы, если вы используете `srcset`. |
| **Dynamic content (JS)** | Используйте `htmlDocument.renderToBitmap(...)` вместо `save`, если нужен растровый снимок. | Некоторые скрипты запускаются только после полного построения DOM. |
| **CI/CD integration** | Оберните код в плагин Maven или задачу Gradle и запускайте его в процессе сборки. | Автоматизирует **test responsive HTML** при каждом pull‑request. |

## Frequently Asked Questions

**Q: Можно ли использовать этот подход с удалённым URL вместо локального файла?**  
A: Конечно. Просто передайте строку URL в конструктор `Document` – песочница всё равно будет применять **device pixel ratio**, который вы задали.

**Q: Работает ли это на безголовых серверах?**  
A: Да. Aspose.HTML — чисто Java‑библиотека; графическая среда не требуется, что делает её идеальной для CI‑конвейеров.

**Q: Что делать, если моя страница использует шрифты, не установленные на сервере?**  
A: Добавьте ссылки на веб‑шрифты в HTML или внедрите шрифты через `@font-face`. Рендерер загрузит их так же, как обычный браузер.

## Wrap‑Up

Теперь у вас есть надёжный рабочий процесс **set device pixel ratio**, который позволяет **convert HTML to mobile**. 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}