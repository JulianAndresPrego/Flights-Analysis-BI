#✈️ Air Traffic Analytics — Power BI
<img src="img/flight.jpg" width="800" />

### <img src="img/us.svg" width="24" /> English

This Power BI report analyzes airline traffic using an Origin–Destination fact table enriched with airports, airlines and aircraft metadata.
It includes KPIs, route-level aggregation, and interactive maps (Icon Map/Azure Maps) to visualize passenger flows.

🔍 What’s inside

- Data prep (Power Query):
  - Built a clean Airports dimension from OpenFlights.
  - Fixed Latitude/Longitude with en-US parsing and range checks (±90/±180).
  - Added AirportOverrides to map generic city/country names (e.g., London, Argentina) to a chosen IATA (e.g., LHR, EZE).
  - Created Routes aggregated table (Origin–Destination) with Passengers, Flights, and lat/lon for both ends.
- Model (Star-Schema):
  - Fact: Airline Flight Datasets (flights/passengers)
  - Dimensions: Airports_Final, AirportOverridesCode, (optional) Airlines, Aircraft
  - Helper table: Routes (O→D aggregated with coordinates)
- Key DAX measures:
  - Total Passengers, Total Flights, Direct Flights, % Direct Flights
  - Avg. Passengers per Flight, Passengers by Airline
  - Total Passengers by Destination, Avg. Passengers/Flight by Aircraft
  - Busiest Routes (Top N by passengers)
  - Optional: Distance (km) using Haversine on route coordinates
- Report pages:
  - KPI Overview, Airlines & Aircraft, Flow Map (O→D), Airports of the World, Route Drill-through, Data Quality / Overrides.

✨ Highlights

- Robust coordinate pipeline: culture-safe parsing + range validation.
- No Bing key required: Icon Map/Azure Maps for flow lines.
- Overrides let you govern ambiguous labels (city/country) → single IATA per case.
- Top routes and densest corridors at a glance with tooltips (passengers, flights, distance).

📈 How to use

1. Open the .pbix in the latest Power BI Desktop.
2. If you add new Origins/Destinations that are cities/countries, update AirportOverridesCode with the IATA you want (e.g., New York → JFK).
3. Use slicers (Airline, Aircraft Type, Origin, Destination, Direct Flights) and drill-through from summary to route details.
4. For the flow map, use Icon Map (Start/End Lat/Lon from Routes) or Azure Maps.

<span id="head4"><img src="img/i_Start.png" width="25" /> Example DAX (illustrative)</span>

```bash
-- Core KPIs
Total Passengers =
SUM('Airline Flight Datasets'[No_of_Passengers])

Total Flights =
COUNTROWS('Airline Flight Datasets')

Direct Flights =
CALCULATE(
    [Total Flights],
    'Airline Flight Datasets'[Direct_Flights] = "Yes"
)

% Direct Flights =
DIVIDE([Direct Flights], [Total Flights])

Avg. Passengers per Flight =
DIVIDE([Total Passengers], [Total Flights])
```

### <img src="img/it.svg" width="24" /> Italiano

Questo report Power BI analizza il traffico aereo partendo da una tabella Fatti Origine–Destinazione, arricchita con metadati di aeroporti, compagnie e aeromobili.
Include KPI, aggregazioni per rotta e mappe interattive (Icon Map/Azure Maps) per visualizzare i flussi di passeggeri.

🔍 Contenuti

- Preparazione dati (Power Query):
  - Creazione della dimensione Airports da OpenFlights.
  - Correzione Latitude/Longitude con parsing en-US e controlli di range.
  - Tabella AirportOverrides per mappare etichette generiche (città/paese) su un IATA scelto.
  - Tabella Routes aggregata (O→D) con passeggeri, voli e coordinate.
- Modello (Schema a Stella):
  - Fatto: Airline Flight Datasets
  - Dimensioni: Airports_Final, AirportOverridesCode, (opz.) Airlines, Aircraft
- Supporto: Routes (O→D con coordinate)

- Misure DAX chiave:
    - Totale passeggeri, Totale voli, Voli diretti, % Voli diretti, Media passeggeri/volo, Passeggeri per compagnia, Passeggeri per destinazione, Media passeggeri/volo per aeromobile, Rotte più trafficate, Distanza (km).

- Pagine report:
  - KPI Overview, Compagnie & Aeromobili, Mappa flussi (O→D), Airports of the World, Drill-through rotte, Qualità dati/Overrides.

✨ Evidenze

- Pipeline coordinate robusta; nessuna Bing key (Icon Map); governance tramite overrides per etichette ambigue; ranking rotte/top corridoi con tooltip.

📈 Come usarlo

- Apri il .pbix (Power BI Desktop aggiornato).
- Aggiungi/aggiorna gli overrides nella tabella AirportOverridesCode (es.: New York → JFK).
- Slicer per compagnia, aeromobile, origine/destinazione; drill-through sulle rotte.
- Per la mappa flussi usa Icon Map o Azure Maps.

<span id="head4"><img src="img/i_Start.png" width="25" /> Esempio DAX (dimostrativo)</span>
(stesse misure della sezione in inglese, adattare alle colonne del modello)
