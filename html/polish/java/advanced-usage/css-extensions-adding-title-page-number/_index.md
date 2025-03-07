---
title: Dostosuj marginesy strony HTML za pomocą Aspose.HTML
linktitle: Rozszerzenia CSS - dodawanie tytułu i numeru strony
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak dostosowywać marginesy stron, dodawać numery stron i tytuły do dokumentów HTML, korzystając z Aspose.HTML dla Java.
weight: 10
url: /pl/java/advanced-usage/css-extensions-adding-title-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dostosuj marginesy strony HTML za pomocą Aspose.HTML

Aspose.HTML for Java to potężna biblioteka do przetwarzania dokumentów HTML w aplikacjach Java. W tym samouczku pokażemy, jak tworzyć niestandardowe marginesy stron i dodawać numery stron oraz tytuły do dokumentów HTML za pomocą Aspose.HTML for Java. Ten przewodnik krok po kroku podzieli proces na łatwe do opanowania kroki, aby pomóc Ci łatwo zintegrować te funkcje z dokumentami HTML.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że na swoim komputerze masz skonfigurowane środowisko programistyczne Java.

2.  Aspose.HTML dla Java: Pobierz i zainstaluj bibliotekę Aspose.HTML dla Java ze strony[Tutaj](https://releases.aspose.com/html/java/).

## Importuj pakiety

Aby rozpocząć, musisz zaimportować niezbędne pakiety z Aspose.HTML dla Java. Dodaj następujące polecenia importu do swojego kodu Java:

```java
// Importuj pakiety Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Teraz podzielimy proces dodawania niestandardowych marginesów stron, numerów stron i tytułów na łatwiejsze do wykonania kroki:

## Krok 1: Zainicjuj konfigurację i marginesy strony

```java
// Zainicjuj obiekt konfiguracji i ustaw marginesy strony dla dokumentu
Configuration configuration = new Configuration();
try {
    // Pobierz usługę User Agent
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Ustaw styl niestandardowych marginesów i utwórz na nich znaczniki
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

W tym kroku inicjujemy obiekt konfiguracji i konfigurujemy niestandardowe marginesy strony, łącznie z położeniem licznika stron i tytułem strony.

## Krok 2: Zainicjuj dokument HTML

```java
// Zainicjuj dokument HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Tutaj tworzymy dokument HTML z przykładową treścią (w tym przypadku komunikatem „Hello World”) i stosujemy konfigurację z kroku 1.

## Krok 3: Zainicjuj urządzenie wyjściowe i wyrenderuj dokument

```java
// Zainicjuj urządzenie wyjściowe
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Wyślij dokument do urządzenia wyjściowego
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

W tym kroku konfigurujemy urządzenie wyjściowe i renderujemy dokument HTML. Dokument zostanie przetworzony i zapisany jako plik XPS z określonymi marginesami strony, numerami stron i tytułem.

## Wniosek

Gratulacje! Udało Ci się nauczyć, jak tworzyć niestandardowe marginesy stron i dodawać numery stron oraz tytuły do dokumentów HTML za pomocą Aspose.HTML dla Java. Ta personalizacja pozwala Ci tworzyć bardziej profesjonalne i atrakcyjne wizualnie dokumenty.

 Jeśli masz jakiekolwiek pytania lub napotkasz jakiekolwiek problemy, możesz odwiedzić naszą stronę[Aspose.HTML dla dokumentacji Java](https://reference.aspose.com/html/java/) lub poszukaj pomocy na[Forum wsparcia Aspose](https://forum.aspose.com/).

## Najczęściej zadawane pytania

### P1: Czym jest Aspose.HTML dla Java?

A1: Aspose.HTML for Java to biblioteka Java oferująca zaawansowane narzędzia do pracy z dokumentami HTML w aplikacjach Java.

### P2: Czy mogę dodatkowo dostosować marginesy strony?

A2: Tak, możesz zmodyfikować style CSS w kroku 1, aby dostosować marginesy strony zgodnie ze swoimi wymaganiami.

### P3: Jak mogę dodać więcej treści do dokumentu HTML?

A3: Możesz zmodyfikować zawartość HTML w kroku 2, zastępując przykładową zawartość własną.

### P4: Czy Aspose.HTML dla Java jest kompatybilny z innymi formatami dokumentów?

A4: Tak, Aspose.HTML for Java można używać do konwersji dokumentów HTML do różnych formatów, w tym PDF, XPS i obrazów.

### P5: Czy potrzebuję licencji, aby używać Aspose.HTML dla Java?

 A5: Tak, możesz uzyskać licencję lub bezpłatną wersję próbną[Tutaj](https://purchase.aspose.com/buy) Lub[Tutaj](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
