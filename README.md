# Trening – redukcja

Prosta aplikacja w przeglądarce do planu 4 dni (Góra A / Dół A / Góra B / Dół B) z hantlami, ławką i bieżnią.

## Co potrafi

- **Trening** – plan na dany dzień, wpisywanie kg i powtórzeń dla każdej serii, podgląd poprzedniego treningu i podpowiedź, czy dołożyć ciężar. Ptaszek ✓ przepisuje wartości z poprzedniego razu (jeśli pole jest puste) i włącza minutnik przerwy. Wpisane serie zapisują się na bieżąco, więc nic nie zniknie po odświeżeniu.
- **Historia** – wszystkie zapisane treningi z seriami, cardio i notatkami.
- **Postęp** – wykres dla każdego ćwiczenia (szacowany 1RM, najcięższa seria, objętość, powtórzenia) oraz liczba serii w tygodniu.
- **Waga** – pomiary wagi i talii, średnia 7-dniowa, tempo spadku na tydzień z podpowiedzią, czy zmienić kalorie.
- **Plan** – rozpiska tygodnia, zasady, cardio i odżywianie.
- Kopia zapasowa: eksport/import pliku JSON, eksport serii do CSV (Excel).

## Jak opublikować na GitHub Pages

1. Załóż na GitHubie nowe repozytorium, np. `trening` (może być publiczne).
2. Kliknij **Add file → Upload files**, wrzuć `index.html` (i ten `README.md`) i kliknij **Commit changes**.
3. Wejdź w **Settings → Pages**. W sekcji *Build and deployment* wybierz **Source: Deploy from a branch**, gałąź **main**, folder **/ (root)** i kliknij **Save**.
4. Po 1–2 minutach strona będzie pod adresem `https://TWOJA-NAZWA.github.io/trening/`.

Uwaga: na darmowym koncie GitHub Pages działa z repozytoriami publicznymi. Kod aplikacji będzie widoczny dla innych, ale Twoje treningi i waga **nie**. Trafiają do przeglądarki albo do osobnego, prywatnego repozytorium (patrz „Synchronizacja” niżej).

## Na telefonie

Otwórz adres strony w telefonie i dodaj ją do ekranu głównego:
- iPhone (Safari): Udostępnij → **Dodaj do ekranu początkowego**
- Android (Chrome): menu ⋮ → **Dodaj do ekranu głównego**

## Synchronizacja: dane w pliku `data.json` na GitHubie

Aplikacja może zapisywać wszystkie treningi i pomiary w pliku `data.json` w Twoim repozytorium. Plik aktualizuje się sam po każdym zapisie treningu lub pomiaru, a także po otwarciu aplikacji. Dzięki temu telefon i komputer mają te same dane.

### 1. Repozytorium na dane (prywatne)

Strona musi być w repozytorium publicznym, ale danych lepiej nie pokazywać światu. Dlatego załóż drugie, **prywatne** repozytorium:

1. GitHub → **New repository** → nazwa np. `trening-dane` → zaznacz **Private** → zaznacz **Add a README file** → **Create repository**.

Pliku `data.json` nie musisz tworzyć, aplikacja zrobi to sama.

### 2. Token dostępu (tylko do tego repozytorium)

1. GitHub → kliknij swoje zdjęcie → **Settings** → na dole **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. **Token name:** np. `trening-app`. **Expiration:** np. 1 rok (po tym czasie wygenerujesz nowy).
3. **Repository access:** *Only select repositories* → wybierz `trening-dane`.
4. **Permissions → Repository permissions → Contents:** *Read and write*. Nic więcej nie zaznaczaj.
5. **Generate token** i skopiuj go (zaczyna się od `github_pat_`). GitHub pokaże go tylko raz.

### 3. Połączenie w aplikacji

Zakładka **Waga → Synchronizacja z GitHubem**: wpisz swoją nazwę użytkownika, `trening-dane`, wklej token i kliknij **Połącz i synchronizuj**. Zrób to samo na każdym urządzeniu (telefon, komputer).

Ikona ☁ w nagłówku pokazuje stan: ✓ to dane zsynchronizowane, „!” to błąd (kliknij, żeby zobaczyć szczegóły).

**Bezpieczeństwo:** token jest zapisany tylko w przeglądarce na danym urządzeniu i nie trafia do `data.json` ani do kopii JSON. Ma dostęp wyłącznie do repozytorium z danymi. Jeśli zgubisz telefon, usuń token na GitHubie (Settings → Developer settings → Fine-grained tokens).

**Jak działa łączenie danych:** gdy dwa urządzenia zapiszą coś w tym samym czasie, aplikacja łączy oba zestawy, więc nic nie ginie. Usunięty trening lub pomiar znika na wszystkich urządzeniach. Bez internetu zapisujesz normalnie, a synchronizacja nastąpi, gdy połączenie wróci.

## Bez synchronizacji

Jeśli nie podłączysz GitHuba, dane są tylko w pamięci przeglądarki na danym urządzeniu. Wtedy rób kopię: **Waga → Eksportuj kopię (JSON)**, a na innym urządzeniu **Importuj kopię**. Wyczyszczenie danych przeglądarki usuwa historię, jeśli nie masz kopii ani synchronizacji.

## Zmiana planu

Ćwiczenia są na początku skryptu w `index.html`, w stałej `PLAN`. Każde ćwiczenie ma `name`, liczbę serii `sets`, zakres powtórzeń `min`–`max`, przerwę `rest` w sekundach i opcjonalnie `side: true` (na stronę), `bw: true` (bez ciężaru) albo `unit: "s"` (na czas). Nie zmieniaj `id` ćwiczeń, które już mają zapisaną historię, bo wykresy przestaną je łączyć.
