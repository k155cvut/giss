# 14GISS – stručný průvodce semestrem geografických informačních systémů na FD {#giss_stručný_průvodce_semestrem_geografických_informačních_systémů_na_fd}

## Data

Webová složka s daty ArcČR a dalšími testovacími datovými sadami je [**k dispozici ke stažení**](https://vltava.fsv.cvut.cz/giss_data). Složka obsahuje: 

-   data ArcČR ve verzi 3.3 (nepracujte s novější verzí 4.2, která je v mnohém ochuzená);
    -   **ArcCR_v3.3.zip**
-   vektorová data ve složce Data_vektory:
    -   **Obce_info.xls** – informace o obcích, jejich názvech, vlajkách apod., data obsahují kód obce pro vazbu na ArcČR;
    -   **Pozarni_stanice.csv** – vybrané požární stanice z OpenStreetMap;
    -   **Rychlost_radary.csv** – vybrané rychlostní radary;
    -   **Vodojemy.xls** – vybrané věžové vodojemy;
-   rastr digitálního modelu reliéfu
    -   **Rastr_DMR.zip** – tento jediný rastr je včetně georeferenční informace;
-   rastrová data ve složce Data_rastry:
    -   **bonita_klimatu.png** – klimatické bonitní regiony v Praze;
    -   **cesko800.gif** – automapa ČR;
    -   **CO_Pnetluky** – rastr tzv. císařského povinného otisku mapy stabilního katastru (první katastrální mapy z 40. let 19. stol.);
    -   **geoCR.png** – geologická mapa ČR;
    -   **hluk.jpg** – hluková mapa Prahy;
    -   **muller_prehled500** – přehledová verze tzv. Müllerovy mapy Čech z 20. let 18. století;
    -   **SMO5_LITC75.jpg** a **SMO5_LITC75.jpg** – tzv. Státní mapa – odvozená 1 : 5000, mapové listy v záp. části okresu Litoměřice;
    -   **Tur_mapa_25tis** – výřez turistické mapy Geodézie On-Line v záp. části okresu Litoměřice.

## GIS a souřadnicové připojení dat {#gis_a_souřadnicové_připojení_dat}

V ArcGIS pro řešeno tzv. on-the-fly transformací (aplikace slícuje data v různých souř. systémech bez nutnosti interakce uživatelem).

**Souřadnicové systémy (SRS) používané na našem území**

| Souřadnicový systém | Systém jednotek | EPSG kód | Hodnoty, okolo kterých se pohybují souřadnice na našem území |
|---|---|---|---|
| S–JTSK | metrický | 5514 | –750 000; –1 100 000 |
| UTM zóna 33N | metrický | 32633 | 500 000; 5 500 000 |
| Web Mercator (Google Mercator) | metrický | 3857 | 1 600 000; 6 400 000 |
| WGS-84 | stupňový | 4326 | 14,5°; 50,0° |

SRS je možné nastavit ve vlastnostech mapy (*Properties \> Reference system*), lze zadat číslo EPSG kódu a příslušný SRS se doplní. SRS jednotlivých vrstev je jejich vlastností (u Shapefile je evidován v souboru PRJ) a lze jej změnit (přetransformovat třídu prvků do jiného SRS) pomocí funkce *Project*. Nemá-li třída prvků definován SRS, ArcGIS ji sice dovede zobrazit (v aktuálně nastaveném SRS mapy bez ohledu na správnost), ale nedokáže transformovat do jiných SRS. Nastavit chybějící informaci o SRS třídě prvků lze funkcí *Define projection*.

Měření délek, ploch apod. je vhodné provádět v systému S–JTSK nebo UTM, jelikož nejsou rozměry zatíženy zkreslením. Více se o souřadnicových systémech a jejich definice v různých formátech je možné najít na webu [spatialreference.org](https://www.spatialreference.org).

## Základní práce s daty {#základní_práce_s_daty}

Data v GIS jsou převážně **vektorová** a **rastrová**.

**Vektory** lze prakticky neomezeně přiblížit, mohou nést atributové informace, jsou vhodné pro jevy diskrétně rozložené v prostoru (bodové objekty, liniové objekty, areálové objekty). Jednotlivé informace jsou sdruženy do **tříd prvků** bodového, liniového nebo polygonového charakteru. Vektory nesou polohovou (geometrickou) a věcnou (atributovou) informaci. Třídy prvků mohou představovat samostatné datové struktury na disku (formát Shapefile) nebo existovat jako vrstvy v databázích (geodatabáze GDB, MDB, Mobile Geodatabase, souborové databáze SQLite, dBase aj. či \"robustní\" databázové stroje typu Oracle, MS SQL Server apod.). Souborová geodatabáze GDB je vždy součástí složky projektu založeného v ArcGISu a představuje výchozí umístění, kam aplikace ukládá nově vypočtené třídy prvků, vrstvy mezivýpočtů apod.

**Rastry** představují matici prostorově umístěných obrazových bodů (pixelů) nesoucích obrazovou nebo atributovou informaci (obrazová data, ortofota, skeny map atd. × rastry výškové, šedotónové, nákladové aj.). Mohou existovat samostatně na disku (klasické formáty TIFF, JPEG, PNG apod.) nebo být součástí databází.

Data lze do projektu přidávat přes volbu *Map \> Add Data*, přetáhnout je z panelu katalogu anebo přímo z jakéhokoli okna správce souborů. Pozor, při přidávání formátu Shapefile, který sestává ze 4–7 souborů, je třeba přetáhnout soubor SHP. Data se vykreslují v pořadí daném pořadím v tabulce obsahu (TOC) vlevo. Vrstvy výše překryjí vrstvy níže, s pořadím je možné interaktivně hýbat, vrstvy je možné přejmenovat (nepřejmenuje samotnou třídu prvků v databázi nebo na disku, pouze její jméno uvnitř mapového projektu). Mapový projekt představuje strukturu, kde v jedné složce na disku je soubor APRX se samotným projektem (neobsahuje data, ale jen referencuje třídy prvků nebo rastry, ale ukládá do sebe nastavení symboliky dat apod.), výchozí geodatabáze GDB, výchozí toolbox ATBX, zálohy a prostorové indexy. Případně jsou zde soubory s uloženými připojeními na externí datová umístění (AGS soubory).

Nové třídy prvků je možné vytvářet v okně katalogu (v k. m. geodatabáze volbou *New \> Feature Class*), kdy se spustí krátký průvodce nastavením geometrického typu nové třídy prvků, jejich atributů, nastavení SRS apod.

Je možné zobrazit atributovou tabulku (v kontextovém menu třídy prvků *Attribute table*), která obsahuje informace o všech prvcích dané třídy prvků, tedy hodnoty atributů (atributových polí, sloupců atp.). Geometrie prvků je vždy v atributu *Shape*. Atributovou informaci je možné editovat (přímo v AT, s výjimkou geometrického atributu *Shape* a tzv. primárního klíče – zpravidla *OBJECTID*, který ArcGIS používá pro řazení a identifikaci dat), atributy je možné pomocí *Add Field* přidávat, přesouvat pořadí, mazat. Je možné mazat také jednotlivé prvky. Atributy mají datové typy podobně jako třeba buňky v MS Excel (Long – celé číslo, Float/Double – reálná čísla, Text, Datum, Raster apod.). Je-li hodnota atributu prázdná, ArcGIS vypisuje hodnotu *`<Null>`{=html}*. Je-li aktuálně vybrána funkce *Explore* (záložka *Map*), Lze se dotazovat na atributovou informaci konkrétního prvku pomocí kliknutí. Atributy daného objektu se objeví ve formě tzv. pop-upu (vyskakovacího okna).

Pomocí funkce *Select* je možné provést (interaktivní) **výběr** klikáním na dané prvky v mapovém okně (s Shift přidáváme k výběru, s Ctrl ubíráme z výběru). Obdobně je možné vybírat prvky pomocí označování záhlaví řádků v AT (Shift vybírá navazující rozsah, Ctrl jednotlivé prvky/řádky –podobně jako při práci v oknech Windows).

Data nebo jejich část (výběr) je možné exportovat do nové vrstvy (v k. m. vrstvy *Data \> Export features* a vybrat si umístnění do geodatabáze (GDB) nebo do složky na disku (výsledkem bude formát Shapefile).

Nebude-li řečeno jinak, budeme pracovat s daty sady ArcČR 500 (vektorová data republiky v měřítku zhruba 1 : 500 tis., poskytovaná firmou ArcData zdarma), případně s daty sady Data200 (vytvářené Zeměměřickým úřadem a poskytované také zdarma). Je vhodné se se strukturou ArcČR seznámit (PDF soubor uvnitř ZIP archívu). Jedná se o dvě geodatabáze (Admin_Cleneni.GDB s daty územních jednotek a ArcCR_33.GDB s daty topografických objektů, jako jsou silnice, vodní toky, lesy apod.). Součástí dodaných dat je také rastr digitálního modelu reliéfu.

!!! tip "Dojde-li k zavření základních panelů (Catalog, Table of contents), lze je znovu vyvolat pomocí volby *View \> Reset panes for Mapping*"

## Výběr prvků (dotazování, query) {#výběr_prvků_dotazování_query}

Výběry je možné provádět také na základě splnění nějaké vlastnosti atributové (**atributový dotaz / Select by attributes**) nebo polohové (**prostorové dotazy / Select by location**). Jedná se o velmi časté úkony při práci v GIS, které jsou mnohdy součástí složitějších workflow.

Takto vybrané prvky se označí (vyberou) stejným způsobem jako při interaktivním výběru myší nebo označením prvků v AT. **Je-li v třídě prvků proveden výběr, všechny gisovské nástroje pracují vždy s prvky zahrnutými do výběru a zbytek třídy prvků je opomenut.** Výběr lze zrušit kliknutím na *Clear*. Implicitně jsou vybrané prvky podbarveny azurově, lze změnit v nastavení programu (*Options,* sekce *Selection*). 

!!! tip "V nastavení programu, v sekci *General \> Project recovery* lze nastavit interval ukládání pracovní verze pro případ pádu programu (nejméně lze 1 minuta)<br /><br /> V menu *General \> Application theme* lze také vybrat tmavou verzi prostředí (vhodné pro delší práci, šetří oči; mapové okno však vždy zůstane s pozadím bílým)."

**Atributový dotaz** spočívá ve splnění podmínky kladené na hodnoty atributů či jejich existenci. Používá se jazyk SQL nebo syntaxe pomocí předdefinovaných klauzulí, z nichž je možné většinu běžných dotazů poskládat. Z jazyka SQL se vyplňuje jen část, která navazuje na klauzuli **`SELECT \* FROM <název_tabulky> WHERE ...`**

| Situace | Příklad SQL syntaxe v hypotetických datech <br /> <span style="font-weight: normal;">(přesné znění závisí na názvech a hodnotách atributů)</span> |
|---|---|
| Vybrat všechny rybníky z vrstvy vodních nádrží. | **`TYP = "rybnik"`** |
| Vybrat všechny letiště, které mají jméno | **`NAME IS NOT NULL`** |
| Všechny silnice delší než 5 km | **`SHAPE_Length > 5000`** |
| Všechny obce s názvem na *Ba–* | **`NAZ_OBCE LIKE "Ba%"`** |
| Všechny vodní plochy s šestipísmenným názvem končícím *–e* | **`NAZEV LIKE "_____e"`** |
| Silnice II. třídy kratší než 2 km | **`TRIDA = "II. třída" AND SHAPE_Length < 2000`** |
| Vodní toky kategorie III a níž | **`KATEGORIE IN (1,2,3)`** |
| Všechny moravské kraje (4 nejvýchodnější) | **`NAZ_KRAJ IN ("Moravskoslezský","Zlínský","Olomoucký","Jihomoravský")`** |
| Úplně všechny prvky třídy prvků | **`OBJECTID >= 0`** nebo **`OBJECTID IS NOT NULL`** |

Pomocí AND a OR je možné vytvářet kombinované dotazy pomocí logického součtu AND (splněno oboje) anebo rozdílu OR (splněno jedno nebo druhé).

**Prostorový dotaz** spočívá v aplikaci geograficky dané podmínky na vstupní data. Podmínka vždy vyjadřuje prostorový vztah dvou vrstev:

| Prostorový vztah | Název v ArcGIS | Popis |
|---|---|---|
| Průnik | Intersect | vrstvy sdílejí nějaké společné body nebo část geometrie, alespoň 1 bod |
| Do vzdálenosti | Within a distance | vrstvy mají společný nenulový průnik s určitou vzdálenostní tolerancí |
| Obsahuje | Contains | vrstva v sobě obsahuje jinou (např. polygon zahrnuje body, linie) anebo její část |
| Je obsaženo | Within | vrstva nebo její část tvoří podmnožinu jiné (bod, linie uvnitř polygonu, bod na linii apod.) |
| Obsahuje kompletně | Completely contains | vrstva v sobě zcela obsahuje jinou (např. polygon zahrnuje body, linie) |
| Je kompletně obsaženo | Completely within | vrstva nebo tvoří podmnožinu jiné (bod, celá linie uvnitř polygonu, bod na linii apod.) |
| Dotyk linií | Boundary touches | vrstva se dotýká hranice jiné vrstvy (bod na polygonu, linie kříží/dotýká se hranice polygonu apod.) |
| Sdílení segmentu | Share a segment with | vrstvy spolu sdílejí alespoň jeden celý segment linie (nestačí jeden bod) |
| Těžiště leží | Have their center in | těžiště (centroid) vrstvy leží uvnitř jiné |

Tyto prostorové vztahy lze vyšetřovat přímo (přesně) anebo se vzdálenostní tolerancí (situace typu *najít všechny body do vzdálenosti 5 km od jiného prvku*; v ArcGIS *Search distance*).

Tyto dotazy nikdy nemění geometrie vstupních vrstev, pouze provádějí výběr. Změnu geometrických vlastností vrstev na základě polohových vztahů umožňují až **prostorové funkce**.

#### Trvalé uložení query nad vrstvou (*Definition query*) {#trvalé_uložení_query_nad_vrstvou_definition_query}

Nad vrstvou je možné nastavit jakýsi trvale volaný filtr/dotaz, který lze nastavit v k. m. vrstvy pod sekcí *Definition query*. Zde je možné vložit úplně stejným způsobem jako u atributového dotazu klauzuli nebo SQL dotaz, který se po uložení trvale aplikuje a datová vrstva se poté chová, jako by data nesplňující nadefinovanou podmínku vůbec neobsahovala. Definition query lze kdykoli vypnout dočasně (odškrtnutím příslušného řádku) nebo trvale. Je možné nadefinovat si více těchto Definition query a dle potřeby mezi nimi přepínat.

## Prostorové (překryvné) funkce {#prostorové_překryvné_funkce}

Umožňují měnit polohové vlastnosti tříd prvků na základě polohové interakce s jinými třídami. V zásadě se jedná o aplikaci základních topologických operací:

| Prostorový vztah | Název prostorové funkce <br />v ArcGIS | Popis |
|---|---|---|
| Průnik | ***Intersect*** | matematický průnik dvou vrstev (výsledkem bod, linie, plocha nebo prázdná třída prvků) |
| Sjednocení | ***Union*** | sjednocení všech vstupujících vrstev, zachovají se atributy všech sloučených dílů |
| Doplněk | ***Symmetrical difference*** | jde o topologický doplněk k první vrstvě |
| Odmazání | ***Erase*** | z vrstvy odstraní tu část, která tvoří s cílovou vrstvou průnik, atributy vstupní vrstvy se zachovávají |
| Ořez | ***Clip*** | z původní vrstvy zachová jen tu část, která s cílovou vrstvou tvoří průnik |
| Sloučení | ***Merge*** | sloučí vstupující vrstvy do jedné souhrnné geometrie bez zachování původních hranic a atributů |
| Obalová zóna | ***Buffer*** | spočte vrstvu, přestavující plochu maximální vzdálenosti od dané vrstvy |

Poněkud stranou stojí dvojice funkcí *Dissolve* a *Multipart to singlepart*, které se váží s prostorovou souvislostí prvků.

**Všechny prostorové funkce a všechny dále probírané analytické funkce GIS umožňují měnit geometrie tříd prvků a jejich atributy. Panel s výběrem funkcí lze vyvolat pomocí *Analysis \> Tools*.**

***Dissolve*** umožňuje proředění vrstvy na základě shody tematického atributu. Tedy lze např. na základě shodného atributu příslušnosti ke kraji proředit vrstvu okresů a převést ji (sloučením) na kraje. Lze k výsledným prvkům přiřadit statistické sumární informace – sekce *Statistic fields*. Zde je možnost nechat si k nově sloučeným prvkům spočítat charakteristiky dle následující tabulky:

| Charakteristika v ArcGIS | Význam | Charakteristika v ArcGIS | Význam | Charakteristika v ArcGIS | Význam |
|---|---|---|---|---|---|
| Count | Počet prvků | Standard deviation | Směrodatná odchylka z hodnot | First | Hodnota prvního prvku |
| Mean | Průměr hodnot | Range | Rozsah hodnot (max – min) | Last | Hodnota posledního prvku |
| Sum | Součet hodnot | Median | Medián hodnot | Unique | Počet unikátních hodnot mezi prvky |
| Minimum | Minimální hodnota | Variance | Rozptyl hodnot | Concatenate | Jednotlivé hodnoty oddělené oddělovačem |
| Maximum | Maximální hodnota |  |  |  |  |

!!! warning "ostatní atributy, nenastavené v rámci *Statistic fields*, se do výsledné vrstvy nepřenesou"

Naproti tomu ***Multipart to singlepart*** umožňuje rozdělit geometrie objektů na jednotlivé původně prostorově nesouvislé díly a odstranit tak z dat takové prvky, které sestávají z více vzájemně nespojitých částí (*parts*). Příkladem může být vrstva obcí, kdy některé obce mají exklávy (geometricky nespojité části), které součástí obce jsou, ale netvoří s vlastním hlavním správním územím obce jeden prostorový celek.

## Import obecných negisovských dat do prostředí GIS {#import_obecných_negisovských_dat_do_prostředí_gis}

Existují tři varianty neprostorových datových sad, které je možné převést na prostorová (gisovská) data. Mimoto existuje velké množství datových sad, které převést na prostorová data nelze, protože se jedná o datové sady zcela bez jakékoli geometrické informace.

Obecně se může jednat o textové soubory (TXT, CSV aj.), jednoduché tabulky (XLS, DBF aj.) i další formáty, strojově zpracovatelné.

**I Data mají souřadnice nikoli přímo součástí geometrického určení, nýbrž uložené v atributech**

Nejjednodušší případ, který lze převést snadno na gisovskou vrstvu, obsahuje souřadnice někde mezi atributy. Vždy je dobré podívat se na data a pokud není znám SRS, pokusit se ho odhadnout ze souřadnic.

Příklad CSV souboru v systému WGS-84 (SRS je patrný z rozměru souřadnic, zřejmě se jedná o stupně zem. šířky a délky):

``` text
ID, Lat, Lon, Category, Name
21, 50.22516, 15.58113, 2,
22, 50.29161, 15.51305, 3, obelisk
23, 50.22913, 14.99161, 3, pomník
28, 50.00546, 15.05396, 1, sv. Václav
31, 50.38337, 15.11831, 2,
```

Taková data lze naimportovat pomocí funkce *Display XY Data* v k. m. třídy prvků. Je třeba provázat atributy dat s geometrickými souřadnicemi (osa X napravo, tedy např. *Lon, Longitude, X, E* apod.) a osa Y nahoru, tedy např. *Lat, Latitude, Y, N* apod.). Výsledná třída prvků se již chová jako jakákoli jiná prostorová data v ArcGIS. Data jednoduchých tabulek jako jsou excelovské soubory se v ArcGIS tváří jako samostatná tabulka pro každý list.

!!! warning "pro import listů MS Excel je třeba mít nainstalované ODBC databázové rozhraní (je standardně součástí MS Office)"

**II Data neobsahují souřadnice, ale jiné prostorově odvoditelné informace (např. adresy)**

Taková data je možné geolokalizovat (i hromadně) za pomoci lokalizační služby (mnohdy placené, ale existuje i zdarma využitelná [geolokalizační služba postavená nad daty registru RÚIAN](https://ags.cuzk.cz/arcgis/rest/services/RUIAN/Vyhledavaci_sluzba_nad_daty_RUIAN/MapServer/exts/GeocodeSOE)). Spouští se funkcí *Geocode table* v k. m. třídy prvků, pomocí průvodce je možné provést geolokalizování na základě adres uložených v jednom nebo více atributových polích dat.

Výsledek geolokalizování je silně závislý na kvalitě dat (adres) a na úplnosti a přesnosti geolokalizační databáze. Je běžné, že se podaří lokalizovat i méně než 90 % vstupních dat, zbytek je třeba upravit nebo provést geolokalizaci ručně.

**III Data neobsahují souřadnice ani adresy, ale obsahují jednoznačné identifikátory provázatelné s prostorovými daty**

Zde jde o propojení negeometrické (neprostorové) tabulky s gisovskými daty na základě shody jednoho z atributů. Velice často se v tomto ohledu používají identifikátory administrativních jednotek (kódy obcí, kódy k. ú.), v případě jednoznačnosti názvů (např. u okresů, ORP aj.) lze použít jako vazebný atribut přímo název.

Prakticky se používá vazba pomocí *Join* (v k. m. cílové (prostorové) vrstvy *Joins and relates \> Add join*), kde je třeba nastavit:

1.  cílovou třídu prvků;
2.  název atributu v cílové vrstvě;
3.  připojovaná data;
4.  název vazebného atributu v připojovaných datech.

Pomocí *Validate join* je možné zobrazit informace o úspěšnosti propojení dat.

Po propojení se příslušné nové atributové sloupce připojí k třídě prvků a lze s nimi pracovat poobně jako se všemi ostatními atributy (dotazování apod.), jen je není možné editovat. Jedná se vlastně o jakousi referenci na další datový soubor.

## Editace geometrií vektorových dat, vektorizace {#editace_geometrií_vektorových_dat_vektorizace}

Pomocí funkcí panelu *Edit* lze editovat data geometricky. Při zapnutém panelu *Attributes* je možné zároveň měnit geometrie prvků i editovat jejich atributy.

Záložka *Edit* umožňuje pomocí tlačítek *Create* nebo *Modify* vybrat typ operace s daty. V případě vytváření nových dat se otevře panel s editačními šablonami, který umožňuje vybrat, do které vrstvy / třídy prvků budou nově vytvářené geometrie zapisovány.

Hlavní nástroje jsou soustředěny v sekci *Tools* a zahrnují nástroje pro přesun prvků (*Move*), sloučení několika prvků dohromady (*Merge*) nebo jejich rozdělení (*Split*), změnu geometrického průběhu linie nebo polygonu (*Reshape*) či editaci jednotlivých lomových bodů (*Edit vertices*). Sada obsahuje množství dalších nástrojů pro speciální editační operace. Při editaci linie nebo polygonu je možné využít fuknci *Trace* (na malém editačním panelu, který se otevírá ve spodní části okna), která slouží k převzetí části geometrie již existující vrstvy (vhodné pro zachování topologické čistoty dat).

Právě editovaná vrstva je ve stavu tzv. sketch – návrhu, kdy je pomocí F2 třeba uložit výslednou geometrii a ukončit editaci příslušného prvku. Celou editovanou třídu prvků je třeba uložit tlačítkem *Save*, do doby uložení nejsou editace propsány do datové sady a jedná se o jakýsi mezistav. Program v případě aplikace analytických funkcí na editovanou vrstvu upozorňuje pomocí výstrahy *Pending edits*, že na vrstvě jsou prozatím neuložené editace.

Editovat popsaným způsobem nelze rastry nebo data připojená přes Join.

## Práce s rastry v GIS, georeferencování {#práce_s_rastry_v_gis_georeferencování}

Rastry jsou v GIS chápány jako datová struktura formy matice, ukládající data do jednotlivých jejích pozic (pixelů). Může se jednat o klasická obrazová data (ortofoto, družicové snímky, mapy, skeny, obrázky), které představují klasické rastrové soubory s R, G, B barevnými kanály. Případně se může jednat o jednokanálová (šedotónová, černobílá) data. Velice často také rastry nesou obecnou, neobrazovou informaci – používají se k ukládání informací o jevech, jež se spojitě mění v prostoru (teplota, nadm. výška, obecně jakákoli kvantitativní nebo kvalitativní informace).

Aby bylo možné s rastrovými daty v GIS pracovat, je třeba je tzv. **georeferencovat** (geolokalizovat, geokódovat, angl. *georeference*, *adjust*, *geolocalise*). Tento proces zahrnuje uložení informace o poloze rastru v prostoru (rovině souř. referenčního systému). To bývá realizováno pomocí souřadnic levého horního rohu (*X~T~*, *Y~T~*), rozměru pixelu ve směru vodorovné a svislé hrany rastru (*m~x~*, *m~y~*) a stočení těchto hran vůči osám *x*, *y* souřadnicového systému (*ω~x~*, *ω~y~*). Tyto informace jsou pak v pořadí *m~x~*, *ω~x~*, *ω~y~*, *m~y~, X~T~, Y~T~* uloženy v souboru, tzv. **world-file**, nesoucím stejný název jako rastr a příponou poskládanou z prvního a posledního písmena přípony formátu rastru, doplněné uprostřed o W, tedy např. TFW pro formát TIFF, JGW pro JPEG apod.

Příklad world-file souboru pro data v systému S–JTSK:

``` text
250.00011407
-0.003468205327
-0.01468499854
-250.00025209
-822765.7312
-1034984.0508
```
Je z něj např. patrné, že rastr byl zřejmě vyexportován v nějakém software v systému JTSK s rozlišením 250 m na pixel (1. a 4. řádek nesou hodnotu přibližně 250 m a 2. a 3. řádek s rotacemi jsou přibližně nulové); že jde o JTSK lze poznat ze souřadnicového posunu v 5. a 6. řádku.

Takto souřadnicově umístěný rastr se po načtení do GIS zobrazí na patřičném místě (provede se matematická transformace v rovině na základě daných parametrů). Není-li georeferenční informace k dispozici, je možné georeferencovat rastr vůči známým bodům (jiné mapě) pomocí volby *Imagery \> Georeference*. Zde se pro rastr, který je aktuálně vybrán v tabulce obsahu, objeví panel *Georeferencing* s funkcemi pro souřadnicové umístění rastrů.

Postup georeferencování je následující:

-   je třeba mít k dispozici podkladovou mapu nebo data, vůči kterým je možné kresbu rastru umístit;
-   ideální pro zdárné georeferencování je pracovat v SRS, ve kterém byl rastr vytvořen/exportován;
-   pomocí volby *Fit to display* je možné rastr dočasně umístit do aktuálního prostoru mapového okna (je vhodné umístit mapové okno přibližně do prostoru, kde má být rastr souřadnicově umístěn) – jinak je levý horní roh rastru v bodě o souřadnicích 0, 0;
-   pomocí volby *Raster Layer \> Transparency* je možné rastr zprůhlednit vůči \"pozadí\" a lépe se orientovat v obou datech;
-   přidáváním identických bodů (IB) volbou *Add control points* se ukládají body o dvojích známých souřadnicích (napřed kliknout v rastru, poté na odpovídající místo v reálném SRS), na základě kterých je později možné rastr transformovat;
-   rastr se automaticky on-the-fly transformuje (překresluje) podle aktuálně vložených bodů;
-   pomocí *Save* se georeferencování uloží do world-file a rastr zůstane v poslední poloze již trvale.

Různé matematické transformace v rovině využívají různý počet IB pro svůj výpočet. V případě, že je k dispozici více IB než je nutný počet, dojde k tzv. vyrovnání a ArcGIS nabídne v tabulce *Control point table* zbytkové střední chyby (*residuals*), jejichž hodnota zhruba odpovídá přesnosti georeferencování. Jde však pouze o statistický odhad, který může (ale v některých případech nemusí) ukazovat na přesnost celého vyrovnání. Lze takto např. odhalit hrubé chyby s výrazně větší hodnotou reziduí, které ukazují na chybné umístění bodu na rastru, resp. skutečném SRS. Při vložení přesně nutného počtu IB prochází rastr všemi body **přesně** (rezidua se vynulují), což lze využít např. při transformaci projektivně na 4 rohy mapového kladu.

| Metoda | Možnosti | Počet nutných IB |
|---|---|---|
| shodnostní | pouze posunutí v prostoru | 1 |
| podobnostní | posunutí, rotace a změna celkového měřítka | 2 |
| afinní | posun, rotace, odlišná změna měřítka ve směru souř. os (deformace úhlu mezi souřadnicovými osami) | 3 |
| projektivní / kolineární | pravoúhelník transformuje na obecný čtyřúhelník, zachovává tzv. dvojpoměr bodů | 4 |
| polynomická II. stupně | úsečku transformuje na oblouk paraboly II. stupně | 6 |
| polynomická III. stupně | úsečku transformuje na oblouk kubické paraboly | 10 |
| spline / TPS | na fyz. principu deformace nekonečně tenkého plátu | 6 |

***Tabulka transformačních metod v rovině***

## Práce s daty webových mapových služeb nebo cloudu ArcGIS Online 

Při řešení úloh v GIS se velice často využívají data, která jsou distribuovaná, tj. neuložená lokálně na pracovní stanici, ale někde na webovém serveru nebo v databázích. Tato data se obecně připojují pomocí volby *Insert \> Connections \> Server*, kde se vybere odpovídající typ dat, případně *Insert \> Connections \> Database* v případě databáze přístupné skrze web.

Rastrové mapové služby přenášejí pouze "náhledy" na data, tedy obrázky, jež nelze editovat. Lze se u nich dotazovat na atributovou informaci pomocí kliknutí funkcí *Explore*. Mezi takové patří webové služby standardu WMS, WMTS, ArcGIS Server Tile Service, ArcGIS Server Image Service. Vektorové mapové služby přenášejí kompletní data, použitelná k dalším analýzám (standard WFS, ArcGIS Server Feature Service). Je třeba znát URL adresu služby (tzv. přístupový bod, např. [https://geoportal.gov.cz/arcgis/services/CENIA/cenia_copernicus_land/MapServer/WmsServer?](https://geoportal.gov.cz/arcgis/services/CENIA/cenia_copernicus_land/MapServer/WmsServer?)). Tyto služby standardů WMS, WMTS a WFS nelze procházet skrze žádné webové rozhraní, je třeba GIS nástroj nebo prohlížečka WMS služeb pro práci s daty takto distribuovanými.

Mapové služby standardu ArcGIS Server lze procházet skrze webové rozhraní REST, např. <https://ags.cuzk.cz/arcgis/rest/>, kde jsou vidět jednotlivé složky s mapovými službami a jejich podvrstvami, které je možné si v případě potřeby zobrazit v mapové prohlížečce nebo pomocí URL adresy připojit do GIS softwaru (*Insert \> Connections \> New ArcGIS Server*, který se pak objeví v panelu katalogu jako nová položka v sekci *Servers*). Odtud je pak možné přidávat jednotlivé vrstvy/služby do projektu, příp. je tam vložit přímou URL adresou přes *Add Data \> Add data from path*.

#### ArcGIS Online {#arcgis_online}

Z důvodu lepší interoperability a sdílení dat vznikají v posledních deseti letech cloudové služby, jejichž součástí bývá mapový server, úložiště dat, možnost provádění prostorových operací skrze web a někdy i API rozhraní pro tvorbu vlastních aplikací. Jedním z nejpoužívanějších je cloud [ArcGIS Online](https://www.arcgis.com), kam je možné publikovat data z desktopové aplikace ArcGIS Pro a zpětně je v této aplikaci používat.

Součástí webového rozhraní je po přihlášení mapová prohlížečka (záložka *Map* nahoře v liště), pomocí které je možné nahlížet data a vytvářet z nich mapové kompozice (*WebMap*). V záložce *Contents* je možné procházet svůj vlastní obsah na cloudu (podobně jako na OneDrive, Google Drive apod.). Obsah je možné do ArcGIS Online publikovat z ArcGIS Pro (v k. m. kterékoli vrstvy v tabulce obsahu je položka *Sharing \> Share as web layer*, případně nahoře v záložce *Share \> Web layer* je možné vypublikovat všechny vrstvy aktuálně otevené v projektu (pozor, i vypnuté / odškrtnuté ze zobrazení). Publikovat lze vrstvy jako vektorové (Feature layer) nebo rastrové (Tile layer). Publikovaná data odečítají tzv. kredity za spotřebování datového úložiště (zhruba 1 kr. / 100 MB / den).

Pro používání vrstev na ArcGIS Online v prostředí ArcGIS Pro je možné je standardně pomocí *Add Data* přidat do mapového projektu. Pouze se v dialogu otevření dat volí vlevo v sekci *Portal* buď *My Content* (hledání ve vlastních datových sadách) anebo *ArcGIS Online* (hledání v celém cloudu). Cizí datové vrstvy (tj. vypublikované do cloudu jiným uživatelem) není možné editovat, ale v režimu pro čtení je možné je prohlížet, analyzovat, dotazovat se na ně apod. V případě potřeby lokálního stažení kopie vrstvy na ArcGIS Online je možné pomocí funkce **Select** (standardně v panelu Geoprocessing nebo přes *Analysis \> Tools*) provést dotaz na vrstvu, jehož výsledkem jsou lokálně uložená data. Tentýž postup je možné použít pro data distribuovaná přes služby WFS nebo ArcGIS Server Feature Service, kde však může být omezen počet prvků na jeden dotaz. Lze vložit SQL podmínku jako v případě atributového dotazu a omezit data, která nás zajímají, na určitý podvýběr.

## Symbolika dat {#symbolika_dat}

ArcGIS standardně přidělí všem vektorovým datům načteným z lokálního umístění výchozí symbolizaci. Tu je možné měnit pomocí položky *Symbology* v k. m. třídy prvků. Není takto možné měnit symboliku u vybraných typů vrstev (např. z webového umístění – webové služby).

#### **Symbolika vektorů** {#symbolika_vektorů}

Implicitně je vždy nastavena hodnota *Single symbol*, vizualizující všechny prvky vrstvy stejným způsobem. Pomocí přepnutí na *Unique values* (v případě kvalitativních dat, kategorií apod.) nebo na *Graduated colors* (v případě kvantitativních dat) je možné symbolizovat data různým způsobem podle příslušnosti k různé hodnotě atributu. V k. m. jednotlivých symbolových tříd pod volbou *Unique values* nebo *Graduated colors* je pak možné nastavit nezávislou symbolizaci jednotlivým hodnotám atributu, případně některé hodnoty z vykreslení zcela vyloučit.

<hr>

# CVIČNÉ ÚLOHY PRO ZPRACOVÁNÍ NA CVIČENÍ {#cvičné_úlohy_pro_zpracování_na_cvičení}

## Vektorová data, atributové dotazy {#vektorová_data_atributové_dotazy}

```{=mediawiki}
{{GISUloha|1|Kolik je v ČR rybníků|VodniPlochy|399}}
```
Návod pro ArcGIS: Table options → Select By Attributes `{{bullet}}`{=mediawiki} `TYP = 2` `{{bullet}}`{=mediawiki} Apply

```{=mediawiki}
{{GISUloha|2|Jaká je celková délka (v km) přirozených vodních toků v ČR|VodniToky|30 412 km}}
```
```{=mediawiki}
{{GISUloha|3|Jaká je průměrná nadmořská výška (v m) vodních nádrží v ČR|VodniPlochy|419 m}}
```
```{=mediawiki}
{{GISUloha|4|Kolik silnic v ČR má více než dva jizdní pruhy|Silnice_2015|1002}}
```
```{=mediawiki}
{{GISUloha|5|Jaká je délka (v km) dálnic v ČR, které mají šest jízdních pruhů|Silnice_2015|36,45 km}}
```
```{=mediawiki}
{{GISUloha|6|Kolik železničních stanic v ČR obsahuje ve svém názvu předložku 'nad'|ZeleznicniStanice|112}}
```
```{=mediawiki}
{{GISUloha|7|Jaká je celková plocha (v {{sq|km}}) sídel v ČR u kterých jejich název začíná na písmeno 'K'|SidlaPlochy|86,41 {{sq|km}}}}
```
```{=mediawiki}
{{GISUloha|8|Ve které obci Ústeckého kraje je největší nezaměstnanost a kolik to je|ObceBody (AC)|Trmice; 17,56%}}
```
```{=mediawiki}
{{GISUloha|9|Najděte obec v ČR, kde je nejvyšší poměr mezi muži a ženami a kolik to je|ObceBody (AC)|Staňkovice; 2,54:1}}
```
```{=mediawiki}
{{GISUloha|10|V kolika obcích v ČR převyšuje počet sňatků počet rozvodů. V jaké obci je počet sňatků nejvyšší vzhledem k aktuálnímu počtu obyvatel|ObceBody (AC)|3808; Podhradí nad Dyjí}}
```
```{=mediawiki}
{{GISUloha|11|Jaká je průměrná hodnota nezaměstnanosti v ORP Beroun|ObceBody (AC)|5,30%}}
```
```{=mediawiki}
{{GISUloha|12|Kolik katastrálních území spadá do oblasti s kódem LAU1 'CZ0327' a jakou mají celkovou výměru (v {{sq|km}})|KatastralniUzemiPolygony (AC)|215; 1 378{{sq|km}}}}
```
```{=mediawiki}
{{GISUloha|13|V kolika případech se shoduje název obce s názvem katastrálního území|KatastralniUzemiPolygony (AC)|4516}}
```
```{=mediawiki}
{{GISUloha|14|Kolik katastrálních území začíná na písmeno 'R' a má přesně tři znaky ve svém názvu|KatastralniUzemiPolygony (AC)|3}}
```
```{=mediawiki}
{{GISUloha|15|Ve kterých krajích je míra nezaměstranosti mužů větší než u žen|KrajePolygony (AC)|Karlovarský, Olomoucký, Moravskoslezský}}
```
```{=mediawiki}
{{GISUloha|16|Jaká je celková délka silnic 1., 2. a 3. třídy|Silnice_2015|1 - 5 794 km; 2 - 14 138 km; 3 - 21 369 km}}
```
```{=mediawiki}
{{GISUloha|17|Jaký název pro obec je nejfrekventovanější, kolik obcí s tímto názvem v ČR je|ObceBody (AC)|14; Nová ves}}
```
```{=mediawiki}
{{GISUloha|18|Pro každý typ vodní plochy najděte nejvyšší nadmořskou výšku|VodniPlochy|Vodní nádrž 773 m; Rybník 731 m; Jezero 1 008 m}}
```
```{=mediawiki}
{{GISUloha|19|Jaký je poměr mezinárodních ku vnitrostátním letištím v ČR|Letiste|18:76}}
```
```{=mediawiki}
{{GISUloha|20|Který okres v ČR se skládá z největšího počtu obcí a kolik to je|ObceBody (AC)|Brno-venkov, 187}}
```
## Prostorové dotazy {#prostorové_dotazy}

```{=mediawiki}
{{GISUloha|31|Existuje v ČR letiště, které leží v lese? Jak se jmenuje|Letiste, Lesy|Točná}}
```
```{=mediawiki}
{{GISUloha|32|Kolika obcemi v ČR neprochází žádná silnice|ObcePolygony (AC), Silnice_2015|241}}
```
*Poznámka:* singleparts vs multiparts

```{=mediawiki}
{{GISUloha|33|Kolik obcí leží na hranici ČR|ObcePolygony (AC), StatPolygon (AC)|285}}
```
```{=mediawiki}
{{GISUloha|34|Vyberte silnice, které kříží vodní toky. Kolik procent z těchto silnic tvoří silnice první třídy|Silnice_2015, VodniToky|14,5%}}
```
```{=mediawiki}
{{GISUloha|35|Kolik procent rybníků z celkového počtu leží celou svojí plochou na území Jihočeského kraje|VodniPlochy, KrajePolygony (AC)|41,85%}}
```
```{=mediawiki}
{{GISUloha|36|Na kolika mapových listech Základní mapy 1<nowiki>:</nowiki>25 000 leží alespoň částečně okres Litoměřice. Kolik mapových listů potom leží v tomto okresu celou svojí plochou|KladZakladnichMap, OkresyPolygon (AC)|19, 4}}
```
```{=mediawiki}
{{GISUloha|37|Kolik železničních stanic leží v lese a zároveň jejich název nezačíná na písmeno 'L'|Lesy, ZeleznicniStanice|100}}
```
```{=mediawiki}
{{GISUloha|38|Které silnice (uveďte jejich číslo) druhé třídy procházejí oblastí bažin a rašelinišť|Silnice_2015, BazinyARaseliniste|103, 169}}
```
```{=mediawiki}
{{GISUloha|39|Jaká je průměrná nadmořská výška výškových kót na území Středočeského kraje|VyskoveKoty, KrajePolygony (AC)|488}}
```
```{=mediawiki}
{{GISUloha|40|Kolik vodních ploch leží alespoň částí své plochy ve vzdálenosti do 10 km od poledníku se zeměpisnou délkou 15&deg;|VodniPlochy, ZemepisnaSitWGS84|45}}
```
```{=mediawiki}
{{GISUloha|41|Kolik obcí se dotýká alespoň jedním liniovým segmentem hranice kraje|KrajePolygony (AC), ObcePolygony (AC)|1248}}
```
```{=mediawiki}
{{GISUloha|42|Vyberte katastrální území, ve kterých leží alespoň částečně jedna vodní plocha, seskupte tyto území podle kódu NUTS (LAU1). Uveďte jaký kód NUTS má největší výměru a z kolika katastrálních území se skládá|KatastralniUzemiPolygony (AC), VodniPlochy (AC)|CZ0313, 78}}
```
```{=mediawiki}
{{GISUloha|43|Uveďte souřadnice reprezentačního bodu (centroidu) největší vodní nádrže v Libereckém kraji. O jakou vodní nádrž se jedná|VodniPlochy, KrajePolygony (AC)|-678660, -971660; Josefův důl}}
```
```{=mediawiki}
{{GISUloha|44|Kolik obcí leží celou svojí plochou na mapovém listu "Pardubice" ZM 1<nowiki>:</nowiki>25 000. Do kolika ORP tyto obce patří a které to jsou|ObcePolygony (AC), KladyZakladnichMap|8; 2; Chrudim, Pardubice}}
```
```{=mediawiki}
{{GISUloha|45|Kolik obcí v ČR leží svoji plochou alespoň na dvou mapových listech Základní mapy 1<nowiki>:</nowiki>50 000|ObcePolygony (AC), KladyZakladnichMap|2357}}
```

––––––––––––––––––––––––––––––––––––

## Prostorové funkce {#prostorové_funkce}

```{=mediawiki}
{{GISUloha|51|Jaká je výměra (v ha) bažin a rašelinišť ležících v lese. Kolik to je procent z celkové výměry bažin a rašelinišť|BazinyARaseliniste, Lesy|5743; 64%}}
```
```{=mediawiki}
{{GISUloha|52|Jaká je výměra (v {{sq|km}}) území omezeného pouze na ČR do 100 m od dálnic|Silnice_2015, StatPolygon (AC)|155,38}}
```
```{=mediawiki}
{{GISUloha|53|Kolik obcí v ČR leží celou svou plochou do vzdálenosti 10 km od řeky Labe? Jaký je celkový počet obyvatel těchto obcí|VodniToky, StatPolygon (AC), ObcePolygony (AC)|520; 868 320}}
```
```{=mediawiki}
{{GISUloha|54|Na kolika místech se kříží dálnice, rychlostní silnice či silnice 1. třídy s železnicí. Kolik z těchto křížení leží do vzdálenosti 1km od nejbližší železniční stanice|Silnice_2015, Zeleznice, ZeleznicniStanice|1165; 442 (x)}}
```
```{=mediawiki}
{{GISUloha|55|Jaká je výměra území (v ha), na kterých leží les či vodní plocha. Existuje území, které by odpovídalo současně oběma podmínkám|Lesy, VodniPlochy|2 832 583; ne}}
```
```{=mediawiki}
{{GISUloha|56|Vytvořte společnou datovou vrstvu pro letiště a železniční stanice. Kolik objektů tato vrstva obsahuje|Letiste, ZeleznicniStanice|1177}}
```
```{=mediawiki}
{{GISUloha|57|Kolik procent z celkové výměry ČR činí uzemí, která jsou vzdálená od nejbližšího rybníku více než 25 km|Vodni Plochy, StatPolygon|6,9%}}
```
```{=mediawiki}
{{GISUloha|58|Jaká je výměra uzemí ČR (v {{sq|km}}), která leží dále než 5 km od nejbližší silnice a zároveň dále než 10 km od nejbližší železniční stanice? Na území kterých obcí leží největší z hledaných lokalit|Silnice_2015, ZeleznicniStanice, StatPolygon (AC)|18,6 {{sq|km}}; Modrava}}
```
```{=mediawiki}
{{GISUloha|59|Kolik procent území Jihočeského kraje tvoří vodní plochy|VodniPlochy, ObcePolygony (AC)| 1,73%}}
```
## Úlohy za bonusové body {#úlohy_za_bonusové_body}

(data pro úlohy jsou k dispozici [ZDE](https://vltava.fsv.cvut.cz/giss_data/))

-   ~~**Úloha 2401** (0,25 bodu)~~

~~Ve které obci je nejvíce úseků el. vedení (vrstva *PowerL* z datasetu *DATA250.zip*) dlouhých alespoň 4 km, které do ní spadají celou svou délkou? Kolik takových úseků nad 4 km celkem je a jaká je jejich průměrná délka? (užijte také *ObcePolygony* z ArcČR 3.3)~~

-   **Úloha 2402** (0,25 bodu)

Kolik z těch maloplošných chráněných území (vrstva *MZChU* z datasetu *MZChU.zip*), které zasahují svou plochou alespoň do dvou okresů (*OkresyPolygony* v ArcČR 3.3), má název (atribut *NAZEV*) o min. třech slovech? Kolik z takových je národní přír. památkou (atribut *KAT* roven *NPP*)?

-   **Úloha 2403** (0,25 bodu)

Kolik % plochy okresů větších než je průměrná velikost okresu v ČR zabírá území, pro které platí, že je vodní plochou a není vzdáleno více než 5 km od nejbližší výškové kóty vysoké alespoň 600 m? (vše v ArcČR 3.3 – vrstvy *OkresyPolygony, VodniPlochy, VyskoveKoty*)

-   **Úloha 2404** (0,25 bodu)

Předpokládejme ochranné pásmo kolem železniční trati, které tvoří pruh území 300 m široký na obě strany od železnice. Kolik rašelinišť se do tohoto ochranného pásma dostane alespoň třetinou své velikosti? (vrstva *SwampA* a *RailrdL* z datasetu *DATA250.zip*)?

!!! warning "POZOR" 

**Pro uznání bodů je třeba zaslat (přes Teams) výsledek jako zabalený projektový balíček (menu *Share* \> *Map *a zde dát *Save package to file*) plus printscreen panelu *History* (menu *Analysis* \> *History*), aby bylo trochu patrné, kterými funkcemi jste se výsledku dobrali.**
