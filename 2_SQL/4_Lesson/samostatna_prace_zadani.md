# Lekce 4: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - CREATE TABLE AS SELECT

1. Vytvořte tabulku s názvem `topSales` pomocí SELECT příkazu, který vybere data z tabulky `sales` kde výnos (`revenue`) je alespoň _3000$_.


2. 
* Přejmenujte sloupec `Zip` v tabulce `topSales` na `PSC`.
* Přejmenujte tabulku `topSales` na `top_sales`
* Nakonec odstraňte tabulku `top_sales` z databáze.


### Úkol 2 - CREATE TABLE

3. Vytvořte tabulku s názvem `shop`, která bude obsahovat následující sloupce:

* `shopID` - primárním klíč s datovým typem `NUMERIC`
* `manager` -  datový typ `TEXT`, který bude uchovávat jméno manažera obchodu
* `numEmployees` - datový typ `NUMERIC`, který bude uchovávat počet zaměstnanců v obchodě
* `zip` - datový typ `NUMERIC`, který bude uchovávat poštovní směrovací číslo.


### [Bonus]

1. Vytvořte kopii tabulky `shop` z předchozího cvičení a pojmenujte ji `shop_copy`. Smažte sloupec `numEmployees` a přidejte do tabulky nový numerický sloupec dle vlastního výběru.


---

## Samostatná práce 2
---

### Úkol 1 - Vložení hodnot do tabulky

1. Vložte do tabulky `shop` (z předchozího cvičení) 4 záznamy, které mají hodnoty:
    * `shopID` = `1`, `manager` = `Anna Thompson`, `numEmployees` = `17`, `zip` = `6026`
    * `shopID` = `2`, `manager` = `Rick Fall`, `numEmployees` = `4`, `zip` = `102`
    * `shopID` = `3`, `manager` = `Beth Lim`, `numEmployees` = `5`, `zip` = `1009`
    * `shopID` = `4`, `manager` = `NULL`, `numEmployees` = `11`, `zip` = `102`

2. Vložte do tabulky `shop` alespoň 2 další záznamy (zvolte hodnoty sloupců dle sebe), pro jeden z nich do sloupce `numEmployees` vložte hodnotu `NULL`.

### Úkol 2 - Změny hodnot v tabulce

1. Upravte následující záznamy v tabulce `shop`:
    * Změňte jméno manažera prodejny s ID 1 na `Anna Richards`
    * Upravte počet zaměstnanců prodejny s ID 2 na `6`
    * Pro všechny pobočky, které mají PSČ 102, změňte jméno manažera na `Rick Fall`

2. Z tabulky `shop` odstraňte záznam, kde `shopID` je 3 (pobočka byla zrušena).


### [Bonus]

1. Vyberte všechny obchody/prodejny z tabulky `sho`p a přidejte k nim informace z tabulky `country` (tabulky lze propojit pomocí sloupce `zip`). Ve výsledku zachovejte všechny prodejny, i ty, pro které v tabulce `country` není záznam.

    _"Skutečné zadání":_
    _Vytvořte kompletní report o prodejnách a jejich lokalitě._


2. Z tabulky `shop` vyberte hodnotu `SUM` pro sloupec `numEmployees`.

    _"Skutečné zadání":_
    _Jaký je celkový počet zaměstnanců na prodejnách?_

3. Vytvořte dotaz, který z tabulky `shop` vypočítá celkový počet zaměstnanců připadajících na každého manažera (`manager`) a seřadí manažery prodejen podle počtu zaměstnanců sestupně.

    _"Skutečné zadání":_
    _Kteří manažeři mají nejvíce zaměstnanců pod svým vedením?_

