# Ćwiczenie 1: moje CV w HTML — od lokalnego Git do GitHuba

## Zadanie

Sklonuj [repozytorium szablonu](https://github.com/ZajdelR/idsik-git-webpage-example) i stwórz własne CV na podstawie `index.html`. Uzupełnij sekcje **O mnie, Edukacja i Doświadczenie**, podmień zdjęcie oraz dodaj odnośniki do swoich profili LinkedIn i GitHub. Załóż konta w obu serwisach, jeśli jeszcze ich nie masz. Rozwijaj projekt lokalnie, zapisując kolejne etapy w Git, a następnie prześlij całe repozytorium wraz z historią na GitHuba.

**Efekt:** działające CV w przeglądarce, uzupełnione profile oraz repozytorium z co najmniej 6 własnymi logicznymi commitami, w tym jedną aktualizacją po pierwszym pushu. Repozytorium na potrzeby ćwiczenia ma być **prywatne**. Oceniane są końcowy plik CV i drzewo zmian na GitHubie. Publikacja strony w internecie nie jest wymagana.

**Narzędzia:** Git, edytor tekstu (np. VS Code), przeglądarka i terminal. Do poleceń SSH używaj Git Bash lub bash w MobaXterm. Fragmenty `TWOJ_LOGIN`, imię i adres e-mail zastąp własnymi wartościami.

## Konspekt pracy

| Etap | Rezultat |
| --- | --- |
| Klonowanie szablonu | Osobny folder z plikami i historią |
| Konfiguracja autora | Rozpoznana historia i adres źródłowego repozytorium |
| Treść CV oraz zdjęcie | Trzy sekcje CV, kilka commitów |
| Konta LinkedIn i GitHub | Uzupełnione profile i linki w CV |
| Kontrola jakości i historii | Sprawdzone CV i uporządkowane zmiany |
| GitHub i pierwszy push | Repozytorium z własną historią, bez commitów szablonu |
| Kolejna aktualizacja i oddanie | Nowy commit, drugi push, prezentacja na zajęciach |

Weryfikację kont można dokończyć poza zajęciami. Git działa lokalnie bez konta na GitHubie i bez internetu.

## 1. Sklonuj repozytorium szablonu

W terminalu przejdź do katalogu na własne projekty, poza repozytorium materiałów kursowych. Wykonaj:

```sh
git clone https://github.com/ZajdelR/idsik-git-webpage-example.git moje-cv
cd moje-cv
```

Clone pobiera pliki **i historię**, tworząc folder `moje-cv` z lokalnym repozytorium. Nie pobieraj ZIP-a i nie wykonuj `git init`. W kolejnym kroku utworzymy nową historię bez kasowania katalogu `.git`. Nie trzeba robić forka ani używać „Use this template”.

Otwórz `index.html` w przeglądarce. Katalogi `assets` i `images` zawierają zasoby strony; pozostaw je w projekcie. Wszystkie dalsze polecenia wykonuj w `moje-cv`.

## 2. Ustaw autora i sprawdź punkt startu

```sh
git config user.name "Imię Nazwisko"
git config user.email "twoj-adres@example.com"
git status
git log --oneline -5
git remote -v
```

Konfiguracja dotyczy nowych commitów w tym repozytorium; nie zmienia autorstwa historii szablonu. Możesz użyć adresu noreply z ustawień GitHuba. Clone ustawił nazwę `origin` dla adresu prowadzącego. Następnie zmienisz origin na własne repozytorium i rozpoczniesz historię od nowa.

### Własny adres i nowa historia — przed edycją CV

Utwórz na swoim koncie GitHub **puste prywatne repozytorium** `moje-cv`, bez README, licencji i .gitignore. Zastąp TWOJ_LOGIN:

```sh
git remote set-url origin git@github.com:TWOJ_LOGIN/moje-cv.git
git remote -v
git checkout --orphan start-cv
git add .
git commit -m "Rozpocznij wlasny projekt CV"
git branch -M main
git log --oneline
```

Wykonaj ten etap **raz, przed własnymi zmianami i przed pierwszym pushem**. Orphan rozpoczyna linię bez rodziców, zachowując pliki. `branch -M main` zastępuje lokalną gałąź z odziedziczoną historią. Log powinien pokazać jeden własny commit. Nie jest to `reset --hard`: nie przywracamy wcześniejszej treści plików. Zachowaj LICENSE.txt i autorstwo HTML5 UP.

Stare obiekty i odwołania mogą pozostać lokalnie; nie należą do nowej historii main i nie zostaną wysłane przez `git push origin main`. Nie używaj `push --all` ani `--mirror`. Jeśli wykonałeś już własne commity przed tym etapem, po zastąpieniu main nie będą widoczne w nowej historii — zachowaj kopię projektu z `.git` przed kontynuacją albo uzgodnij przejście z prowadzącym.

Wymagane jest co najmniej **6 własnych logicznych commitów**, licząc nowy commit początkowy oraz dalsze zmiany. Opcjonalny PLAN.md nie podlega osobnej ocenie.

## 3. Uzupełniaj CV małymi etapami

W `index.html` wyszukaj `UZUPEŁNIJ`, `TWOJ_LOGIN` i teksty w nawiasach kwadratowych.

- **Dane i O mnie:** tytuł karty, imię i nazwisko, nagłówek zawodowy, 3–5 zdań o sobie oraz konkretne umiejętności.
- **Edukacja:** co najmniej jeden wpis z nazwą szkoły lub uczelni, kierunkiem i okresem nauki. Kolejne wpisy dodawaj przez kopiowanie całego elementu `<article>`.
- **Doświadczenie:** co najmniej jeden wpis z rolą, okresem, zadaniami i rezultatem. Możesz opisać projekt z zajęć, koło naukowe lub wolontariat, jeśli nie masz doświadczenia zawodowego.
- **Zdjęcie:** zastąp `images/avatar.jpg` własnym zdjęciem. Przy innej nazwie lub formacie popraw `src` w HTML. Uzupełnij opis `alt`.

Po każdej logicznej części zapisz plik, odśwież stronę i wykonaj:

```sh
git status
git diff
git add index.html
git diff --cached
git commit -m "Uzupełnij sekcję O mnie"
```

Dostosuj komunikat do wykonanej zmiany. Dla zdjęcia dodaj również jego plik:

```sh
git add index.html images/avatar.jpg
git diff --cached --stat
git commit -m "Dodaj własne zdjęcie profilowe"
```

Jeśli używasz innej nazwy zdjęcia, zmień ją w poleceniu. Git zapisuje wersje obrazów, ale zwykły `git diff` nie pokaże ich różnic wizualnych — obejrzyj zdjęcie w przeglądarce.

Zaplanuj własne commity: O mnie, edukacja, doświadczenie, zdjęcie, profile, poprawki wyglądu lub umiejętności. Nie wykonuj pustych commitów tylko dla osiągnięcia wymaganej liczby.

## 4. Załóż konta i uzupełnij profile

1. Załóż konto na [LinkedIn](https://www.linkedin.com/) i [GitHubie](https://github.com/). Jeśli masz konto, wykorzystaj istniejące. Dokończ weryfikację wymaganą przez serwis.
2. W LinkedIn uzupełnij nagłówek, opis, edukację i doświadczenie lub projekt zgodne z CV.
3. W GitHubie uzupełnij nazwę wyświetlaną i krótki opis profilu.
4. Skopiuj adresy swoich profili. W sekcji „LinkedIn i GitHub” zmień **zarówno `href`, jak i widoczny tekst linku**. Nie wstawiaj adresu strony głównej serwisu ani ustawień konta.
5. Kliknij oba linki i sprawdź, czy prowadzą do właściwych profili. Zapisz zmianę w kolejnym commicie.

Repozytorium ćwiczenia pozostaje prywatne. Na profilach LinkedIn i GitHub publikuj tylko dane, które chcesz udostępnić publicznie. Nie dodawaj adresu zamieszkania, numerów dokumentów, haseł ani tokenów. Późniejsze usunięcie danych z HTML nie usuwa ich ze starych commitów.

## 5. Sprawdź jakość i prześledź historię

```sh
git status
git log --oneline --graph main
git show --stat HEAD
git diff HEAD~1 HEAD -- index.html
```

Ostatnie polecenie wymaga co najmniej dwóch commitów. Przeanalizuj, czym różni się `git diff` od `git diff --cached`, co zawiera wybrany commit i dlaczego został wydzielony. Nie trzeba przygotowywać osobnego raportu ani zrzutów historii — oceniana będzie rzeczywista historia na GitHubie.

Sprawdź w przeglądarce:

- Wszystkie trzy wymagane sekcje zawierają własną treść.
- Zdjęcie jest widoczne i ma własny opis `alt`.
- Linki do profili i nawigacja między sekcjami działają.
- Strona jest czytelna po zwężeniu okna do szerokości telefonu; menu mobilne otwiera się.
- Nie pozostały przykładowe teksty `[Imię i nazwisko]`, `TWOJ_LOGIN` ani inne pola do wypełnienia. Komentarze instruktażowe można usunąć.
- Zachowano informację o HTML5 UP i plik licencji.

Zapisz ewentualne poprawki w Git. Przed wysłaniem zmian `git status` powinien pokazywać brak niezatwierdzonych zmian.

## 6. Utwórz klucz SSH, dodaj go do GitHuba i wykonaj push

Repozytorium `moje-cv` na Twoim koncie jest puste, a lokalny origin wskazuje już jego adres SSH. Poniższe polecenia wykonuj w **Git Bash lub terminalu bash MobaXterm**, nie w PowerShell.

### Utwórz klucz

```sh
ssh-keygen -t ed25519 -C "twoj-adres@example.com"
```

Wpisz własny e-mail jako etykietę. Przyjmij domyślną lokalizację, jeśli plik klucza jeszcze nie istnieje. **Nie nadpisuj istniejącego klucza**; możesz użyć już posiadanego, a przy innej nazwie dopasuj dalsze ścieżki. Ustaw passphrase. Plik `~/.ssh/id_ed25519` jest prywatny; `~/.ssh/id_ed25519.pub` jest publiczny. Żadnego z nich nie dodawaj do projektu CV.

### Dodaj klucz publiczny do GitHuba

```sh
cat ~/.ssh/id_ed25519.pub
```

Skopiuj całą linię. Na swoim koncie wybierz **Settings → SSH and GPG keys → New SSH key**, wpisz nazwę komputera, wybierz **Authentication Key**, wklej linię do pola **Key** i kliknij **Add SSH key**. Nigdy nie wklejaj klucza prywatnego.

### Sprawdź połączenie i wyślij projekt

```sh
ssh -T git@github.com
```

SSH odczyta klucz z domyślnej lokalizacji `~/.ssh/id_ed25519`; jeśli jest chroniony passphrase, poprosi o jej wpisanie. Przy niestandardowej nazwie skonfiguruj `IdentityFile` w `~/.ssh/config`, aby zarówno test, jak i push używały właściwego klucza.

Przy pierwszym połączeniu porównaj odcisk serwera z [oficjalnymi odciskami GitHuba](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints), zanim zaakceptujesz serwer. Poprawny komunikat zawiera `Hi TWOJ_LOGIN! You've successfully authenticated, but GitHub does not provide shell access.` Kod zakończenia 1 jest normalny dla tego testu.

```sh
git remote -v
git log --oneline
git push -u origin main
```

Origin musi wskazywać `git@github.com:TWOJ_LOGIN/moje-cv.git`. Push wysyła nową historię main — własny początkowy commit oraz późniejsze zmiany, bez przodków z repozytorium szablonu. `-u` ustawia powiązanie z origin/main. Nie używaj `--all`, `--mirror` ani `--force`. Odśwież własne repozytorium i sprawdź pliki oraz autora commitów. Sam push nie publikuje strony WWW.

Przy `Permission denied (publickey)` sprawdź, czy dodano właściwy klucz publiczny do właściwego konta i czy odpowiadający mu klucz prywatny znajduje się w `~/.ssh/id_ed25519`. Przy odrzuconym pushu sprawdź, czy docelowe repozytorium rzeczywiście było puste; nie wymuszaj nadpisania.

Źródła: [generowanie klucza SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent), [dodawanie klucza do GitHuba](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## 7. Zaktualizuj CV po pierwszym pushu

Zmień konkretny element, np. dodaj właśnie poznany Git do umiejętności wraz z przykładem użycia. Przeprowadź pełny cykl:

```sh
git status
git diff
git add index.html
git diff --cached
git commit -m "Dodaj umiejętność wersjonowania projektu w Git"
git push
git fetch origin
git status -sb
git log --oneline origin/main..main
```

Pusta lista z ostatniego polecenia oznacza, że nie ma lokalnych commitów na `main`, których brakuje w pobranym `origin/main`. Sprawdź również najnowszy commit na stronie GitHuba. Ustawienie `-u` przy pierwszym pushu pozwala teraz używać samego `git push`.

Dalsza praca: **jedno zadanie → edycja → podgląd → diff → add → commit → push**. Jeśli pracujesz też na innym komputerze, przed nową edycją i przy czystym katalogu roboczym wykonaj `git pull --ff-only`. Jeśli Git zgłosi rozbieżność historii, zatrzymaj się i wyjaśnij ją przed dalszymi zmianami.

## 8. Opcjonalna praca własna: gałąź i Netlify

### Gałąź robocza → pull request → merge na GitHubie

Przy czystym katalogu roboczym pobierz aktualny `main` i utwórz gałąź:

```sh
git status
git switch main
git pull --ff-only
git switch -c poprawa-opisu
```

Ulepsz opis projektu w CV, zapisz plik i sprawdź stronę. Następnie:

```sh
git diff
git add index.html
git commit -m "Doprecyzuj rezultat projektu"
git push -u origin poprawa-opisu
```

Na GitHubie:

1. Otwórz **Pull requests → New pull request**.
2. Wybierz **base: main** i **compare: poprawa-opisu**.
3. Sprawdź różnice, podaj tytuł i opis, kliknij **Create pull request**.
4. Przejrzyj **Files changed** i commity. Rozwiąż ewentualne konflikty lub niespełnione wymagania przed scaleniem.
5. Wybierz **Create a merge commit**, następnie **Merge pull request → Confirm merge**. Ten sposób zachowuje commity gałęzi w historii.

### Pull do lokalnego repozytorium

Po scaleniu na GitHubie wróć do terminala Mobe:

```sh
git switch main
git pull --ff-only
git log --oneline --graph --decorate --all
git branch --merged main
```

Otwórz lokalne CV i sprawdź zmianę. Gałąź `poprawa-opisu` powinna być na liście gałęzi scalonych z `main`.

### Usuń gałąź po scaleniu

Na stronie scalonego PR kliknij **Delete branch**, aby usunąć gałąź z GitHuba. Jeśli została usunięta automatycznie, pomiń ten krok. Następnie, pozostając lokalnie na `main`, wykonaj:

```sh
git branch -d poprawa-opisu
git fetch --prune
git branch -a
git status
```

`git branch -d` usuwa lokalną gałąź. Jeśli odmawia, sprawdź, czy wykonano merge i pull; nie zastępuj go automatycznie `-D`. `git fetch --prune` usuwa nieaktualne odwołanie `origin/poprawa-opisu`. Usunięcie gałęzi nie usuwa commitów włączonych do historii `main`.

**Netlify — niewymagane:** po ćwiczeniu możesz samodzielnie rozważyć opublikowanie strony przez [Netlify](https://docs.netlify.com/deploy/create-deploys/), np. przez przesłanie folderu z `index.html` i zasobami strony. Repozytorium GitHub nadal może pozostać prywatne; publiczna strona udostępnia jednak treść CV. Nie przesyłaj katalogu `.git`. Hosting nie jest wymagany i nie wpływa na ocenę.

## Oddanie i ocena

Podczas zajęć pokaż prowadzącemu **końcowe CV w przeglądarce oraz historię zmian w prywatnym repozytorium na swoim koncie GitHub**. Nie trzeba nadawać prowadzącemu dostępu do repozytorium. Końcowa wersja `index.html` oraz wszystkie zasoby potrzebne do jej otwarcia (`assets`, zdjęcie w `images`) mają znajdować się na gałęzi `main`.

Oceniane będą dwa elementy:

1. **Końcowy plik CV (`index.html`)** — własna treść sekcji O mnie, Edukacja i Doświadczenie, podmienione zdjęcie, poprawne linki do LinkedIna i GitHuba, czytelność i działanie strony wraz z zasobami, brak tekstów zastępczych.
2. **Drzewo zmian na GitHubie** — co najmniej 6 własnych logicznych commitów (od nowego commita początkowego) dokumentujących rzeczywisty rozwój CV, opisowe komunikaty, sensowny podział zmian i aktualizacja po pierwszym pushu. Prowadzący przejrzy historię commitów oraz różnice między wersjami. Liniowa historia na `main` wystarczy; dodatkowe gałęzie nie są wymagane.

Nie jest wymagany osobny raport, oddanie planu ani publiczny adres strony. `PLAN.md` może służyć jako pomoc w organizacji pracy. Linki do profili mają być zawarte w CV.

## Dokumentacja i pochodzenie szablonu

- [Przesyłanie lokalnego projektu na GitHub](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)
- [Opcjonalna publikacja w Netlify](https://docs.netlify.com/deploy/create-deploys/)
- Szablon wizualny: **Read Only — HTML5 UP**, adaptacja do ćwiczenia CV. Oryginalne informacje: `README.txt`; licencja: `LICENSE.txt`.
