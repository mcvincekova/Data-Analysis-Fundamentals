# Lekce 3: Samostatná práce

## Samostatná práce 1
---

### Úkol 1 - VIEWs & CTEs

1. Vytvořte pohled (`VIEW`) s názvem `CentralSalesView` obsahující sloupce:
    * productid, 
    * zip, 
    * units, 
    * revenue, 
    * state
    * region

    Data budou získána ze spojení tabulek `sales` a `country` podle sloupce `Zip`, přičemž vyberte pouze záznamy kde hodnota sloupce `region` je `Central`.

    
2. Použijte pohled `CentralSalesView` na vyřešení následujících úkolů:

    * Zjistěte počet unikátních produktů prodaných v každém státě z centrálního regionu.
    * Vybere maximální hodnotu sloupce `units` pro záznamy, kde hodnota sloupce (stát) `state` začíná na písmeno `I`.

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

    * Zjistěte, kolik produktů nevygenerovalo žádný výnos (neprodalo se).
    * Vyberte všechny záznamy, kde nám chybí (je `NULL`) informace o výnosu, ale máme informace o prodaných kusech.


---
## Samostatná práce 2
---

### Úkol 1 - Řetězce 

1. Vyberte všechny unikátní regiony z tabulky country, názvy regionů zobrazte velkými písmeny

2. Vyberte všechny jedinečné okresy (`district`) z tabulky `country` a k nim jejich orientační číslo - orientační číslo je v názvu okresu za znakem `#`.


### Úkol 2 - CASE

1. Vyberte všechny prodeje z tabulky `sales` a přiřaďte jim kategorii velikosti balíku (`packageSize`) podle počtu prodaných kusů následovně:
    * `LARGE` – pokud prodej zahrnoval 15 kusů nebo více
    * `MEDIUM` – pokud podaný počet kusů byl mezi 14 a 5 (včetně)
    * `SMALL` – pokud prodej zahrnoval méně než 5 kusů.


### [Bonus]

1. Předchozí příklad vyřešte pomocí jednoduchého i hledaného CASE příkazu.

2. Prodeje spolu s kategorií velikosti balíků (z příkladu 2.1) si uložte jako nový VIEW s názvem dle vlastního výběru. Za pomoci tohoto VIEW zjistěte:

    * Kolik velkých (`LARGE`), středně velkých (`MEDIUM`) a malých (`SMALL`) balíků bylo odesláno (prodáno).
    * Celkový a průměrný výnos pro každou kategorii velikosti balíku.
    * Kolik malých balení (`SMALL`) bylo celkově odesláno v roce `2014` a kolik v roce `2013`.
