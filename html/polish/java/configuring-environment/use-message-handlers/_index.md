---
date: 2026-02-10
description: Dowiedz się, jak używać Aspose do obsługi uszkodzonych linków w Javie,
  konwertować HTML na PNG i ładować dokument HTML w Javie przy użyciu Aspose.HTML
  for Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konwertuj HTML do PNG przy użyciu obsługiwaczy komunikatów Aspose.HTML w Javie
url: /pl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie HTML do PNG przy użyciu obsługi wiadomości Aspose.HTML w Javie

## Introduction
W tym samouczku dowiesz się, **jak konwertować HTML do PNG** przy jednoczesnym eleganckim obsługiwaniu brakujących zasobów przy użyciu Aspose.HTML dla Javy. Przejdziemy przez tworzenie małej strony HTML, która odwołuje się do nieistniejącego obrazu, podłączenie **niestandardowego obsługiwacza wiadomości** do **przechwytywania żądań sieciowych**, konfigurację **usługi sieciowej**, załadowanie dokumentu oraz ostateczne wykonanie **konwersji HTML do obrazu**. Po zakończeniu będziesz mieć solidny wzorzec zarówno dla **obsługi zepsutych linków java**, jak i wysokiej jakości wyjścia PNG — idealny do raportów, miniatur lub podglądów e‑mail.

## Quick Answers
- **Co robi obsługiwacz wiadomości?** Przechwytuje operacje sieciowe (np. żądania obrazów) i pozwala reagować na kody statusu, takie jak 404.  
- **Czy Aspose.HTML może konwertować HTML do PNG?** Tak — `Converter.convertHTML` wykonuje konwersję w jednym wywołaniu.  
- **Czy potrzebna jest licencja do tego przykładu?** Tymczasowa licencja usuwa ograniczenia wersji ewaluacyjnej; stała licencja jest wymagana w środowisku produkcyjnym.  
- **Jaką wersję Javy obsługuje?** Dowolny JDK 8+ (przykład działa na JDK 11).  
- **Czy mogę skonfigurować usługę sieciową?** Oczywiście — użyj `configuration.getService(INetworkService.class)`, aby dodać swój obsługiwacz.

## Prerequisites
Zanim zaczniemy, upewnij się, że masz przygotowane następujące elementy:

