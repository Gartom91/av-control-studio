# Weryfikacja AV Control 1.6.6

## Zakres wydania

Wydanie łączy poprawkę rysowania lokalnego kiosku HDMI z obsługą M5Stack TAB5 ST7123: parowaniem, wysyłaniem wybranych stron z projektanta lub ustawień Studio, biblioteką SD oraz aktualizacją firmware przez Wi‑Fi. Zachowuje ukrywanie instrukcji przyciskiem X i przywracanie ich w ustawieniach.

Firmware TAB5 ma wersję **0.2.4**. Kopia panelu odczytana z pamięci wewnętrznej lub SD wymaga pobrania właściwego dokumentu z kontrolera przed włączeniem sterowania. Zmiana układu unieważnia stare odczyty, dotknięcia i oczekujące żądania. Skanowanie biblioteki ma ograniczenia liczby plików, stron, rozmiaru etykiet i danych.

## HDMI: potwierdzony wynik na RPi 4B

[Raport naprawy z 12 października](WERYFIKACJA-HDMI-2026-10-12.md) obejmuje rzeczywistą malinę 4B, monitor 2560 × 1440, zapis ekranu przed i po zmianie oraz potwierdzenie właściciela: obraz jest poprawny. Zmiana ustawia `WEBKIT_DISABLE_DMABUF_RENDERER=1` w usłudze kiosku. Zrestartowano kiosk; silnik i dane instalacji pozostały zachowane.

Próbę fizyczną wykonano na istniejącym **1.6.5 z poprawką**. Poprawkę włączono do obrazu i aktualizacji 1.6.6. [Sprawdzenie nowego obrazu](evidence/hdmi-1.6.6/image.json) oraz [natywnego GTK/WebKit na wirtualnym Wayland](evidence/hdmi-1.6.6/kiosk-view.json) są osobnymi próbami. Wirtualne wyjście nie zastępuje rozruchu nowej fizycznej karty SD.

## TAB5: sprzęt i nowe pliki

[Odbiór TAB5](WERYFIKACJA-TAB5.md) dokumentuje prototyp **0.2.3** przed integracją wydania: USB, potwierdzoną aktualizację OTA, zachowanie ustawień i parowania, kartę exFAT oraz przełączanie dwóch różnych paneli z 12 i 19 elementami. Zrzuty pochodzą z pamięci obrazu tego urządzenia.

Nowe binaria **0.2.4** mają osobny [raport pakowania](evidence/tab5-1.6.6.json), skrót źródeł i sumy czterech obrazów do USB. Pakiet OTA zawiera tylko aplikację. Pierwsza instalacja używa bootloadera, tablicy partycji, selektora OTA i aplikacji pod adresami podanymi w pakiecie; nie wymaga rutynowego wymazywania ustawień.

Test interfejsu Studio sprawdza parowanie, podgląd i wysyłanie panelu, potwierdzenie odbioru, aktualizację firmware oraz odwołanie dostępu. Test przenośnego komponentu C++ sprawdza stan po starcie i odczycie SD, tę samą rewizję, spóźnione odpowiedzi, oczekujące polecenia i powrót po sprawdzeniu dokumentu przez kontroler.

**Fizyczne wgranie i odbiór nowych binariów 0.2.4 nie są potwierdzone.** Wyników prototypu 0.2.3 nie przenosimy na nowy hash aplikacji. Nie wykonano wymuszonego zaniku zasilania, błędnego startu aplikacji ani próby Secure Boot/eFuse.

## Przegląd bezpieczeństwa i naprawa

Przegląd Codex Security obejmował niezmienny zakres od bazy `b455bc9` do integracji `d408d04`, 20 pozycji zmiany. Zgłoszono jeden problem o niskiej wadze: równoczesne dopuszczanie strumieni TAB5 mogło przekroczyć limit dwóch połączeń jednego urządzenia. Wymagało to ważnego, sparowanego urządzenia i bieżącego panelu; nie wykazano awarii całego kontrolera.

Przed poprawką osiem rzeczywistych żądań HTTP do izolowanego Uvicorn dopuściło cztery strumienie utrzymane równocześnie przez dwie sekundy. Po poprawce dopuszczono **dwa**, pozostałe sześć otrzymało HTTP 429. Rezerwacja jest wykonywana przed utworzeniem odpowiedzi i zwalniana także przy przerwaniu, anulowaniu lub błędzie przed rozpoczęciem transmisji. [Dowód przed i po naprawie](evidence/hmi-stream-admission-1.6.6.json).

24 testy HMI i OTA przeszły lokalnie. Próby obejmują odwołanie dostępu, błędy nagłówka odpowiedzi, anulowanie przed pierwszą ramką i zakończenie podglądu. Dwa przypadki dotyczące fizycznie zmienionej karty SD były poza zakresem polityki audytu; mimo to wprowadzono opisane wyżej sprawdzanie panelu i ograniczenia biblioteki. Audyt pierwotnej zmiany oraz sprawdzenie napraw mają odrębne dowody; nie jest to deklaracja braku wszystkich możliwych luk.

