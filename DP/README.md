# Diplomová práca
## Automatizácia spracovania ionosférických dát pomocou hlbokého učenia

Študijný program: Hospodárska informatika  
Študijný odbor: Informatika  
Školiace pracovisko: Ústav umelej inteligencie (ÚUI)  
Školiteľ: doc. Ing. Peter Butka, PhD.  
Konzultanti: Ing. Viera Krešňáková, PhD.; RNDr. Šimon Mackovjak, PhD.  
Doménoví experti: RNDr. Jaroslav Chum, Ph.D.; Mgr. Jan Rusz, Ph.D.  
Vypracoval: Bc. Marek Zboray

### Abstrakt 
Táto diplomová práca sa zaoberá automatizovaným spracovaním ionosférických dát pomocou hlbokého učenia, pričom hlavným cieľom je rekonštrukcia priebehu dopplerovského signálu počas výskytu spread‑F javov a následná detekcia týchto udalostí. Práca opisuje celý postup spracovania, od prípravy obrazových vstupov a tvorby segmentačných masiek až po implementáciu segmentačného modelu určeného na identifikáciu oblastí ovplyvnených spread‑F. Na základe predikovaných masiek sa dopĺňa narušený priebeh signálu a extrahujú sa parametre potrebné na určenie výskytu jednotlivých udalostí. Výsledky potvrdzujú, že navrhnutý prístup dokáže rekonštruovať chýbajúce signálové štruktúry a umožňuje spoľahlivú automatizovanú detekciu spread‑F javov.

### Návod na použitie
Je potrebné mať nainštalované prostredie, ktoré podporuje súbory typu .ipynb. Kedže ide o súbory typu Jupyter Notebook, jednotlive bloky predstavujú čiastkovú funkcionalitu celého kódu. Jednotlivé časti kódu (bloky) sú priamo popísané v každom súbore

### Štruktúra repozitára
Repozitár je rozdelený podľa jednotlivých etáp spracovania dát a tréningu modelov. Každý priečinok alebo notebook predstavuje samostatnú časť pipeline, ktorá bola použitá v diplomovej práci.

#### Priečinok DeepLabV3
Tento priečinok obsahuje implementáciu segmentačného modelu DeepLabV3. Jednotlivé notebooky obsahuju tréningové skripty.
Obsah priečinka:
- 10_11_0DeepLabV3.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, bez dilatacie masiek, predtrénované váhy weights=imagenet, zložitejšia augmentácia)
- 10_11_2DeepLabV3.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, s dilatáciou masiek - kernel_size = 2,  predtrénované váhy weights=imagenet, zložitejšia augmentácia)
- 10_11_3DeepLabV3.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, s dilatáciou masiek - kernel_size = 3,  predtrénované váhy weights=imagenet, zložitejšia augmentácia)
- 10_12DeepLabV3.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, s dilatáciou masiek - kernel_size = 3, opätovné pretréno-
vanie modelu 10_11_3DeepLabV3, weights=None, zložitejšia augmentácia)
- 10_13DeepLabV3.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, s dilatáciou masiek - kernel_size = 3, náhodná inicializácia
weights=None, zložitejšia augmentácia)
- 9DeepLabV3.ipynb (model trénovaný na časti dát - zásielky 9/13, s dilatáciou masiek - kernel_size = 3,  predtrénované váhy weights=imagenet, jemná augmentácia)
- 8DeepLabV3.ipynb (model trénovaný na časti dát - zásielky 9/13, s dilatáciou masiek - kernel_size = 3,  predtrénované váhy weights=imagenet, jemná augmentácia)
- 7DeepLabV3.ipynb (model trénovaný na časti dát - zásielky 7/13, s dilatáciou masiek - kernel_size = 3,  predtrénované váhy weights=imagenet, zložitejšia augmentácia)
- 6DeepLabV3.ipynb (model trénovaný na časti dát - zásielky 7/13, s dilatáciou masiek - kernel_size = 3,  predtrénované váhy weights=imagenet, jemná augmentácia)

#### Priečinok Pix2pix
Priečinok obsahuje implementáciu modelu Pix2pix, ktorý bol použitý ako alternatívna segmentačná architektúra pre porovnanie s DeepLabV3.
Obsah priečinka:
- pix2pix_all_data.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, bez dilatacie masiek)

#### Priečinok U-net
Priečinok obsahuje implementáciu modelu U‑Net, ktorý bol použitý ako alternatívna segmentačná architektúra pre porovnanie s DeepLabV3.
Obsah priečinka:
- 3U-net.ipynb (model trénovaný na časti dát - zásielky 10/13, bez dilatacie masiek)
- 4U-net.ipynb (model trénovaný na všetkých dátach - zásielky 13/13, bez dilatacie masiek)

#### 1_Algorithmic_mask_creation.ipynb
Prvý krok pipeline. Notebook obsahuje:
- algoritmickú tvorbu segmentačných masiek zo spektrogramov,
- detekciu štruktúr spread‑F pomocou prahovania a morfologických operácií,
- generovanie ground‑truth masiek pre trénovanie modelov.

#### 2_Algorithmic_mask_creation.ipynb
Druhá verzia algoritmickej tvorby masiek:
- vylepšené prahovanie,
- robustnejšie morfologické operácie,
- automaticka detekcia jednotlivých frekvencií(v 1_Algorithmic_mask_creation.ipynb len pôvodne staticke delenie spektrogramu na 3 časti)

#### Cropping_spectrograms.ipynb
Notebook určený na:
- načítanie pôvodných spektrogramov po jednotlivých zásielkach,
- ich orezanie na relevantné časovo‑frekvenčné oblasti.

#### Dashboard_PredictAnalysis.ipynb
Notebook slúži na:
- načítanie spektrogramov a prislušných .mat súborov,
- predikcia masiek, zvoleným modelom,
- extrakciu parametrov potrebných pre detekciu spread‑F udalostí,
- vizualizáciu výsledkov v prehľadnom dashboarde.

#### Release
Z dôvodu veľkosti súborov nie sú natrénované modely uložené priamo v repozitári. Všetky finálne verzie modelov použitých v diplomovej práci sú dostupné v sekcii Releases:
- natrénované modely DeepLabV3 (všetky verzie uvedené v priečinku DeepLabV3),
- natrénované modely U‑Net (všetky verzie z priečinka U-net),
- natrénovaný model pix2pix na všetkých dátach,
- video‑tutoriál, ktorý ukazuje, ako pracovať s notebookom Dashboard_PredictAnalysis.ipynb.  

Tieto materiály umožňujú používateľovi okamžite pracovať s modelmi bez potreby opätovného trénovania modelov.

#### Dáta
Dáta použité v diplomovej práci sú dostupné na školskom datalabe v rámci Ústavu umelej inteligencie. Nachádzajú sa v jednotlivých zásielkach. Surové dáta na ceste: **data/lightning/MarekZboray/DP/data/RawData**, predspracované spektrogramy na ceste **data/lightning/MarekZboray/DP/data/CropPictures** a ručne vytvorené masky na ceste **data/lightning/MarekZboray/DP/data/RucneMasky**.
  
#### README.md
Tento súbor obsahuje popis diplomovej práce, návod na použitie a štruktúru repozitára.



