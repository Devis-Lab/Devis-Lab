# Devis-Lab Profile README — Design Spec

**Data:** 2026-05-21
**Status:** Approved, ready to ship
**Target repo:** `github.com/Devis-Lab/Devis-Lab` (profile README)

## Cel

Wzbogacić README profilu GitHub o pixel-art elementy spójne z istniejącym banerem (`devis-lab.pages.dev/brand/github-banner-pixel-blue-*.png`). Banner zostaje nietknięty — wszystkie nowe assety lądują w repo `Devis-Lab/Devis-Lab` i są serwowane przez GitHub raw.

## Constraints

- **NIE TYKAĆ** plików strony `devis-lab.pages.dev` — tym zarządza Codex.
- Wszystkie SVG idą do repo profilu jako `assets/*.svg`.
- Wsparcie dla `prefers-color-scheme: dark` i `light` przez `<picture>` (jak istniejący banner).
- Stonowane, pixel-art, brand-spójne (cyan→violet gradient + mint `#4DECD4` akcent).

## Final story — kolejność elementów w README

1. **Banner** (istniejący, z pages.dev) — bez zmian
2. **Tagline** — bez zmian (`Small lab. Big projects. Clear signal.` + `Building digital products...`)
3. **🆕 ELIXIR HERO** — animowany pixel art Erlenmeyer flask, klikalny → `/brand-lab`
4. **CTA** — `Take me to the Lab ->` (bez zmian)
5. **🆕 Pixel divider** — subtelny separator (linia + mint/violet kropki)
6. **🆕 `// lab.equipment()`** — shelf z 5 pixel narzędziami (flask, tube, scope, code, chip, ✦)
7. **🆕 `// lab.projects()`** — constellation map (klikalne nody, `devis-lab` highlighted)
8. **🆕 `// lab.brewing.now()`** — terminal-style auto-typing z aktualnymi projektami

## Paleta kolorów

### Dark mode (na `#0d1117` → `#1a1340` → `#2d1b4e` background)
- **Mint accent (z bannera!):** `#4DECD4` (main), `#80F4E5` (light), `#26D4C0` (dark)
- **Cyan liquid:** `#4dd0e1`, `#26c6da`, `#00bcd4`, `#0097a7`
- **Violet liquid:** `#5e35b1`, `#673ab7`, `#7c4dff`, `#6200ea`, `#4527a0`, `#311b92`
- **Magenta accent:** `#e040fb` (krzyżyki)
- **Glass (kolba):** `#5f7a9f` (walls), `#7a8cb3` (rim), `#4a5680` (cork dark)
- **Background base:** `#1a2847` (bottom liquid), `#11161f` (cards)

### Light mode (na `#d4f5ed` → `#e8e8ff` → `#e6d4ff` background)
- **Mint accent:** `#00BFA5` (main), `#1DE9B6` (light), `#00897B` (dark)
- **Cyan liquid:** `#00838f`, `#00897b`, `#006064`
- **Violet liquid:** `#5e35b1`, `#4527a0`, `#311b92`, `#1a0f5e`
- **Magenta accent:** `#9c27b0`
- **Glass:** `#7a8cb3` (walls), `#6b7896` (rim), `#3d4a6b` (cork dark)

## Komponent 1 — Elixir Hero

**Plik:** `assets/elixir-dark.svg` + `assets/elixir-light.svg`
**Wymiary SVG:** viewBox `0 0 44 64`, wyświetlany ~120px szerokości w README
**Klikalność:** cały SVG owinięty w `<a href="https://devis-lab.pages.dev/brand-lab">`

### Struktura

- **Pixel clusters** (statyczne, mrugają):
  - Lewy: `(2,28)` 2x2 mint + `(1,31)` 1x1 light-mint — twinkle 2.6s
  - Prawy: krzyżyk ✦ `(40,28)+(39,29 3px)+(40,30)` mint — twinkle 3s, delay 1.1s
