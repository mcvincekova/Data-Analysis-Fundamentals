# Lekce 3: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - VIEWs

1. Vytvořte pohled (`VIEW`) s názvem `CentralSalesView` obsahující sloupce:
    * productid, 
    * zip, 
    * units, 
    * revenue, 
    * state
    * region

    Data budou získána ze spojení tabulek `sales` a `country` podle sloupce `Zip`, přičemž vyberte pouze záznamy kde hodnota sloupce `region` je `Central`.


**Řešení**
> SQL dotaz:
>```sql
>CREATE VIEW SalesCountryView AS
>SELECT
>   productid,
>   s.zip,
>   units,
>   revenue,
>   state,
>   region
>FROM
>   sales s INNER JOIN country c ON s.Zip = c.Zip
>WHERE
>   region = 'Central'
>```
>

    
2. Použijte pohled `CentralSalesView` na vyřešení následujících úkolů:

    * Zjistěte počet unikátních produktů prodaných v každém státě z centrálního regionu.
    * Vybere maximální hodnotu sloupce `units` pro záznamy, kde hodnota sloupce (stát) `state` začíná na písmeno `I`.

**Řešení**

> Postupně vykonáme následující příkazy:
>
>
> Počet unikátních produktů prodaných v každém státě:
> SQL dotaz:
>```sql
>SELECT 
>   COUNT(DISTINCT productid),
>   state
>FROM 
>   SalesCountryView
>GROUP BY
>   state
>```
>
> Maximální hodnota sloupce `units`:
>```sql
>SELECT 
>   MAX(units)
>FROM 
>   SalesCountryView
>WHERE 
>   state LIKE 'I%'
>```
>


3. Následující CTE získá informace o celkových výnosech a počtech prodaných kusů pro každý produkt:

    ```sql
    WITH SalesByProduct AS
    (
        SELECT
            p.productId,
            SUM(s.Revenue) AS TotalRevenue,
            SUM(s.Units) AS TotalUnits
        FROM
            product p LEFT JOIN sales s ON p.ProductID = s.ProductID
        GROUP BY
            p.ProductID
    )
    ```

    Použijte daný tabulkový výraz a:

    * Zjistěte, kolik produktů nevygenerovalo žádný (`NULL`) výnos (produkty se neprodaly nebo nemáme informace).
    * Vyberte všechny záznamy, kde nám chybí (je `NULL`) informace o výnosu, ale máme informace o prodaných kusech.

**Řešení**

> Postupně vykonáme následující příkazy:
>
>
> Kolik produktů nevygenerovalo žádný výnos:
>```sql
>WITH SalesByProduct AS
>(
>   SELECT
>       p.productId,
>       SUM(s.Revenue) AS TotalRevenue,
>       SUM(s.Units) AS TotalUnits
>   FROM
>       product p LEFT JOIN sales s ON p.ProductID = s.ProductID
>   GROUP BY
>       p.ProductID
>)
>
>SELECT 
>   COUNT(productid)
>FROM 
>   SalesByProduct
>WHERE 
>   TotalRevenue IS NULL
>```
>
>
> Záznamy, kde nám chybí (je `NULL`) informace o výnosu, ale máme informace o prodaných kusech:
>```sql
>WITH SalesByProduct AS
>(
>   SELECT
>       p.productId,
>       SUM(s.Revenue) AS TotalRevenue,
>       SUM(s.Units) AS TotalUnits
>   FROM
>       product p LEFT JOIN sales s ON p.ProductID = s.ProductID
>   GROUP BY
>       p.ProductID
>)
>
>SELECT
>   *
>FROM 
>   SalesByProduct
>WHERE 
>   TotalRevenue IS NULL
>   AND TotalUnits IS NOT NULL


---
## Samostatná práce 2
---

### Úkol 1 - Řetězce 

1. Vyberte všechny unikátní regiony z tabulky country, názvy regionů zobrazte velkými písmeny

**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   DISTINCT UPPER(region)
>FROM 
>   country
>```
>

2. Vyberte všechny jedinečné okresy (`district`) z tabulky `country` a k nim jejich orientační číslo - orientační číslo je v názvu okresu za znakem `#`. Seřaďte výsledek podle orientačního čísla vzestupně.

