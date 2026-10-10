<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="media/logo-light.svg" />
  <img src="media/logo-dark.svg" width="310" alt="AV Control â€” Control Systems" />
</picture>

# Jedna instalacja. Twoje urzÄ…dzenia. Twoja logika.

Projektuj panele, podĹ‚Ä…czaj urzÄ…dzenia i programuj instalacjÄ™ lokalnie.

**Polski Â· [English](README.en.md)**

[**Pobierz 1.6.1 â€” Signal Workshop**](https://github.com/Gartom91/av-control-studio/releases/tag/v1.6.1) Â· [Historia wydaĹ„](CHANGELOG.md) Â· [Kurs szkoleniowy](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Szkolenie-1.6.1.zip)

**Windows Â· Raspberry Pi 3B / 4B / 5 Â· Player Linux Â· Panele WWW**

</div>

---

AV Control to konfigurowalna platforma do sal AV, wystaw i innych instalacji. Definiujesz urzÄ…dzenia, protokoĹ‚y, panele i logikÄ™; Raspberry Pi wykonuje projekt samodzielnie po zamkniÄ™ciu Studio. Codzienne sterowanie dziaĹ‚a lokalnie, bez chmury i internetu.

To **oficjalne repozytorium dystrybucyjne**: instalatory, obrazy kontrolera, aktualizacje, instrukcje i raporty weryfikacji. ĹąrĂłdĹ‚a i historia rozwoju produktu znajdujÄ… siÄ™ w osobnym prywatnym repozytorium. Automatyczne archiwa â€žSource codeâ€ť GitHub zawierajÄ… dokumentacjÄ™ tego repozytorium dystrybucyjnego.

<picture>
  <source media="(prefers-color-scheme: light)" srcset="media/studio-light.png" />
  <img src="media/signal-workshop.png" alt="Signal Workshop â€” logika, sygnaĹ‚y, urzÄ…dzenia i uporzÄ…dkowane poĹ‚Ä…czenia" />
</picture>

*Rzeczywiste zrzuty aplikacji. PrzykĹ‚ady uĹĽywajÄ… wirtualnych transportĂłw i wyĹ‚Ä…czonych poĹ‚Ä…czeĹ„ sprzÄ™towych.*

## Wybierz aplikacjÄ™

| Aplikacja | Zastosowanie | Pobierz 1.6.1 |
| --- | --- | --- |
| **Studio** | UrzÄ…dzenia, protokoĹ‚y, panele i logika; symulacja, debugger i publikowanie. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Studio-1.6.1-Windows-x64.exe) |
| **Player** | ObsĹ‚uga opublikowanych paneli na osobnym komputerze, takĹĽe w peĹ‚nym ekranie. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Player-1.6.1-Windows-x64.exe) Â· [Linux .deb](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Player-1.6.1-Linux-all.deb) Â· [Archiwum Linux](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Player-1.6.1-Linux.tar.gz) |
| **Imager** | WybĂłr modelu RPi, ustawienia kont i sieci, zapis i weryfikacja karty SD. Obraz jest doĹ‚Ä…czony. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Imager-1.6.1-Windows-x64.exe) |
| **Kontroler RPi** | Samodzielne wykonywanie logiki i komunikacja z urzÄ…dzeniami. | [Obraz SD, ARM64](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-RPi-1.6.1-arm64.img.xz) Â· [Aktualizacja Runtime](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Runtime-1.6.1-arm64.zip) |
| **Panel WWW** | ObsĹ‚uga tych samych paneli na komputerze, tablecie lub telefonie. | OtwĂłrz adres HTTPS kontrolera. |

Windows: Windows 10 22H2 / Windows 11, x64; .NET i instalator WebView2 offline sÄ… doĹ‚Ä…czone. Publiczny Player Linux: Debian 13 / CPython 3.13 z GTK i WebKit. Obraz RPi: Raspberry Pi OS Lite 64-bit. Pakiet Runtime sĹ‚uĹĽy do aktualizacji istniejÄ…cego kontrolera AV Control.

## Signal Workshop

