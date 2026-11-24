# Smartfox manual Recharge Boiler
Boiler Heating Element Control (manual recharge), a simple HA automation solution to manually recharge the Smartfox boiler element.

**Version:** 1.1.0
**Date:** 2026-11-24

This automation supplements PV surplus heating within a weekly schedule, up to the configured amount of energy per heating day.

### Features

- **Time control:** Via a Home Assistant schedule. 
- **Dynamic kWh top-up:** Every 5 minutes, a newly calculated target power, rounded to whole percent (1–100 %).
- **Minimum temperature:** Independent of the schedule and kWh target, heats at 50 % when the temperature drops below the minimum, until minimum temperature + 3 K is reached. A value of 0 disables this feature.
- **Priority:** Minimum temperature takes precedence over kWh top-up. 
- **Operating mode:** Manual during top-up, then back to PV automatic mode.

### Notes

A second input_boolean helper is required for the 3 K hysteresis. The device's own temperature limit always takes precedence. If the minimum temperature is enabled and the temperature sensor is invalid, any active manual top-up is stopped. A device-side safety/fallback mechanism is recommended in case of a Home Assistant or Modbus outage.

### Changelog

- **1.1.0:** Optional minimum temperature with 3 K hysteresis, additional temperature sensor and state helper.
- **1.0.0:** Schedule, dynamic kWh top-up, Modbus control.