- **Mint particles** (6 sztuk, wystrzelają z otworu kolby, fade-out trajektorie):
  - P1: `(21,11)→(20,6)→(18,0)`, 2.4s, 1x1
  - P2: `(22,10)→(22,5)→(22,-2)`, 2.8s + 0.5s delay, 2x2 light-mint
  - P3: `(24,11)→(25,6)→(27,1)`, 2.6s + 1s delay, 1x1
  - P4: `(20,11)→(18,7)→(15,3)`, 3s + 0.2s delay, 1x1 dark-mint
  - P5: `(24,10)→(26,6)→(29,2)`, 2.7s + 1.4s delay, 2x2
  - P6: `(23,11)→(23,5)→(24,-1)`, 2.5s + 1.8s delay, 1x1 light-mint
- **Kolba (Erlenmeyer):**
  - Cork: y=15-17 (3 rows)
  - Rim: y=18 (10px wide)
  - Neck: y=19-24 (2px walls każda strona, gap 4px środek)
  - Body cone: y=25-37 (wall expanding outward by 1px per row each side)
  - Body vertical: y=37-49 (28px wide)
  - Base: y=50-52
- **Liquid:** y=32-48 (17 rows)
  - Mint top: y=32-34 (`#4DECD4`, `#26D4C0`, `#26C6DA`)
  - Cyan mid-upper: y=34-36 (`#00BCD4`, `#0097A7`)
  - Violet blend: y=37-44 (`#5E35B1`, `#673AB7`, `#7C4DFF`, `#6200EA`)
  - Deep violet bottom: y=45-48 (`#5E35B1`, `#4527A0`, `#311B92`, `#1A2847`)
- **Mint core** (świetlisty rdzeń jak w środku logo D):
  - `(21,39)` 2x2 `#4DECD4` + `(20,40)` 1x1 `#80F4E5` + `(23,40)` 1x1 `#80F4E5`
  - Animacja: opacity pulse 0.8→1.0, 2.2s
- **Bubbles** (animowane, idą w górę, fade):
  - B1: x=14 `#80F4E5`, y=46→42→38, 2.5s
  - B2: x=26 `#4DECD4`, y=48→44→40, 2.8s + 0.5s delay
- **Highlight** (mint na szkle): `(10,35-44)` mint @0.5 + `(18,21-23)` light-mint @0.6

### Decyzje designerskie (historia iteracji)

- v1: Klasyczny SVG vector (gładki) — odrzucone, użytkownik chciał true pixel
- v2: Pixel art ale za dużo elementów wokół (9 pikseli rozsianych) — odrzucone, "za dużo"
- v3: Mint core dodany do wnętrza płynu — przybliżony do celu ale wciąż za dużo elementów wokół
- v4: Cząsteczki mint wystrzelają z otworu kolby + 2 statyczne clustery — kierunek OK
- v5 (FINAL): Krzyżyk przeniesiony z dołu na prawy bok dla balansu z lewym clusterem

## Komponent 2 — Equipment Shelf

**Plik:** `assets/equipment-shelf-dark.svg` + `assets/equipment-shelf-light.svg`
**Wymiary:** viewBox `0 0 100 18`, wyświetlany ~320px szerokości
**Nagłówek w README:** `// lab.equipment()` (cyan/violet monospace)

### Items na półce (od lewej)

1. **Mini kolba** (echo elixiru): x=2-9, body z mint+violet liquid (subtelny callback)
2. **Probówka:** x=17-21, violet liquid z mint top
3. **Mikroskop:** x=29-38, mint lens
4. **Laptop/code:** x=43-58, czarny ekran z cyan/violet/light-mint kodem
5. **AI chip:** x=66-76, dark socket z mint+violet pinami i 6 side-pins
6. **Pixel sparkle ✦:** x=88-93, mint krzyżyk + violet 2x2

**Półka:** y=16 (`#3d4a6b`) + y=17 (`#2d3b58`) — pasek u dołu
**Subtitle pod shelf:** `flask · tube · scope · code · chip · ✦`

