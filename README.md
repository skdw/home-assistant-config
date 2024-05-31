# home-assistant-config

![Check config](https://github.com/skdw/home-assistant-config/actions/workflows/ci.yml/badge.svg)

My [Home Assistant](http://home-assistant.io) configuration. The system is running live on Raspberry Pi 4 with Home Assistant OS.

Dashboards are optimized for desktop browser, mobile app and wall panel display.

## Integrations

- [Matter](https://www.home-assistant.io/integrations/matter)
  - Zigbee lights (IKEA, Philips) via Dirigera Hub
- [HomeKit Device](https://www.home-assistant.io/integrations/homekit_controller)
  - IKEA Dirigera
    - Temperature, humidity sensors
    - Motion sensors sensors
    - Door sensors
    - Water leakage sensors
  - [Aqara FP2](https://www.aqara.com/eu/product/presence-sensor-fp2/) presence sensor
- [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
  - Wall light switches
  - Remote light switches, audio knobs
  - `[TODO]` Curtains
  - `[TODO]` Energy monitoring
- [SmartThings](https://www.home-assistant.io/integrations/smartthings/) - home appliances
  - Air conditioner
  - Oven
  - Cooktop
- [Onkyo](https://www.home-assistant.io/integrations/onkyo/) - Pioneer home cinema (5.1 + Zone 2 + Zone 3)
- [Spotify](https://www.home-assistant.io/integrations/spotify/)
- [Android TV](https://www.home-assistant.io/integrations/androidtv/)
- [System Bridge](https://www.home-assistant.io/integrations/system_bridge/) - Windows PC
- [IPP](https://www.home-assistant.io/integrations/ipp/) - Printer
- [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) - HASS entities accessible in HomeKit
- [OpenAI Conversation](https://www.home-assistant.io/integrations/openai_conversation/)
- [Strava](https://github.com/craibo/ha_strava) - exercises tracking
- [GIOŚ](https://www.home-assistant.io/integrations/gios/) - air quality index
- [RESTful sensor](https://www.home-assistant.io/integrations/sensor.rest/) - Warsaw public transport live tracking
- [InfluxDB](https://www.home-assistant.io/integrations/influxdb/) - history logging
- [Cloudflared](https://github.com/brenner-tobias/addon-cloudflared) - DNS tunnel for remote access
- [ESPHome](https://www.home-assistant.io/integrations/esphome/) - PWM-controlled fans `[TODO]`
