# Ročníkový projekt - specifikace

Cílem práce je vytvořit webovou aplikaci, která bude interaktivně zobrazovat data z voleb do Poslanecké sněmovny 2021 jako mapu výsledků v jednotlivých volebních okrscích.

## Analýza již existujícího software

#### Český rozhlas - volební mapa 

https://www.irozhlas.cz/zpravy-domov/mapa-okrsky-volby-evropsky-parlament_1905270640_cib

Jedná se o interaktivní mapu voleb do Evropského parlamentu v roce 2018. Mapa zobrazuje výsledky jednotlivých stran a volební účast

##### Parametry:
- podkladová mapa - je možné oddalovat a přibližovat, při prvním načtení se zobrazí oddálená na celou ČR
- výsledky zobrazené podle okrsků vždy pro jednu stranu (nebo volební účast)
- mezi stranami je možné přepínat na liště - strany jsou seřazené sestupně podle množství získaných hlasů
- výsledky stran v okrscích jsou vizualizované zabarvením okrsku odstínem barvy odpovídajícímu procentuálnímu výsledku
- při najetí kurzorem na okrsek se zobrazí jméno okrsku a volební výsledky v daném okrsku
- je možné vyhledat konkrétní okrsek - mapa na okrsek zazoomuje a ukáže výsledek v danném okrsku

#### Lidové noviny - volební mapa 

https://www.lidovky.cz/obecni-volby-2018.aspx

Zde je to interaktivní mapa 2. kola senátních voleb 2021.
Má podobné základní charakteristiky jako mapa Českého rozhlasu, mapa se liší v některých aspektech kvůli charakteru voleb:
- okrsek je zabarvený podle kandidáta, který zvítězil
- barvy nejsou škálované podle procentuálního výsledku
- mapa má jednu vrstvu, ve které jsou zároveň všichni kandidáti

Tyto rozdíly nejsou pro můj projekt relevantní, protože budu zpracovávat volby do poslanecké sněmovny - mapa tedy bude více podobná prvnímu příkladu.

Důležitý rozdíl této mapy je možnost embedovat vybrané souřadnice s vlastním zoomem.

## Analýza požadavků

Mapu vytvářím pro Český rozhlas. Cílem je vytvořit samostatný modul interaktivní volební mapy, který bude možné nezávislé vkládat do různých článků, týkajících se voleb. 

#### Vizuální stránka

Vizuálně by měla být mapa podobná mapě Českého rozhlasu pro volby do Evropského parlamentu. Tedy na mapě jsou vrstvy které odpovídají výsledkům jednotnlivých stran a účasti. Každá strana má přidělenou barvu, jednotlivé volební okrsky jsou zbarvené odstínem této barvy, odpovídajícím procentuálnímu výsledku. Při tom je nutné kompenzovat rozdíly ve výsledcích stran (pro strany s vyššími zisky je nutné nastavit jinou škálu barev než pro strany s nižšími zisky).

#### Opakované použití

Očekává se, že mapu bude možné opakovaně používat, jak v rámci voleb 2021, tak případně pro další volby. Nebude se tedy jednat o samostatnou webovou aplikaci, ale spíše o modul, který je možné embedovat do jiných aplikací.

Implementace by proto měla být optimalizovaná pro časté změny mapového stylu a měla by mít možnost importu stylu.

#### Šablona iROZHLAS.cz

Model s volební mapou je potřeba implementovat tak, aby ho bylo možné používat spolu se snowball šablonou, kterou iROZHLAS.cz používá ke generování interaktivních článků. Projekt tedy musí mít určitou strukturu dannou šablonou.

#### Embedování souřadnic

Mapa by měla mít podobně jako mapa Lidových novin možnost embedovat vybrané souřadnice s vlastním zoomem. To znamená možnost zadefinovat předem souřadnice, na které se mapa při prvním načtení automaticky přiblíží. Toto je možné využít například v článku s volebními výsledky konkrétního regionu - použije se stejná interaktivní mapa jako pro celou ČR, ale zazoomovaná na daný region.

#### Mobilní telefony

Mapa by měla být odladěná pro mobilní telefony (uvažujeme aktuální Android a iOS, prohlížeče Safari a Chrome). Jedná se hlavně o optimalizaci zobrazení a přiblížení mapy tak, aby při se při načtení přiblížila maximálně vzhledem k velikosti obrazovky.

