# Deploy instrukcja - jak wgrać do GitHuba

## Co tu jest

```
devis-lab-readme/
├── README.md         ← nowy README profilu (gotowy do skopiowania)
├── SPEC.md           ← pełna dokumentacja designu (zachowane decyzje)
├── INSTALL.md        ← ten plik
└── assets/
    ├── elixir-dark.svg               ← pixel elixir (dark mode)
    ├── elixir-light.svg              ← pixel elixir (light mode)
    ├── equipment-shelf-dark.svg      ← półka z 6 narzędziami (dark)
    ├── equipment-shelf-light.svg     ← półka z 6 narzędziami (light)
    ├── projects-constellation-dark.svg  ← mapa projektów (dark)
    ├── projects-constellation-light.svg ← mapa projektów (light)
    ├── brewing-now-dark.svg          ← terminal z rotującymi projektami (dark)
    └── brewing-now-light.svg         ← terminal z rotującymi projektami (light)
```

## Wgranie do repo `Devis-Lab/Devis-Lab`

### Wariant A: GitHub Desktop (rekomendowane)

1. Otwórz **GitHub Desktop**
2. **File → Clone repository** → wybierz `Devis-Lab/Devis-Lab` (jeśli nie istnieje, najpierw stwórz go na github.com - profile repo musi się nazywać tak samo jak username)
3. Sklonowane lokalnie, otwórz folder w eksploratorze
4. Skopiuj:
   - `README.md` z tego folderu → do roota sklonowanego repo (nadpisz istniejący)
   - Cały folder `assets/` → do roota sklonowanego repo
5. Wróć do GitHub Desktop - zobaczysz zmiany
6. Commit message: `feat: pixel art elixir hero + equipment shelf + projects constellation + brewing terminal`
7. **Commit to main** → **Push origin**
8. Sprawdź profil na `github.com/Devis-Lab` - powinno renderować

### Wariant B: bezpośrednio przez github.com (drag & drop)

1. Otwórz `github.com/Devis-Lab/Devis-Lab`
2. Kliknij **Add file → Upload files**
3. Przeciągnij cały folder `assets/` z tego stagingu
4. Otwórz `README.md` na github.com → ołówek (edit) → wklej zawartość z `devis-lab-readme/README.md`
5. Commit changes

## Checklist po wgraniu

- [ ] Otwórz `github.com/Devis-Lab` (publiczny widok profilu)
- [ ] Banner się ładuje (pages.dev - bez zmian)
- [ ] Pod tagline widać animowany pixel elixir
- [ ] Klik w elixir → przenosi do `devis-lab.pages.dev/brand-lab`
- [ ] Equipment shelf pokazuje 6 narzędzi z subtelnymi animacjami (świecący mikroskop, kursor laptopa, chip pinów)
- [ ] Projects constellation z `devis-lab` highlighted (mint label)
- [ ] Brewing terminal rotuje 4 projekty (10s loop)
- [ ] Przełącz tryb na light (settings GitHuba) → wszystkie SVG-i mają wersję light

## Znane potencjalne problemy

### Animacje nie działają

GitHub README może blokować niektóre SVG animacje w pewnych kontekstach. Test po pushu:

- Jeśli animacje nie ruszają w README → SVG działają jako statyczne obrazy (ostatnia klatka). Estetyka pixel art zostaje, ale brak ruchu.
- Workaround: konwertować do GIF/PNG (utrata jakości pixel) lub hostować na pages.dev (user wykluczył tę opcję).

### Constellation nodes nie są klikalne

Aktualne SVG-i mają tekstowe label nodes. **Klikalność wymaga obwijania każdego node w `<a>`** wewnątrz SVG. To trzeba dodać ręcznie jeśli chcesz prawdziwe linki do konkretnych repo:

```svg
<a xlink:href="https://github.com/Devis-Lab/repo-name">
  <rect x="9" y="9" width="2" height="2" fill="#4decd4"/>
</a>
```

Albo prościej: pod constellation w README dopisać listę linków:
```markdown
**Projects:** [devis-lab](URL) · [ai-tools](URL) · [pipelines](URL) · ...
```

### Aktualizacja brewing-now

Żeby zmienić rotujące projekty:
1. Otwórz `assets/brewing-now-dark.svg`
2. Znajdź 4 elementy `<text>` z `→ AI workflows for content ops` itd
3. Zmień text wewnątrz drugiego `<tspan>` każdego
4. Powtórz w `brewing-now-light.svg`
5. Commit + push

## Co jeśli profile repo `Devis-Lab/Devis-Lab` jeszcze nie istnieje

GitHub special: repo o nazwie identycznej z username staje się "profile readme" - README z tego repo jest widoczny na stronie profilu.

1. Na github.com kliknij **+ (New repository)**
2. Owner: `Devis-Lab`
3. Repository name: **`Devis-Lab`** (dokładnie tak samo)
4. Public, Add README
5. Następnie wgraj pliki według instrukcji powyżej

## Następne kroki

- [ ] Wgrać pliki
- [ ] Zaktualizować linki w constellation (na razie wszystkie prowadzą do tych samych node-ów - nic nie linkuje na zewnątrz)
- [ ] Opcjonalnie: dodać listę projektów pod constellation jako markdown links (klikalność)
- [ ] Co kilka tygodni: aktualizować `brewing-now-*.svg` z aktualnymi projektami
