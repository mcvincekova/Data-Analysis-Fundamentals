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

2. Každou podmínku (1. 2. a 3.) v následujícím SQL dotazu zkuste napsat jiným způsobem, tak aby funkce SQL dotazu zůstala nezměněna. Například: 

`productID != 1` lze také zapsat jako `productID <> 1`

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
    AND (zip between 45880 AND 87050)
```

---
