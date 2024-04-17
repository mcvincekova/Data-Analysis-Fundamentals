# Lekce 2: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - Řazení

1. Vyberte všechny sloupce tabulky `sales` a seřaďte výsledky sestupně dle výše výnosu (`revenue`) 
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

1. Vyberte všechny prodeje z tabulky `sales`, jejichž výnos (`revenue`) je nejméně _7000$_ a nejvýše _30000$_ (včetně).

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

2. Vyberte všechny prodeje z tabulky `sales`, jejichž výnos (`revenue`) je alespoň _20000$_ a zároveň počet prodaných kusů (`units`) je více než 30.

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

3. Vyberte všechny jedinečné státy (`state`) z tabulky `country`, kde (`region`) je `Central`.

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

2. Každou podmínku (1. 2. a 3.) v následujícím SQL dotazu zkuste napsat jiným způsobem, tak aby funkce SQL dotazu zůstala nezměněna. Například: `productID != 1` lze také zapsat jako `productID <> 1`

```sql 
SELECT 
    zip, 
    state, 
    region
FROM 
    country
WHERE 
    -- 1. podminka
    (region LIKE '%t' AND region LIKE '____')
    -- 2. podminka 
    AND (state = 'OH' OR state = 'PA' OR state = 'NM')
    -- 3. podminka
    AND (zip BETWEEN 45880 AND 87050)
```

**Řešení**
> SQL dotaz:
>```sql 
>SELECT 
>    zip, 
>    state, 
>    region
>FROM 
>    country
>WHERE 
>    -- 1. podminka
>    -- (region LIKE '%t' AND region LIKE '____')
>    region LIKE '___t'
>    -- 2. podminka 
>    -- AND (state = 'OH' OR state = 'PA' OR state = 'NM')
>    AND state IN ('OH', 'PA', 'NM')
>    -- 3. podminka
>    -- AND (zip BETWEEN 45880 AND 87050)
>    AND zip >= 45880 AND zip <= 87050
>```
>
---

## Samostatná práce 2
---

### Úkol 1 - Agregační funkce

1. Z tabulky `sales` vyberte celkovou sumu prodaných kusů (`units`) zboží ze všech prodejů.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   SUM(units)
>FROM
>   sales
>

2. Z tabulky `sales` zjistěte průměrný výnos ze všech prodejů produktů s ID (`productId`) 1 anebo 2.

**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   AVG(revenue)
>FROM 
>   sales
>WHERE 
>   productId IN (1, 2)
>```
>

3. Vybere minimální a maximální hodnotu psč kódů (`zip`) pro každou oblast (`region`) z tabulky `country`. Přejmenujte sloupce s minimální a maximální hodnoty psč na `minPSC` a `maxPSC`.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   MIN(zip) AS minPSC,
>    MAX(zip) AS maxPSC,
>    region
>FROM
>   country
>GROUP BY
>   region
>```
>

4. Vybere počet psč kódů (`zip`) pro každý stát (`state`) z tabulky `country` a seřaďte výsledky sestupně podle počtu psč kódů.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   COUNT(zip),
>   state
>FROM
>   country
>GROUP BY
>   state
>ORDER BY
>   COUNT(zip) DESC
>```
>

### [Bonus]

1. Určete dotaz SQL, který z tabulky `sales` vybere průměrné hodnoty výnosu (`revenue`) a jednotek (`units`) pro každý produkt s ID vyšším než 500, seřadí výsledky sestupně podle průměrného výnosu a omezí výstup jen na prvních 10 výsledků.

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   AVG(revenue),
>   AVG(units),
>   productId
>FROM
>   sales
>WHERE 
>   productid > 500
>GROUP BY
>   productId
>ORDER BY
>   AVG(revenue) DESC
>LIMIT 
>   10
>```
>

---

## Samostatná práce 3 - Agregační funkce & Analytické úkoly
---

### Úkol 1 - Agregační funkce

1. Napište dotaz SQL, který z tabulky `country` zjistí počet unikátních měst (`city`) pro každý stát (`state`), a poté zobrazí pouze ty státy, které mají více než 1000 unikátních měst. Přejmenujte sloupec počtu měst na `pocetMest`. Kolik takových států je?

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   count(DISTINCT city) AS pocetMest,
>    state
>FROM
>   country
>GROUP bY
>   state
>HAVING
>   pocetMest > 1000
>```
>

### Úkol 2 - Analytické úkoly

1. Jaká je průměrná cena nabízených produktů v jednotlivých kategoriích?

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   AVG(pricenew),
>   category
>FROM
>   product
>GROUP BY
>   category
>```
>

2. Popřemýšlejte nad tím, co dělá níže uvedený SQL dotaz. Jaké by bylo technické vs. skutečné zadání pro tento dotaz?

```sql
SELECT
    COUNT(productId),
    manufacturerId
FROM 
    product
WHERE
    priceNew < 100
GROUP BY
    manufacturerId
```

**Řešení**
> Technické zadání:
>
>_Určete dotaz SQL, který spočítá počet produktů (`productId`) pro každého výrobce (`manufacturerId`) z tabulky `product`, kde je cena (`priceNew`) produktu nižší než 100$._
>
> Skutečné zadání:
>
>_Kolik produktů levnějších než 100 $ nabízí každý výrobce?_
>

### [Bonus]

1. Kolik unikátních produktů bylo prodáno v prvním a druhém měsíci roku 2014? _(Nápověda: Rok a měsíc lze získat z formátu date pomocí funkce `strftime`.)_

**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   COUNT(DISTINCT productid),
>   strftime('%m', date)
>FROM
>   sales
>WHERE
>   strftime('%m', date) IN ('01', '02')
>   AND strftime('%Y', date) = '2014'
>GROUP BY
>   strftime('%m', date)
>```
>
