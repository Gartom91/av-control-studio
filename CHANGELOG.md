# Releases · Wydania

## TAB5 0.3.1 — 2026-10-19

PL: Osobna poprawka płynności TAB5: bezpośrednia kompozycja DSI, PPA, kopiowanie fragmentów wipe/slide i próbkowanie zoom na dwóch rdzeniach. Pomiar sprzętowy: 15–58 kl./s zamiast 4–8 kl./s. Kontroler i aplikacje pozostają na 1.6.8. [Instalacja i pomiary](docs/releases/tab5-v0.3.1.md).

EN: Standalone TAB5 performance fix: direct DSI composition, PPA, strip copies for wipe/slide and dual-core zoom sampling. Physical-device timing: 15–58 fps instead of 4–8 fps. Controller and desktop apps remain at 1.6.8. [Installation and measurements](docs/releases/tab5-v0.3.1.md).

## 1.6.8 — 2026-10-19

PL: Pięć przejść stron: fade, wipe, wash, slide i zoom, ustawienia czasu/kierunku/tempa/koloru i podgląd w edytorze. Efekty działają we wspólnym rendererze Studio/Player/WWW/HDMI oraz natywnie na TAB5 z firmware 0.3.0. Pięć stron istniejącej Wirtualnej sali AV demonstruje animacje. Ulepszono OTA TAB5, ochronę przed cofaniem firmware i udostępnianie dołączonego obrazu przez aktualizację Runtime. [Opis i pobieranie](docs/releases/v1.6.8.md#polski).

EN: Five page transitions: fade, wipe, wash, slide and zoom, with duration, direction, easing, colour and editor preview. Effects use the shared Studio/Player/web/HDMI renderer and native TAB5 firmware 0.3.0. The existing five-page classroom demonstrates them. TAB5 OTA, downgrade protection and bundled firmware staging were improved. [Details and downloads](docs/releases/v1.6.8.md#english).

## 1.6.7 — 2026-10-18

PL: Naprawiono wszystkie 25 ustaleń audytu: logikę i protokoły, kontrolki i pliki Studio, sesję HDMI, odzyskiwanie aktualizacji, kontrakty API i dokumentację oraz trzy problemy bezpieczeństwa. Lokalny symulator używa prywatnego poświadczenia właściciela zamiast wspólnego hasła. TAB5 0.2.5: kontrolki z samą akcją i blokada konfiguracji USB. Dodano regresje i zaktualizowano tekst podręcznika, zachowując jawne historyczne pochodzenie ilustracji. [Pełna lista i pobieranie](docs/releases/v1.6.7.md#polski).

EN: Fixed all 25 audit findings across logic and protocols, Studio controls and files, HDMI sessions, update recovery, API contracts and documentation, including three security issues. The local simulator uses a private owner credential instead of a shared password. TAB5 0.2.5 adds action-only controls and USB configuration locking. Added regression checks and revised handbook text while retaining explicit historical illustration provenance. [Full list and downloads](docs/releases/v1.6.7.md#english).

## 1.6.6 — 2026-10-12

PL: Poprawka HDMI Raspberry Pi, oficjalna obsługa TAB5 ST7123, biblioteka SD, parowanie i firmware 0.2.4 przez Wi‑Fi. Podręcznik ma 217 stron, 55 rozdziałów i 83 ilustracje. Pakiety i siedem bramek CI zbudowano lokalnie. [Szczegóły i pobieranie](docs/releases/v1.6.6.md#polski).

EN: Raspberry Pi HDMI fix, official TAB5 ST7123 support, SD panel library, pairing and Wi‑Fi firmware 0.2.4 updates. The handbook has 217 pages, 55 chapters and 83 illustrations. Packages and seven CI gates were built locally. [Details and downloads](docs/releases/v1.6.6.md#english).

## 1.6.5 — 2026-10-11

PL: Przycisk X ukrywa 100 rodzajów podpowiedzi i instrukcji w Studio. Ustawienia pozwalają wyszukać i przywrócić pojedynczy blok lub wszystkie naraz. Wybór jest zapamiętywany na stanowisku, także po restarcie. Pakiety zbudowano i sprawdzono lokalnie; pełny podręcznik Signal Workshop jest dołączony. [Szczegóły i pobieranie](docs/releases/v1.6.5.md#polski).

EN: X buttons hide 100 guidance topics in Studio. Settings support search, individual restoration and restoring everything. Preferences persist on the workstation across restarts. Packages were built and verified locally and include the full Signal Workshop handbook. [Details and downloads](docs/releases/v1.6.5.md#english).

## 1.6.4 — 2026-10-11

PL: Wydanie zawiera pełny, 206-stronicowy podręcznik Signal Workshop w instalatorach, obrazie RPi, dokumentacji i kursie offline. Poprawiono pięć luk potwierdzonych w przeglądzie Daybreak oraz inne błędy wykryte podczas kontroli. Nowe aktualizatory sprawdzają podpisany manifest; ograniczenie pierwszej aktualizacji ze starszej wersji opisano w informacji o wydaniu. [Szczegóły i pobieranie](docs/releases/v1.6.4.md#polski).

EN: This release includes the complete 206-page Signal Workshop handbook in the installers, Pi image, documentation and offline course. Five vulnerabilities confirmed by Daybreak and other reviewed defects were fixed. New updaters verify a signed manifest; the first upgrade from an older version is covered in the release notes. [Details and downloads](docs/releases/v1.6.4.md#english).

## 1.6.3 — rewizja dokumentacji / documentation revision — 2026-10-11

PL: Zweryfikowano treść i ilustracje głównego podręcznika względem aplikacji 1.6.3; poprawiono ścieżki UI, instrukcje Python/NumPy i bibliotek, debugger, transporty, diagnostykę, konta i klawiaturę oraz konfigurację Proton Mail. Nowy podręcznik ma **206 stron, 52 rozdziały, 4 dodatki, 74 aktualne zrzuty aplikacji i 3 diagramy**. Program: **10 sesji / 22 godziny**, opcjonalnie **1 godzina fizycznego HDMI**. Rewizję pobiera się osobno; instalatory, obraz RPi, Runtime i pierwotne załączniki 1.6.3 pozostają niezmienione. Aplikacje nadal mają osadzony wcześniejszy podręcznik; nowy zostanie osadzony w kolejnym wydaniu. [Szczegóły i pliki](docs/releases/v1.6.3.md#rewizja-dokumentacji-20261011).

EN: Reviewed the original handbook's text and illustrations against application 1.6.3; corrected UI paths, Python/NumPy and library instructions, debugger, transports, diagnostics, accounts/keyboard and Proton Mail setup. The revised handbook contains **206 pages, 52 chapters, 4 appendices, 74 current application screenshots and 3 diagrams**. Programme: **10 sessions / 22 hours**, with an optional **1-hour physical HDMI module**. Download the revision separately; 1.6.3 installers, Pi image, Runtime and original release assets remain unchanged. Applications still embed the earlier handbook; the next release will include the revision. [Details and downloads](docs/releases/v1.6.3.md#documentation-revision-20261011).

## 1.6.3 — 2026-10-10

PL: Naprawa przezroczystego okna konta i niewidocznych pól hasła. Niezależne okno, motywy Studio i panelu, układ responsywny, przewijanie nad klawiaturę i testy natywnych rendererów. Podręcznik i program zaktualizowane w miejscu. [Pełny opis](docs/releases/v1.6.3.md#polski).

EN: Fixed the transparent account dialog and invisible password fields. Independent dialog, Studio and panel palettes, responsive layout, keyboard scrolling and native renderer checks. The original handbook and training programme are updated in place. [Full notes](docs/releases/v1.6.3.md#english).

## 1.6.2 — 2026-10-10

PL: Poprawka fokusu klawiatury wirtualnej i obowiązkowe testy regresji. Agent 1.1.1, kreator Proton Mail na TECHNIKAV 0.12.408, podręcznik 195 stron / 75 ilustracji. [Pełny opis](docs/releases/v1.6.2.md#polski).

EN: Virtual keyboard focus fix with mandatory regression checks. Agent 1.1.1, Proton Mail wizard on TECHNIKAV hosting 0.12.408, 195-page handbook / 75 illustrations. [Full notes](docs/releases/v1.6.2.md#english).

## 1.6.1 — 2026-10-10

PL: **Wydanie testowe:** odtworzono błąd fokusu klawiatury; poprawka jest w 1.6.2.

EN: **Prerelease:** a keyboard focus race was reproduced; fixed in 1.6.2.

PL: Agent 1.1.1: poprawka fałszywego alarmu systemu plików. Kreator Proton Mail w TECHNIKAV, szyfrowany token SMTP, test bez wysyłki i harmonogram. Podręcznik 195 stron / 75 ilustracji. [Pełny opis](docs/releases/v1.6.1.md#polski).

EN: Agent 1.1.1 fixes the false read-only filesystem alarm. TECHNIKAV Proton Mail wizard, encrypted SMTP token, no-mail connection test and scheduling. Handbook: 195 pages / 75 illustrations. [Full notes](docs/releases/v1.6.1.md#english).

## 1.6.0 — 2026-10-10

PL: Powitanie i metryka projektu, autonomiczna diagnostyka i raporty TECHNIKAV, tła/9-slice, klawiatura PC ukryta domyślnie i HDMI włączona, główny podręcznik 191 stron. [Pełny opis](docs/releases/v1.6.0.md#polski).

EN: Welcome/project records, autonomous diagnostics and TECHNIKAV reports, backgrounds/nine-slice, PC keyboard hidden by default and HDMI enabled, 191-page integrated handbook. [Full notes](docs/releases/v1.6.0.md#english).

## 1.5.5 — 2026-10-10

PL: Konta i hasła, logowanie do WWW/Player/HDMI, opcjonalne pamiętanie, wysuwana klawiatura z Alt/Shift i jednakowymi klawiszami; poprawka APT offline.

EN: Accounts/passwords, browser/Player/HDMI sign-in, optional remembered sessions, sliding Alt/Shift keyboard with equal keys; offline APT fix.


**[English README](README.en.md) · [Polski README](README.pl.md)**

Every release has matching Polish and English notes. Download the packages from [GitHub Releases](https://github.com/Gartom91/av-control-studio/releases).

Każde wydanie ma odpowiadający sobie opis po polsku i angielsku. Pakiety pobierzesz z [GitHub Releases](https://github.com/Gartom91/av-control-studio/releases).

| Version / Wersja | Date / Data | Changes / Zmiany | Files / Pliki |
| --- | --- | --- | --- |
| **1.5.4** | 2026-10-10 | [PL: lokalny panel HDMI i USB](docs/releases/v1.5.4.md#polski) · [EN: local HDMI/USB operator kiosk](docs/releases/v1.5.4.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.4) |
| **1.5.3** | 2026-10-10 | [PL: wyszukiwane, stylizowane menu projektów](docs/releases/v1.5.3.md#polski) · [EN: searchable themed project menu](docs/releases/v1.5.3.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.3) |
| **1.5.2** | 2026-10-10 | [PL: wyróżniony selektor projektu](docs/releases/v1.5.2.md#polski) · [EN: prominent project selector](docs/releases/v1.5.2.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.2) |
| **1.5.1** | 2026-10-10 | [PL: układ, osobny debugger i poprawki](docs/releases/v1.5.1.md#polski) · [EN: workspace, detached debugger and fixes](docs/releases/v1.5.1.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.1) |
| **1.5.0** | 2026-10-10 | [PL: Signal Workshop, Python, debugger i wygląd](docs/releases/v1.5.0.md#polski) · [EN: Signal Workshop, Python, debugger and appearance](docs/releases/v1.5.0.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.0) |
| **1.4.1** | 2026-10-09 | [PL: dodatkowy LAN, ekspandery i szkolenie](docs/releases/v1.4.1.md#polski) · [EN: extra LAN, serial gateways and training](docs/releases/v1.4.1.md#english) | [Release / Wydanie](https://github.com/Gartom91/av-control-studio/releases/tag/v1.4.1) |

Release 1.4.1 was moved here with unchanged application packages. Earlier development history remains in the private source repository; the original MIT terms remain valid.

Wydanie 1.4.1 przeniesiono tutaj bez zmiany pakietów aplikacji. Wcześniejsza historia pozostaje w prywatnym repozytorium źródeł; pierwotne warunki MIT zachowują ważność.
