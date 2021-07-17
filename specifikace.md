# Ročníkový projekt - specifikace

Cílem práce je vytvořit webovou aplikaci, která bude interaktivně zobrazovat data z voleb do Poslanecké sněmovny 2021 jako mapu výsledků v jednotlivých volebních okrscích.

## Analýza již existujícího software

#### Český rozhlas - volební mapa 

https://www.irozhlas.cz/zpravy-domov/mapa-okrsky-volby-evropsky-parlament_1905270640_cib

Jedná se o interaktivní mapu voleb do Evropského parlamentu v roce 2019. Mapa zobrazuje výsledky jednotlivých stran a volební účast

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


