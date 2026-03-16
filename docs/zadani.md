# Zadání: Interaktivní nápověda a prezentace aplikace

## Kontext

Máme složitou webovou aplikaci se složitými procesy. Cílem je vytvořit:

1. **Interaktivní nápovědu** — HTML help systém, kde si uživatelé najdou jak co funguje, s vyhledáváním, screenshoty a krok-za-krokem návody
2. **Interaktivní prezentaci hlavních funkcionalit** — Vizuální HTML prezentace, kterou si může proklikat nový uživatel, stakeholder nebo kolega při onboardingu

## Co potřebuji

Potřebuji přístup do aplikace přes prohlížeč (URL + přihlašovací údaje). Claude si aplikaci sám prokliká, udělá screenshoty, zmapuje navigaci, obrazovky a hlavní procesy, a z toho pak vygeneruje oba výstupy.

## Postup — 3 fáze

### Fáze 1: Průzkum aplikace (app-discovery skill)

Claude dostane URL a přihlášení k aplikaci a systematicky ji prozkoumá:

- Prokliká celou navigaci a všechny hlavní sekce
- Udělá screenshoty každé důležité obrazovky
- Zmapuje strukturu aplikace (menu, podmenu, sekce)
- Projde hlavní pracovní postupy (workflows) krok za krokem
- Zaznamená poznámky — co je matoucí, co může uživatele zmást, co je fajn
- Výstup: složka `discovery-data/` se strukturovanými JSON soubory a screenshoty

**Pokyny pro tuto fázi:**
```
Mám aplikaci na [URL]. Přihlašovací údaje: [username / password].
Použij skill app-discovery a prozkoumej celou aplikaci. Proklikej všechny sekce,
udělej screenshoty a zmapuj hlavní procesy. Všechna data ulož do discovery-data/.
```

### Fáze 2: Vytvoření interaktivní nápovědy (interactive-help-builder skill)

Z discovery dat se vygeneruje kompletní HTML help systém:

- Sidebar navigace zrcadlící strukturu aplikace
- Stránky pro každou funkci s popisem, screenshoty a návody
- Krokové návody pro hlavní procesy (workflows)
- FAQ sekce
- Řešení problémů (troubleshooting)
- Fulltextové vyhledávání (client-side)
- Responzivní design (funguje i na mobilu)

**Pokyny pro tuto fázi:**
```
V discovery-data/ jsou zmapovaná data z naší aplikace. Použij skill
interactive-help-builder a vytvoř z nich kompletní interaktivní HTML nápovědu.
Piš v češtině. Nápověda by měla pokrýt všechny hlavní funkce a procesy.
```

### Fáze 3: Vytvoření interaktivní prezentace (app-presenter skill)

Z discovery dat se vytvoří vizuální prezentace hlavních funkcí:

- Slideshow formát s plynulými přechody
- Screenshoty s anotacemi a callouty
- Workflow demo — proklikávací kroky procesů
- Ovládání šipkami, myší i na dotykových zařízeních
- Fullscreen režim

**Pokyny pro tuto fázi:**
```
V discovery-data/ jsou data z průzkumu naší aplikace. Použij skill app-presenter
a vytvoř interaktivní HTML prezentaci hlavních funkcionalit. Cílová skupina:
[noví uživatelé / stakeholdeři / interní tým]. Jazyk: čeština.
```

## Nainstalované skilly

Před spuštěním je třeba nainstalovat tyto 3 skilly (přiložené .skill soubory):

1. **app-discovery** — Systematický průzkum a mapování webové aplikace
2. **interactive-help-builder** — Generování interaktivní HTML nápovědy
3. **app-presenter** — Tvorba interaktivní HTML prezentace

## Celkový prompt pro novou session

Zkopíruj toto do nové session:

---

```
Ahoj, mám projekt na vytvoření interaktivní nápovědy a prezentace pro naši aplikaci.

Mám nainstalované 3 skilly: app-discovery, interactive-help-builder a app-presenter.

Aplikace je na: [URL]
Přihlášení: [username] / [password]

Prosím postupuj takto:

1. Použij skill app-discovery — proklikej celou aplikaci, udělej screenshoty,
   zmapuj navigaci, obrazovky a hlavní pracovní postupy. Všechno ulož do discovery-data/.

2. Až bude průzkum hotový, ukaž mi co jsi našel (hlavní sekce, kolik obrazovek,
   kolik procesů) a já ti řeknu jestli je to kompletní nebo jestli něco chybí.

3. Pak použij skill interactive-help-builder a vytvoř HTML nápovědu v češtině.

4. Pak použij skill app-presenter a vytvoř HTML prezentaci hlavních funkcí
   pro nové uživatele, taky v češtině.

Neptej se mě na zbytečnosti, prostě to udělej. Když si nebudeš jistý, použij
nejlepší úsudek. Po každé fázi mi ukaž výsledek a já řeknu co upravit.
```

---

## Další nápady na budoucí rozšíření

- **Onboarding wizard** — Interaktivní průvodce prvním spuštěním (step-by-step setup)
- **Video-style walkthrough** — Animovaný GIF/video z proklikávání aplikace
- **Procesní mapy** — Vizuální diagramy (flowcharty) hlavních procesů
- **Changelog helper** — Skill na dokumentování změn v aplikaci
- **Kontextová nápověda** — Tooltips/popovery přímo v aplikaci (vyžaduje úpravu zdrojového kódu)
