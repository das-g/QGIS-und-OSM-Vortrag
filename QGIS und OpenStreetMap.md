---
type: slide
slideOptions:
  transition: slide
---

# QGIS und OpenStreetMap

---

* OpenStreetMap (OSM)
    * Datenmodell
    * Konzeptionelle Unterschiede
* OSM-Daten beziehen
* OSM-Daten in QGIS importieren / nutzen

---

<!-- .slide: data-background="#cfc" -->

## OpenStreetMap

![OSM logo](https://wiki.openstreetmap.org/w/images/7/79/Public-images-osm_logo.svg)

---

### Name "OpenStreetMap"

* "O", "S" & "M" gross geschrieben
* keine Leerschläge
* kein Plural "-s"

----

### Name "OpenStreetMap"

aber: Nicht nur eine Karte

----

#### OSM: Nicht nur _eine_ Karte

osm.org
osm.ch
tools.geofabrik.de/mc

----

#### OSM: Nicht _nur_ eine Karte

Sondern eine Geodatenbank / ein Geodatensatz

planet.osm.org

---

### OSM-Datenmodell

Im Vergleich zu (Q)GIS & OGC Simple Features

----

#### (Q)GIS-Datenmodell

- Layer (Ebenen)
    - oft thematisch, z.B. "Strassen" oder "Wasserflächen"
- Features (Objekte) in den Layern mit
    - Geometrie
    - Attributen (Eigenschaften)
- Feste Attribut-Menge pro Layer

&rarr; DBMS-Perspektive: Jeder Layer kann als Relation / Tabelle gesehen werden

----

#### "OGC Simple Features"-Geometriemodell

- `Point`
- `LineString`
- `Polygon`
---
- `MultiPoint`
- `MultiLineString`
- `MultiPolygon`

----

### OSM-Datenmodell

* Node
* Way
* Relation
---
* Tag (Schlüssel-Wert-Paare)

----

#### OSM-"Node"

:::warning
:warning: Nicht zu verwechseln mit OSM-"No**t**e"
:::

* (OSM-interne) ID
* WGS84-Koordinate mit `x` & `y` (keine Höhe!)
* Tags

----

#### OSM-"Way"

* (OSM-interne) ID
* Geordnete Liste von Node-Referenzen
* Tags

:::info
:bulb: keine "eigene" Geometrie -- nur via enthaltener Nodes
:::

----

#### OSM-"Relation"

:::danger
:warning: Nicht zu verwechseln mit Mathe-/DB-Konzept "Relation"
:::

* "Members" (mit je 1 "Role")
* Tags

----

#### OSM-"Relation"

* Fasst mehrere OSM-Objekte (Nodes, Ways, Relations) zusammen
* Jedes Teil-Objekt hat in der Relation eine "Rolle"
* Haupt-Verwendungszwecke:
    * "Multipolygone"
    * Gemeinde-, Kantons- und Ländergrenzen
    * benannte oder nummerierte "Routen"
        * Velo, ÖV-Linien
    * Flüsse u.Ä.

----

#### OSM-"Tags"

* Key-Value pairs
  (Schlüssel-Wert-Paare)
* Bestimmen **sowohl** Objekt-Typ **als auch** Eigenschaften

"Freies Schema"

"schemaless schema"

Doku: wiki.osm.org

----

#### Flächen?

----

#### Flächen in OSM

* Geschlossener Way (1. Node == letzter Node)
    * mit Tag `area=yes`
    * oder mit Tag(s), die Fläche implizieren, z.B.
        * `building=house`
        * `natural=water` + `water=lake`
* oder Relation mit `type=multipolygon`
    * notwendig für
        * "echte" Multi-Polygone
        * Flächen mit Löchern

----

### OSM &lrarr; (Q)GIS

(Meta-)Conceptual Mismatch

&rarr; "Übersetzung" notwendig

---

## OSM-Daten beziehen

----

### OSM-eigene Formate

* XML:
    * `.osm`
    * `.osm.xml`
* ProtoBuf:
    * `.osm.pbf`

----

### gängige GIS-Formate

je nach Quelle

----

### Bezugsquellen

----

#### Gesamt-Datensatz (ganze :earth_africa:)

planet.osm.org

(nur OSM-eigene Formate)

----

#### Ganze Länder, ganze Kontinente

download.geofabrik.de

* täglich aktualisiert
* keine Wartezeit, dafür nicht minuten-aktuell

auch ESRI Shapefile (eigenes Schema / Mapping)

----

#### Schweiz

planet.osm.ch

----

#### Benutzerdefinierte Ausschnitte

extract.bbbike.org

osmaxx.hsr.ch

* diverse Formate
* eigenes Schema / Mapping je Service
* Grössen-Beschränkung
* aktuelle Daten, dafür Wartezeit

---

### OSM-Daten in QGIS nutzen

![](https://www.qgis.org/en/_downloads/qgis-logo.svg)

----

Daten oder nur (Basis-)Karte?

----

#### OSM als Basis-Karte

QGIS-Plugins
* QuickMapServices (Raster-Tiles)
* Vector Tiles Reader

----

#### OSM-eigene Formate

* als Vektor-Layer öffnen
* rudimentäre Übersetzung OSM&rarr;GIS

----

#### GIS-Formate

Underschiedliche Schemata / Mappings je nach Anbieter

* semantische Layer
* einige Eigenschaften als Attribute
* Rest evtl. als Column-Store-Attribut

----

#### OSM-Daten direkt in QGIS abrufen

* Plugins
    * QuickOSM (erlaubt Queries)
    * OSMDownloader (bbox)

---

### Weitere Plugins

* OSM place search (Nominatim)
* ORS Tools (openrouteservice.org)
    * Routing
    * Isochronen
    * Matrix-Berechnungen