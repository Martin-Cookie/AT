Specifikace API Workforce Management systému
============================================

Tento dokument definuje minimální požadavky na API pro integraci
Workforce management systému s ostatními softwarovými platformami.

Funkční rozsah integrace
------------------------

-   Autentizace a autorizace klientských aplikací pomocí OAuth 2.0.
    Správa

-   Bulk Synchronization API: hromadná synchronizace kmenových dat
    (personální data zaměstnanců, organizační struktura, pracovní
    pozice, atd.)

-   Administrativní API: administrace a konfigurace WFM z externích
    systémů přes API.

-   API pro import provozních dat: import historických dat, předpovědí
    objemů práce, potřeb provozu a stavů zaměstnanců ze zdrojových
    systémů přes API.

-   API pro reporting: automatický reporting/export dat do cílových
    systémů (DWH, mzdový system) přes API.

-   API pro komunikaci s agenturami práce: objednávání externích
    agenturních pracovníků, obsazování volných směn agenturami,
    reporting směn odpracovaných agenturami přes API.

Dokumentace
-----------

Dodavatel poskytne kompletní a aktuální technickou dokumentaci včetně
OpenAPI specifikace (OAS 3.x) pro veškeré endpointy zahrnuté v rozsahu
dodávky.

Formáty a protokoly
-------------------

-   REST over HTTPS (TLS 1.2+)

-   JSON payloady pro aplikační endpointy

-   Paging/Filtering

Bezpečnost a přístupová práva
-----------------------------

### OAuth 2.0 -- Client Credentials

Dodavatel musí implementovat a doložit následující:

-   Získání access tokenu pomocí grant\_type=client\_credentials.

-   Předání client\_id a client\_secret v těle požadavku
    (x-www-form-urlencoded).

-   Vrácení access\_token, token\_type (bearer) a doby exporace v
    sekundách.

-   Obnova tokenu při vypršení platnosti nebo při chybách 401/403.

-   Externí dodavatelé/agentury musí používat samostatné client
    credentials

### Použití Bearer tokenu

-   Všechny chráněné endpointy musí přijímat hlavičku Authorization:
    Bearer \<access\_token\>.

-   Dodavatel popíše požadavky na cache tokenu, doporučené chování při
    souběžných požadavcích a rotaci tajných klíčů.

### Oprávnění a přístupová matice

Přístup k API metodám je řízen oprávněními, dodavatel dodá kompletní
matici oprávnění mapující pro každý endpoint.

Chybové stavy a interoperabilita
--------------------------------

Dodavatel musí jednotně podporovat standardní HTTP kódy a popsat
minimálně následující kódy:

401 -- validační chyba (doporučeno application/problem+json).

402 - neoprávněný přístup (neplatný/expirující token).

403 -- zakázáno (nedostatečná práva).

404 -- nenalezeno (pro item endpointy).

422 -- validační chyba pro business pravidla (kde je relevantní).

500 -- interní chyba serveru (včetně návratové struktury).

Funkční moduly a minimální katalog endpointů
--------------------------------------------

### Bulk Synchronization API

WFM musí implementovat endpointy pro hromadnou synchronizaci dat:

-   Organizační struktury

-   Personálních dat zaměstnanců

    -   Smlouvy

    -   Úvazky

    -   Role

    -   Pozice

    -   Uživatelsky definovatelné vlastnosti

    -   Nároky na nepřítomnosti

-   Číselníků

    -   Pracovní smlouvy

    -   Modely pracovní doby

    -   Pracovní pozice

### Administrativní API

WFM musí implementovat endpointy pro administraci v minimálním rozsahu:

-   Pracovní smlouvy

-   Modely pracovní doby

-   Aktivity, typy přestávek, ptupy nepřítomností

-   Typy požadavků

-   Pracovních pozic

-   Rolí

-   Znalostí/Skills

-   Front/Queues

-   Externích událostí změn stavu a stavů zaměsntanců

-   Časových preferencí zaměstnanců

API pro import provozních dat
-----------------------------

WFM musí implementovat minimálně endpointy pro import provozních dat:

-   Historických dat na jednotlivých typech práce/komunikačních kanálech
    a frontách

-   Předpovědi objemu práce na jednotlivých typech práce/komunikačních
    kanálech a frontách

-   Realtime stavů zaměstnanců pro vyhodnocení adherence, optimálně přes
    protokol WebSoket

API pro reporting
-----------------

WFM musí umožňovat uživatelsky definovat reporty, které jsou dostupné
jak v uživatelském rozhraní, tak přes API pro export dat do externích
systémů. API pro reporty musí umožňovat stránkování a filtrování.

WFM musí umožnit definovat reporty s údaji potřebnými pro export
mzdových dat do mzdového systému ve formátu požadovaným mzdovým
systémem.

API pro komunikaci s agenturami práce
-------------------------------------

WFM musí implementovat endpointy pro komunikaci s agenturami práce:

-   Zobrazení nabídky volných/neobsazených směn

-   Obsazení volných směn

-   Zrušení obsazení volných směn

-   Seznam směn obsazených jednotlivými agenturami
