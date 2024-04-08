# Lekce 1: Samostatná práce - Řešení

## Samostatná práce 1
---

### Úkol 1 - Příprava prostředí

Spusťte [sqliteonline.com](https://sqliteonline.com/) a importujte data podle [návodu](Data-Analysis-Fundamentals/2_SQL/sql.md)

### Úkol 2 - Seznámení s daty

1. Vyberte data z tabulky `country`
    - data o které zemi jsou v této tabulce uložena?

**Řešení**
> Na zobrazení dat použijeme následující dotaz
> 
> ```sql 
> SELECT * FROM country
> ```
>
> Země, kterou hledáme, je uvedena ve sloupci  `Country` - `USA`

2. Vyberte data z tabulek `product` a `manufacturer`
    - který výrobce vyrábí produkt s ID 1? 
    - jak vypadá logo tohoto výrobce?

**Řešení**
> Na zobrazení dat použijeme následující dotazy:
> 
> ```sql
> SELECT * FROM product
> ```
>
> ```sql
> SELECT * FROM manufacturer
> ```
>
> Ve tabulce `product` můžeme vidět, že produkt s `ProductID` 1 je vyráběn výrobcem s `ManufacturerID` 1. Následně v tabulce `manufacturer` hledáme výrobce, kterého `ManufacturerID` je 1 - `Abbas`

### [Bonus] - Relace

1. Podívejte se opět na tabulky `product` a `manufacturer` 
    - které sloupce jsou použity k vytvoření vztahu mezi těmito tabulkami?

**Řešení**
> Sloupec `ManufacturerID` v tabulce `manufacturer` a slopuec `ManufacturerID` (představuje cizí klíč) v tabulce `product`.


2. Prozkoumejte tabulku `sales`. Tato tabulka obsahuje 3 sloupce, které slouží jako cizí klíče odkazující na tři další tabulky.     
    - Které sloupce to jsou a na které tabulky odkazují?

**Řešení**
> * `ProductID` - odkazuje na tabulku `product`
> * `Date` - odkazuje na tabulku `date`
> * `Zip` - odkazuje na tabulku `country`

---

## Samostatná práce 2
---

### Úkol 1 - Výběr sloupců pomocí příkazu SELECT

1. Vyberte následující sloupce z tabulky `sales`: 
    - `date`
    - `zip`
    - `revenue`

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   date,
>   zip,
>   revenue
>FROM
>   sales
>```
>

2. Sloupce z předchozího dotazu přejmenujte následovně:
    - `date`        - `datum`
    - `zip`         - `psc`
    - `revenue`     - `zisk`

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   date AS datum,
>   zip AS psc,
>   revenue AS zisk
>FROM
>   sales
>```
>

### Úkol 2 - LIMIT a DISTINCT

1. Vyberte všechny sloupce z tabulky `product` a zobrazte pouze prvních 5 řádků.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   *
>FROM
>   product
>LIMIT
>   5
>```
>

2. Vyberte jedinečné kategorie (`category`) produktů z tabulky `product` (tak aby tam žádná kategorie nebyla víckrát).

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   DISTINCT category
>FROM
>   product
>```
>

3. Vyberte jedinečné regiony (`region`) z tabulky `country` (tak aby tam žádný region nebyl víckrát) a zobrazte pouze první záznam.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   DISTINCT region
>FROM
>   country
>LIMIT
>   1
>```
>

### [Bonus]

1. SQL dotaz uvedený níže má vybrat sloupce `month`, `quarter` a `year` z tabulky `date` a zobrazit pouze 10 řádků. Bohužel ale obsahuje syntaktickou chybu a nedá se spustit. Opravte dotaz a přidejte do výsledného SQL jednořádkový komentář s informací o tom, kde byla chyba.

```
LIMIT
    10
SELECT
    month
    quarter,
    year
FROM
    date
```

**Řešení**
> SQL dotaz:
>```sql
>-- Chyby: chybejici carka za nazvem sloupcu 'month', sekce LIMIT presunuta za sekci FROM
>SELECT
>   month,
>   quarter,
>   year
>FROM
>   date
>LIMIT
>   10
>```
>

---

## Samostatná práce 3
---

### Úkol 1 - Řazení

1. Vyberte všechny sloupce tabulky `sales` a seřaďte výsledky sestupně dle výše zisku (`revenue`) 
    - `date`
    - `zip`
    - `revenue`

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   date,
>   zip,
>   revenue
>FROM
>   sales
>ORDER BY
>   revenue DESC
>```
>

2. V předcházejícím dotazu omezte výsledek na pouze 10 řádků.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   date,
>   zip,
>   revenue
>FROM
>   sales
>ORDER BY
>   revenue DESC
> LIMIT
>   10
>```
>

### Úkol 2 - WHERE

1. Vyberte všechny prodeje z tabulky `sales`, jejichž zisk (`revenue`) je nejméně _7000$_ a nejvýše _30000$_ (včetně).

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   *
>FROM
>   sales
>WHERE
>   revenue BETWEEN 7000 AND 30000
>-- alternativa
>-- revenue >= 7000 AND revenue <= 30000
>```
>

2. Vyberte všechny prodeje z tabulky `sales`, jejichž zisk (`revenue`) je alespoň _20000$_ a zároveň počet prodaných kusů (`units`) je více než 30.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   *
>FROM
>   sales
>WHERE
>   revenue >= 20000
>   AND units > 30
>```
>

3. Vyberte všechny jedinečné státy (`state`) z tabulky `country` kde (`region`) je `Central`.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   DISTINCT state
>FROM
>   country
>WHERE
>   region = 'Central'
>```
>

### [Bonus]

1. Vyberte jedinečné názvy produktů z tabulky `product`, pro které platí následující:
    - produkt je v kategorii (`category`) `Mix`
    - cena produktu (`priceNew`) je nižší než _200$_
    - název produktu (`product`) začíná na písmeno `P` nebo obsahuje písmeno `Q`
    
    Výsledek seřaďte vzestupně.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   DISTINCT product
>FROM
>   product
>WHERE
>   (product LIKE 'P%' OR product LIKE '%Q%')
>   AND category = 'Mix'
>   AND pricenew < 200
>ORDER BY 
>   product
>```
>
---
