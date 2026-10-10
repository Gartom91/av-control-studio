# AV Control 1.5.5 — fizyczna aktualizacja po publikacji / Physical update after publication

## Polski

Fizyczna Raspberry Pi **4B** przeszła aktualizację **1.5.3 → 1.5.5** z publicznego GitHub Releases. Test obejmował sprawdzenie oferty, pobranie paczki o SHA256 zgodnym z manifestem, rzeczywisty instalator systemd oraz ponowne uruchomienie silnika. Końcowy stan aktualizacji: **complete**. Usługi silnika, konfiguracji i Agent **1.0.4** są aktywne.

Zachowano aktywny projekt **avctrl-training-room-v1**, rewizję **4**, jego pełną treść, certyfikat HTTPS, pamięci i sygnały trwałe, konta, istniejącą sesję, powiązanie Agenta, domyślny UART oraz preferencje aktualizacji. Weryfikacja korzystała ze sprawdzania CA, nazwy hosta i przypiętego certyfikatu. Test nie aktywował innego projektu i nie wywoływał akcji sterujących. Wszystkie transporty fizyczne były wyłączone. Formularz konfiguracji sieci był wyłącznie walidowany; ustawień sieci nie zastosowano.

Istniejący projekt ma **20 skonfigurowanych akcji startowych**. Po restarcie wykonuje je zgodnie z zapisanymi ustawieniami; Stan działającego programu może zmienić się po wykonaniu tych akcji; wartości odtworzone przed ich uruchomieniem sprawdzono oddzielnie. Zachowanie pamięci zweryfikowano przez porównanie zamrożonej kopii SQLite po zatrzymaniu starego silnika z wartościami odtworzonymi przez nowy, skompilowany silnik przed tymi akcjami. Nie utożsamiano późniejszego wykonania programu z utratą pamięci. Konfiguracji startowej nie zmieniono.

Pięć paneli porównano dla **11 wspólnych zdarzeń**, wraz z jakością i znacznikami czasu sygnałów. Nowy interfejs i zasoby offline są dostępne z kontrolera. Bezpośrednio z fizycznego kontrolera otwarto nowe stylizowane menu projektów, sprawdzono wyszukiwanie i zamknięcie Escape bez zmiany dokumentu. Natywne Studio, Player i Imager **1.3.0** poprawnie wykryły publiczną aktualizację **1.5.5**; ta próba sprawdzała ofertę, bez instalowania aktualizacji Windows.

**Wykryty błąd 1.5.5:** po aktualizacji konto kiosku nie miało dostępu do katalogu programu i publicznych plików interfejsu. Na testowanej RPi poprawiono te uprawnienia ręcznie, bez restartu silnika i bez zmiany projektu. Poniższy wynik kiosku dotyczy stanu po tej poprawce; pierwotna paczka 1.5.5 jej nie zawiera. Trwała poprawka instalatora jest przygotowana w 1.6.0. Prywatne dane i poświadczenia zachowały ograniczone uprawnienia.

Na fizycznej 4B sprawdzono aktywne usługi kiosku i seatd, konsolę tty2, maskowanie getty tty1, osobne konto bez uprawnień administratora, uprawnienia plików oraz rzeczywisty lokalny most operatora ze sprawdzaniem certyfikatu i odrzucaniem administracji. Konfiguracja WWW poprawnie pokazuje oczekiwanie na HDMI. Oba złącza są odłączone: **fizyczny obraz HDMI, mysz/touchpad/dotyk USB i przełączanie konsoli klawiaturą pozostają niepotwierdzone**.

[Dowód RPi](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/RPI-4B-1.5.5-VERIFICATION.json) · [Dowód Windows](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/WINDOWS-UPDATES-1.5.5-VERIFICATION.json) · [Sumy dodatkowych raportów](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/SHA256-POST-PUBLICATION.txt).

Nie jest to próba świeżego fizycznego rozruchu SD, RPi 3B/5, awarii zasilania ani elektrycznej komunikacji RS232/RS485/UART/GPIO. Obraz SD i testy QEMU mają odrębne dowody w podstawowym manifeście. Oryginalne paczki wydania i ich manifest pozostają bez zmian.

Odczyt kontrolny obejmuje bazę SQLite i jej dziennik WAL w prywatnej kopii tymczasowej. Oryginalną kopię aktualizatora pozostawiono bez zmian.

## English

A physical Raspberry Pi **4B** completed the public GitHub release update **1.5.3 → 1.5.5**, including discovery, download with a matching SHA256, the real systemd installer and engine restart. Final updater phase: **complete**. Runtime, configuration and Agent **1.0.4** services are active.

The active project **avctrl-training-room-v1**, revision **4**, complete project contents, HTTPS certificate, retained memory/signals, users, existing session, Agent connection, default UART and update preferences were preserved. CA, hostname and pinned-certificate verification remained enabled. The test did not replace the project or invoke control actions; all physical transports were disabled and network configuration was validated only.

The existing project explicitly configures **20 startup actions**, which run after restart. Live program state can change after those actions; restored values before startup were checked separately. Retention was verified by comparing the frozen pre-update SQLite checkpoint with the state restored by the new compiled engine before those actions. Subsequent program execution was distinguished from memory loss. Startup configuration was preserved.

Five panels agreed at **11 shared events**, including signal quality and timestamps. The new interface and offline assets are served by the controller. The themed project menu, search and Escape dismissal were checked directly from the physical controller without changing the document. Native Studio, Player and Imager **1.3.0** discovered public version **1.5.5**; this check did not install the Windows update.

**1.5.5 defect found:** the updated kiosk account could not read the program directory and public UI assets. Those permissions were corrected manually on this Pi, without restarting the runtime or changing the project. Kiosk results below describe the corrected installation; the original 1.5.5 package does not include that correction. The permanent installer fix is prepared in 1.6.0. Private data and credential permissions remain restricted.

The physical 4B passed checks of the kiosk/seatd services, tty2 login, tty1 getty mask, unprivileged account, restricted file permissions, and the real certificate-pinned local operator bridge with administration denied. Web settings correctly report waiting for HDMI. Both ports are disconnected: **physical HDMI, USB mouse/touchpad/touchscreen and keyboard console switching remain unverified**.

[Pi evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/RPI-4B-1.5.5-VERIFICATION.json) · [Windows evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/WINDOWS-UPDATES-1.5.5-VERIFICATION.json) · [Additional report checksums](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/SHA256-POST-PUBLICATION.txt).

Fresh physical SD boot, Pi 3B/5, power-loss interruption and electrical serial/GPIO acceptance remain unverified. Image-file and QEMU evidence is separate. Original release packages and manifest were not changed.

Recorded: 2026-10-10T16:09:56.953517+00:00. Product source commit: `d0b4c685c21db7b6893a19616a196cf23b8d3280`.

Retention verification includes SQLite and its WAL journal in a private temporary copy. The original updater backup remains unchanged.
