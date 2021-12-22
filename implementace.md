# Ročníkový projekt - implementace

## Architektura

Projekt je rozdělený na dva moduly. První modul obsahuje samotnou mapu. 
Druhý je samostatný modul, který obsahuje specifikovaný styl, který mapa využívá.

### Modul s mapou

Modul je rozdělený do několika tříd. 

Třída `Map` reprezentuje samotnou mapu a obsahuje všechny její funkcionality.
Využívá několika pomocných tříd (`MapLegend`, `PartySelector` a `GeocodeFinder`), které reprezentují komponety mapy -
popisek, výběr vrstvy v mapě a vyhledávač.
Při vytvoření mapy se postupně instanciují její komponenty. 
V komponentách se vytvoří události, které jsou navázané na mapu, tedy při interakci s mapou se vyvolá událost v potřebné komponentě.

Poslední třídou v modulu je `MapEmbeder`. 
Tato třída slouží pro embedování mapy do HTML dokumentu.
Embeder najde v dokumentu všechny elementy, které jsou označené pro embedování mapy (pomocí CSS třídy), 
a pro každý element vytvoří odpovídající instanci třídy `Map`.
Tuto třídu nainicializuje výchozími parametry, které získá z daného elementu.
Takovými parametry jsou například souřadnice, na které bude mapa vycentrovaná nebo výchozí zobrazená vrstva.


### Modul se stylem

Zobrazování volebních výsledků vypadá tak, že je okrsek zbarvený odstínem barvy, 
jehož sytost odpovídá ziskum hlasů v daném okrsku.
Podle výsledků je potřeba nastavit odstupňování barev pro jednotlivé strany tak, aby byly rozdíly zisků mezi různými okrsky dobře rozpoznatelné. Tyto přechody jsou definované v samostatném souboru (`breaks.js`), který modul se stylem využívá.
Také je žádoucí, aby strany byly na mapě zobrazené barvou, která je s nimi asociovaná.

Kvůli těmto faktorům byl požadavek, aby byly mapové styly co nejvíc oddělené od funkcionalit mapy 
a aby barvy mohl samostně nastavit designér.

Tyto požadavky jsem řešila tak, že jsem vytvořila modul (soubor `style.js`), ve kterém jsou definované odstupňované odstíny barev pro různé strany.
Dále modul obsahuje funkce, které používají definované barvy a vytvářejí styl pro mapu.
Ve stylu jsou definované barvy strany a procentuální hranice přechodu a také jaký styl se má použít (lineární interpolace).
Tyto funkce používá modul s mapou, když vytváří vrstvu v mapě pro danou stranu.
Barvy je tedy možné změnit beze změny kódu samotné mapy.

V modulu se nachází také odkaz na podkladový styl mapy, který je zveřejněný na stránkách iRozhlasu.

Ve své implementaci jsem použila placeholdery stylů, které byly použité v jiné mapě iRozhlasu, abych mohla mapu otestovat.
Odstupňování barev se totiž musí spočítat až po získání kompletních volebních výsledků.
Tyto placeholdery je možné nahradit správnými barvami při použití mapy pro konkrétní volby.

## Řešené problémy

### Více map v jednom článku

V implementaci mapy pro volby do Evropského parlamentu, ze které jsem vycházela, bylo možné, aby článek obsahoval pouze jednu mapu.
Mapa se embedovala do elementu označeného určitým ID. 
Ve své implementaci, jsem místo ID použila označení třídou. 
Mapa se embeduje do všech elementů, které jsou označené touto třídou a mají určitou strukturu.

### Embedování výchozích parametrů mapy

Hlavním řešeným problémem bylo umožnit k mapě přidat souřadnice, na které bude mapa při načtení vycentrovaná. 
Prvním řešením, nad kterým jsem přemýšlela, bylo přidat souřadnice jako parametry v URL.
Toto řešení jsem zavrhla. Pokud by v jednom článku bylo více map, 
a také pokud by se kromě souřadnic specifikovaly i další výchozí parametry (zobrazená vrstva, zoom), pak by počet parametrů narůstal a URL by se nepřiměřeně prodlužovalo.

Řešení, které jsem zvolila využívá data atributů v HTML dokumentu. 
Pokud je potřeba nastavit nějaký parametr mapy, pak se do elementu, do kterého se má mapa embedovat (je označený potřebnou třídou),
přidá data atribut s požadovaným parametrem.
Pro parametry, které nejsou specifikované, se použijí výchozí hodnoty.

HTML element, do kterého se má embedovat mapa, který má specifikované všechny výchozí parametry mapy:
```HTML
 <div id="map1" class="container" data-center-lng="14.10285088807273" data-center-lat="50.14733556497221" data-zoom="12" data-party="part_30">
    <div class="map"></div>
 </div>
```


### Oddělení stylu

Jedním z požadavků bylo také oddělení stylu od ostatního kódu. 
Pro oddělení stylu bylo potřeba shromáždit všechny konstanty a části, které se týkají stylu a odsunout je do samostatného modulu.
Struktura modulu je popsaná v předchozí části. 
