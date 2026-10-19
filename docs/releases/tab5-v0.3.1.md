# TAB5 0.3.1 — poprawka płynności przejść

Wersja przyspiesza pięć animacji na TAB5 ST7123. Kontroler pozostaje na 1.6.8.
Kompozycja trafia bezpośrednio do bufora DSI. Fade i wash korzystają z PPA,
zoom dzieli próbkowanie obrazu między dwa rdzenie i przekazuje mieszanie do PPA.
Wipe kopiuje jedynie nowo odsłaniany pasek; slide kopiuje całe ciągłe fragmenty.
Usunięto dodatkowe czekanie po zakończeniu obliczania każdej klatki.

## Pomiar na fizycznym TAB5

Ten sam panel szkoleniowy, pięć stron, czas 520 ms. Każde przejście uruchomiono
przez rzeczywisty przycisk nawigacji firmware. Podczas ruchu nie odpytywano USB
ani nie wykonywano zrzutów ekranu. FPS = (liczba klatek − 1) / czas przejścia.

| Efekt | 0.3.0 kl./s | 0.3.1 kl./s | Klatki 0.3.1 | Przyspieszenie |
| --- | ---: | ---: | ---: | ---: |
| wipe | 8.05 | 58.14 | 31 | 7.22× |
| wash | 6.77 | 39.43 | 23 | 5.82× |
| slide | 7.23 | 29.74 | 17 | 4.11× |
| zoom | 4.19 | 15.15 | 10 | 3.62× |
| fade | 4.82 | 30.52 | 18 | 6.33× |

Akcelerator przeszedł na urządzeniu test RGB565 i jednolitego koloru wash.
Brak błędów PPA i awaryjnych pominięć przejść. Potwierdzony rozruch OTA,
połączenie z kontrolerem oraz zachowanie siedmiu zapisanych paneli.
Projekt szkoleniowy pozostał na opublikowanej rewizji 23; przywrócono stronę Sala.
Kontroler 1.6.8 jest zdrowy i zachował certyfikat TLS.

Zoom pozostaje najcięższym efektem: około 15 kl./s, wobec około 4 kl./s wcześniej.
Pomiar przez USB nie stanowi odbioru fizycznego dotyku ani obserwacji płynności LCD
przez użytkownika. Obserwacja braku błysków podczas OTA 0.3.0 nie jest nowym
potwierdzeniem wizualnym aktualizacji 0.3.1.

## Instalacja

1. Pobierz `AV-Control-TAB5-ST7123-0.3.1-OTA.bin` z [wydania TAB5 0.3.1](https://github.com/Gartom91/av-control-studio/releases/tag/tab5-v0.3.1).
2. Na kontrolerze 1.6.8 otwórz **Ustawienia → Panele M5Stack TAB5**.
3. W **Plik firmware TAB5** dodaj pobrany plik. Wybierz **0.3.1** i **Aktualizuj firmware** przy swoim TAB5.
4. Poczekaj na **Aktualizacja potwierdzona · 0.3.1 · 100%**.

Panel z ustawionymi przejściami pozostaje zapisany; nie wymaga ponownego wysyłania.
ZIP jest pakietem do pierwszej instalacji lub odzyskania przez USB. Zwykła
aktualizacja Wi-Fi zapisuje aplikację w drugim slocie i zachowuje NVS oraz bibliotekę.
Wydanie nie zastępuje ani nie zmienia podpisanych pakietów aplikacji 1.6.8 i firmware 0.3.0.

## Weryfikacja źródeł i artefaktów

- Commit źródeł: `d7b22fc950a43f3d1358a44f8e4b9377ff4104ab`.
- Źródła produktu: `440167a47105e2b54b6e964b8ff21cfe633e2093de343d952cae3be02e8406a6`.
- SDK i partycje zachowują profil pre-v3, PSRAM XIP i sprzętowy rollback.
- 1100 klatek porównania RGB565: identyczny wynik dla pięciu efektów i czterech kierunków.
- ASan/UBSan: bez błędów; dodatkowo sprawdzono narastający wipe i podział zoom między rdzenie.
- 15 testów OTA i sesji firmware na Linux: zaliczone.
- [Raport pomiaru](../verification/tab5-transitions-0.3.1.json).

Manifest wydania obejmuje skróty pakietów i raportu. Podpis P-256 weryfikuje
się dotychczasowym publicznym kluczem AV Control.
