Program: Hospodárska informatika

Vypracoval: Marek Zboray

Bakalárska práca: : Využitie vysvetliteľných techník modelov hlbokého učenia v oblasti spracovania geofyzikálnych dát

Vedúci bakalárskej práce: doc. Ing. Peter Butka, PhD.

Konzultanti: Ing. Viera Krešňáková, PhD., Ing. Lenka Kališková 

Pre prácu s modelom a vysvetliteľnosťou modelu je potrebné na začiatku nainštalovať potrebné balíky. Je potrebné mať nainštalované prostredie, ktoré podporuje súbory typu .ipynb. Kedže ide o súbory typu Jupyter Notebook, jednotlive bloky predstavujú čiastkovú funkcionalitu celého kódu. Pre fungovanie vizualizacie (dashbordu) je potrebné načitať knižnice, načítať dáta, spracovať dáta pomocou TimeSeriesGenerator, natrénovať alebo načítať model, spustiť funkciu pre dashboard a spustiť samotný dashboard. Jednotlivé časti kódu (bloky) sú priamo popísané v každom súbore. 

Popis štruktúry programu:

Súbor: data_priprava.ipynb
- súbor obsahuje prípravu dát a ich uloženie do csv súboru omni_full_plus_indexes.csv

Súbor: final_train_test.ipynb
- súbor obsahuje prípravu finálnych train a test csv súborov a ich uloženie do súborov train_omni.csv a test_omni.csv

Súbor: 6_1_model_XAI.ipynb
- súbor obsahuje trénovanie modelu na základe DST indexu 6 h dozadu, predikcia súčasnej hodnoty
- súčasťou tohto súboru je samostatne uložený model a predikcie modelu: model_6_1.hdf5, predikcie_6_1.csv
- v súbore sa zároveň nachádza časť venovaná XAI, čo zahrňuje definiciu peturbačnej metódy, vizualizaciu v podobe dashbordu a samotnú analýzu aplikovanej perturbačnej metódy
- súčasťou tohto súboru sú priečinky: grafy_prvotna_analyza_6_1, analyza_perturb_test_6_1_lok_minimum_2004_2022 a analyza_perturb_test_6_1_lok_minimum_2004_2022_priemerna_lok_hodnota

Súbor: 6_2_model_XAI.ipynb
- súbor obsahuje trénovanie modelu na základe DST indexu 2h dopredu 6h dozadu
- súčasťou tohto súboru je samostatne uložený model a predikcie modelu: model_6_2.hdf5, predikcie_6_2.csv
- v súbore sa zároveň nachádza časť venovaná XAI, čo zahrňuje definiciu peturbačnej metódy a samotnú analýzu aplikovanej perturbačnej metódy
- súčasťou tohto súboru sú priečinky: grafy_prvotna_analyza_6_2, analyza_perturb_test_6_2_lok_minimum_2004_2022 a analyza_perturb_test_6_2_lok_minimum_2004_2022_priemerna_lok_hodnota

Súbor: 6_6_model_XAI.ipynb
- súbor obsahuje trénovanie modelu na základe DST indexu 6h dopredu 6h dozadu
- súčasťou tohto súboru je samostatne uložený model a predikcie modelu: model_6_6.hdf5, predikcie_6_6.csv
- v súbore sa zároveň nachádza časť venovaná XAI, čo zahrňuje definiciu peturbačnej metódy a samotnú analýzu aplikovanej perturbačnej metódy
- súčasťou tohto súboru sú priečinky: grafy_prvotna_analyza_6_6, analyza_perturb_test_6_6_lok_minimum_2004_2022 a analyza_perturb_test_6_6_lok_minimum_2004_2022_priemerna_lok_hodnota

Dáta: omni_full.csv
- stiahnutie OMNI dat: https://github.com/Marek929Z/BP-MarekZboray/releases/download/v1.0/omni_full.csv

Dáta: train_omni.csv
- stiahnutie train OMNI dat: https://github.com/Marek929Z/BP-MarekZboray/releases/download/v1.1/train_omni.csv

Dáta: test_omni.csv
- stiahnutie test OMNI dat: https://github.com/Marek929Z/BP-MarekZboray/releases/download/v1.2/test_omni.csv

