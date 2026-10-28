---
category: general
date: 2026-04-23
description: Применяйте стиль шрифта программно и узнайте, как удалить подчеркивание
  из текста, изменить стиль текста и установить полужирный текст программно в кратком
  руководстве.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: ru
og_description: Применяйте стиль шрифта программно и узнайте, как удалить подчеркивание
  текста, изменить стиль текста и установить полужирный шрифт программно в коротком
  практическом руководстве.
og_title: Применение стиля шрифта программно — Краткое руководство по C#
tags:
- csharp
- ui
- text-formatting
- programming
title: Применение стиля шрифта программно — Краткое руководство по C#
url: /ru/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применение стиля шрифта программно – Краткое руководство C#

Когда‑то вам нужно было **применить стиль шрифта** к элементу UI, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этим, когда впервые пробуют динамическое форматирование текста. Хорошая новость? Через несколько минут вы точно будете знать, как изменить внешний вид метки, убрать подчеркивание из текста и задать жирный шрифт программно, не копаясь в бесконечных документах.

В этом **уроке по форматированию текста** мы пройдем полный, готовый к запуску пример, объясним «почему» каждой строки и добавим практические советы, которые можно скопировать‑вставить в любой проект WinForms или WPF. Без лишних слов, только то, что действительно работает.

---

## Что вы узнаете

- Как **применить стиль шрифта** с помощью небольшого вспомогательного класса.  
- Точные шаги для **удаления подчеркивания из текста**, оставляя остальные стили нетронутыми.  
- Способы **изменения стиля текста** (жирный, курсив, подчеркивание) «на лету».  
- Полный, готовый к копированию фрагмент, который **задает жирный текст программно**.  
- Распространённые подводные камни и обработка граничных случаев, чтобы вас не удивило позже.

**Предварительные требования:** .NET 6+ (или любой современный .NET Framework), базовые знания C#, и IDE по вашему выбору (Visual Studio, Rider или VS Code). Всё — без дополнительных пакетов NuGet.

---

## Шаг 1 – Применить стиль шрифта к вашему элементу управления

Суть любой операции **apply font style** — это перечисление `FontStyle`, комбинируемое с объектом `Font`. Чтобы код оставался чистым, мы обернём логику перечисления в небольшой класс `WebFontStyle`. Этот класс отражает свойства, которые вы видели в оригинальном фрагменте (`Bold`, `Italic`, `Underline`), и формирует значение `FontStyle`, которое можно передать в `Font`.

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**Почему это важно:**  
Изолируя логику построения флагов, вы избегаете разбросанных побитовых операций `|` по всему UI‑коду. Это проще читать, проще тестировать и — самое главное — делает намерение **apply font style** кристально ясным.

---

## Шаг 2 – Удалить подчеркивание из текста (и сохранить остальные стили)

Предположим, вы получили метку, которая уже подчёркнута, но дизайн требует обычного жирного текста. Вы не хотите терять жирность, удаляя подчеркивание. Здесь на помощь приходит класс `WebFontStyle`.

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**Ключевой момент:** Установка `Underline = false` явно сообщает помощнику *исключить* флаг подчеркивания. Если бы вы просто опустили эту строку, предыдущее подчеркивание осталось бы, что часто становится источником багов, когда разработчики меняют только свойство `Bold`.

---

## Шаг 3 – Изменить стиль текста: жирный, курсив и прочее

Вы можете задаться вопросом: «А что, если нужно переключить курсив тоже?» Тот же объект работает для любой комбинации. Ниже представлена быстрая таблица, к которой можно обращаться во время кодинга.

| Требуемый стиль | `Bold` | `Italic` | `Underline` |
|-----------------|--------|----------|-------------|
| **Только жирный** | true   | false    | false       |
| *Только курсив*   | false  | true     | false       |
| **Жирный + Курсив** | true   | true     | false       |
| **Жирный + Подчёркнутый** | true   | false    | true        |

Просто задайте нужные свойства и вызовите `ToFont`. Помощник выполнит всю тяжёлую работу за вас, позволяя сосредоточиться на логике UI.

---

## Полный пример – Задать жирный текст программно

Ниже представлен **полный, готовый к запуску пример WinForms**, демонстрирующий всё, что мы рассмотрели. Вставьте его в новый проект WinForms в стиле console‑style и нажмите **F5**.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### Ожидаемый результат

При запуске программы появится окно с текстом **«Hello, world!»**, отображённым **жирным**, **не курсивом** и **без подчеркивания**. Этот визуальный результат подтверждает, что логика **apply font style** отработала безупречно.

---

## Профессиональные советы и граничные случаи

- **Динамические обновления:** Если нужно изменить стиль после отображения формы (например, в ответ на чекбокс), просто создайте новый экземпляр `WebFontStyle` или измените его свойства и переустановите `lbl.Font`. UI обновится мгновенно.  
- **Учёт High‑DPI:** При замене объекта `Font` Windows автоматически масштабирует его в соответствии с текущим DPI. Дополнительный код не требуется, если только вы не обрабатываете масштабирование вручную.  
- **Эквивалент в WPF:** В WPF вы будете привязывать `FontWeight`, `FontStyle` и `TextDecorations` вместо замены объекта `Font`. Та же логическая разъединённость применима — держите логику стилей вне уровня представления.  
- **Избежание утечек памяти:** Переустановка `Label.Font` создаёт новый объект `Font`. При частой смене стилей освобождайте старый: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Заключение

Теперь вы знаете, как **apply font style** к любому элементу .NET, **удалять подчеркивание из текста** и **изменять стиль текста** «на лету», сохраняя код чистым и переиспользуемым. Маленький помощник `WebFontStyle` превращает несколько булевых флагов в надёжный, тестируемый компонент, а полный пример доказывает, что вы можете **задать жирный текст программно** всего в несколько строк.

Что дальше? Попробуйте сочетать этот подход с пользовательскими настройками или поэкспериментируйте с другими флагами `FontStyle`, такими как `Strikeout`. Вы даже можете создать небольшую панель UI, позволяющую нетехническим пользователям выбирать жирный, курсив или подчеркивание во время выполнения — без необходимости перекомпиляции.

Если этот **урок по форматированию текста** оказался полезным, оставьте комментарий или поделитесь своими вариантами. Приятного кодинга, и пусть ваш UI всегда выглядит именно так, как вы задумали! 

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}