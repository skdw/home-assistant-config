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
  - [Aqara FP2](https://www.aqara.com/eu/product/presence-sensor-fp2/)
    - Human presence sensor
    - Light level sensor
- [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
  - Wall light switches
  - Remote light switches, audio knobs
  - `[TODO]` Curtains
  - `[TODO]` Energy monitoring
- [SmartThings](https://www.home-assistant.io/integrations/smartthings/) - home appliances
  - Air conditioner
  - Oven
  - Cooktop
- [ESPHome](https://www.home-assistant.io/integrations/esphome/)
  - PWM-controlled fans
  - MAX7219 matrix display
- [Onkyo](https://www.home-assistant.io/integrations/onkyo/) - Pioneer home cinema (5.1 + Zone 2 + Zone 3)
- [Spotify](https://www.home-assistant.io/integrations/spotify/)
- [Android TV](https://www.home-assistant.io/integrations/androidtv/)
- [System Bridge](https://www.home-assistant.io/integrations/system_bridge/) - Windows PC
- [IPP](https://www.home-assistant.io/integrations/ipp/) - Printer
- [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) - HASS entities accessible in HomeKit
- [OpenAI Conversation](https://www.home-assistant.io/integrations/openai_conversation/)
- [Strava](https://github.com/craibo/ha_strava) - exercises tracking
- [Electricity Maps](https://www.home-assistant.io/integrations/co2signal/) - CO2 intensity of home energy
- [GIOŚ](https://www.home-assistant.io/integrations/gios/) - air quality index
- [RESTful sensor](https://www.home-assistant.io/integrations/sensor.rest/) - Warsaw public transport live tracking
- [InfluxDB](https://www.home-assistant.io/integrations/influxdb/) - history logging
- [Cloudflared](https://github.com/brenner-tobias/addon-cloudflared) - DNS tunnel for remote access

## Setup

### Overwrite core integrations
Perform `home-assistant core` repo sparse checkout (instead of full submodule init)
```
cd repos

# History of commits is too long for cloning
# git clone --no-checkout git@github.com:skdw/home-assistant-core.git
# remote: Total 1006214 (delta 115), reused 215 (delta 64), pack-reused 1005899 (from 1)
# Receiving objects: 100% (1006214/1006214), 642.25 MiB | 18.14 MiB/s, done.

# Clone only the latest commit
git clone --no-checkout --depth=1 git@github.com:skdw/home-assistant-core.git
remote: Total 21317 (delta 4059), reused 8738 (delta 2323), pack-reused 0 (from 0)
Receiving objects: 100% (21317/21317), 21.64 MiB | 1.30 MiB/s, done.

# Sparse checkout
cd home-assistant-core/
git sparse-checkout init --cone
git sparse-checkout set homeassistant/components/onkyo
git checkout skynet

# Validate sparse checkout
home-assistant-core git:(skynet) find -type f | wc -l
85
```