**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   DISTINCT district,
>   SUBSTR(district, INSTR(district, '#') + 1) AS orientNumber
>FROM 
>   country
>ORDER BY 
>   orientNumber
>```
>

### Úkol 2 - CASE

1. Vyberte všechny prodeje z tabulky `sales` a přiřaďte jim kategorii velikosti balíku (`packageSize`) podle počtu prodaných kusů následovně:
    * `LARGE` – pokud prodej zahrnoval 15 kusů nebo více
    * `MEDIUM` – pokud podaný počet kusů byl mezi 14 a 5 (včetně)
    * `SMALL` – pokud prodej zahrnoval méně než 5 kusů.

**Řešení**
> SQL dotaz:
>```sql
>SELECT 
>   *,
>   CASE
>       WHEN units >= 15 THEN 'LARGE'
>       WHEN units >= 5 THEN 'MEDIUM'
>       ELSE 'SMALL'
>   END AS packageSize
>FROM 
>   sales
>```
>

### [Bonus]

1. Předchozí příklad vyřešte pomocí jednoduchého i hledaného CASE příkazu.

**Řešení**
> > Hledaný CASE příkaz:
>```sql
>SELECT 
>   *,
>   CASE
>       WHEN units >= 15 THEN 'LARGE'
>       WHEN units >= 5 THEN 'MEDIUM'
>       ELSE 'SMALL'
>   END AS packageSize
>FROM 
>   sales
>```
>
>
> Hledaný CASE příkaz:
>```sql
>SELECT 
>*,
>   CASE units
>       WHEN 1 THEN 'SMALL'
>       WHEN 2 THEN 'SMALL'
>       WHEN 3 THEN 'SMALL'
>       WHEN 4 THEN 'SMALL'
>       WHEN 5 THEN 'MEDIUM'
>       WHEN 6 THEN 'MEDIUM'
>       WHEN 7 THEN 'MEDIUM'
>       WHEN 8 THEN 'MEDIUM'
>       WHEN 9 THEN 'MEDIUM'
>       WHEN 10 THEN 'MEDIUM'
>       WHEN 11 THEN 'MEDIUM'
>       WHEN 12 THEN 'MEDIUM'
>       WHEN 13 THEN 'MEDIUM'
>       WHEN 14 THEN 'MEDIUM'
>       ELSE 'LARGE'
>   END AS packageSize
>FROM 
>   sales
>```
>

2. Prodeje spolu s kategorií velikosti balíků (z příkladu 2.1) si uložte jako nový VIEW s názvem dle vlastního výběru. Za pomoci tohoto VIEW zjistěte:

    * Kolik velkých (`LARGE`), středně velkých (`MEDIUM`) a malých (`SMALL`) balíků bylo odesláno (prodáno).
    * Celkový a průměrný výnos pro každou kategorii velikosti balíku.
    * Kolik malých balení (`SMALL`) bylo celkově odesláno v roce `2014` a kolik v roce `2013`.

**Řešení**
> Nový VIEW:
>```sql
>CREATE VIEW SalesPackageSize AS
>SELECT 
>   *,
>   CASE
>       WHEN units >= 15 THEN 'LARGE'
>       WHEN units >= 5 THEN 'MEDIUM'
>       ELSE 'SMALL'
>   END AS packageSize
>FROM 
>   sales
>```
>
> Kolik velkých (`LARGE`), středně velkých (`MEDIUM`) a malých (`SMALL`) balíků bylo odesláno (prodáno):
>
>```sql
>SELECT
>   COUNT(*),
>   packageSize
>FROM 
>   SalesPackageSizeView
>GROUP BY
>   packageSize
>```
>
> Celkem bylo odesláno: `98` velkých, `1150` středně velkých a `1006454` malých balíků.
>
>
> Celkový a průměrný výnos pro každou kategorii velikosti balíku:
>
>```sql
>SELECT
>   AVG(revenue),
>   SUM(revenue),
>   packageSize
>FROM 
>   SalesPackageSizeView
>GROUP BY
>   packageSize
>```
>
> Kolik malých balení (`SMALL`) bylo celkově odesláno v roce `2014` a kolik v roce `2013`:
>
>```sql
>SELECT
>   COUNT(packageSize),
>   strftime('%Y', date) AS saleYear
>FROM 
>   PackageSizeSearched
>WHERE
>   packageSize = 'SMALL'
>GROUP BY 
>   saleYear
>HAVING
>   saleYear in ('2013', '2014')
>```
>
> V roce `2014` bylo celkově odesláno `411687` malých balení, v roce `2013` to bylo `379875`.
>