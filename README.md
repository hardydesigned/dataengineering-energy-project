# Data-Science Industrie Projekt

[English version](#Overview)

# Überblick

Hier wird ein Fallbeispiel eines Business Intelligence und Data Science
Projektes vorgestellt, für eine Firma die Gegenstände des täglichen Bedarfs
produziert. Das Ziel des Projektes ist es die vorhandenen Daten des Unternehmens
zu analysieren und auf Basis der vorhandenen Daten Vorhersagen zu erstellen. Die
Daten kommen aus dem firmensinternen ERP- und MES-System.

## Vorüberlegungen

Das Ziel des Projekt ist es, mehrere Dashboards für Finanz-, und
Produktionsdaten zu erstellen.

Im Bereich Finanzen sollen aktuelle wichtige Kennzahlen (ua. Umsatz, Gewinn,
Deckungsbetrag) visualisiert werden, und die Kunden segmentiert. Die Produktion
soll in Echtzeit überwacht werden und zukünftige Störungen vorhergesagt.

Die Daten kommen zum Einen aus dem ERP System und beinhalten die Verkaufs und
Kundendaten. Zum Anderen liefert das installierte EMS, Daten über den
Energieverbrauch, den Nutzungsgrad, die aktuelle Auslastung, den Störungstypen
und die Auslastung.

Die hier benutzten Daten kommen von:

### Sales Daten:

-   https://archive.ics.uci.edu/dataset/352/online+retail

Hier wurden die Steuern (19%) hinzugefügt, die variablen Produktionskosten
(5-15%) und die Produktkategorie. Zudem wurden die Kunden segmentiert und in
einer neuen Datenbank gespeichert.

Später interessante Analysen für den Kunden sind:

### Finanzen

Ebenen:

-   Gesamtes Unternehmen
-   Standort
    -   Land
-   Kunden
    -   Kundensegment
-   Produkte
    -   Produktgruppen
    -   Einzelne Produkte
-   Zeitliche Ebene
    -   Jahr, Monat, Woche, Tag

Finanzkennzahlen:

-   Umsatz
-   Gewinn
-   Bruttogewinn und Bruttogewinnmarge
-   EBIT (Earnings Before Interest and Taxes): Gewinn vor Zinsen und Steuern.
-   Deckungsbeitrag (Umsatz abzüglich variabler Kosten)

### Energie Daten

-   https://archive.ics.uci.edu/dataset/851/steel+industry+energy+consumption

Hier wurden die Produktkategorien hinzugefügt und eine Störung falls der
Energieverbrauch sehr niedrig ist (Leerlauf).

Später interessante Analysen für den Kunden sind:

Ebenen:

-   Gesamtes Unternehmen
-   Standort
    -   Land
-   Produkte
    -   Produktgruppen
-   Zeitliche Ebene

    -   Jahr, Monat, Woche, Tag

-   Produktionszahlen
    -   Durchsatz
    -   Produktionsauslastung
    -   Maschinenverfügbarkeit
    -   Stillstandzeiten
    -   Störungsursachen und Häufigkeit

# Benutzte Technologien

Die Daten werden mit Python in einem ETL Prozess geladen, transformiert und
gespeichert. Dazu werden sie bereinigt, standardisiert und Ausreißer werden
behoben. Dann folgt eine Datenanalyse um Potentiale zu erkennen und wichtige
Faktoren zu definieren.

Die transformierten Daten werden dann per Power BI geladen und in
übersichtlichen Dashboards dargestellt. Hierbei werden zusätzliche Kennzahlen
wie bsp. der Deckungsbeitrag berechnet. Das fertige Dashboard ist weiter unten
zu sehen.

Dann werden die Kunden mithilfe des k-Means Algorithmus segmentiert. Dies
erfolgt anhand der Metriken: Warenkorbert, Letzter Kauf und Kauffrequenz. Zudem
werden dann weitere Informationen über den Kunden gewonnen mittels einer
Standort und Kategorieanalyse. Die herausgestellten Segmente werden ebenfalls im
Dashboard visualisiert und für weitere Analysen genutzt.

Zuletzt wird die Art einer Störung bei bestimmten Maschineneinstellungen mit dem
XGBoost Klassifizierer ermittelt. Hierbei erreicht der Algorithmus eine
Genauigkeit von beeindruckenden 89%. Die so ermittelten Prognosen werden im
Dashboard dargestellt und sind über Filter interaktiv analysierbar.

# Dashboard

Das Dashboard, erstellt mit Power BI:

![Overview](assets/overview.png)

![Report pdf](assets/power_bi_analysis.pdf)

# Kosten

Nach einer aktuellen Analyse würde dieses Projekt monatlich ca. 110€ Kosten. Die
Kosten bestehen aus:

-   Hosting der ETL Pipeline (30€)
-   Compute Ressourcen ML Algorithmen (50€)
-   Daten speichern (20€)
-   Daten visualisieren (10€ / Nutzer)

Die Entwicklungszeit betrug: 50h

# Overview

This document presents a case study of a Business Intelligence and Data Science
project for a company producing everyday consumer goods. The goal of the project
is to analyze the company's existing data and make predictions based on it. The
data comes from the company's internal ERP and MES systems.

## Preliminary Considerations

The project's objective is to create multiple dashboards for financial and
production data.

### Financial Dashboards:

-   Visualize key financial metrics (e.g., revenue, profit, contribution margin)
-   Segment customers

### Production Dashboards:

-   Monitor production processes in real-time
-   Predict potential disruptions

The data is sourced from the ERP system, which provides sales and customer data,
and the MES system, which supplies data on energy consumption, utilization
rates, current load, fault types, and machine downtimes.

### Data Sources:

#### Sales Data:

-   [Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)

For the project, additional data was generated, such as:

-   Taxes (19%)
-   Variable production costs (5-15%)
-   Product categories

Customer segmentation was also performed and stored in a new database.

#### Energy Data:

-   [Steel Industry Energy Consumption Dataset](https://archive.ics.uci.edu/dataset/851/steel+industry+energy+consumption)

Product categories were added, and machine disruptions were labeled when energy
consumption was exceptionally low (indicating idle states).

---

## Analytical Scope

### Financial Data

Analysis Dimensions:

-   **Company-wide**
-   **By location**:
    -   Country
-   **By customer**:
    -   Customer segment
-   **By product**:
    -   Product groups
    -   Individual products
-   **By time**:
    -   Year, month, week, day

Key Metrics:

-   Revenue
-   Profit
-   Gross profit and gross profit margin
-   EBIT (Earnings Before Interest and Taxes)
-   Contribution margin (revenue minus variable costs)

---

### Energy Data

Analysis Dimensions:

-   **Company-wide**
-   **By location**:
    -   Country
-   **By product**:
    -   Product groups
-   **By time**:
    -   Year, month, week, day

Key Metrics:

-   Throughput
-   Production utilization
-   Machine availability
-   Downtime
-   Causes and frequency of disruptions

---

## Technologies Used

The data is processed using Python in an ETL pipeline, where it is cleaned,
standardized, and outliers are addressed. After transformation, the data
undergoes analysis to identify potential improvements and key factors.

The processed data is loaded into Power BI, where it is visualized in
user-friendly dashboards. Additional metrics, such as contribution margins, are
calculated and displayed in the dashboards.

Customer segmentation is performed using the k-Means algorithm, based on metrics
such as basket size, last purchase, and purchase frequency. Additional insights,
such as location and category analyses, are derived. These segments are also
visualized in the dashboards for further analysis.

Machine disruptions are classified using the XGBoost classifier. The algorithm
achieves an impressive accuracy of 89%, predicting the type of disruption for
given machine settings. These predictions are integrated into the dashboard and
are interactively analyzable through filters.

---

## Dashboard

The dashboard created using Power BI:

![Overview](assets/overview.png)

[![Power BI Analysis PDF](assets/power_bi_analysis.pdf)](assets/power_bi_analysis.pdf)

---

## Costs

A current analysis estimates that this project would cost approximately **€110
per month**. The costs include:

-   Hosting the ETL pipeline: €30
-   Compute resources for machine learning algorithms: €50
-   Data storage: €20
-   Data visualization: €10/user

Development time: **50 hours**
