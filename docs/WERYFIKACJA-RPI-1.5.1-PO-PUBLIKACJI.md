# AV Control 1.5.1 — fizyczna aktualizacja po publikacji / Physical update after publication

## Polski

Fizyczna Raspberry Pi **4B** przeszła aktualizację **1.5.0 → 1.5.1** z publicznego GitHub Releases. Test obejmował sprawdzenie oferty, pobranie paczki o SHA256 zgodnym z manifestem, rzeczywisty instalator systemd oraz ponowne uruchomienie silnika. Końcowy stan aktualizacji: **complete**. Usługi silnika, konfiguracji i Agent **1.0.4** są aktywne.

Zachowano aktywny projekt **avctrl-training-room-v1**, rewizję **4**, jego pełną treść, certyfikat HTTPS, pamięci i sygnały trwałe, konta, istniejącą sesję, powiązanie Agenta, domyślny UART oraz preferencje aktualizacji. Weryfikacja korzystała ze sprawdzania CA, nazwy hosta i przypiętego certyfikatu. Test nie aktywował innego projektu i nie wywoływał akcji sterujących. Wszystkie transporty fizyczne były wyłączone. Formularz konfiguracji sieci był wyłącznie walidowany; ustawień sieci nie zastosowano.

Istniejący projekt ma **20 skonfigurowanych akcji startowych**. Po restarcie wykonuje je zgodnie z zapisanymi ustawieniami; m.in. impuls sceny zwiększył licznik Python z 23 do 24. Zachowanie pamięci zweryfikowano przez porównanie zamrożonej kopii SQLite po zatrzymaniu starego silnika z wartościami odtworzonymi przez nowy, skompilowany silnik przed tymi akcjami. Nie utożsamiano późniejszego wykonania programu z utratą pamięci. Konfiguracji startowej nie zmieniono.

Pięć paneli porównano dla **11 wspólnych zdarzeń**, wraz z jakością i znacznikami czasu sygnałów. Nowy interfejs i zasoby offline są dostępne z kontrolera. Natywne Studio, Player i Imager **1.3.0** poprawnie wykryły publiczną aktualizację **1.5.1**; ta próba sprawdzała ofertę, bez instalowania aktualizacji Windows.

[Dowód RPi](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/RPI-4B-1.5.1-VERIFICATION.json) · [Dowód Windows](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/WINDOWS-UPDATES-1.5.1-VERIFICATION.json) · [Sumy dodatkowych raportów](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/SHA256-POST-PUBLICATION.txt).

Nie jest to próba świeżego fizycznego rozruchu SD, RPi 3B/5, awarii zasilania ani elektrycznej komunikacji RS232/RS485/UART/GPIO. Obraz SD i testy QEMU mają odrębne dowody w podstawowym manifeście. Oryginalne paczki wydania i ich manifest pozostają bez zmian.

## English

A physical Raspberry Pi **4B** completed the public GitHub release update **1.5.0 → 1.5.1**, including discovery, download with a matching SHA256, the real systemd installer and engine restart. Final updater phase: **complete**. Runtime, configuration and Agent **1.0.4** services are active.

The active project **avctrl-training-room-v1**, revision **4**, complete project contents, HTTPS certificate, retained memory/signals, users, existing session, Agent connection, default UART and update preferences were preserved. CA, hostname and pinned-certificate verification remained enabled. The test did not replace the project or invoke control actions; all physical transports were disabled and network configuration was validated only.

The existing project explicitly configures **20 startup actions**, which run after restart. A configured scene pulse increased the Python counter from 23 to 24. Retention was verified by comparing the frozen pre-update SQLite checkpoint with the state restored by the new compiled engine before those actions. Subsequent program execution was distinguished from memory loss. Startup configuration was preserved.

Five panels agreed at **11 shared events**, including signal quality and timestamps. The new interface and offline assets are served by the controller. Native Studio, Player and Imager **1.3.0** discovered public version **1.5.1**; this check did not install the Windows update.

[Pi evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/RPI-4B-1.5.1-VERIFICATION.json) · [Windows evidence](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/WINDOWS-UPDATES-1.5.1-VERIFICATION.json) · [Additional report checksums](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.1/SHA256-POST-PUBLICATION.txt).

Fresh physical SD boot, Pi 3B/5, power-loss interruption and electrical serial/GPIO acceptance remain unverified. Image-file and QEMU evidence is separate. Original release packages and manifest were not changed.

Recorded: 2026-10-10T07:51:24.462201+00:00. Product source commit: `25e37bb62eec8c4d294876a7748ec146fc01aac9`.
