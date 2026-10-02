# U Edka — strona uedka.gwar.bar

Statyczny HTML/CSS, bez frameworka, bez builda, bez zależności. Hosting: GitHub Pages (`CNAME` → `uedka.gwar.bar`), repo `gwarbar/gwarmenuponte`. Lokal: **U Edka — Zapiekanki w stylu PRL, Mostowa 4, Kraków (Kazimierz)**.

## Mapa stron

| Adres | Plik | Rola |
|---|---|---|
| `/` | `index.html` | Landing PL pod Google Ads (cel: wizyta w lokalu → „Wyznacz trasę") |
| `/en` | `en.html` | Landing EN (osobny plik, nie generowany) |
| `/ordergwar` | `ordergwar.html` | Instrukcja zamawiania dla gości Baru Gwar (cel nowych kodów QR) |
| `/landing` | `landing.html` | Przekierowanie na `/` |
| `/jak-zamowic` | `jak-zamowic.html` | Przekierowanie na `/ordergwar` |
| `/menu-u-edka` | `menu-u-edka.html` | Stare menu PL/EN — **nieaktualne** (ma „Na działce", brak ceny bagietek) |
| `/regulamin`, `/polityka-prywatnosci` | | Podlinkowane z GoPOS — nie zmieniać adresów |
| `/google05588f61c778d423.html` | | Weryfikacja Google Search Console — nie usuwać |

`mapa.html`, `pdf/`, `JeanLuc-Webfonts/`, `images/` to pozostałości Baru Gwar — nie ruszać bez pytania.

## Zasady treści

- Nie wymyślać informacji o lokalu: cen, pozycji menu, opinii, usług, numeru telefonu, kodu pocztowego. Źródłem prawdy jest tablica menu (`assets/uedka/foto/tablica-menu-*.webp`) i to, co poda właściciel.
- Godziny: Pon–Pt 13:00–00:00, Sob 12:00–00:00, Nd 12:00–23:00.
- Menu PL = zdjęcie tablicy; menu EN = tekst w `en.html`. **Zmiana cen → poprawić oba miejsca.** Nazwy bagietek (Na Gubałówce, W Hotelu Forum, Na Hawajach) zostają po polsku także w EN; drugi blok menu EN nazywa się „Our compositions".
- Każda zmiana w `index.html` ma swój odpowiednik w `en.html` (i odwrotnie).
- Właściciel nie chce zdjęć pojedynczych zapiekanek — tylko zdjęcie grupowe (na dole, w sekcji zamówienia).

## Linki

- Zamówienia z odbiorem: `https://uedka.goorder.pl/` (tylko po polsku — w EN jest o tym dopisek).
- Trasa: `https://www.google.com/maps/dir/?api=1&destination=U+Edka%2C+Mostowa+4%2C+Krak%C3%B3w`.
- Dostawa (Pyszne, Uber Eats, Wolt, Glovo, Bolt Food): `utm_source=uedka.gwar.bar&utm_medium=referral`, w EN dodatkowo `utm_content=en`. Nie dodawać parametrów Google (`rwg_token` itp.).
- Instagram: `https://www.instagram.com/u.edka/`.

## Tracking

- Google Ads tag `AW-17300910083` w `<head>` obu landingów. GA4 brak.
- Kliknięcia: atrybuty `data-track` / `data-track-location` → skrypt na końcu strony wysyła `gtag('event', …)` z `cta_location` i `page_lang`. Zdarzenia: `wyznacz_trase`, `zobacz_menu`, `zamow_z_odbiorem`, `zamow_z_dostawa`, `dostawa`, `instagram`, `jezyk`.
- Etykiety konwersji Google Ads jeszcze nie podane. Brak banera zgody na cookies (Consent Mode v2) — otwarta decyzja właściciela.
- Nie dodawać innych trackerów ani wymyślonych ID.

## Wydajność (PageSpeed mobile 100 — nie zepsuć)

- Zero zasobów blokujących renderowanie: CSS inline, brak Google Fonts.
- Bebas Neue hostowany lokalnie (`assets/uedka/fonts/BebasNeue-latin*.woff2`), preload, `font-display: swap` + font zastępczy `Bebas Fallback` (Arial, `size-adjust: 58%`) i `text-transform: uppercase` — dzięki temu podmiana fontu nie przesuwa układu. Przyciski mają `white-space: nowrap`.
- **Pliki HK Grotesk w `assets/uedka/fonts/` są uszkodzone** (nie dekodują się). Landingi używają fontu systemowego; inne strony nadal je ładują.
- Obrazy: WebP w kilku szerokościach z `srcset`/`sizes`, zawsze `width`/`height`, poniżej pierwszego ekranu `loading="lazy"`. Logo = PNG 16 kolorów (`uedka-logo-landing-400/800.png`). Oryginał `uedka-logo.png` (399 KB) nie trafia na landing.
- Mobile-first: wszystkie CTA hero mieszczą się na pierwszym ekranie przy 375×812.

## Praca lokalna i deploy

- Podgląd: `.claude/launch.json` → `npx serve -l 4173 .` (czyste adresy jak na Pages: `/en`, `/ordergwar`).
- Deploy = push na `main`. GitHub Pages publikuje w ok. 1–2 min; potwierdzać przez `curl "https://uedka.gwar.bar/?t=$RANDOM"`.
- Pages wysyła `cache-control: max-age=600` — przeglądarka może przez 10 min pokazywać starą wersję. Nie da się tego zmienić w repo.
- W repo regularnie zostaje pusty `.git/index.lock` bez procesu git. Jeśli jest starszy niż minuta i `pgrep -x git` nic nie zwraca, można go usunąć.
- Push na `main` tylko na wyraźną prośbę właściciela.
