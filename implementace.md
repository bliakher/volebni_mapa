# Ročníkový projekt - implementace

## Architektura

Projekt je rozdělený na dva moduly. První modul obsahuje samotnou mapu a všechny její funkcionality a dále třídu, která umožňuje embedovaní mapy do předpřipravené struktury v HTML. Druhý je samostatný modul, který obsahuje specifikovaný styl, který mapa využívá.

### Modul s mapou

Modul je rozdělený do několika tříd. 

Třída `Map` reprezentuje samotnou mapu a obsahuje všechny její funkcionality.
Využívá několika pomocných tříd (`MapLegend`, `PartySelector` a `GeocodeFinder`), které reprezentují komponety mapy -
popisek, výběr vrstvy v mapě a vyhledávač.
Při vytvoření mapy se postupně instancují její komponenty. 
V komponentách se vytvoří události, které jsou navázané na mapu, tedy při interakci s mapou se vyvolá událost v potřebné komponentě.

Poslední třídou v modulu je `MapEmbeder`. 
Tato třída slouží embedování mapy do HTML dokumentu.
Třída najde v dokumentu všechny elementy, které jsou označené pro embedování mapy (pomocí třídy), 
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
Barvy je tedy možné změnit beze změny samotné mapy.

V modulu se nachází také odkaz na podkladový styl mapy, který je zveřejněný na stránkách iRozhlasu.

Ve své implementaci jsem použila placeholdery stylů, které byly použité v jiné mapě iRozhlasu, abych mohla mapu otestovat.
Odstupňování barev se totiž musí spočítat až po získání kompletních volebních výsledků.
Tyto placeholdery je možné nahradit správnými barvami při použití mapy pro konkrétní volby.

