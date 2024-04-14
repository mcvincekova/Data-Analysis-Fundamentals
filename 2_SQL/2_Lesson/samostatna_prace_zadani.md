# Lekce 2: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - Řazení

1. Vyberte všechny sloupce tabulky `sales` a seřaďte výsledky sestupně dle výše výnosu (`revenue`) 
    - `date`
    - `zip`
    - `revenue`
2. V předcházejícím dotazu omezte výsledek na pouze 10 řádků.

### Úkol 2 - WHERE

1. Vyberte všechny prodeje z tabulky `sales`, jejichž výnos (`revenue`) je nejméně _7000$_ a nejvýše _30000$_ (včetně).

2. Vyberte všechny prodeje z tabulky `sales`, jejichž výnos (`revenue`) je alespoň _20000$_ a zároveň počet prodaných kusů (`units`) je více než 30.

3. Vyberte všechny jedinečné státy (`state`) z tabulky `country`, kde (`region`) je `Central`.

### [Bonus]

1. Vyberte jedinečné názvy produktů z tabulky `product`, pro které platí následující:
    - produkt je v kategorii (`category`) `Mix`
    - cena produktu (`priceNew`) je nižší než _200$_
    - název produktu (`product`) začíná na písmeno `P` nebo obsahuje písmeno `Q`
    
    Výsledek seřaďte vzestupně.

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

---

## Samostatná práce 2
---

### Úkol 1 - Agregační funkce

1. Z tabulky `sales` vyberte celkovou sumu prodaných kusů (`units`) zboží ze všech prodejů.

2. Z tabulky `sales` zjistěte průměrný výnos ze všech prodejů produktů s ID (`productId`) 1 anebo 2.

3. Vybere minimální a maximální hodnotu psč kódů (`zip`) pro každou oblast (`region`) z tabulky `country`. Přejmenujte sloupce s minimální a maximální hodnoty psč na `minPSC` a `maxPSC`.

4. Vybere počet psč kódů (`zip`) pro každý stát (`state`) z tabulky `country` a seřaďte výsledky sestupně podle počtu psč kódů.

### [Bonus]

1. Určete dotaz SQL, který z tabulky `sales` vybere průměrné hodnoty výnosu (`revenue`) a jednotek (`units`) pro každý produkt s ID vyšším než 500, seřadí výsledky sestupně podle průměrného výnosu a omezí výstup jen na prvních 10 výsledků.

---

## Samostatná práce 3 - Agregační funkce & Analytické úkoly
---

### Úkol 1 - Agregační funkce

1. Napište dotaz SQL, který z tabulky `country` zjistí počet unikátních měst (`city`) pro každý stát (`state`), a poté zobrazí pouze ty státy, které mají více než 1000 unikátních měst. Přejmenujte sloupec počtu měst na `pocetMest`. Kolik takových států je?

### Úkol 2 - Analytické úkoly

1. Jaká je průměrná cena nabízených produktů v jednotlivých kategoriích?

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

### [Bonus]

1. Kolik unikátních produktů bylo prodáno v prvním a druhém měsíci roku 2014? _(Nápověda: Rok a měsíc lze získat z formátu date pomocí funkce `strftime`.)_
