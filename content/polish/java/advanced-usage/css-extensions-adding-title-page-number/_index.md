---
title: Dostosuj marginesy strony HTML za pomocą Aspose.HTML
linktitle: Rozszerzenia CSS - Dodawanie tytułu i numeru strony
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak dostosować marginesy strony, dodać numery stron i tytuły do dokumentów HTML za pomocą Aspose.HTML dla Java.
type: docs
weight: 10
url: /pl/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java to potężna biblioteka do przetwarzania dokumentów HTML w aplikacjach Java. W tym samouczku przyjrzymy się, jak tworzyć niestandardowe marginesy strony oraz dodawać numery stron i tytuły do dokumentów HTML za pomocą Aspose.HTML dla Java. Ten przewodnik krok po kroku podzieli proces na łatwe do wykonania kroki, które pomogą Ci łatwo zintegrować te funkcje z dokumentami HTML.

## Warunki wstępne

Zanim zaczniemy, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że na komputerze jest skonfigurowane środowisko programistyczne Java.

2.  Aspose.HTML dla Java: Pobierz i zainstaluj bibliotekę Aspose.HTML dla Java ze strony[Tutaj](https://releases.aspose.com/html/java/).

## Importuj pakiety

Aby rozpocząć, musisz zaimportować niezbędne pakiety z Aspose.HTML dla Java. Dodaj następujące instrukcje importu do kodu Java:

```java
// Importuj pakiety Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Podzielmy teraz proces dodawania niestandardowych marginesów strony, numerów stron i tytułów na łatwe do wykonania kroki:

## Krok 1: Zainicjuj konfigurację i marginesy strony

```java
// Zainicjuj obiekt konfiguracyjny i ustaw marginesy strony dokumentu
Configuration configuration = new Configuration();
try {
    // Uzyskaj usługę Agenta użytkownika
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

Na tym etapie inicjujemy obiekt konfiguracyjny i ustawiamy niestandardowe marginesy strony, w tym położenie licznika strony i tytuł strony.

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

Na tym etapie konfigurujemy urządzenie wyjściowe i renderujemy dokument HTML. Dokument zostanie przetworzony i zapisany jako plik XPS z określonymi marginesami strony, numerami stron i tytułem.

## Wniosek

Gratulacje! Pomyślnie nauczyłeś się tworzyć niestandardowe marginesy strony oraz dodawać numery stron i tytuły do dokumentów HTML za pomocą Aspose.HTML dla Java. To dostosowanie umożliwia tworzenie bardziej profesjonalnych i atrakcyjnych wizualnie dokumentów.

 Jeśli masz jakieś pytania lub napotkasz jakiekolwiek problemy, zapraszamy do odwiedzenia strony[Aspose.HTML dla dokumentacji Java](https://reference.aspose.com/html/java/) lub poproś o pomoc na stronie[Forum wsparcia Aspose](https://forum.aspose.com/).

## Często zadawane pytania

### P1: Co to jest Aspose.HTML dla Java?

O1: Aspose.HTML for Java to biblioteka Java zapewniająca zaawansowane narzędzia do pracy z dokumentami HTML w aplikacjach Java.

### P2: Czy mogę bardziej dostosować marginesy strony?

Odpowiedź 2: Tak, możesz modyfikować style CSS w kroku 1, aby dostosować marginesy strony zgodnie ze swoimi wymaganiami.

### P3: Jak mogę dodać więcej treści do dokumentu HTML?

O3: Możesz zmodyfikować treść HTML w kroku 2, zastępując przykładową treść własną.

### P4: Czy Aspose.HTML dla Java jest kompatybilny z innymi formatami dokumentów?

O4: Tak, Aspose.HTML for Java może być używany do konwersji dokumentów HTML do różnych formatów, w tym PDF, XPS i obrazów.

### P5: Czy potrzebuję licencji na używanie Aspose.HTML dla Java?

 Odpowiedź 5: Tak, możesz uzyskać licencję lub bezpłatną wersję próbną[Tutaj](https://purchase.aspose.com/buy) Lub[Tutaj](https://releases.aspose.com/).