- **BieĹĽÄ…cy podglÄ…d logiki:** przeliczenie po zmianach i co okoĹ‚o 200 ms, bez publikowania; niezaleĹĽna pamiÄ™Ä‡ i reset podglÄ…du.
- **Rzetelny stan komunikacji:** gotowoĹ›Ä‡ gniazda UDP lub portu szeregowego jest odrĂłĹĽniona od aktualnej odpowiedzi; TCP korzysta z systemowego keepalive.
- **Powitanie i metryka projektu:** osobny ekran startowy, dane instalacji/klienta/zespoĹ‚u/serwisu, lista odbiorowa i historia.
- **Autonomiczna diagnostyka:** stan kontrolera, awarie komunikacji, brak odpowiedzi i incydenty; opcjonalne raporty i popup w TECHNIKAV oraz e-mail konfigurowany przez wĹ‚aĹ›ciciela.
- **Wprowadzanie tekstu:** klawiatura ekranowa domyĹ›lnie ukryta na PC/WWW, a wĹ‚Ä…czona na lokalnym HDMI. WĹ‚Ä…czysz jÄ… lokalnie w Ustawieniach, Moje konto lub ustawieniach logowania.
- **TĹ‚a panelu:** upload z inspektora, gradienty, kadrowanie/skala/pozycja/kafelki i naroĹĽniki 9-slice; wspĂłlny wyglÄ…d edytora i operatora.
- **Panel lokalny HDMI:** automatyczny kiosk na Raspberry Pi, mysz/touchpad/dotyk USB, strona poczÄ…tkowa i konsola tty2. [Instrukcja i Ä‡wiczenia](docs/PANEL-HDMI-PL.md).
- **Jeden obszar logiki:** urzÄ…dzenia, sygnaĹ‚y, protokoĹ‚y, komendy, sekwencje i Python we wspĂłlnym eksploratorze z ustawieniami kontekstowymi. Nazwa i ikona urzÄ…dzenia opisujÄ… rzeczywisty sprzÄ™t.
- **Czytelne schematy:** porty wyrĂłwnane z opisami, prowadzenie przewodĂłw wokĂłĹ‚ symboli, rozdzielanie tras i oznaczanie przeciÄ™Ä‡. Bramki o zmiennej liczbie wejĹ›Ä‡, Truth table, impulsowy Interlock z SET ALL/CLEAR, timery, liczniki, pamiÄ™ci, zatrzaski i przerzutniki.
- **PeĹ‚ny Python:** edytor kodu, typowane porty, stan, parametry, moduĹ‚y pomocnicze i dokĹ‚adne wersje bibliotek. Import NumPy i innych bibliotek, instalacja z PyPI lub zgodnych wheel offline oraz prĂłba w Studio. Administrator zatwierdza konkretny kod, helpery i wymagania; zmiana uniewaĹĽnia zgodÄ™. PeĹ‚ny CPython wykonuje zaufany kod i nie jest piaskownicÄ… bezpieczeĹ„stwa.
- **WybĂłr projektu:** wyszukiwanie, peĹ‚ne nazwy i znacznik bieĹĽÄ…cego projektu w dopasowanej do motywu liĹ›cie; strzaĹ‚ki, Enter i Escape. Konto, motyw i ustawienia pozostajÄ… po prawej.
- **Debugger:** wartoĹ›ci i jakoĹ›Ä‡ sygnaĹ‚Ăłw, pamiÄ™ci, timery, sekwencje, TX/RX, Ĺ›lad zdarzeĹ„ i przyczyny blokad. Wymuszanie wejĹ›Ä‡ oraz pauza/krok logiki w symulatorze. Pauza nie zamraĹĽa komunikacji, trwajÄ…cych sekwencji ani procesĂłw Python. Regulowany podziaĹ‚ w czterech poĹ‚oĹĽeniach, peĹ‚ny obszar roboczy i osobne okno z zachowaniem sesji.
- **Codzienna edycja:** prawy klik i skrĂłty do wycinania, kopiowania, wklejania, duplikacji, usuwania, zmiany nazwy, wyrĂłwnywania, grup, warstw, kopiowania wyglÄ…du, blokowania pozycji i przechodzenia do koĹ„cĂłw poĹ‚Ä…czenia.
- **WĹ‚asny wyglÄ…d:** jasny, ciemny i systemowy motyw programu, dopasowane przewijanie oraz osiem motywĂłw paneli z dostrajaniem poszczegĂłlnych elementĂłw.

