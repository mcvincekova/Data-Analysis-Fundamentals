# Lekce 1: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - Příprava prostředí

Spusťte [sqliteonline.com](https://sqliteonline.com/) a importujte data podle [návodu](Data-Analysis-Fundamentals/2_SQL/sql.md)

### Úkol 2 - Seznámení s daty

1. Vyberte data z tabulky `country`
    - data o které zemi jsou v této tabulce uložena?
2. Vyberte data z tabulek `product` a `manufacturer`
    - který výrobce vyrábí produkt s ID 1? 
    - jak vypadá logo tohoto výrobce?


### [Bonus] - Relace

1. Podívejte se opět na tabulky `product` a `manufacturer` 
    - které sloupce jsou použity k vytvoření vztahu mezi těmito tabulkami?
2. Prozkoumejte tabulku `sales`. Tato tabulka obsahuje 3 sloupce, které slouží jako cizí klíče odkazující na tři další tabulky.     
    - Které sloupce to jsou a na které tabulky odkazují?

---

## Samostatná práce 2
---

### Úkol 1 - Výběr sloupců pomocí příkazu SELECT

1. Vyberte následující sloupce z tabulky `sales`: 
    - `date`
    - `zip`
    - `revenue`
2. Sloupce z předchozího dotazu přejmenujte následovně:
    - `date`        - `datum`
    - `zip`         - `psc`
    - `revenue`     - `zisk`

### Úkol 2 - LIMIT a DISTINCT

1. Vyberte všechny sloupce z tabulky `product` a zobrazte pouze prvních 5 řádků.

2. Vyberte jedinečné kategorie (`category`) produktů z tabulky `product` (tak, aby tam žádná kategorie nebyla víckrát).

3. Vyberte jedinečné regiony (`region`) z tabulky `country` (tak, aby tam žádný region nebyl víckrát) a zobrazte pouze první záznam.

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

---

## Samostatná práce 3
---

### Úkol 1 - Řazení

1. Vyberte všechny sloupce tabulky `sales` a seřaďte výsledky sestupně dle výše zisku (`revenue`) 
    - `date`
    - `zip`
    - `revenue`
2. V předcházejícím dotazu omezte výsledek na pouze 10 řádků.

### Úkol 2 - WHERE

1. Vyberte všechny prodeje z tabulky `sales`, jejichž zisk (`revenue`) je nejméně _7000$_ a nejvýše _30000$_ (včetně).

2. Vyberte všechny prodeje z tabulky `sales`, jejichž zisk (`revenue`) je alespoň _20000$_ a zároveň počet prodaných kusů (`units`) je více než 30.

3. Vyberte všechny jedinečné státy (`state`) z tabulky `country` kde (`region`) je `Central`.

### [Bonus]

1. Vyberte jedinečné názvy produktů z tabulky `product`, pro které platí následující:
    - produkt je v kategorii (`category`) `Mix`
    - cena produktu (`priceNew`) je nižší než _200$_
    - název produktu (`product`) začíná na písmeno `P` nebo obsahuje písmeno `Q`
    
    Výsledek seřaďte vzestupně.

---
