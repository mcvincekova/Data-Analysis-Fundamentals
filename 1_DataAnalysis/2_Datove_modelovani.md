# Agenda

- Základní pojmy
- Model databáze
- Vývoj modelu databáze
- ER diagram


# Základní pojmy

## Data
Údaje, používané pro popis nějakého jevu nebo vlastnosti pozorovaného objektu. Data se získávají zápisem, měřením nebo pozorováním

<img src = "https://upload.wikimedia.org/wikipedia/commons/d/d2/Sonar_tracking_of_tungsten_ball_underneath_research_vessel_for_calibration_%2816824332958%29.jpg" height = "200px" title="Data">
<p>&nbsp;</p>

## Databáze 
Množina záznamů a objektů (např. tabulek), které jsou organizovány za určitým účelem.

**Předtím**

<img src= "https://upload.wikimedia.org/wikipedia/commons/3/3b/SML-Card-Catalog.jpg" height = "200px">

**Nyní**

<img src = "https://upload.wikimedia.org/wikipedia/commons/e/e0/A_view_of_the_server_room_at_The_National_Archives.jpg"  height = "200px">

#### Přínosy

- Rychlost
- Řízení dat
- Přesnost
- Bezpečnost

#### Druhy

- Relační databáze
- Objektová databáze
- Graph databáze
- atd.

<p>&nbsp;</p>

## Model databáze
Způsob uspořádání a způsob manipulace s daty

<img src = "../Resources/Images/DataAnalysis/model.png"  height = "300px">

- Síťové DBS (1969, 1971)
- Relační (2. pol. 70. let, 80. léta) a objektově relační (90. léta) DBS – ORACLE, Informix, Sybase, MS SQL Server, Progress, DB/2, MySQL, ...
- Objektové DBS (90. léta) – Orion, GemStone, Ontos, Object, Store
- NoSQL DBS (2005+) - BigTable, HBase, SimpleDB, Dynamo

<p>&nbsp;</p>

## Vývoj modelu databáze
### Konceptuální model

- Výběr konceptů
- Volba rozlišení (jaké detaily)

### Logický model

- Identifikace vlastností - převod koncept entita
- Identifikace vazeb - relace s kardinalitami
- Dekompozice - podmínka splnění požadované normální formy

#### Fyzický model

- Způsob fyzického uložení dat
- V případě databází není součástí návrhu

<p>&nbsp;</p>

## Relační model dat

### Postup vytváření

- Vymezit informace, které budeme uchovávat
- Určit vlastnosti, které jsou pro nás důležité, dostupné
- Přemýšlet o tom, jaké jsou mezi objekty vztahy
- Datové modelování = návrh datového modelu (ER diagram)

<p>&nbsp;</p>

### Entity Relationship Diagram
- Design relačních databází
- Logický model

<img src = "https://upload.wikimedia.org/wikipedia/commons/b/b4/Example_ERD2.png">

### Pojmy

- **Entita:** věc schopná samostatné existence a je jednoznačně identifikovatelná.
- **Atribut:** vlastnost entity, která nás v kontextu daného problému zajímá.
- **Relace:** vztahy mezi tabulkami.
- **Kardinalita / Multiplicita:** kolikrát se může instance dané entity účastnit vztahu s instancemi druhé entity.
  - 1:1, 1:N, M:N

<p>&nbsp;</p>

#### Příklad - Pacient

- Entita Pacient - jaké může mít atributy?

- Uděláme tabulku pacient - co všechno evidujeme o pacientovi?
  - Jméno
  - Příjmení
  - Datum narození
  - Pohlaví

#### Příklad - Střední škola

O studentovi víme, jak se jmenuje, v jakém ročníku je, kdy se narodil a odkud pochází.
Předmět je vypsán pro určitý počet studentů. Má svůj kód. Každý předmět má právě jednoho učitele.  
Každý student studuje několik předmětů. Předmět je vyučován v učebně. Předmět se učí ve specializované učebně (Biologie se nemůže učit v učebně matematiky).
Učitel může učit více předmětů.

**Řešení:** [Lucidchart](https://lucid.app/lucidchart/0c00c625-cd48-422d-b1b1-c17bbdb2cf18/edit?viewport_loc=-908%2C81%2C1664%2C781%2C0_0&invitationId=inv_b76faaf5-ad59-4e93-9636-3784cb722954)

<p>&nbsp;</p>

### Klíče
**Primární klíč (PK)** – jednoznačně identifikuje řádek

**Cizí klíč (FK)** – použitý v dalším výskytu k vyjádření vazeb mezi objekty zachycenými v relační databázi
FK = zkratka z anglického “foreign key”

<p>&nbsp;</p>

### Normální forma
<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/NF.png"  height = "300px">

#### 1NF 
Všechny atributy tabulky musí být atomické, tedy dále nedělitelné

<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/NF1.png"  height = "300px">

#### 2NF 
Každý neklíčový atribut musí být plně závislý na primárním klíči

<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/NF2.png"  height = "300px">

#### 3NF 
Neklíčová data jsou závislá jen na klíči a ne mezi sebou

<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/NF3.png"  height = "300px">

<p>&nbsp;</p>

#### Samostatná práce - Sklad

Vlastníte několik skladů, které po částech pronajímáte dalším firmám/zákazníkům.

Zachyťte pomocí ER-diagramu:
- Entity a jejich atributy
- Vazbu mezi zákazníkem/firmou a skladem
    - Sklad může užívat více firem naráz (mít pronajatou část skladu)
    - Zákazník si může pronajímat prostory ve více skladech

<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/sklad.png"  height = "300px">

<p>&nbsp;</p>

#### Příklad - ER diagram z dat

[Excel - prodej výrobků](https://docs.google.com/spreadsheets/d/1JoaxmCtcCjT9EuUGbrUL9yHz8QJ1R98WJwCJO9xVyNA/edit?usp=drive_link)

<p>&nbsp;</p>

## KPI
Key performance indicator (Klíčové ukazatele výkonnosti)

- celkové výnosy,
- průměrný výnos na 1 návštěvu,
- počet objednávek,
- průměrná hodnota objednávky,
- míra konverze objednávkových formulářů.

### Návrh KPI

- **Účelnost ukazatele** – uživatelé by si měli uvědomit, co přesně chtějí měřit a zjistit.
- **Jednoznačnost ukazatele** – ukazatel musí být interpretovatelný jen jedním způsobem. 
- **Zjistitelnost ukazatele** – pro měření ukazatele musí být v podniku dostupná data. Jejich zajištění je často relativně náročné. 
- **Interpretace ukazatele** – uživatelé musí být schopni KPI správně chápat a využívat

<p>&nbsp;</p>

## Zdroje pro samostudium (nepovinné)

- [Modelování databází](https://www.root.cz/clanky/modelovani-databazi/)
- [ER Diagrams](https://www.lucidchart.com/pages/er-diagrams)
- [Informační systémy - Databáze](http://lucie.zolta.cz/index.php/iformacni-systemy-databaze/42-relacni-datovy-model)
- alternativní nástroj pro tvorbu diagramů - [draw.io](https://www.draw.io)