![Sala konferencyjna â€” panel Liquid z czytelnym ukĹ‚adem i subtelnymi odbiciami](media/liquid-panel.png)

*Jeden przykĹ‚adowy panel, jeden ukĹ‚ad i te same powiÄ…zania. Liquid filtruje rzeczywiste tĹ‚o pod kontrolkami. To zrzut dziaĹ‚ajÄ…cego panelu, z wirtualnymi sygnaĹ‚ami i bez komend sprzÄ™towych.*

<details>
<summary>PorĂłwnaj Frost, Soft Dark i Paper</summary>

**Frost** â€” jasne, rozproszone powierzchnie nad spokojnym tĹ‚em.

![Ten sam panel w motywie Frost](media/frost-panel.png)

**Soft Dark** â€” subtelnie wypukĹ‚e przyciski i ciemne gradienty.

![Ten sam panel w motywie Soft Dark](media/softdark-panel.png)

**Paper** â€” jasny, oszczÄ™dny wyglÄ…d i wyraĹşna typografia.

![Ten sam panel w motywie Paper](media/paper-panel.png)

</details>

[Pobierz edytowalny projekt demonstracyjny](media/Sala-konferencyjna.avctrl) â€” cztery strony o tym samym ukĹ‚adzie; otwĂłrz w Studio 1.6.0 lub nowszym i uruchom symulacjÄ™. Projekt zawiera wyĹ‚Ä…cznie wirtualne sygnaĹ‚y, bez urzÄ…dzeĹ„, akcji i poleceĹ„ startowych. [Raport renderowania](media/panel-showcase-verification.json).

[Instrukcja wyboru projektu ze zrzutami](docs/WYBOR-PROJEKTU-PL.md)

## PoĹ‚Ä…czenia i automatyzacja

| Obszar | Funkcje |
| --- | --- |
| **Porty szeregowe i GPIO** | USBâ€“RS232/RS485, UART RPi i cyfrowe GPIO; stabilne identyfikatory USB, wykrywanie linii, konflikty, format transmisji, kontrola przepĹ‚ywu i kierunek RS485. UART jest domyĹ›lnie wĹ‚Ä…czony w czystym obrazie bez konsoli szeregowej. |
| **Rozbudowa sieci** | Klient/nasĹ‚uch TCP, UDP, dodatkowe adaptery USBâ€“Ethernet na malinie oraz ekspandery Ethernet/Wi-Fi z ustawieniami kanaĹ‚Ăłw, TCP/UDP i standardowym RFC2217, jeĹ›li sprzÄ™t go obsĹ‚uguje. Presety wyjaĹ›niajÄ… Unitek Y-105, USR-W610 i CH343P TTL. |
| **WĹ‚asne protokoĹ‚y** | ASCII/UTF-8/HEX, parametry, koĹ„ce/dĹ‚ugoĹ›ci ramek, kolejnoĹ›Ä‡ bajtĂłw, SUM/XOR/CRC, pola odpowiedzi, mapowanie stanĂłw, komunikaty spontaniczne i odpytywanie. Profile wielokrotnego uĹĽytku z osobnymi adresami instalacji. |
| **Panele WYSIWYG** | Strony, przyciski, przeĹ‚Ä…czniki, fadery, slidery, pokrÄ™tĹ‚a, wartoĹ›ci, kontrolki, tekst i grafiki z dysku; opcjonalne etykiety, ramki, rogi, CSS i warianty PC/tablet/telefon. Edytor i operator uĹĽywajÄ… wspĂłlnego renderera. |
| **Akcje i sekwencje** | Oczekiwanie, timeouty i anulowanie; zezwolenia oraz wzajemne wykluczanie sprawdzane przez silnik dla API i wielu paneli. JakoĹ›Ä‡ sygnaĹ‚u rozrĂłĹĽnia wartoĹ›ci poprawne, przeterminowane, nieznane i bĹ‚Ä™dne. |
| **Publikowanie i praca** | Walidacja, przygotowanie, aktywacja, historia/przywracanie, role administrator/operator, HTTPS i przypiÄ™cie certyfikatu. Ustawienia RPi przez WWW z potwierdzeniem/powrotem sieci. Aktualizacje GitHub wszystkich aplikacji Windows i Runtime ze sprawdzeniem SHA256 i powrotem RPi po bĹ‚Ä™dzie uruchomienia. |

