# Smartfox manual Recharge Boiler
Boiler Heating Element Control (manual recharge), a simple HA automation solution to manually recharge the Smartfox boiler element.

**Version:** 1.1.0

**Last change:** 22.11.2026

## Dynamische, zeitgesteuerte Boiler-Nachladung

Die Automation ergänzt die PV-Überschussheizung innerhalb eines Wochenzeitplans bis zur konfigurierten Energiemenge pro Heiztag.

### Funktionen
- **Zeitsteuerung:** Über einen Home-Assistant-Zeitplan.
- **Dynamische kWh-Nachladung:** Alle 5 Minuten eine neu berechnete, auf ganze Prozent gerundete Soll-Leistung (1–100 %).
- **Mindesttemperatur:** Unabhängig von Zeitplan und kWh-Ziel bei Unterschreitung mit 50 % heizen, bis Mindesttemperatur + 3 K erreicht ist. Wert 0 deaktiviert diese Funktion.
- **Priorität:** Mindesttemperatur vor kWh-Nachladung.
- **Betriebsart:** Manuell beim Nachladen, anschließend PV-Automatik.

### Hinweise

Für die 3-K-Hysterese ist ein zweiter input_boolean-Helfer nötig. Die geräteseitige Temperaturbegrenzung hat immer Vorrang. Bei aktivierter Mindesttemperatur und ungültigem Temperatursensor wird eine manuelle Nachladung beendet. Nach einem Home-Assistant- oder Modbus-Ausfall ist eine geräteseitige Sicherheits-/Rückfallsicherung empfehlenswert.

### Änderungsverlauf

- **1.1.0:** Optionale Mindesttemperatur mit 3-K-Hysterese, zusätzlicher Temperaturfühler und Zustandshelfer.
- **1.0.0:** Zeitplan, dynamische kWh-Nachladung, Modbus-Ansteuerung.