1. **Java Development Kit (JDK)** – pobierz ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – pobierz bibliotekę ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans sprawdzą się doskonale.  
4. **Podstawowa znajomość Javy** – powinieneś być zaznajomiony z klasami, try‑with‑resources oraz obsługą wyjątków.  
5. **Tymczasowa licencja** – jeśli korzystasz z wersji próbnej, zdobądź [tymczasową licencję](https://purchase.aspose.com/temporary-license/), aby uniknąć znaków wodnych.

## Import Packages
Najpierw zaimportuj klasę Java I/O, której będziemy potrzebować do obsługi plików. Reszta klas Aspose jest odwoływana pełnymi nazwami później, co utrzymuje listę importów schludną.

```java
import java.io.IOException;
```

## Step 1: Prepare the HTML Code
Krok 1: Przygotuj kod HTML  
Tworzymy minimalny fragment HTML, który celowo odwołuje się do brakującego obrazu. To spowoduje wywołanie naszego obsługiwacza, gdy silnik spróbuje pobrać zasób.

```java
String code = "<img src='missing.jpg'>";
```

## Step 2: Write the HTML Code to a File
Krok 2: Zapisz kod HTML do pliku  
Następnie zapisujemy fragment do *document.html*. Użycie bloku try‑with‑resources zapewnia, że `FileWriter` zostanie prawidłowo zamknięty.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Step 3: Write a Custom Message Handler
Krok 3: Napisz własny obsługiwacz wiadomości  
Teraz tworzymy **niestandardowy obsługiwacz wiadomości**, który sprawdza kod statusu HTTP każdego żądania sieciowego. Jeśli odpowiedź nie jest `200`, logujemy przyjazne ostrzeżenie. Zwróć uwagę na wywołanie `invoke(context);` na końcu — przekazuje ono żądanie do kolejnego obsługiwacza w łańcuchu, zapobiegając rekurencji.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Step 4: Configure the Network Service
Krok 4: Skonfiguruj usługę sieciową  
Aby Aspose.HTML był świadomy naszego obsługiwacza, pobieramy **usługę sieciową** z instancji `Configuration` i dodajemy obsługiwacz do jej kolekcji. To jest krok, w którym **konfigurujemy usługę sieciową** dla niestandardowego zachowania.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Step 5: Load the HTML Document
Krok 5: Załaduj dokument HTML  
Po przygotowaniu konfiguracji ładujemy *document.html*. Silnik teraz używa naszej usługi sieciowej, więc żądanie brakującego obrazu jest przechwytywane przez właśnie dodany obsługiwacz.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Step 6: Convert HTML to PNG
Krok 6: Konwertuj HTML do PNG  
Oto serce procesu **konwersji HTML do obrazu**. Metoda `Converter.convertHTML` przyjmuje załadowany `HTMLDocument`, opcjonalne `ImageSaveOptions` (gdzie możesz dostosować DPI lub jakość) oraz nazwę pliku wyjściowego.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Step 7: Clean Up Resources
Krok 7: Posprzątaj zasoby  
Dobre praktyki Javy nakazują zwolnienie wszystkich zasobów natywnych. Blok `finally` zapewnia, że `Configuration` zostanie zwolniona, nawet jeśli wyjątek zostanie wyrzucony.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Why Use Message Handlers?
Dlaczego używać obsługiwaczy wiadomości?  
Obsługiwacze wiadomości dają **precyzyjną kontrolę** nad każdym żądaniem sieciowym — czy to obraz, CSS, JavaScript, czy plik czcionki. Zamiast pozwalać bibliotece na ciche niepowodzenie, możesz logować brakujące zasoby, dostarczać treść zastępczą lub nawet ponowić żądanie. Dzięki temu Twój potok przetwarzania HTML staje się **solidny**, **gotowy do produkcji** i łatwiejszy w debugowaniu.

## Common Issues and Solutions
Typowe problemy i rozwiązania
- **Rekurencja obsługiwacza** — wywołaj `invoke(context);` tylko raz, aby uniknąć nieskończonych pętli.  
- **Brak licencji** — bez ważnej licencji wygenerowany PNG będzie zawierał znak wodny.  
- **Nieprawidłowe ścieżki plików** — używaj ścieżek bezwzględnych lub poprawnie ustaw katalog roboczy przy ładowaniu `document.html`.  
- **Nieobsługiwane typy zasobów** — upewnij się, że zasób, który chcesz przechwycić (obraz, CSS itp.) jest rzeczywiście żądany przez silnik HTML.

## Frequently Asked Questions
Najczęściej zadawane pytania

**P: Czy mogę łączyć wiele obsługiwaczy wiadomości?**  
O: Tak, możesz dodać kilka obsługiwaczy do kolekcji `network.getMessageHandlers()`; zostaną one wykonane w kolejności dodania.

**P: Czy obsługiwacz działa również dla zasobów CSS lub skryptów?**  
O: Absolutnie — każde żądanie sieciowe wykonywane przez silnik HTML (obrazy, CSS, JS, czcionki) przechodzi przez obsługiwacz.

**P: Jak zmienić żądanie HTTP przed jego wysłaniem?**  
O: Zaimplementuj obsługiwacz, który modyfikuje `context.getRequest()` przed wywołaniem `invoke(context)`.

**P: Czy istnieje sposób, aby wyciszyć ostrzeżenie dla konkretnych URL-i?**  
O: W obsługiwaczu sprawdź `context.getRequest().getRequestUri()` i warunkowo pomiń logowanie.

**P: Jakiej wersji Aspose.HTML wymaga ten kod?**  
O: Kod działa z Aspose.HTML for Java 22.10 i nowszymi.

## Conclusion
Podsumowanie  
Masz teraz kompletny, end‑to‑end przykład **jak konwertować HTML do PNG** przy użyciu **niestandardowego obsługiwacza wiadomości**, aby **przechwytywać żądania sieciowe** i **obsługiwać zepsute linki java**. Konfigurując usługę sieciową, ładując dokument i wywołując konwerter, możesz niezawodnie generować miniatury PNG lub pełno‑stronne zrzuty ekranu w dowolnej aplikacji Java.

---

**Ostatnia aktualizacja:** 2026-02-10  
**Testowano z:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}