Nie ma staĹ‚ego limitu liczby urzÄ…dzeĹ„, stron ani blokĂłw. Praktyczna pojemnoĹ›Ä‡ zaleĹĽy od kontrolera i obciÄ…ĹĽenia. Jeden kontroler wykonuje jeden aktywny projekt; Studio przechowuje wiele projektĂłw i poĹ‚Ä…czeĹ„ z kontrolerami.

## Zacznij bez sprzÄ™tu

1. Zainstaluj **Studio** i zaloguj siÄ™ do lokalnego symulatora: `admin` / `simulation`.
2. Wybierz **OtwĂłrz projekt szkoleniowy** oraz **PodrÄ™cznik szkoleniowy**.
3. SprawdĹş przykĹ‚ady i wybierz **Uruchom symulacjÄ™**. Przed wĹ‚Ä…czeniem transportĂłw fizycznych zdefiniuj wĹ‚asne polecenia sprzÄ™tu.
4. Przygotuj SD aplikacjÄ… **Imager**; przed jej wymazaniem potwierdĹş wybrany noĹ›nik.
5. Opublikuj projekt i obsĹ‚uguj go w **Playerze** albo panelu WWW kontrolera.

## Pierwsze uruchomienie Raspberry Pi

Po przygotowaniu karty w **AV Control Imager** i pierwszym starcie domyĹ›lny adres to **https://av-control.local:8443/**. WĹ‚asna nazwa, np. `sala-a`, daje **https://sala-a.local:8443/**. IP przydziela DHCP; obraz nie ma staĹ‚ego adresu `192.168.1.23`.

Zaloguj siÄ™ do WWW jako **`admin`** hasĹ‚em ustawionym w Imagerze. **`avoperator`** jest odrÄ™bnym kontem Linux/SSH. Odczytaj `AV-Control-parowanie.txt` i `AV-Control-CA.crt` z partycji boot po zakoĹ„czeniu pierwszej konfiguracji: Studio/Player uĹĽywajÄ… adresu i odcisku, przeglÄ…darka wymaga zaufania wĹ‚aĹ›ciwemu CA i zgodnoĹ›ci nazwy certyfikatu. NastÄ™pnie opublikuj pierwszy projekt; nowa karta oczekuje na panel.

[**PeĹ‚na procedura first-run**](docs/PIERWSZE-URUCHOMIENIE-PL.md) â€” Imager, sieÄ‡ i DHCP, certyfikaty, konta, publikowanie, logowanie i HDMI/USB, aktualizacje, opcjonalny TECHNIKAV oraz rozwiÄ…zywanie problemĂłw.

## Nauka i weryfikacja

- [Kurs offline](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Szkolenie-1.6.1.zip) â€” **52 rozdziaĹ‚y, cztery dodatki, 75 ilustracji** i neutralne projekty przykĹ‚adowe.
- [PDF: 195 stron](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Studio-Tutorial-PL-Signal-Workshop.pdf) Â· [Program szkolenia](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/PROGRAM-SZKOLENIA-PL.md) â€” **10 sesji / 22 godziny**.
- [PeĹ‚na dokumentacja](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/AV-Control-Studio-1.6.1-Dokumentacja.zip) Â· [Python](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/SYMBOLE-PYTHON-PL.md) Â· [USB, RS485 i UART](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/USB-RS485-UART-PL.md) Â· [Ekspandery](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/EKSPANDERY-SIECIOWE-PL.md).
- [Raport weryfikacji](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/WERYFIKACJA-1.6.1.md) Â· [Manifest budowania i testĂłw](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/RELEASE-MANIFEST.json) Â· [Sumy SHA256](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/SHA256SUMS.txt).

