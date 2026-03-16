# Přehled materiálů — AristoTelos WFM

## O aplikaci

**AristoTelos** je systém pro profesionální plánování a řízení směn v kontaktních centrech.
Claim: "Profesionální plánování a řízení směn s čistou hlavou"

Hlavní oblasti funkcionality:
- Plánování směn (automatické i manuální)
- Předpovědi objemu práce (statistické + ML)
- Požadavky zaměstnanců (dovolené, preference, výměny směn)
- Reporting a export dat
- API integrace s externími systémy

## Dokumenty v repo

### Use Cases (docs/use-cases/)

| Soubor | Obsah |
|--------|-------|
| UseCasePlanovani.md | Automatické plánování směn — příprava podkladů, automatizace, legislativa, interní pravidla |
| UseCasePredictions.md | Předpovědi objemu práce — statistické metody, ML, vizualizace, export |
| Use case Pozadavky.md | Požadavky zaměstnanců — typy požadavků, zadávání, limity, schvalování, rezervace směn |

### API Specifikace (docs/api/)

| Soubor | Obsah |
|--------|-------|
| WFM-API-Requirements.md | Minimální požadavky na API — OAuth 2.0, REST/JSON, bulk sync, admin, import, reporting, agentury |

### Video materiály (docs/videos/)

| Soubor | Obsah | Stav |
|--------|-------|------|
| intro-frames/ | Snímky z úvodního videa aplikace (10 framů) | Zpracováno |
| O2 use case video (96 min) | Demo AristoTelos pro O2 | K přepisu |
| EON schůzka (54 min) | Jednání AristoTelos s E.ON | K přepisu |
| ČSAS transcript | Teams transcript — PRÁZDNÝ placeholder | Potřeba stáhnout .vtt z Teams |
| ČSAS pokračování transcript | Teams transcript — PRÁZDNÝ placeholder | Potřeba stáhnout .vtt z Teams |

## Hlavní sekce aplikace (z úvodního videa)

1. **Nastavení** — Konfigurace systému
2. **Plány směn** — Hlavní pracovní obrazovka s kalendářovým přehledem
3. **Reporty** — Reporting a export

## Klíčové funkce (shrnutí z use-casů)

### Plánování směn
- Automatické plánování na základě predikce objemu práce
- Zohlednění kvalifikací, kompetencí a znalostí zaměstnanců
- Dodržení legislativy (pracovní doba, odpočinek, přesčas)
- Konfigurovatelná pravidla (rotace, víkendy, noční, home office)
- Plánování přestávek, porad, školení, 1:1 setkání

### Předpovědi
- Statistické metody (měsíce, týdny, dny, intervaly)
- Strojové učení pro komplexní vzory
- Předpověď průměrné doby zpracování (AHT)
- Manuální korekce pro známé vlivy
- Near-realtime import dat z externích zdrojů

### Požadavky zaměstnanců
- Dovolené, lékař, dny volna, home office, preferované směny
- Konfigurovatelný schvalovací proces (1-2 stupně)
- Limity požadavků (denní, per období, auto-schválení)
- Výměna směn mezi kolegy
- Rezervace budoucích směn

### API
- OAuth 2.0 (Client Credentials)
- REST/HTTPS + JSON
- Bulk sync (org struktura, personální data, číselníky)
- Admin API (smlouvy, modely, aktivity, skills, fronty)
- Import (historická data, předpovědi, realtime stavy)
- Reporting API (export do DWH, mzdový systém)
- API pro agentury práce
