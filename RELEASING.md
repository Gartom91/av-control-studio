# Release standard · Standard wydań

**[Polski](#polski) · [English](#english)**

## Polski

Jeden tag `vX.Y.Z`, jeden opis z sekcjami **Polski** i **English**. Oba opisują te same zmiany, sposób aktualizacji, testy i ograniczenia. Nazwy plików są identyczne. GitHub nie dobiera języka według kraju odwiedzającego — służą do tego odsyłacze u góry.

1. Przygotuj pakiety i raport weryfikacji dokładnej wersji. Odróżniaj komputer, emulację i fizyczny sprzęt.
2. Publiczne repozytorium zawiera dokumentację i materiały prezentacyjne. Źródła, historia rozwoju, narzędzia budowania i dane dostępowe pozostają prywatne.
3. Zapisz oba opisy w `docs/releases/vX.Y.Z.md` według [szablonu](docs/releases/TEMPLATE.md). Usuń placeholdery.
4. Zaktualizuj oba README, CHANGELOG i screenshoty do opublikowanej wersji. Oznacz funkcje w przygotowaniu.
5. Utwórz wydanie robocze. Dołącz instalatory, obraz, Runtime, instrukcje, neutralne przykłady, raporty, manifest i SHA-256. Nie dołączaj ZIP-a źródeł produktu.
6. Sprawdź rozmiar, stan i sumę każdego załącznika na GitHub, wersje aplikacji, nazwy wymagane przez aktualizatory i kompletność obu języków. Dopiero wtedy publikuj stabilne wydanie.
7. Po publikacji sprawdź anonimowe pobieranie, odsyłacze i rozpoznanie wydania przez aktualizatory. Późniejsze wyniki dołącz jako dowód po publikacji; nie podmieniaj sprawdzonych instalatorów ani obrazu.

Wymagane sekcje: **Co się zmieniło**, **Instalacja i aktualizacja**, **Weryfikacja i ograniczenia**, **Dystrybucja i licencja**. Planistyczna EULA nie jest warunkiem aktualizacji.

Przed pierwszym wydaniem stosującym nową EULA uzupełnij dane Licencjodawcy będącego osobą fizyczną, jej zakres wersji i sposób akceptacji. Sprawdź zgodność treści w instalatorach, aktualizatorach i opisie wydania. Historyczne MIT oraz licencje komponentów muszą pozostać w pakietach. Nie przypisuj EULA wstecz do 1.4.1 ani innych wcześniej wydanych kopii MIT; nie publikuj nowej oferty płatnej z placeholderami.

## English

One `vX.Y.Z` tag, one description with **Polski** and **English** sections. Both describe the same changes, update procedure, checks and limitations. Asset names are identical. GitHub does not choose language by a visitor's country; use the links at the top.

1. Prepare packages and a verification report for the exact version. Separate computer tests, emulation and physical hardware.
2. Keep documentation and presentation material public. Sources, development history, build tools and credentials remain private.
3. Save both descriptions in `docs/releases/vX.Y.Z.md` using the [template](docs/releases/TEMPLATE.md). Remove placeholders.
4. Update both READMEs, CHANGELOG and screenshots to the published version. Label work in progress.
5. Create a draft. Attach installers, SD image, Runtime, manuals, neutral examples, reports, a manifest and SHA-256. Do not attach a product source ZIP.
6. Verify each uploaded asset's size, state and digest, consistent application versions, updater-required names and both languages. Only then publish a stable release.
7. Verify anonymous downloads, links and updater discovery. Attach later results as post-publication evidence; do not replace verified installers or images.

Required sections: **What changed**, **Install and update**, **Verification and limitations**, **Distribution and licensing**. A planning EULA is not an update requirement.

Before the first release applying the new EULA, complete the individual licensor's details, version scope and acceptance process. Verify consistency across installers, updaters and release notes. Historical MIT and third-party notices must remain in packages. Do not apply the EULA retroactively to 1.4.1 or other previously released MIT copies; do not publish a new paid offer with placeholders.