## Komponent 3 — Projects Constellation

**Plik:** `assets/projects-constellation-dark.svg` + `assets/projects-constellation-light.svg`
**Wymiary:** viewBox `0 0 70 40`, wyświetlany ~320px szerokości
**Nagłówek w README:** `// lab.projects()`

### Nodes (klikalne — każdy `<a href="...">`)

1. **devis-lab** (HIGHLIGHTED, `#4DECD4`, light-mint label `#80F4E5`): node at (9,9), 2x2 → linkuje do `devis-lab.pages.dev/brand-lab`
2. **ai-tools** (violet `#7C4DFF`): (21,17), 3x3 → TBD link
3. **pipelines** (mint `#4DECD4`): (34,7), 2x2 → TBD link
4. **content-ops** (magenta `#E040FB`): (37,27), 3x3 → TBD link
5. **automations** (mint `#4DECD4`): (49,13), 2x2 → TBD link
6. **tools** (violet): (54,29), 2x2 → TBD link
7. **experiments** (mint): (57,21), 3x3 → TBD link

### Lines (constellation connections)

Stroke `#3d4a6b` 0.3px:
- (10,10)→(22,18), (22,18)→(35,8), (22,18)→(38,28), (35,8)→(50,14), (38,28)→(55,30), (50,14)→(58,22)

**Labels:** font-size 2.5, monospace, `#5f7a9f` (default) / `#80F4E5` (devis-lab highlighted)
**Subtitle:** `click any node → open project`

## Komponent 4 — Brewing Now Terminal

**Implementacja:** Auto-typing SVG. Dwie opcje:
- **A) Własny SVG z SMIL** (więcej kontroli, ale 100+ linii)
- **B) Generator readme-typing-svg** (URL-config, łatwo aktualizować)

**Rekomendacja:** A — własny SVG dla pełnej kontroli + brand-spójność (cyan/mint colors). Jeśli czas presses → B z customizowanymi parametrami koloru.

### Layout (jeśli A — własny SVG)

- Tło ramki: `#11161f` (rounded 6px)
- Top: `━━ devis-lab.log ━━` w `#5f7a9f` mono 10px
- Prompt: `$ now_brewing()` w `#4DECD4`
- Output (typing): `→ <project>` w `#80F4E5`, blinking cursor `#4DECD4`
- Rotating items:
  - "AI workflows for content ops"
  - "Automation pipelines"
  - "Digital products"
  - "Brand experiments"
- Footer: `// rotating · automation · digital products · ai-tools` w `#7c4dff` 10px

### Layout (jeśli B — readme-typing-svg)

URL pattern:
```
https://readme-typing-svg.demolab.com?font=Consolas&size=14&pause=1500&color=4DECD4&background=11161f&center=true&vCenter=true&width=400&height=30&lines=AI+workflows+for+content+ops;Automation+pipelines;Digital+products;Brand+experiments
```

## Wgranie do repo

### Files to add do `Devis-Lab/Devis-Lab`

```
assets/
  elixir-dark.svg
  elixir-light.svg
  equipment-shelf-dark.svg
  equipment-shelf-light.svg
  projects-constellation-dark.svg
  projects-constellation-light.svg
README.md  (nowy, zastępuje istniejący)
```

### Linki w README

SVG-i serwowane via GitHub raw URL pattern:
```
https://raw.githubusercontent.com/Devis-Lab/Devis-Lab/main/assets/elixir-dark.svg
```
LUB relatywnie (`assets/elixir-dark.svg`) — GitHub renderuje OK dla README profili.

**Uwaga:** Animowane SVG nie działają w niektórych kontekstach GitHub. Test po pushu obowiązkowy. Jeśli animacje nie ruszają — alternatywa: hostować SVG na pages.dev (ale user prosi nie tykać tej części).

## Final README.md structure

Patrz: `devis-lab-readme/README.md` (gotowy do skopiowania)

## Deploy steps

Patrz: `devis-lab-readme/INSTALL.md`
