<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="media/logo-light.svg" />
  <img src="media/logo-dark.svg" width="310" alt="AV Control — Control Systems" />
</picture>

# Jedna instalacja. Twoje urządzenia. Twoja logika.

Projektuj panele, łącz urządzenia i steruj instalacją lokalnie.

**Polski · [English](README.en.md)**

[**Pobierz najnowsze wydanie**](https://github.com/Gartom91/av-control-studio/releases/latest) · [Historia wydań](CHANGELOG.md) · [Kurs szkoleniowy](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Szkolenie-1.4.0.zip)

**Windows · Raspberry Pi 3B / 4B / 5 · Panele w przeglądarce**

</div>

---

AV Control to konfigurowalna platforma do sal AV, ekspozycji i innych instalacji urządzeń. Samodzielnie definiujesz urządzenia, protokoły, panele operatora oraz logikę działania. Projekt pracuje na Raspberry Pi niezależnie od komputera użytego do projektowania. Codzienne sterowanie działa bez chmury i internetu.

To **oficjalne repozytorium dystrybucji**: instalatory, obrazy kontrolera, aktualizacje, instrukcje i raporty weryfikacji. Rozwój produktu i historia źródeł znajdują się w osobnym repozytorium prywatnym. Automatyczne archiwa GitHub „Source code” zawierają dokumentację tego repozytorium dystrybucji.

> **Aktualne wydanie stabilne: 1.4.1.** Nowy interfejs Signal Workshop, debugger i rozbudowane środowisko Python są w przygotowaniu. Poniżej opisujemy funkcje wydanej wersji.

## Wybierz aplikację

| Aplikacja | Do czego służy | Pobieranie 1.4.1 |
| --- | --- | --- |
| **Studio** | Konfiguracja urządzeń, projektowanie paneli i logiki, symulacja oraz publikowanie projektów. | [Instalator Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Studio-1.4.1-Windows-x64.exe) |
| **Player** | Obsługa opublikowanych paneli na osobnym komputerze, także na pełnym ekranie. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Player-1.4.1-Windows-x64.exe) · [Linux .deb](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Player-1.4.1-Linux-all.deb) · [Archiwum Linux](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Player-1.4.1-Linux.tar.gz) |
| **Imager** | Zapis i weryfikacja karty SD; wybór modelu maliny oraz pierwsza konfiguracja konta i sieci. Zawiera obraz kontrolera. | [Instalator Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Imager-1.4.1-Windows-x64.exe) |
| **Kontroler RPi** | Samodzielne wykonywanie logiki i komunikacja z urządzeniami po zamknięciu Studio. | [Obraz SD, ARM64](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-RPi-1.4.1-arm64.img.xz) · [Aktualizacja Runtime](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Runtime-1.4.1-arm64.zip) |
| **Panel WWW** | Obsługa tych samych paneli z komputera, tabletu lub telefonu. | Otwórz adres HTTPS kontrolera; nie wymaga osobnego instalatora. |

Aplikacje Windows obsługują Windows 10 22H2 i Windows 11, x64. Instalatory dostarczają .NET oraz instalator WebView2 offline. Obraz RPi opiera się na Raspberry Pi OS Lite 64-bit. Pakiet Runtime aktualizuje istniejący kontroler AV Control — nie jest obrazem SD.

## Najważniejsze możliwości

| Obszar | Funkcje |
| --- | --- |
| **Połączenia** | Konwertery USB–RS232/RS485, UART maliny, klient/nasłuch TCP, UDP i cyfrowe GPIO. Stabilny wybór USB przez `by-id` lub `by-path`, wykrywanie konfliktów i diagnostyka. |
| **Rozbudowa sieci** | Dodatkowe adaptery USB–Ethernet na RPi; ekspandery szeregowe Ethernet/Wi-Fi z adresami kanałów, TCP/UDP oraz standardowym RFC2217, jeśli urządzenie go obsługuje. |
| **Własne protokoły** | Ramki ASCII/UTF-8/HEX, parametry, zakończenia ramek, kolejność bajtów, SUM/XOR/CRC, odczyt odpowiedzi, komunikaty spontaniczne i odpytywanie. Profile wielokrotnego użytku, adresy i porty konkretnej instalacji. |
| **Panele WYSIWYG** | Strony, przyciski, przełączniki, fadery, suwaki, pokrętła, wartości, kontrolki, teksty i grafiki. Przeciąganie, rozmiar, wyrównywanie, warstwy, grupy, cofanie/ponawianie i warianty PC/tablet/telefon. Import grafik, ukrywanie etykiet, ramki, zaokrąglenia i własny CSS. |
| **Logika graficzna** | Bramki z regulowaną liczbą wejść, działania, porównania, zbocza, timery, liczniki, trwałe pamięci, zatrzaski i przerzutniki. Impulsowy Interlock z SET ALL/CLEAR, edytowalna Truth table i moduły wielokrotnego użytku. |
| **Automatyzacja** | Komendy i sekwencje z opóźnieniami, warunkami, oczekiwaniem na odpowiedź, timeoutem i anulowaniem. Zezwolenia i wzajemne wykluczanie sprawdzane w silniku także dla API i wielu paneli. |
| **Symbole Python** | Typowane porty, parametry, pamięć, próba działania w aplikacji i podręcznik offline. Wersja 1.4.1 korzysta z ograniczonego środowiska symboli. |
| **Symulacja** | Wirtualne transporty, wymuszanie wejść, odpowiedzi, opóźnień i awarii; diagnostyka ramek, jakości sygnałów, pamięci, sekwencji i przyczyn blokad. |
| **Publikowanie** | Walidacja, przygotowanie i aktywacja projektu, historia wdrożeń oraz przywracanie. Aktualizacje Studio, Playera, Imagera i Runtime RPi ze sprawdzaniem SHA-256. RPi wykonuje kopię danych i powrót po nieudanym sprawdzeniu uruchomienia. |

