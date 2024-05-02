# Lekce 4: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - CREATE TABLE AS SELECT

1. Vytvořte tabulku s názvem `topSales` pomocí SELECT příkazu, který vybere data z tabulky `sales` kde výnos (revenue) je alespoň _3000$_.


**Řešení**
> SQL dotaz:
>```sql
>CREATE TABLE topSales AS
>SELECT
>   *
>FROM 
>   sales
>WHERE
>   revenue >= 3000
>```
>

2. 
* Přejmenujte sloupec `Zip` v tabulce `topSales` na `PSC`.
* Přejmenujte tabulku `topSales` na `top_sales`
* Nakonec odstraňte tabulku `top_sales` z databáze.


**Řešení**

> Postupně vykonáme následující příkazy:
>
>
> Přejmenujte sloupec:
>```sql
>ALTER TABLE 
>   topSales 
>RENAME COLUMN Zip TO PSC
>```
>
>
> Přejmenujte tabulku:
>```sql
> ALTER TABLE 
>   topSales 
> RENAME TO top_sales
>```
>
>
> Odstraňte tabulku:
>```sql
>DROP TABLE topSales;
>```
>


### Úkol 2 - CREATE TABLE

3. Vytvořte tabulku s názvem `shop`, která bude obsahovat následující sloupce:

* `shopID` - primárním klíč s datovým typem `NUMERIC`
* `manager` -  datový typ `TEXT`, který bude uchovávat jméno manažera obchodu
* `numEmployees` - datový typ `NUMERIC`, který bude uchovávat počet zaměstnanců v obchodě
* `zip` - datový typ `NUMERIC`, který bude uchovávat poštovní směrovací číslo.


**Řešení**
> SQL dotaz:
>```sql
>CREATE TABLE shop
>(
>   shopID NUMERIC PRIMARY KEY,
>   manager TEXT,
>   numEmployees NUMERIC,
>   zip NUMERIC
>)
>```
>

### [Bonus]

1. Vytvořte kopii tabulky `shop` z předchozího cvičení a pojmenujte ji `shop_copy`. Smažte sloupec `numEmployees` a přidejte do tabulky nový numerický sloupec dle vlastního výběru.


> Postupně vykonáme následující příkazy:
>
>
> Vytvořte kopii tabulky:
>```sql
>CREATE TABLE shop_copy AS
>SELECT * FROM shop
>```
>
>
> Smažte sloupec:
>```sql
>ALTER TABLE shop_copy
>DROP COLUMN numEmployees
>
>```
>
>
> Přidejte nový numerický sloupec:
>```sql
>ALTER TABLE shop_copy
>ADD COLUMN daysOpen NUMERIC;
>```
>


---
## Samostatná práce 2
---

### Úkol 1 - Vložení hodnot do tabulky

1. Vložte do tabulky `shop` (z předchozího cvičení) 4 záznamy, které mají hodnoty:
    * `shopID` = `1`, `manager` = `Anna Thompson`, `numEmployees` = `17`, `zip` = `6026`
    * `shopID` = `2`, `manager` = `Rick Fall`, `numEmployees` = `4`, `zip` = `102`
    * `shopID` = `3`, `manager` = `Beth Lim`, `numEmployees` = `5`, `zip` = `1009`
    * `shopID` = `4`, `manager` = `NULL`, `numEmployees` = `11`, `zip` = `102`


**Řešení**
> SQL dotaz:
>```sql
>INSERT INTO 
>   shop (shopID, manager, numEmployees, zip)
>VALUES
>   (1, 'Anna Thompson', 17, 6026),
>   (2, 'Rick Fall', 4, 102),
>   (3, 'Beth Lim', 5, 1009),
>   (4, NULL, 11, 102)
>```
>


2. Vložte do tabulky `shop` alespoň 2 další záznamy (zvolte hodnoty sloupců dle sebe), pro jeden z nich do sloupce `numEmployees` vložte hodnotu `NULL`.


**Řešení**
> SQL dotaz:
>```sql
>INSERT INTO 
>   shop (shopID, manager, numEmployees, zip)
>VALUES
>   (5, 'Jane Terr', 2, 7),
>   (6, 'Adam Leny', NULL, 1)
>```
>

### Úkol 2 - Změny hodnot v tabulce

1. Upravte následující záznamy v tabulce `shop`:
    * Změňte jméno manažera prodejny s ID 1 na `Anna Richards`
    * Upravte počet zaměstnanců prodejny s ID 2 na `6`
    * Pro všechny pobočky, které mají PSČ 102, změňte jméno manažera na `Rick Fall`


**Řešení**
> Postupně vykonáme následující příkazy:
>
>
> Změňte jméno manažera prodejny s ID 1 na `Anna Richards`
>```sql
>UPDATE 
>   shop
>SET 
>   manager = 'Anna Richards'
>WHERE 
>   shopID = 1
>```
>
>
> Upravte počet zaměstnanců prodejny s ID 2 na `6`
>```sql
>UPDATE 
>   shop
>SET 
>   numEmployees = 6
>WHERE 
>   shopID = 2
>```
>
>
> Pro všechny pobočky, které mají PSČ 102, změňte jméno manažera na `Rick Fall`
>```sql
>UPDATE 
>   shop
>SET 
>   manager = 'Rick Fall'
>WHERE 
>   zip = 102;
>```
>

2. Z tabulky `shop` odstraňte záznam, kde `shopID` je 3 (pobočka byla zrušena).


**Řešení**
> SQL dotaz:
>```sql
>DELETE FROM shop
>WHERE shopID = 3;
>```
>


### [Bonus]

1. Vyberte všechny obchody/prodejny z tabulky `sho`p a přidejte k nim informace z tabulky `country` (tabulky lze propojit pomocí sloupce `zip`). Ve výsledku zachovejte všechny prodejny, i ty, pro které v tabulce `country` není záznam.

    _"Skutečné zadání":_
    _Vytvořte kompletní report o prodejnách a jejich lokalitě._


**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   *
>FROM
>   shop LEFT JOIN country ON shop.zip = country.zip
>```
>

2. Z tabulky `shop` vypočítejte součet hodnot ve sloupci `numEmployees` a pojmenujte jej jako `totalEmployees`.

    _"Skutečné zadání":_
    _Jaký je celkový počet zaměstnanců na prodejnách?_


**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>    SUM(numEmployees) AS totalEmployees
>FROM 
>    shop;
>```
>


3. Vytvořte dotaz, který z tabulky `shop` vypočítá celkový počet zaměstnanců připadajících na každého manažera (`manager`) a seřadí manažery prodejen podle počtu zaměstnanců sestupně.

    _"Skutečné zadání":_
    _Kteří manažeři mají nejvíce zaměstnanců pod svým vedením?_


**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   SUM(numemployees), 
>   manager
>FROM 
>   shop
>GROUP BY 
>   manager 
>ORDER BY 
>   SUM(numemployees) DESC
>```
>
