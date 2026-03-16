# AT — App Toolkit

Sada nástrojů pro automatizované prozkoumání webové aplikace a tvorbu interaktivní nápovědy a prezentací.

## Co to umí

| Skill | Popis |
|-------|-------|
| **app-discovery** | Systematicky prokliká aplikaci, udělá screenshoty, zmapuje navigaci a procesy |
| **interactive-help-builder** | Z discovery dat vygeneruje interaktivní HTML nápovědu s vyhledáváním |
| **app-presenter** | Z discovery dat vytvoří interaktivní HTML prezentaci hlavních funkcí |

## Struktura projektu

```
AT/
├── skills/                          # Claude Cowork skilly
│   ├── app-discovery/SKILL.md
│   ├── interactive-help-builder/SKILL.md
│   └── app-presenter/SKILL.md
├── discovery-data/                  # Data z průzkumu aplikace
│   └── screenshots/                 # Screenshoty obrazovek
├── outputs/                         # Výstupní soubory (HTML help, prezentace)
├── docs/                            # Projektová dokumentace
│   └── zadani.md                    # Zadání projektu
└── README.md
```

## Jak to funguje

### Fáze 1: Průzkum (app-discovery)
Claude dostane URL a přihlášení k aplikaci. Prokliká celou navigaci, udělá screenshoty každé obrazovky a zmapuje hlavní procesy. Výstup uloží do `discovery-data/`.

### Fáze 2: Nápověda (interactive-help-builder)
Z discovery dat se vygeneruje kompletní HTML help systém — sidebar navigace, screenshoty s anotacemi, krokové návody, FAQ, vyhledávání.

### Fáze 3: Prezentace (app-presenter)
Z discovery dat se vytvoří interaktivní HTML prezentace hlavních funkcí — slideshow s přechody, anotovanými screenshoty a workflow demy.

## Použití

1. Nainstaluj skilly do Claude Cowork (`.skill` soubory ve složce `skills/`)
2. Otevři novou session v Cowork
3. Zadej URL aplikace a přihlašovací údaje
4. Spusť postupně fáze 1–3 (viz `docs/zadani.md`)

## Technologie

- Claude Cowork + Claude in Chrome (browser automation)
- HTML/CSS/JS (self-contained výstupy)
- JSON (strukturovaná discovery data)