Nie ma stałego limitu liczby urządzeń, stron ani bloków. Praktyczna pojemność zależy od kontrolera i obciążenia. Jeden kontroler wykonuje jeden aktywny projekt; Studio przechowuje wiele projektów i połączeń z kontrolerami.

![Panel operatora wydanej wersji — projekt szkoleniowy Wirtualna sala AV](media/operator-panel.png)

*Rzeczywisty zrzut z wydanego projektu szkoleniowego. Połączenia sprzętowe w przykładzie są wyłączone.*

## Zacznij bez sprzętu

1. Zainstaluj **Studio** z tabeli powyżej.
2. Zaloguj się do lokalnego symulatora: `admin` / `simulation`. Te dane dotyczą wyłącznie lokalnego symulatora.
3. Wybierz **Otwórz projekt szkoleniowy**, a następnie **Podręcznik szkoleniowy**.
4. Sprawdź panele i wybierz **Uruchom symulację**. Przed podłączeniem sprzętu skonfiguruj własne komendy.
5. Przygotuj kartę SD aplikacją **Imager**. Zapis obrazu usuwa zawartość wskazanej karty; najpierw sprawdź wybrany nośnik.
6. Opublikuj projekt. Do codziennej obsługi użyj **Playera** lub panelu WWW; Studio nie musi pozostawać otwarte.

## Nauka i weryfikacja

- [Kurs offline: HTML i projekt](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Szkolenie-1.4.0.zip) — 32 rozdziały, cztery dodatki, 39 screenshotów i trzy schematy.
- [Podręcznik PDF](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Studio-Tutorial-PL-1.4.0.pdf) — 116 stron; kurs 1.4.0 obejmuje również 1.4.1.
- [Pełna dokumentacja](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/AV-Control-Studio-1.4.1-Dokumentacja.zip) · [Ekspandery](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/EKSPANDERY-SIECIOWE-PL.md) · [USB, RS485 i UART](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/USB-RS485-UART-PL.md).
- [Weryfikacja wydania](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/WERYFIKACJA-1.4.1.md) · [Raport aktualizacji fizycznej 4B](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/WERYFIKACJA-RPI-1.4.1-PO-PUBLIKACJI.md).

Szczegółowy kurs i interfejs aplikacji są obecnie po polsku. README i opisy wydań są po polsku i angielsku.

Wyniki komputerowe, emulacja ARM64 i fizyczna 4B są raportowane oddzielnie. Nie potwierdzono fizycznej pracy 3B/5, rozruchu świeżej karty na wszystkich modelach, elektrycznej komunikacji UART/GPIO ani zakupionych adapterów. Zakres prób opisuje raport danego wydania. Instalatory AV Control nie mają obecnie podpisu Authenticode.

## Aktualizacje, integralność i licencja

Pobieraj pliki z sekcji **Assets** wydania. [SHA256-DISTRIBUTION.txt](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/SHA256-DISTRIBUTION.txt) i [DISTRIBUTION-MANIFEST.json](https://github.com/Gartom91/av-control-studio/releases/download/v1.4.1/DISTRIBUTION-MANIFEST.json) opisują publiczne pakiety. Pierwotny historyczny manifest wymienia także archiwum źródeł produktu wyłączone z tej dystrybucji.

Zainstalowane aplikacje nadal korzystają z `Gartom91/av-control-studio` do aktualizacji. Podział repozytoriów nie wymaga ponownego zapisu SD ani zmiany projektów. Sterowanie pozostaje lokalne; aktualizacje online wymagają internetu.

**Planowane nowe elementy produktu będą objęte własną EULA.** Historyczny tekst MIT dotyczy wcześniejszych wydań i pochodzących z nich części kodu; nie jest ogólną licencją wszystkich nowych elementów przyszłych wersji. Zobacz [zakres licencji](LICENSE).

Wcześniej wydane kopie MIT zachowują swoje warunki: [MIT dla 1.4.1](LICENSE-MIT-1.4.1.txt). Historyczne pakiety Python mogą zawierać czytelny kod Runtime; prywatne repozytorium źródeł nie oznacza uniemożliwienia analizy dystrybuowanych aplikacji.

[Projekt przyszłej EULA](EULA-PL-PROJEKT.md) wskazuje **osobę fizyczną** jako planowanego Licencjodawcę, z placeholderami imienia i nazwiska, adresu do korespondencji oraz e-maila. Rozważamy opcjonalne przyszłe opłaty; dokument nie uruchamia opłat ani nowych wiążących warunków. Licencje bibliotek innych autorów pozostają zachowane.

## Uwagi i zgłoszenia

[Zgłoś błąd lub propozycję funkcji](https://github.com/Gartom91/av-control-studio/issues). Podaj wersję, model kontrolera i sposób odtworzenia problemu. Usuń hasła, tokeny i adresy instalacji ze zrzutów oraz raportów.

[Format dwujęzycznych wydań](RELEASING.md) · [English](README.en.md) · [Wszystkie wydania](https://github.com/Gartom91/av-control-studio/releases)