## Aplikacje, obraz i lokalne CI

Brama publikacji wymaga powodzenia **siedmiu zadań na lokalnych runnerach dla dokładnego commitu**: firmware TAB5, kiosk, interfejs, pakiet Windows, Player Linux i silnik na Windows oraz Linux. Manifest zapisuje nazwy runnerów i etykiety `self-hosted` oraz `av-control-local`. Budowanie instalatorów i obrazu także wykonano na lokalnym Windows i w lokalnym środowisku Linux; minuty runnerów GitHub nie są używane.

Raporty pakietów obejmują:

- [Studio: instalacja, natywny WebView2 i odinstalowanie](evidence/installation-1.6.6.json), [praca aplikacji](evidence/native-studio-1.6.6.json) i [CPython z NumPy z wheel offline](evidence/python-native-windows-1.6.6.json).
- [Player i Imager: instalacja oraz próby natywne](evidence/companions-installation-1.6.6.json). Imager pozostaje w Program Files; nie zapisano fizycznej karty.
- [Skompilowany pakiet Player Linux](evidence/linux-player-1.6.6.json): logowanie, przypięcie TLS, sterowanie, pełny ekran, blokada administracji i brak powtarzania poleceń po powrocie sieci.
- [ARM64 w emulatorze](evidence/arm-1.6.6.json), [UART czystego obrazu](evidence/uart-clean-image-1.6.6.json) i [migracja starego aktualizatora 1.5.3 do 1.6.6](evidence/update-arm-1.6.6.json), wraz z zachowaniem danych i powrotem po błędzie kontroli zdrowia.
- [Powiązanie sprawdzonych plików z wejściami budowania](evidence/package-verification-1.6.6.json). Podpisany manifest i SHA256 są osobnymi załącznikami wydania.

## Podręcznik

Rewizja z **12 października 2026** ma **217 stron, 55 rozdziałów, cztery dodatki i 83 ilustracje**: 80 ekranów i trzy diagramy. Rozdziały 53–55 opisują TAB5, bibliotekę SD, firmware przez Wi‑Fi, HDMI oraz ukrywanie i przywracanie instrukcji. Program zawiera 22 godziny podstawy, opcjonalny moduł HDMI 60 minut oraz TAB5 90 minut.

**217/217 stron PDF obejrzano indywidualnie — PASS.** [Rejestr stron](tutorial/page-review.json) i [raport PDF](tutorial/workshop-verification.json) wiążą kontrolę z SHA256 `acf495d51676dc45d4da50dadb9918c4a592d4e6d2ba1e12cfb6be9bfe4a0ecf`. Każda zmieniona strona była oglądana ponownie; wcześniejsze oględziny przyjęto tylko dla identycznych bajtowo PNG. Sprawdzono 99 lokalnych odnośników i pochodzenie wszystkich ilustracji. Ten sam PDF musi znajdować się w trzech aplikacjach Windows i aktualizacji ARM.

[Integracja podręcznika ze Studio 1.6.6](evidence/training-1.6.6.json) sprawdza hashe wszystkich 83 ilustracji, pobranego finalnego PDF i programu, lokalne odnośniki, 59 nagłówków oraz ćwiczenia operatora i geometrię portów. Próba przeszła bez błędów JavaScript, w izolowanym symulatorze z wyłączonymi transportami fizycznymi.

[Zgodność podręcznika w paczkach](evidence/packaged-handbook-1.6.6.json) potwierdza identyczne bajty końcowego PDF i treści Markdown w trzech aplikacjach Windows, obu kopiach w aktualizacji ARM oraz obu kopiach w obrazie RPi. Odświeżony instalator Imagera ponownie przeszedł instalację i próbę natywną w Program Files; zapisano hashe faktycznie zainstalowanego obrazu i PDF.

Starsze ilustracje i audyty zachowują pierwotne daty, wersje i zakres prób. Nowe widoki Studio przedstawiają izolowany symulator 1.6.6; fizyczne obrazy TAB5 i HDMI są oznaczone własnymi wersjami. Symulacja telefonu, sieci lub hostingu nie jest fizycznym odbiorem urządzeń.

## Pozostałe granice

Pełna fizyczna aktualizacja 1.6.6 i rozruch nowej SD pozostają niezweryfikowane. Dotyczy to też RPi 3B/5, dotyku USB, transmisji elektrycznej UART/RS232/RS485/GPIO, zakupionych konwerterów i fizycznych urządzeń mobilnych. Starsze testy parametrów silnika i usług pozostają oznaczoną wersją bazą odniesienia. Instalatory produktu nie mają podpisu Authenticode; producentów WebView2 i Raspberry Pi Imager sprawdzono osobno. Nie wysyłano rzeczywistej poczty i nie wykonywano nowego wdrożenia na hostingu.
