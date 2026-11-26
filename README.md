# RomeMap

An interactive map that overlays **ancient Rome on modern Rome**. Pan and zoom like any web map, fade between the modern city and the ancient city with two opacity sliders, and click points of interest to learn more.

**Live page:** https://jackacasey.github.io/romemap/

A personal project made for family and friends. It is a single static file (`index.html`) with no build step and no backend.

## Features

- **Modern city layer** — current streets and buildings, with an opacity slider.
- **Ancient Rome layer** — buildings, roads, walls and aqueducts of the ancient city, drawn as footprints on top of the modern map, with its own opacity slider.
- **Year slider** (100 BC – AD 450, default AD 250) — structures appear and disappear according to their recorded start and end dates, so you can see the city as it stood in the mid-to-late Empire.
- **50 points of interest** — colour-coded by type (forums, temples, arenas and theatres, baths, tombs and monuments, walls/roads/infrastructure, early Christian sites), each with a short caption, the Latin name, a photo and a link to Wikipedia.
- **Clickable ancient features** — each mapped ancient structure shows its name, Latin name, dates and a Wikipedia link where one is recorded.
- **Collapsible control panel**, which starts collapsed on phones.

The map covers central Rome within the Aurelian Walls, plus the Vatican area and a few sites just outside the walls along the Appian Way.

## Sources and credits

### Ancient Rome layer — OpenHistoricalMap

The ancient buildings, roads, walls and aqueducts come from **[OpenHistoricalMap](https://www.openhistoricalmap.org/)** (OHM), a community-built, date-aware sibling of OpenStreetMap. Every feature in OHM carries `start_date` and `end_date` tags, which is what drives the year slider. The data is fetched live from OHM's Overpass API (`overpass-api.openhistoricalmap.org`) and cached in the visitor's browser.

- Data: © OpenHistoricalMap contributors, released under **CC0** (public domain dedication).
- The page's names, Latin names, dates and Wikipedia links for ancient structures are taken directly from the OHM tags.
- OHM's own project notes (see the [OpenHistoricalMap Rome project page](https://wiki.openstreetmap.org/wiki/OpenHistoricalMap/Projects/Rome)) aim to reconstruct imperial and pre-imperial Rome from historians' research, using sources such as city maps and lists of ancient monuments. They also warn that sources sometimes disagree on exact locations of buildings and minor roads, and that most buildings have no certain end date because they were dismantled slowly during the Middle Ages.
- **Accuracy note:** this is volunteer-built reconstruction data. Coverage is uneven, and many structures have no end date, so they appear to stand until the end of the slider. Treat the ancient layer as an informed approximation, not an authoritative survey.

### Modern map

- **Street tiles:** Esri *World Street Map* — Tiles © Esri — Esri, HERE, Garmin, OpenStreetMap contributors.
- **Optional "surviving ruins" outline layer:** archaeological sites and ruins from **[OpenStreetMap](https://www.openstreetmap.org/copyright)**, © OpenStreetMap contributors, available under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). Loaded on demand through the public Overpass API.

### Points of interest

- **Captions** are short summaries written for this project.
- **Links and photos:** each point links to its English Wikipedia article. Thumbnails are fetched at runtime from Wikipedia's public REST API and are shown with a link back to the article; each image carries its own licence on Wikipedia / Wikimedia Commons. Wikipedia text is available under CC BY-SA.
- **Coordinates** were cross-checked against the coordinates published on the corresponding Wikipedia articles and OpenStreetMap's Nominatim geocoder. Some pins are approximate (for example the Appian Way and the Aurelian Walls, which are long linear features marked by a single pin).

### Software

- [Leaflet](https://leafletjs.com/) — map library (BSD 2-Clause).
- [osmtogeojson](https://github.com/tyrasd/osmtogeojson) — converts Overpass data to GeoJSON (MIT).

## Running locally

Open `index.html` in a browser, or serve the folder with any static server:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`. An internet connection is needed for the map tiles, the ancient layer and the Wikipedia photos.

## Hosting

Served with GitHub Pages from the `main` branch. The first visit takes a few seconds while the ancient layer downloads from OpenHistoricalMap; later visits use the browser cache.

## Ideas for the future

- Save a snapshot of the OHM data in the repo, so the page loads faster and still works if OHM's server is down.
- Add more points of interest (aqueducts, more of the Vatican area, individual Palatine palaces).
- A swipe or "spyglass" comparison mode.
