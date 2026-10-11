# Wykład 1: Krajobraz zagrożeń, anatomia podatności i zautomatyzowane testowanie kodu

Katalog materiałów dydaktycznych do pierwszego wykładu z przedmiotu **Bezpieczeństwo Aplikacji** (Informatyka, Studia II stopnia magisterskie, Uniwersytet WSB Merito we Wrocławiu).

- **Wykładowca:** mgr Przemysław Żarnecki
- **Repozytorium kursu (Git):** `https://dev.zarnecki.org/Merito/bezpieczenstwo_aplikacji.git`
- **Materiały w chmurze (Nextcloud):** `https://chmura.zarnecki.org/s/iLdT3J5YGTTYCPr`

---

## Zawartość katalogu

```text
wyklad_01/
├── README.md               # Niniejszy przewodnik dla prowadzącego
├── obrazy/                 # Zasoby graficzne wykorzystywane w materiałach
│   ├── ekspres_ithardware.jpg # Zdjęcie ekspresu Keurig z artykułu o transferze 1 TB danych
│   └── logo_merito.png     # Oficjalne logo Uniwersytetu WSB Merito
├── prezentacja/            # Prezentacja wykładowa w HTML
│   └── index.html          # Samodzielny, interaktywny deck slajdów (działa offline)
└── skrypt/                 # Skrypt akademicki w LaTeX
    ├── wyklad_01_skrypt.tex # Źródło LaTeX (styl WSB Merito, tcolorbox, listings)
    └── wyklad_01_skrypt.pdf # Skompilowany dokument PDF (8 stron, gotowy do dystrybucji)
```

---

## 1. Prezentacja HTML (`prezentacja/index.html`)

Prezentacja została przygotowana jako lekka, w 100% samodzielna strona HTML/CSS/JS (brak zewnętrznych zależności CDN czy npm — działa w pełni offline w salach wykładowych).

### Jak uruchomić:
Wystarczy dwukrotnie kliknąć plik `index.html` lub otworzyć go w dowolnej przeglądarce (Chrome, Firefox, Safari, Edge):
```bash
xdg-open prezentacja/index.html
```

### Sterowanie i interakcja:
- **`→` / `Spacja` / `PageDown` / `L` / `J`**: Następny slajd (główny rozdział poziomy).
- **`←` / `PageUp` / `H` / `K`**: Poprzedni slajd.
- **`↓` / `Kółko myszy w dół`**: Przewinięcie aktywnego slajdu do sekcji szczegółowych (*drill-down* / słowniczek / karty podatności).
- **`↑` / `Kółko myszy w górę`**: Przewinięcie aktywnego slajdu do góry.
- **Kliknięcie wiersza w tabeli OWASP Top 10**: Płynne zjechanie w dół do dedykowanej analizy danej podatności (A01–A10).
- **`Home` / `End`**: Skok do pierwszego / ostatniego slajdu.
- **`F`**: Włączenie / wyłączenie trybu pełnoekranowego (*Fullscreen*).
- **`O` / `Esc`**: Otwarcie / zamknięcie siatki podglądu wszystkich slajdów (*Overview lightbox*).

### Układ slajdów (12 głównych osi tematycznych z rozwinięciami w dół):
1. **Strona tytułowa** — branding WSB Merito, metadane kursu, studia magisterskie II stopnia, link do repozytorium git.
2. **Humorystyczne otwarcie** — *„Kochanie, czy nasz ekspres do kawy właśnie pinguje Chiny?”* (zdjęcie ekspresu z ITHardware, statystyki routera: 1 TB wysłanych danych w 10 dni).
3. **Anatomia incydentu** — Dlaczego to nie był ekspres, a podatny serwer Linux z otwartym REST API, domyślnymi hasłami i włączeniem do botnetu.
4. **Upadek koncepcji Zamku i Fosy** — Dlaczego tradycyjne zapory sieciowe (firewalle L3/L4) są ślepe na ataki w warstwie aplikacji.
5. **Warstwa L7, AI i Słownik skrótów** — 80-90% zewnętrznych bibliotek, błędy logiki biznesowej, **halucynacje pakietów AI (AI Package Hallucination / Slopsquatting)**, niezweryfikowany kod generowany przez LLM + **rozwijany słowniczek skrótów (L7, WAF, IDOR, BOLA, ORM, CVE, SBOM, ReDoS)**.
6. **OWASP Top 10 (2025) & Szczegółowa anatomia** — Tabela główna z możliwością kliknięcia dowolnej pozycji i zjechania do kart analitycznych (A01 Broken Access Control & SSRF, A02 Misconfiguration, A03 Supply Chain, A04 Cryptography, A05 Injection, A06-A10 Design, Auth, Integrity, Logs, Exceptions).
7. **Modelowanie zagrożeń (STRIDE) & Scenariusze** — 6 głównych kafelków + zjazd w dół do realnych scenariuszy architektonicznych (Spoofing z fałszywym tokenem, Tampering z parametrem ceny, Repudiation bez logów, DoS z nielimitowanym API, Elevation z mass-assignment).
8. **Triada automatyzacji (SAST, DAST, SCA) & Macierz inżynierska** — Wprowadzenie + zjazd w dół do pełnej tabeli porównawczej (perspektywa, narzut czasowy, false positives) oraz szczegółowych opisów analizy AST / Fuzzingu / SBOM.
9. **Narzędzia w akcji (CLI) & Reguły własne** — Autentyczne makiety terminala (Semgrep findings box, Trivy CVE table) + zjazd w dół do tworzenia własnych reguł Semgrep w YAML oraz definicji potoku GitHub Actions.
10. **Podejście Shift-Left** — Wykres relacji kosztów usuwania luki: od 1x (w edytorze IDE) do 100x+ (na produkcji / wyciek RODO).
11. **Złote zasady: Secure by Design** — Least Privilege, Defense in Depth, Zero Trust Input, Secure Defaults.
12. **Most do laboratorium** — Wprowadzenie do platformy *KrasnalShop* w kontenerach Docker Compose, zadania zaliczeniowe, rola studenta studiów magisterskich jako architekta i audytora bezpieczeństwa.

---

## 2. Skrypt wykładowy (`skrypt/wyklad_01_skrypt.pdf`)

Uniwersalny, 8-stronicowy skrypt akademicki przygotowany w LaTeX:
- **Styl graficzny**: Oficjalne kolory WSB Merito (`#141E50`, `#006EFA`), typografia TeX Gyre Heros (Helvetica), przejrzyste ramki `tcolorbox`.
- **Zawartość merytoryczna**: Pełny opis inżynierski bez zbędnego żargonu biurokratycznego, wzbogacony o zagadnienia AI (halucynacje zależności, kod generowany przez LLM) oraz słowniczek pojęć.
- **Kompilacja**:
  ```bash
  pdflatex -interaction=nonstopmode wyklad_01_skrypt.tex
  ```
