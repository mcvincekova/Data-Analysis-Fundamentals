# Lekce 3: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - Inner Join

1. Napište dotaz SQL, který vybere všechny sloupce z tabulek produkt (`product`) a výrobce (`manufacturer`) a spojí je podle sloupce `ManufacturerID`. Výsledky seřaďte sestupně podle sloupce `productID` a omezte výstup na prvních 50 řádků.
    
    _"Skutečné zadání":_
    _Zjistěte úplné informace o produktu a výrobci pro 50 nejnovějších produktů (čím vyšší ID produktu, tím novější produkt)._

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   *
>FROM
>   product JOIN manufacturer ON product.ManufacturerID = manufacturer.ManufacturerID
>ORDER BY
>   productid DESC
>LIMIT
>   50
>```
>

2. Vybere sloupce `productid`, `date`, `zip`, `units`, `revenue` a `region` z tabulek `sales` a `country`, které jsou spojeny podle sloupce `zip`. Zobrazte pouze prodej s nejvyšším výnosem (`revenue`).
    
    _"Skutečné zadání":_
    _Jak vypadají úplné informace o nejvýnosnějším prodeji včetně dat o tom, v kterém regionu se prodej uskutečnil?_

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   productid,
>   date,
>   sales.zip,
>   units,
>   revenue,
>   region
>FROM
>   sales JOIN country ON sales.zip = country.zip
>ORDER BY
>   revenue DESC
>LIMIT
>   1
>```
>

### Úkol 2 - Inner Join & Aggregace

1. Určete dotaz SQL, který spočítá celkový výnos pro každý stát z tabulek `sales` a `country`, které jsou spojeny podle sloupce `zip`. Výsledky seřaďte sestupně podle celkového výnosu (`revenue`).

    _"Skutečné zadání":_
    _Ve kterých státech jsme vydělali nejvíce?_

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   State,
>   SUM(Revenue)
>FROM
>   Sales s JOIN Country c ON s.Zip = c.Zip
>GROUP BY
>   State
>ORDER BY
>   SUM(Revenue) DESC
>```
>

### [Bonus]

1. Který výrobce (zjistěte jméno) vyrábí nejvíce různých výrobků?

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>SELECT
>   COUNT(productid) as pocetProduktu,
>   manufacturer
>FROM
>   product JOIN manufacturer ON product.ManufacturerID = manufacturer.ManufacturerID
>ORDER BY
>   pocetProduktu DESC
>LIMIT
>   1
>```
>
> `Abbas` vyrábí nejvíce různých výrobků - 2412.

2. Ve kterých státech se za rok 2015 celkově prodalo alespoň 10000 kusů produktů?

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   COUNT(units) AS totalUnits,
>   state
>FROM
>   sales JOIN country ON sales.Zip = country.Zip
>   WHERE
>   strftime('%Y', date) = '2015'
>GROUP BY
>   state
>HAVING
>   totalUnits >= 10000
>ORDER BY
>   totalUnits DESC
>```
>

---
## Samostatná práce 2
---

### Úkol 1 - Left Join & Agregace

1. Určete dotaz SQL, který spočítá celkový výnos pro každý produkt z tabulek `product` a `sales`, které jsou spojeny podle sloupce `productID`. Zobrazte také produkty, které se neprodaly.

    _"Skutečné zadání":_
    _Jaký je celkový výnos z prodeje za jednotlivé produkty.?_

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   p.ProductID,
>   SUM(revenue)
>FROM 
>   Product p LEFT JOIN sales s ON s.ProductID = p.ProductID
>GROUP BY
>   p.ProductID
>```
>

2. Vyberte všechny ID a názvy produktů z tabulky `product`, kde prodej tohoto produktu není zaznamenán v tabulce `sales`.

    _"Skutečné zadání":_
    _Které produkty se vůbec neprodaly?_

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   p.ProductId,
>   product
>FROM 
>   Product p LEFT JOIN sales s ON s.ProductID = p.ProductID
>WHERE 
>   s.productid IS NULL
>```
>

3. Zjistete počet produktů z tabulky `product`, kde prodej produktu není zaznamenán v tabulce `sales`.

    _"Skutečné zadání":_
    _Kolik produktů se nikdy neprodalo?_

**Řešení**
> SQL dotaz:
>```sql
>SELECT
>   COUNT(DISTINCT p.ProductId)
>FROM
>   Product p LEFT JOIN sales s ON s.ProductID = p.ProductID
>WHERE 
>    s.productid IS NULL;
>```
>

### [Bonus]

Následující dotaz počítá celkový výnos z prodeje za jednotlivé měsíce v roce 2015. Zkuste dotaz spustit ve variantách s LEFT a INNER join. Jaký je rozdíl ve výsledcích? 

```sql
SELECT 
    MonthName,
    Sum(revenue) AS totalRevenue    
FROM 
    -- varianda LEFT join
    date d LEFT JOIN sales s ON s.Date = d.Date
    -- varianta INNER join
    -- date d INNER JOIN sales s ON s.Date = d.Date
WHERE 
    d.Year = '2015'
GROUP BY 
    d.MonthName
ORDER BY 
    d.MonthNo
```

**Řešení**
> Varianta s `LEFT JOIN` ve výsledcích zobrazí i měsíce, za které neevidujeme žádné prodeje (žádný výnos) v tabulce `sales`, zatímco varianta s `INNER JOIN` vybere pouze měsíce, které obsahují korespondující data o prodejích v tabulce `sales`.
