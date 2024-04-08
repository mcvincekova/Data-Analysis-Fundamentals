# SQL

---
## Data
---

V tomto kurzu budeme pracovat s databází, která obsahuje data o prodeji různých produktů.
Data obsahují následující entity (tabulky): 
* `Product` - _Produkt_
* `Sales` - _Prodeje_
* `Date` - _Datum_
* `Manufacturer` - _Výrobce_
* `Country` - _Země_

Vztahy mezi těmito entitami zachycuje následující datový model:

![Data Model](/Resources/Images/SQL/dataModel.png)

---
## Příprava Databáze
---

Pro práci s daty budeme využívat online databázový editor SQLite Online.

**Jak na to**

1. Otevřete [SQLite Online](https://sqliteonline.com/) ve svém oblíbeném webovém prohlížeči.
2. Stáhněte si datový soubor - [database.db](/Resources/Data/database.db) _(pamatujte si, kam jste soubor uložili)_.
![DB Download](/Resources/Images/SQL/dbDownload.png)
3. Nahrajte datový soubor do SQLite Online pomocí `File -> Open DB`.
![Sqlite DB load](/Resources/Images/SQL/loadData.png)
4. To, že všechno proběhlo správně, poznáte podle toho, že vaše databáze `database.db` bude dostupná v levém bočním menu.
![Sqlite DB location](/Resources/Images/SQL/dataLoaded.png)

