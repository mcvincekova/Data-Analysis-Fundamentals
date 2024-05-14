## Ukol 1

1. Který výrobci nabízejí produkty pokrývající širokou škálu tržních segmentů (působí nejméně v 6 segmentech)?

    "Technické zadání":
    Vyberte výrobce (`manufacturer`), kteří nabízejí produkty (`product`) v alespoň 6 různých segmentech trhu.


**Možné Řešení**

```sql
SELECT
    m.Manufacturer,
    COUNT(DISTINCT Segment)
FROM
   	Product p JOIN Manufacturer m ON p.ManufacturerID = m.ManufacturerID
GROUP BY
     m.Manufacturer
HAVING 
	COUNT(DISTINCT Segment) >= 6
ORDER BY
    COUNT(DISTINCT Segment) DESC
```

```txt
"Pomum"     "8"
"Natura"    "8"
"Currus"    "8"
"Aliqui"    "8"
"Abbas"     "8"
"Pirum"     "7"
"Victoria"  "6"
"VanArsdel" "6"
"Fama"      "6"
```

2. Který produkt měl nejvyšší počet prodaných kusů během prosince 2014?

    _Napište SQL dotaz, který spočítá celkový počet prodaných kusů každého produktu v za prosinec 2014. Zobrazte pouze produkt s nejvyšším počtem prodaných kusů za toto období._

**Možné Řešení**

```sql
SELECT
    p.ProductID,
    p.Product,
    SUM(s.Units) AS UnitsSold
FROM
    Sales s 
    JOIN Product p ON p.ProductID = s.ProductID
    JOIN Date d ON d.date = s.date
WHERE
    d.Year = 2014 AND d.MonthNo = 12
GROUP BY
    p.ProductID
ORDER BY
    SUM(s.Units) DESC
LIMIT 1
```

```txt
"792"   "Natura RP-80"  "1964"
```


3. Zjistěte, kolik produktů bylo prodáno v každém městě na západě USA, kde název města začíná slovem `West`. Jména měst zobrazte bez přípony `', USA'`. Zahrňte i města, kde nebylo nic prodáno.

    _Napište SQL dotaz, který spočítá celkový počet prodaných produktů v každém městě na západě USA (region je `West`), kde název města začíná slovem `West`. Použijte tabulky `country` a `sales` a zahrňte i města, kde nebylo nic prodáno. Jména měst ve výsledku zobrazte bez přípony `', USA'` a výsledek seřaďte podle počtu prodaných produktů vzestupně._

**Možné Řešení**

```sql
SELECT 
    REPLACE(c.city, ', USA', ''),
    COUNT(s.productid) pocet_produktu
 FROM 
 	country c	LEFT JOIN sales s ON s.ZIP = c.ZIP
 WHERE 
 	c.Region = 'West'
    AND c.City LIKE 'West%'
 GROUP BY 
 	c.city
 ORDER BY 
 	pocet_produktu
```

```txt
"West Glenn County, CA"     "0"
"West Pima County, AZ"      "0"
"West Tehama County, CA"    "0"
"Westfall, OR"              "0"
"West Glacier, MT"          "1"
"Westfir, OR"               "2"
"Westley, CA"               "2"
"Westmorland, CA"           "2"
"Westlake, OR"              "3"
"Westport, CA"              "3"
"Weston, OR"                "5"
"Westport, WA"              "5"
"West Wendover, NV"         "7"
"Weston, ID"                "7"
"West Point, CA"            "8"
"West Yellowstone, MT"      "16"
"Westwood, CA"              "18"
"West Hills, CA"            "85"
"West Hollywood, CA"        "89"
"Westlake Village, CA"      "93"
"West Richland, WA"         "96"
"West Sacramento, CA"       "116"
"West Linn, OR"             "148"
"Westminster, CA"           "218"
"West Covina, CA"           "252"
"West Jordan, UT"           "358"
```

4. V roce 2015 vstoupil do platnosti změněný daňový zákon. Přidejte ke každému prodeji z tohoto roku informaci o tom, jaká daň musí být odvedena na základě výše výnosu, kde:
* vysokou 'HIGH' daň odvádíme z výnosu nad 5000$, 
* nízkou 'LOW' z výnosu nad 1000$ (ale do 5000$), 
* a žádnou 'NONE' z prodejů s výnosem pod 1000$. 

Zjistěte celkový výnos z prodejů pro každou daňovou kategorii.


```sql
WITH taxes2015 AS
(
SELECT 
    *,
    CASE 
    	WHEN revenue > 5000 THEN 'HIGH_TAX'
        WHEN revenue > 1000 THEN 'LOW_TAX'
        ELSE 'NO_TAX'
    END AS tax_info
FROM 
	sales
WHERE
	strftime('%Y', date) = '2015'
)

SELECT
	SUM(revenue),
    SUM(units),
    tax_info
FROM
	taxes2015 JOIN country ON taxes2015.zip = country.zip 
WHERE
	state = 'TX'
GROUP BY
	tax_info
```

```txt
"18613.77"      "21"        "HIGH_TAX"
"2357669.895"   "1913"      "LOW_TAX"
"6855937.3575"  "13197"     "NO_TAX"
```

