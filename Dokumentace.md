# Načtení dat
Nahrál jsem soubory/faktové tabulky: 
- kzt6p.csv
- sldb2021_vek10_pohlavi.csv

Nahrál jsem soubory/dimenzní tabulky: 
- cisob.csv
- kzcoco.csv
- kzciskr.csv
- kzrkl.csv

Využil jsem pro to definování parametru `Data_složka` abych nemusel u každé tabulky měnit a absolutní cestu.

# Úprava tabulky sčítání obyvatelstva
- kopie originálu
- přejmenování sloupců (uzemi_kod -> Území kód, vek_txt -> Věková skupina, uzemi_text -> Území text, hodnota -> Počet obyvatel)
- Odstranění zbytečných sloupců
- Přeuspořádání sloupců
- Odstranění prázdných řádek ze sloupce Věková skupina
- Group By: Sum sloupce Počet obyvatel nový sloupec Počet věk (zanechány zbylé sloupce)
- Odstranění textu ze sloupce Věková skupina pomocí rozdělení sloupce podle čísel na dva a smazání druhé sloupce s textem
- Vytvoření nového sloupce s věkovými skupinami (0-17, 18-29, 30-59, 60+)
- Pivot Column -> Věková skupina (Don´t agregate) podle Počet obyvatel
- Vytvoření sloupce počet obyvatel 


# Úprava tabulky Výsledky voleb
- kopie originálu
- Odstranění zbytečných sloupců zůstaly (OKRES, OBEC, KSTRANA, POC_HLASU)
- přejmenování sloupců (OKRES -> Okres, OBEC -> Obec, KSTRANA -> ID Strany, POC_HLASU -> Počet Hlasů)
- GroupBy: Sum sloupce Počet hlasů nový sloupec Počet hlasů (zanechány zbylé sloupce)


# Spojení tabulek
- spojení tabulek sčítání obyvatelstva a výsledků voleb přes sloupec Obec kód a Území kód a vytvoření nové tabulky výsledky `voleb + sčítání obyvatelstva`
- úprava skupin obvytel podle věku spojení skupin obyvatel do skupin 20 - 39, 40 - 59, 60 a více (Není důvod dělit na voliče podle 10 let)

# Úprava tabulky Záznamy stran
- kopie originálu
- Odstranění zbytečných sloupců zůstaly (KSTRANA, NAZEVCELK, ZKRATKAK8)
- přejmenování sloupců (KSTRANA -> ID Strany, NAZEVCELK -> Název strany, ZKRATKAK8 -> Zkratka strany)
- Odstranění duplicit: záznamy pro každý kraj chceme unikátní seznam

# Vytvoření tabulky Geografie
- Vznik pomocí merge ({číselník obcí, městských částí, městských obvodů a volebních okrsků}, číselník krajů, číselník ORP, číselník okresů)
- Odstranění zbytečných sloupců (CPOU, KRZAST, MINOKRSEK1, MAXOKRSEK1, OBEC_PREZ)
- přejmenování sloupců 
  - KRAJ -> Kraj
  - číselník kraje.NAZEVKRZ -> Název kraje
  - OKRES -> Okres
  - číselník okresů.NAZEVNUTS -> Název okres
  - ORP -> ORP
  - číselník ORP.text -> Název ORP
  - OBEC -> Obec
  - NAZEVOBCE -> Název obce