# Smartfox manual Recharge Boiler
Boiler Heating Element Control (manual recharge), a simple HA automation solution to manually recharge the Smartfox boiler element.

The Smartfox control is annoying with its opaque documentation and unreliable functionality. Since I never want to be in a situation again where there's no hot water for showering, I built an automation in HA that ensures you can have hot showers every day. Especially during the dark lull (winter)...

**Version:** 1.1.0
**Date:** 2026-11-24

This automation supplements PV surplus heating within a weekly schedule, up to the configured amount of energy per heating day.

### Features

- **Time control:** Via a Home Assistant schedule. 
- **Dynamic kWh top-up:** Every 5 minutes, a newly calculated target power, rounded to whole percent (1–100 %).
- **Minimum temperature:** Independent of the schedule and kWh target, heats at 50 % when the temperature drops below the minimum, until minimum temperature + 3 K is reached. A value of 0 disables this feature.
- **Priority:** Minimum temperature takes precedence over kWh top-up. 
- **Operating mode:** Manual during top-up, then back to PV automatic mode.

### Installation

You can add the blueprint in HA via *Settings → Automations & Scenes → Blueprints → Import* Blueprint using this URL. 
  
You also can use the 'Import Blueprint' button below:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fatillakati%2FSmartfox-Manual-Recharge-Boiler%2Fblob%2Fmain%2Fsmartfox_boiler_dynamische_nachladung.yaml)

### Notes

You will need an existing modbus connection to the SmartFox controller.
```yaml
# modbus tcp connection to Smartfox controller
modbus:
 - type: tcp
   name: "smartfox_modbus"
   host: <your smartfox IP>
   port: 502

   switches:
    - name: smartfox_verbrauchsregler_mode
      unique_id: smartfox_verbrauchsregler_mode
      address: 42560
      write_type: holdings
      command_on: 2
      command_off: 0
      verify:
        input_type: holding
        state_on: 2
        state_off: [0,1]
```

A second input_boolean helper is required for the 3 K hysteresis. The device's own temperature limit always takes precedence. If the minimum temperature is enabled and the temperature sensor is invalid, any active manual top-up is stopped. A device-side safety/fallback mechanism is recommended in case of a Home Assistant or Modbus outage.

### Changelog

- **1.1.0:** Optional minimum temperature with 3 K hysteresis, additional temperature sensor and state helper.
- **1.0.0:** Schedule, dynamic kWh top-up, Modbus control.