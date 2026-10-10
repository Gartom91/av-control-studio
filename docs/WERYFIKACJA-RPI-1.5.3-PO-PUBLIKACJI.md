# AV Control 1.5.3 — fizyczna aktualizacja po publikacji / Physical update after publication

## Polski

Fizyczna Raspberry Pi **4B** przeszła aktualizację **1.5.2 → 1.5.3** z publicznego GitHub Releases. Test obejmował sprawdzenie oferty, pobranie paczki o SHA256 zgodnym z manifestem, rzeczywisty instalator systemd oraz ponowne uruchomienie silnika. Końcowy stan aktualizacji: **complete**. Usługi silnika, konfiguracji i Agent **1.0.4** są aktywne.

Zachowano aktywny projekt **avctrl-training-room-v1**, rewizję **4**, jego pełną treść, certyfikat HTTPS, pamięci i sygnały trwałe, konta, istniejącą sesję, powiązanie Agenta, domyślny UART oraz preferencje aktualizacji. Weryfikacja korzystała ze sprawdzania CA, nazwy hosta i przypiętego certyfikatu. Test nie aktywował innego projektu i nie wywoływał akcji sterujących. Wszystkie transporty fizyczne były wyłączone. Formularz konfiguracji sieci był wyłącznie walidowany; ustawień sieci nie zastosowano.

Istniejący projekt ma **20 skonfigurowanych akcji startowych**. Po restarcie wykonuje je zgodnie z zapisanymi ustawieniami; Stan działającego programu może zmienić się po wykonaniu tych akcji; wartości odtworzone przed ich uruchomieniem sprawdzono oddzielnie. Zachowanie pamięci zweryfikowano przez porównanie zamrożonej kopii SQLite po zatrzymaniu starego silnika z wartościami odtworzonymi przez nowy, skompilowany silnik przed tymi akcjami. Nie utożsamiano późniejszego wykonania programu z utratą pamięci. Konfiguracji startowej nie zmieniono.

Pięć paneli porównano dla **10 wspólnych zdarzeń**, wraz z jakością i znacznikami czasu sygnałów. Nowy interfejs i zasoby offline są dostępne z kontrolera. Bezpośrednio z fizycznego kontrolera otwarto nowe stylizowane menu projektów, sprawdzono wyszukiwanie i zamknięcie Escape bez zmiany dokumentu. Natywne Studio, Player i Imager **1.3.0** poprawnie wykryły publiczną aktualizację **1.5.3**; ta próba sprawdzała ofertę, bez instalowania aktualizacji Windows.

[Dowód RPi](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/RPI-4B-1.5.3-VERIFICATION.json) · [Dowód Windows](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/WINDOWS-UPDATES-1.5.3-VERIFICATION.json) · [Sumy dodatkowych raportów](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/SHA256-POST-PUBLICATION.txt).

Nie jest to próba świeżego fizycznego rozruchu SD, RPi 3B/5, awarii zasilania ani elektrycznej komunikacji RS232/RS485/UART/GPIO. Obraz SD i testy QEMU mają odrębne dowody w podstawowym manifeście. Oryginalne paczki wydania i ich manifest pozostają bez zmian.

Odczyt kontrolny obejmuje bazę SQLite i jej dziennik WAL. Pierwszy próbny odczyt pomijał WAL; naprawiono sam test i powtórzono wyłącznie weryfikację. Kopię aktualizatora pozostawiono bez zmian, a instalacji nie powtarzano.

## English

A physical Raspberry Pi **4B** completed the public GitHub release update **1.5.2 → 1.5.3**, including discovery, download with a matching SHA256, the real systemd installer and engine restart. Final updater phase: **complete**. Runtime, configuration and Agent **1.0.4** services are active.

The active project **avctrl-training-room-v1**, revision **4**, complete project contents, HTTPS certificate, retained memory/signals, users, existing session, Agent connection, default UART and update preferences were preserved. CA, hostname and pinned-certificate verification remained enabled. The test did not replace the project or invoke control actions; all physical transports were disabled and network configuration was validated only.

The existing project explicitly configures **20 startup actions**, which run after restart. Live program state can change after those actions; restored values before startup were checked separately. Retention was verified by comparing the frozen pre-update SQLite checkpoint with the state restored by the new compiled engine before those actions. Subsequent program execution was distinguished from memory loss. Startup configuration was preserved.

Five panels agreed at **10 shared events**, including signal quality and timestamps. The new interface and offline assets are served by the controller. The themed project menu, search and Escape dismissal were checked directly from the physical controller without changing the document. Native Studio, Player and Imager **1.3.0** discovered public version **1.5.3**; this check did not install the Windows update.

[Pi evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/RPI-4B-1.5.3-VERIFICATION.json) · [Windows evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/WINDOWS-UPDATES-1.5.3-VERIFICATION.json) · [Additional report checksums](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.3/SHA256-POST-PUBLICATION.txt).

Fresh physical SD boot, Pi 3B/5, power-loss interruption and electrical serial/GPIO acceptance remain unverified. Image-file and QEMU evidence is separate. Original release packages and manifest were not changed.

Recorded: 2026-10-10T09:18:45.398373+00:00. Product source commit: `a8509d68b52a90b5d17b0dcbae715af43f79514d`.

Retention verification includes SQLite and its WAL journal. The first read-only probe omitted WAL; only the probe was corrected and verification repeated. The original updater backup was unchanged, and installation was not repeated.