SzczegĂłĹ‚owy kurs i interfejs sÄ… obecnie po polsku. README i opisy wydaĹ„ sÄ… w obu jÄ™zykach; wybĂłr znajduje siÄ™ u gĂłry.

[Fizyczna RPi 4B przeszĹ‚a aktualizacjÄ™ GitHub 1.5.3 â†’ 1.5.5](docs/WERYFIKACJA-RPI-1.5.5-PO-PUBLIKACJI.md), z zachowaniem projektu, ustawieĹ„, kont, sesji i certyfikatu oraz zgodnoĹ›ciÄ… piÄ™ciu paneli. Testy komputerowe i emulacja ARM64 majÄ… odrÄ™bne dowody. Fizyczne 3B/5, rozruch nowej karty, komunikacja elektryczna UART/RS232/RS485/GPIO, zakupione adaptery i rzeczywiste urzÄ…dzenia mobilne wymagajÄ… osobnych prĂłb sprzÄ™towych. Instalatory AV Control nie majÄ… obecnie podpisu Authenticode wydawcy; instalatory producentĂłw sÄ… sprawdzane osobno.

## Dystrybucja i licencja

Pobieraj zaĹ‚Ä…czniki z sekcji **Assets**. Manifest wiÄ…ĹĽe sprawdzone paczki z produktem i udanym CI dokĹ‚adnego commitu. Wersja 1.5 dostarcza skompilowane aplikacje i dokumentacjÄ™, bez ZIP-a ĹşrĂłdeĹ‚ produktu. Kod bajtowy i pakiety przeglÄ…darkowe nie sÄ… szyfrowaniem ani gwarancjÄ… ochrony przed analizÄ…. [SzczegĂłĹ‚y pakowania](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.1/PAKOWANIE-BINARNE-1.5-PL.md).

Aplikacje nadal korzystajÄ… z tego repozytorium do aktualizacji. PodziaĹ‚ repozytoriĂłw nie wymaga ponownego zapisu SD ani wymiany projektu. Aktualizacje online i instalacja z PyPI wymagajÄ… internetu; praca lokalna pozostaje od nich niezaleĹĽna.

WczeĹ›niejsze wydania MIT i pochodzÄ…cy z nich kod zachowujÄ… [pierwotne warunki MIT](LICENSE-MIT-1.4.1.txt). MIT nie jest ogĂłlnÄ… licencjÄ… wszystkich nowych elementĂłw rozwijanych po 1.4.1; zobacz [zakres licencji](LICENSE). Komponenty innych autorĂłw zachowujÄ… swoje licencje.

[Projekt przyszĹ‚ej EULA](EULA-PL-PROJEKT.md) wskazuje osobÄ™ fizycznÄ… z placeholderami danych, adresu i kontaktu. Opisuje moĹĽliwe przyszĹ‚e opĹ‚aty; nie uruchamia pĹ‚atnoĹ›ci ani nowych wiÄ…ĹĽÄ…cych warunkĂłw. Licencjonowanie przez TECHNIKAV pozostaje planowanÄ… usĹ‚ugÄ… opcjonalnÄ….

[ZgĹ‚oĹ› bĹ‚Ä…d lub propozycjÄ™](https://github.com/Gartom91/av-control-studio/issues) Â· [Standard dwujÄ™zycznych wydaĹ„](RELEASING.md) Â· [English](README.en.md)

- [Konta uĹĽytkownikĂłw i wysuwana klawiatura](docs/KONTA-I-LOGOWANIE-PL.md): logowanie do paneli, wĹ‚asne hasĹ‚o, administracja i moduĹ‚ szkoleniowy.
