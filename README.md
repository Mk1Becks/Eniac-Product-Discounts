# Eniac: Produktrabatte analysieren

Teamprojekt im Rahmen der Data-Science-Weiterbildung an der WBS Coding School.
Wir sind das **Eniac Data Analytics Team „Pandas 67"** und haben untersucht, wie stark der Online-Shop Eniac (Apple-Zubehör und Technik) seine Produkte rabattiert und ob sich das je nach Produktart unterscheidet.

**Tools:** Python, pandas, seaborn, Google Colab

---

## Die Fragestellung

- Wie stark werden Produkte bei Eniac rabattiert?
- Unterscheidet sich das nach Produktkategorie und Preisniveau?
- Was bedeutet das für die Rabattstrategie?

## Die Daten

Ausgewertet wurden **53.231 Bestellpositionen** (Januar 2017 bis März 2018) aus vier Tabellen: Orders, Orderlines, Products und Brands.
Der Rabatt wurde pro Position berechnet: Listenpreis (`price`) gegen tatsächlich bezahlten Preis (`unit_price`). Als „reduziert" gilt eine Position ab mehr als 1 % Rabatt.

Die Rohdaten liegen nicht in diesem Repo. Das Notebook lädt sie direkt in Google Colab.

---

### Datenaufbereitung

Vor der Analyse mussten die Daten sauber gemacht werden:

- Orders, Orderlines, Products und Brands wurden über Bestellnummer und `sku` zusammengeführt (`merge`).
- Die Preisspalten waren als Text gespeichert, mit falsch gesetzten Punkten (zum Beispiel `1.367.11` statt `1367.11`). Ich habe das Muster erkannt und die Werte repariert, statt die Zeilen zu löschen.
- Datumsspalten wurden in `datetime` umgewandelt, Duplikate und fehlende Werte geprüft.

## Mein Teil: Kategorien und Preisverteilung

Die Produkte hatten keine Kategorie. Ich habe sie deshalb über Stichwörter im Produktnamen in **10 Kategorien** eingeteilt (zum Beispiel Hüllen & Taschen, Speicher, Monitore, Audio). Alles, was nicht passt, landet in „Sonstiges".

### Verkaufte Positionen je Kategorie

![Verkaufte Positionen je Kategorie](images/kategorien_anzahl.png)

Hüllen & Taschen (ca. 10.100), Laden & Kabel (ca. 9.200) und Speicher (ca. 8.500) machen zusammen über die Hälfte aller Positionen aus.

### Preisverteilung je Kategorie

![Mittlerer Preis je Kategorie](images/preis_median_kategorie.png)

Die Preise unterscheiden sich stark: Laden & Kabel liegt im Median bei ca. 40 €, Apple Geräte bei ca. 640 €. Je teurer die Kategorie, desto breiter die Preisspanne.

### Grenzen der Analyse

- Die Einteilung läuft über Stichwörter und ist deshalb nicht perfekt. Etwa 12 % der Positionen sind „Sonstiges".
- Der Boxplot im Notebook blendet extreme Ausreißer aus, sonst wäre er nicht lesbar.
- „Apple Geräte" enthält nur Originalgeräte (iPhone, iPad, MacBook usw.). Zubehör steckt in den anderen Kategorien.

---

## Ergebnisse des Teams

Aus der gemeinsamen Präsentation:

- Die Rabatte liegen im Schnitt bei **18,6 %** (Median 17,5 %).
- Höhere Rabatte gingen mit **höherem Umsatz** einher, nicht mit niedrigerem.
- Der durchschnittliche Bestellwert ist im Beobachtungszeitraum um **15 % gestiegen**, nicht gefallen.
- **Black Friday** (24.11.2017) ist der stärkste Einzeltag. Neun Tage im November machen 14 % des Jahresumsatzes aus.

### Empfehlung

1. **Teure Produkte stärker in den Fokus nehmen.** Produkte über 300 € machen nur 14 % der Verkäufe aus, bringen aber fast die Hälfte des Umsatzes.
2. **Rabatte gezielt statt überall einsetzen.** Fast alles wird mit Rabatt verkauft. Das ist riskant, weil Kunden sich an niedrige Preise gewöhnen.
3. **Die Datenerfassung verbessern.** Einkaufspreis, Normalpreis und Aktionspreis sollten pro Produkt gespeichert werden, damit sich berechnen lässt, ob sich ein Rabatt wirklich lohnt.

---

## Repo-Struktur

```
Eniac-Product-Discounts/
├── notebooks/
│   └── eniac_kategorien_preise.ipynb   # Daten zusammenführen, Kategorien, Charts
├── presentation/
│   └── Eniac_Produktrabatte_Praesentation.pptx
├── images/                             # Charts für dieses README
└── README.md
```

## So lässt sich das Notebook ausführen

1. Notebook in Google Colab öffnen.
2. Zellen von oben nach unten ausführen. Die Daten werden beim ersten Schritt geladen, daraus entsteht `df.csv`.

## Team

Taris, Florian und Matias
