# AV Control 1.5.0 — weryfikacja po publikacji / post-publication verification

**[Polski](#polski) · [English](#english)**

Data / date: **2026-10-10**. [Wydanie / release](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.0).

## Polski

### Wynik

**Test istniejącej fizycznej Raspberry Pi 4B zakończył się powodzeniem.** Kontroler pobrał paczkę z publicznego wydania GitHub i zaktualizował Runtime **1.4.1 → 1.5.0**. Agent działa w wersji **1.0.4**. Usługi `avcontrol`, `avcontrol-config` i `avcontrol-agent` były aktywne po aktualizacji.

To dodatkowy raport sporządzony po opublikowaniu 35 podstawowych załączników. Nie zastępuje manifestu budowy ani ich sum; nie zmieniono instalatorów, obrazu SD i paczki Runtime. Osobne sumy czterech dodatkowych raportów zawiera `SHA256-POST-PUBLICATION.txt`.

### Aktualizacja i zachowanie instalacji

| Sprawdzenie | Wynik |
| --- | --- |
| Publiczna dystrybucja | 35 podstawowych załączników miało zgodny rozmiar i SHA256 w metadanych GitHuba; wszystkie działały przez anonimowe HEAD. Manifest, sumy i Runtime pobrano anonimowo i sprawdzono. |
| Realny updater RPi | Sprawdzenie i pobranie z publicznego GitHuba; instalacja przez systemd zakończona stanem `complete`, poprzednia wersja 1.4.1 dostępna w historii. |
| TLS | Weryfikacja CA i nazwy hosta oraz zgodność przypiętego certyfikatu przed/po aktualizacji. |
| Dane | Zachowane identyfikator, rewizja i kanoniczny SHA256 aktywnego projektu, sygnały i pamięci trwałe, konta, sesja, połączenie Agenta i preferencje aktualizacji. |
| UART | Ustawienie włączonego UART zachowane; ten test nie wysyłał danych elektrycznych. |
| Konfiguracja sieci WWW | Podgląd konfiguracji przypisanej do MAC oraz odrzucenie nieobecnego MAC; nie zastosowano zmian sieci. |

SHA256 pobranej i zainstalowanej paczki Runtime:

`bc0abf258812f1b077a3541d441fee4cece37943419257402e8866d3f6bc15c4`

### Pięć paneli i tutorial

Pięć klientów WebSocket połączono z rzeczywistym kontrolerem. Porównano **11 wspólnych numerów zdarzeń** we wszystkich panelach, włącznie z wartościami, jakością i znacznikami czasu sygnałów; stany były zgodne. Panel WWW nie zgłosił błędów JavaScript. Podręcznik na kontrolerze poprawnie załadował **41 nagłówków rozdziałów/dodatków i 59 ilustracji** we wspólnej domenie aplikacji.

Próba przeglądarkowa była odczytowa. Zarejestrowano trzy zwolnienia momentary leases podczas sprzątania, bez pozyskania lease i bez żądań sterujących. Nie aktywowano projektu ani nie wysłano komend urządzeń. Odczyt metadanych środowiska Python używa POST `/api/v1/python/status`; test dopuszcza ten odczyt i nadal odrzuca instalowanie, zatwierdzanie, uruchamianie kodu oraz pozostałe mutacje w tej części próby.

### Własne moduły Python i biblioteki na ARM64

Na zainstalowanym Runtime 1.5.0 wykonano osobną próbę własnego symbolu w izolowanym projekcie roboczym, bez wdrażania go jako aktywnego projektu:

1. Przesłano zgodny wheel **NumPy 2.5.3 / CPython 3.13 / Linux ARM64**, zweryfikowany sumą producenta z PyPI.
2. Przygotowano świeże środowisko offline z dokładnym wymaganiem `numpy==2.5.3`.
3. Własny `filters.py` importował NumPy i obliczał średnią z okna trzech próbek. Wartości wejściowe 10, 20, 30, 40, 50 dały wyniki **10, 15, 20, 30, 40**.
4. Worker działał jako użytkownik usługi **avcontrol**, z **Python 3.13.5** i NumPy 2.5.3. Potwierdzono import helpera oraz zachowanie stanu między wywołaniami.
5. Zmiana helpera unieważniła zatwierdzenie kodu.
6. Drugie środowisko przygotowano z użyciem **PyPI online**, z wymaganiami `numpy==2.5.3` i `six==1.17.0`; sprawdzono wersje zainstalowanych bibliotek oraz wykonanie własnego symbolu.

Próba nie zmieniła aktywnego projektu, pamięci instalacji, kont, połączenia Agenta, UART ani certyfikatu. Dodała wyłącznie cache bibliotek, zatwierdzenia izolowanych projektów i wpisy audytu. Pełny CPython wykonuje zaufany kod z uprawnieniami procesu usługi; nie jest sandboxem bezpieczeństwa.

### Aktualizacje aplikacji Windows

Rzeczywiste starsze aplikacje **Studio, Player i Imager 1.3.0** uruchomiono oddzielnie w natywnym WebView2. Każda wykryła publiczne wydanie **1.5.0**, właściwą paczkę, rozmiar i stan dostępności bez błędu. Ta próba sprawdzała wykrywanie wydania; **nie uruchamiała pobrania i instalacji aktualizacji Windows**. Instalację/deinstalację samych gotowych pakietów 1.5 opisują oddzielne dowody podstawowego wydania.

### Zakres i dowody

- `RPI-4B-1.5.0-VERIFICATION.json` — realna aktualizacja, zachowanie danych, usługi, TLS i pięć paneli.
- `RPI-PYTHON-1.5.0-VERIFICATION.json` — ARM64, NumPy offline/PyPI, import helpera, wyniki i unieważnienie zatwierdzenia.
- `WINDOWS-UPDATES-1.5.0-VERIFICATION.json` — wykrycie nowego wydania przez trzy starsze natywne aplikacje Windows.
- `SHA256-POST-PUBLICATION.txt` — sumy tego dokumentu i trzech powyższych JSON-ów.

**Nadal wymagają osobnej próby fizycznej:** Pi 3B i 5, rozruch nowej zapisanej SD, elektryczne RS232/RS485/UART/GPIO, zakupione adaptery i USR-W610, dodatkowy USB–Ethernet, fizyczny telefon/tablet oraz przerwanie zasilania przy aktualizacji. Ręczny i automatyczny rollback sprawdzono pod QEMU; nie wykonywano rollbacku na tej fizycznej 4B. Pięć klientów przeglądarki nie zastępuje pięciu fizycznych urządzeń.

## English

### Result

**The existing physical Raspberry Pi 4B passed verification.** It downloaded the package from the public GitHub release and updated Runtime **1.4.1 → 1.5.0**. Agent **1.0.4** is running. Services `avcontrol`, `avcontrol-config` and `avcontrol-agent` were active after the update.

This additional report was produced after publication of the 35 base assets. It does not replace their build manifest or checksums; the installers, SD image and Runtime bundle were not changed. `SHA256-POST-PUBLICATION.txt` covers the four additional reports separately.

### Update and installation preservation

| Check | Result |
| --- | --- |
| Public distribution | All 35 base assets matched GitHub size/SHA256 metadata and anonymous HEAD requests worked. The manifest, checksums and Runtime were anonymously downloaded and verified. |
| Real Pi updater | Checked and downloaded from public GitHub; systemd installation reached `complete`, with previous version 1.4.1 recorded in history. |
| TLS | Strict CA/hostname verification and an unchanged pinned certificate before/after the update. |
| Data | Active project ID, revision and canonical SHA256, retained signals/memory, users, session, Agent connection and update preferences were preserved. |
| UART | Its enabled configuration was preserved; no electrical data was sent by this test. |
| Browser network configuration | MAC-bound configuration preview and rejection of an absent MAC; no network changes were applied. |

Downloaded and installed Runtime SHA256:

`bc0abf258812f1b077a3541d441fee4cece37943419257402e8866d3f6bc15c4`

### Five panels and the course

Five WebSocket clients connected to the real controller. **11 shared event sequences** were compared across every panel, including signal values, quality and timestamps; all states agreed. The browser UI had no JavaScript errors. Its manual loaded **41 chapter/appendix headings and 59 illustrations** from the application's origin.

The browser trial was read-only. Cleanup released three momentary leases; it acquired no leases and made no actuating requests. It did not activate a project or issue device commands. Python environment metadata is read through POST `/api/v1/python/status`; the test allows that read while continuing to reject installation, approval, code execution and other mutations in this phase.

### User Python modules and ARM64 libraries

A separate custom-symbol trial ran on the installed Runtime 1.5.0 using an isolated draft project, without activating it:

1. Uploaded a compatible **NumPy 2.5.3 / CPython 3.13 / Linux ARM64** wheel verified against its official PyPI digest.
2. Prepared a fresh offline environment pinned to `numpy==2.5.3`.
3. A user `filters.py` imported NumPy and calculated a three-sample moving mean. Inputs 10, 20, 30, 40, 50 produced **10, 15, 20, 30, 40**.
4. The worker ran as service user **avcontrol**, using **Python 3.13.5** and NumPy 2.5.3. Helper import and state across invocations were verified.
5. Changing the helper invalidated code approval.
6. A second environment was prepared using **online PyPI**, pinned to `numpy==2.5.3` and `six==1.17.0`; installed versions and custom-symbol execution were checked.

The active project, retained installation memory, users, Agent connection, UART configuration and certificate remained unchanged. Only library caches, isolated-project approvals and audit records were added. Full CPython runs trusted code with the service process's permissions; it is not a security sandbox.

### Windows application updates

Older real **Studio, Player and Imager 1.3.0** applications were launched separately in native WebView2. Each detected public release **1.5.0**, its correct package, size and availability without errors. This trial checked release discovery; it **did not download or install the Windows update**. Installation/uninstallation of the final 1.5 packages is covered by separate base-release receipts.

### Scope and evidence

- `RPI-4B-1.5.0-VERIFICATION.json` — real update, data preservation, services, TLS and five panels.
- `RPI-PYTHON-1.5.0-VERIFICATION.json` — ARM64, offline/PyPI NumPy, helper import, results and invalidated approval.
- `WINDOWS-UPDATES-1.5.0-VERIFICATION.json` — release discovery by the three older native Windows applications.
- `SHA256-POST-PUBLICATION.txt` — checksums of this document and those three JSON files.

**Separate physical trials are still required for:** Pi 3B/5, a fresh written SD boot, electrical RS232/RS485/UART/GPIO, purchased adapters and USR-W610, additional USB–Ethernet, physical phones/tablets and power loss during an update. Manual/automatic rollback passed under QEMU; no physical rollback was performed on this 4B. Five browser clients do not qualify five physical devices.
