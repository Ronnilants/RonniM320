# Wetter-Warn-System

## Beschreibung
Eine Konsolen-Applikation, die aktuelle Wetterdaten für eine Stadt abruft und Benutzer über kritische Wetterbedingungen informiert.

## Funktionen
- Abruf aktueller Wetterdaten von OpenWeatherMap API
- Konfigurierbare Warn-Schwellwerte (Temperatur, Windgeschwindigkeit)
- Automatische Benachrichtigungen bei kritischen Bedingungen
- Delegation Pattern für flexible Benachrichtigungs-Handler
- Robuste Input-Validierung mit Custom Exceptions

## Architektur

### Schichten-Trennung
```
┌─────────────────────────────────────┐
│  Main (Applikations-Start)          │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  UserInterface (Input/Output)       │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  WeatherWarningService (Logik)      │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  WeatherApiService (API-Calls)      │
└─────────────────────────────────────┘
```

### Delegation
- **WarningHandler Interface**: Definiert Vertrag für Benachrichtigungen
- **ConsoleWarningHandler**: Konkrete Implementation für Konsolen-Ausgabe
- **WeatherWarningService**: Delegiert Warnungen an registrierte Handler

### Exception Handling
- **InvalidCityException**: Bei ungültigen Stadt-Namen
- **InvalidThresholdException**: Bei ungültigen Schwellwerten
- **WeatherApiException**: Bei API-Fehlern

## Verwendete Technologien
- Java 17+
- OpenWeatherMap API
- JSON Parsing (org.json)
- Delegation Pattern (Observer-ähnlich)

## Setup
1. API-Key von [OpenWeatherMap](https://openweathermap.org/api) holen
2. In `WeatherApiService.java` den Key eintragen
3. JSON-Bibliothek hinzufügen (Maven/Gradle)

## Verwendung
```bash
javac -cp ".:json.jar" *.java
java -cp ".:json.jar" Main
```

Beispiel-Session:
```
Stadt eingeben: Zürich
Temperatur-Schwellwert (°C): 0
Wind-Schwellwert (km/h): 50

=== Wetter in Zürich ===
Temperatur: -2.5°C
Wind: 35 km/h
Bedingung: Leichter Schnee

⚠️ WARNUNG: Temperatur unter 0°C!
```

## Lernziele-Abdeckung
✅ Eigene Beschreibung (dieses Dokument)
✅ Delegation (WarningHandler Interface)
✅ Input-Validierung mit Custom Exceptions
✅ Saubere Trennung (UI → Service → API)
