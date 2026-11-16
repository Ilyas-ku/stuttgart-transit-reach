# Stuttgart transit reach — reliability-adjusted isochrones from any point

Interactive map: **https://ilyas-ku.github.io/stuttgart-transit-reach/**

Pick any point in the Stuttgart region and a departure time between 05:00 and 23:00:
the page shows where public transport takes you within 20–60 minutes, door to door,
and how far that reach shrinks once real delays and cancellations are counted.

- **Timetable:** GTFS (DELFI via gtfs.de), weekday (Tuesday 20 Oct 2026, a day without rail-replacement buses), in hourly
  chunks that the browser loads on demand.
- **Delays:** my own collector of the operators' GTFS-Realtime feed, weekday observations
  since 24 Sep 2026, per stop, line and hour (median, 80th, 90th, 95th percentile,
  cancellation rate).
- **Routing:** a forward Connection Scan runs in the browser on every change;
  walking 4.8 km/h on a 1.3× detour, ≥2 min per transfer.
- **Commute cost:** home ● and work ◆; a reverse Connection Scan (latest departure that still
  arrives by the chosen time) in the morning and a forward one 9 h later, timetable vs. the
  chosen reliability level, averaged over arrivals ±30 min, times the commute days a year.
- **Population:** Zensus 2022, 100 m grid.

Same method as the Rhein-Main and Munich maps: https://ilyas-ku.github.io/rhein-main-transit-reach/ ,
https://ilyas-ku.github.io/munich-transit-reach/

`pipeline/`: `CITY=Stuttgart DAY=20261020 VER=a1da8ddd1195 export_inputs.py 3 28` and `CITY=Stuttgart export_delays.py 0 24`
run against the collector's DuckDB, `CITY=Stuttgart build_explore.py` packs `meta.json` and `c/HH.json`.

Data: DELFI / gtfs.de (CC BY-SA 4.0), Zensus 2022 (dl-de/by-2-0),
© OpenStreetMap contributors, geocoding Nominatim, basemap © Esri.
