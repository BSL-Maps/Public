<div align="center">

<img src="assets/logo.png" alt="BSL Maps Logo" width="120" />

# BSL Maps

### 🗺️ Indoor-Navigationssystem für die Staatliche Berufsschule Lauingen

Eine responsive Webanwendung, mit der sich Schüler, Lehrer und Besucher
schnell und zielsicher im Schulgebäude zurechtfinden – inklusive
Raumsuche, Routenplanung und einem Administrationspanel zur Datenpflege.

<br/>

![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)
![Blazor](https://img.shields.io/badge/Blazor_Server-512BD4?logo=blazor&logoColor=white)
![SQL Server](https://img.shields.io/badge/Microsoft_SQL_Server-CC2927?logo=microsoftsqlserver&logoColor=white)
![Dapper](https://img.shields.io/badge/ORM-Dapper-FF6A00)
![Leaflet](https://img.shields.io/badge/Leaflet.js-199900?logo=leaflet&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![JWT](https://img.shields.io/badge/Auth-JWT-000000?logo=jsonwebtokens&logoColor=white)
![Hosting](https://img.shields.io/badge/Hosting-IONOS-003D8F)
![Status](https://img.shields.io/badge/Status-Abgeschlossen-2ea44f)

</div>

---

## 📌 Über das Projekt

**BSL Maps** ist ein IT-Ausbildungsprojekt der Klasse **EIT12A** an der
Staatlichen Berufsschule Lauingen. Ausgangspunkt war ein reales Problem:
Besucher – unter anderem aus internationalen Partnerschulen – sowie neue
Schüler und Vertretungslehrer finden sich im Schulgebäude nur schwer
zurecht und kommen dadurch zu spät zu Terminen.

Unsere Lösung ist eine **über den Browser erreichbare Indoor-Navigation**:
Auf einer interaktiven Karte lassen sich Räume suchen, auswählen und per
Routenplanung miteinander verbinden. Ein separates, nicht öffentlich
indexiertes **Adminpanel** ermöglicht die komfortable Pflege aller
Raum-, Klassen- und Lehrerdaten über eine Oberfläche statt direkt in der
Datenbank.

> 💡 Ursprünglich war eine Handy-App mit NFC-Standorterkennung und
> AR-Navigation geplant. Aus Zeit- und Budgetgründen (Deadline 28.02.2025,
> Budget ≤ 60 €) haben wir uns bewusst für eine schlanke, performante
> **Webanwendung** entschieden.

---

## ✨ Features

| | Feature | Beschreibung |
|---|---|---|
| 🗺️ | **Interaktive Karte** | Gebäudekarte über **drei Stockwerke** mit Zoom, Etagenwechsel und anklickbaren Raum-Markern (Leaflet.js). |
| 🔍 | **Raumsuche** | Suchleiste mit Live-Vorschlägen – der gefundene Raum wird direkt auf der Karte fokussiert und markiert. |
| 🧭 | **Routenplanung** | Start und Ziel eingeben, der optimale Weg wird berechnet und auf der Karte visualisiert. |
| ⚡ | **Schnellauswahl** | Direktzugriff auf wichtige Orte wie Ausgang, Toiletten usw. |
| 🔐 | **Adminpanel** | Verwaltung von Räumen, Klassen und Lehrern mit JWT-Login und rollenbasiertem Zugriff. |
| 📱 | **Responsive & barrierefrei** | Optimiert für Desktop und Smartphone, hohe Ladegeschwindigkeit und gute Zugänglichkeit. |

---

## 🖥️ Einblicke in die Anwendung

<table>
  <tr>
    <td width="60%" valign="top">
      <b>Navigations- / Startseite</b><br/>
      Kartenansicht mit Suchleiste, Rauminfos und Datentabellen.
      <br/><br/>
      <img src="assets/ui-admin-startseite.png" alt="Startseite mit Karte und Suche" />
    </td>
    <td width="40%" valign="top">
      <b>Adminpanel-Login</b><br/>
      Geschützter Zugang über JWT-Authentifizierung.
      <br/><br/>
      <img src="assets/ui-login.png" alt="Login des Adminpanels" />
    </td>
  </tr>
</table>

<sub>Die Abbildungen zeigen die in Adobe XD erstellten UI-Entwürfe, die als Grundlage der Umsetzung dienten.</sub>

**Auffindbar über Suchmaschinen** – die SEO-optimierte Startseite:

<img src="assets/seo-vorschau.png" alt="Google-Suchergebnis-Vorschau von bsl-maps.com" width="620" />

---

## 🏗️ Architektur & Technologie

Die Anwendung besteht aus **drei Komponenten** auf Basis von **.NET 8**:

```
┌─────────────────────┐     ┌─────────────────────┐
│  Adminpanel         │     │  Navigation +       │
│  (Blazor Server)    │     │  Homepage           │
│                     │     │  (Blazor Server)    │
└──────────┬──────────┘     └──────────┬──────────┘
           │                           │
           └───────────┬───────────────┘
                       ▼
          ┌─────────────────────────┐
          │  Backend                │
          │  C#-Klassenbibliothek   │
          │  Services · Repositories│
          │  Dapper (ORM)           │
          └────────────┬────────────┘
                       ▼
          ┌─────────────────────────┐
          │  Microsoft SQL Server   │
          │  (gehostet auf IONOS)   │
          └─────────────────────────┘
```

| Bereich | Technologie |
|---|---|
| **Frontend** | Blazor Server (2 Web-Apps), Razor Components |
| **Karte** | Leaflet.js mit `L.CRS.Simple` (pixelbasierte Gebäudepläne) |
| **Backend** | C#-Klassenbibliothek (Services, Repositories, DTOs) |
| **Datenzugriff** | Dapper (ORM) + `Microsoft.Data.SqlClient` |
| **Datenbank** | Microsoft SQL Server, versioniert per Installations-Skripten |
| **Authentifizierung** | JWT (im Cookie gespeichert), rollenbasierter Zugriff (RBAC) |
| **Hosting / Deployment** | IONOS, Veröffentlichung via FTP-Publish-Profil (Visual Studio) |

### 🗄️ Datenbankmodell

Relationales Schema mit Räumen, Knoten (für die Wegfindung), Klassen,
Lehrern und deren Zuweisungen. Eine `DBVersion`-Tabelle ermöglicht
versionierte Datenbank-Updates.

<img src="assets/datenbankmodell.png" alt="Logisches Datenbankmodell" width="820" />

### 👥 Anwendungsfälle

<img src="assets/use-case.png" alt="Use-Case-Diagramm für Administrations- und Benutzeroberfläche" width="620" />

---

## 🧩 Technisches Highlight – Karteninitialisierung

Die Karte nutzt Bilder der einzelnen Stockwerke als Overlays und ein
einfaches Pixel-Koordinatensystem statt Geo-Koordinaten. Die Raumdaten
werden aus dem C#-Backend als JSON an die JavaScript-Funktion übergeben:

<img src="assets/code-leaflet.png" alt="Leaflet-Karteninitialisierung mit Stockwerk-Overlays" width="640" />

---

## 📊 Qualität & Performance

Getestet mit **Google PageSpeed Insights** – mit Fokus auf Ladezeit,
Barrierefreiheit und SEO:

<table>
  <tr>
    <td align="center"><b>Homepage</b><br/><img src="assets/pagespeed-homepage.png" alt="PageSpeed Homepage" /></td>
  </tr>
  <tr>
    <td align="center"><b>Kartenansicht</b><br/><img src="assets/pagespeed-karte.png" alt="PageSpeed Karte" /></td>
  </tr>
  <tr>
    <td align="center"><b>Adminseite</b><br/><img src="assets/pagespeed-adminseite.png" alt="PageSpeed Adminseite" /></td>
  </tr>
</table>

**Weitere Teststufen:**

- ✅ **Unit-Tests** – eigener C#-`TestClient` (Konsolenanwendung) zum
  isolierten Testen der Backend-Klassenbibliothek.
- ✅ **Integrationstests** – End-to-End-Tests mit **Cypress**
  (Navigation, Suche, Routenberechnung, Adminfunktionen, Fehlerszenarien).
- ✅ **Performance & Barrierefreiheit** – Bild-/Skript-Optimierung,
  Caching, Farbkontraste, Tastaturnavigation und Screenreader-Kompatibilität.

---

## 🛠️ Eingesetzte Werkzeuge

| Kategorie | Tools |
|---|---|
| **Entwicklung** | Visual Studio 2022, Visual Studio Code |
| **Datenbank** | SQL Server Management Studio, DBeaver, SQLite (lokal) |
| **Design** | Adobe XD (Mockups), Photoshop (Kartenmaterial) |
| **Diagramme** | Lucidchart (DB-Modell), Umletino (UML) |
| **Organisation** | Redmine (Projektmanagement), GitHub (Versionskontrolle) |

---

## 📁 Projektstruktur

```
.
├── README.md                     – dieses Dokument
├── SECURITY.md                   – Sicherheitsrichtlinie & Meldeverfahren
├── assets/                       – Bilder & Diagramme für die Doku
└── Files/
    ├── Dokumentation.docx        – ausführliche Projektdokumentation
    └── Präsentation.pptx         – Projektpräsentation
```

> 📄 Die vollständige **Projektdokumentation** (Anforderungen, Entwurf,
> Implementierung, Tests) findest du unter
> [`Files/Dokumentation.docx`](Files/Dokumentation.docx),
> die Präsentation unter
> [`Files/Präsentation.pptx`](Files/Präsentation.pptx).

---

## 👨‍💻 Team

Entwickelt im Rahmen der Ausbildung (Klasse **EIT12A**) an der
Staatlichen Berufsschule Lauingen:

| | Entwickler | GitHub |
|---|---|---|
| 👨🏾‍💻 | **Paul Bischoff** | [@PaulPaulus123](https://github.com/PaulPaulus123) |
| 👨🏻‍💻 | **David Kramer** | [@thatdavid0451](https://github.com/thatdavid0451) |
| 👨🏽‍💻 | **Marc Rettinger** | [@Marc12341](https://github.com/Marc12341) |

**Zeitraum:** November 2024 – Februar 2025 · **Deployment:** IONOS (`bsl-maps.com`)

---

## 🔐 Sicherheit

Sicherheitslücken bitte vertraulich melden – Details und Meldeverfahren
findest du in der [`SECURITY.md`](SECURITY.md).

---

<div align="center">
<sub>Ein Schulprojekt der Staatlichen Berufsschule Lauingen · EIT12A · 2025</sub>
</div>
