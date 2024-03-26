## Základní pojmy

### Data
Údaje, používané pro popis nějakého jevu nebo vlastnosti pozorovaného objektu. Data se získávají zápisem, měřením nebo pozorováním

<img src = "https://upload.wikimedia.org/wikipedia/commons/d/d2/Sonar_tracking_of_tungsten_ball_underneath_research_vessel_for_calibration_%2816824332958%29.jpg" height = "200px" title="Data">
<p>&nbsp;</p>

### Databáze 
Množina záznamů a objektů (např. tabulek), které jsou organizovány za určitým účelem.

**Předtím**

<img src= "https://upload.wikimedia.org/wikipedia/commons/3/3b/SML-Card-Catalog.jpg" height = "200px">

**Nyní**

<img src = "https://upload.wikimedia.org/wikipedia/commons/e/e0/A_view_of_the_server_room_at_The_National_Archives.jpg"  height = "200px">
<p>&nbsp;</p>

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

## MODEL DATABÁZE
Způsob uspořádání a způsob manipulace s daty

<img src = "https://github.com/mcvincekova/Data-Analysis-Fundamentals/blob/main/1_DataAnalysis/Images/model.png"  height = "200px">

- Síťové DBS (1969, 1971)
- Relační (2. pol. 70. let, 80. léta) a objektově relační (90. léta) DBS – ORACLE, Informix, Sybase, MS SQL Server, Progress, DB/2, MySQL, ...
- Objektové DBS (90. léta) – Orion, GemStone, Ontos, Object, Store
- NoSQL DBS (2005+) - BigTable, HBase, SimpleDB, Dynamo


### Vývoj modelu databáze
#### Konceptuální model

- Výběr konceptů
- Volba rozlišení (jaké detaily)

#### Logický model

- Identifikace vlastností - převod koncept entita
- Identifikace vazeb - relace s kardinalitami
- Dekompozice - podmínka splnění požadované normální formy

#### Fyzický model

- Způsob fyzického uložení dat
- V případě databází není součástí návrhu

<p>&nbsp;</p>

## RELAČNÍ MODEL DAT

### Postup vytváření

- Vymezit informace, které budeme uchovávat
- Určit vlastnosti, které jsou pro nás důležité, dostupné
- Přemýšlet o tom, jaké jsou mezi objekty vztahy
- Datové modelování = návrh datového modelu (ER diagram)

### Entity Relationship Diagram

- Design relačních databází
- Logický model

### Datový model

- **Entita:** věc schopná samostatné existence a je jednoznačně identifikovatelná.
- **Atribut:** vlastnost entity, která nás v kontextu daného problému zajímá.
- **Relace:** vztahy mezi tabulkami.
- **Kardinalita / Multiplicita:** kolikrát se může instance dané entity účastnit vztahu s instancemi druhé entity.
  - 1:1
  - 1:N
  - M:N

### POJMY

- Entita Pacient - jaké může mít atributy?
- Udělat tabulku pacient - protože je v kartotéce - co všechno evidujeme o pacientovi?...
  - Jméno
  - Příjmení
  - Datum narození
  - Pohlaví

### STŘEDNÍ ŠKOLA

- Klíč
  - Primární klíč (PK)
  - Cizí klíč (FK)

### RELAČNÍ MODEL DAT

- Autorem prof. E.F.Codd (první publikace 1969 a 1970).
- První komerční implementace 1977 IBM System R.
- K manipulaci s daty možno použít relační kalkul nebo operace relační algebry (sjednocení, průnik).
- Model dat založený na predikátové logice prvního řádu.

## ZDROJE PRO SAMOSTUDIUM (nepovinné)

- [Modelování databází](https://www.root.cz/clanky/modelovani-databazi/)
- [ER Diagrams](https://www.lucidchart.com/pages/er-diagrams)
- [Informační systémy - Databáze](http://lucie.zolta.cz/index.php/iformacni-systemy-databaze/42-relacni-datovy-model)
- [draw.io](https://www.draw.io)
