# home-assistant-config

![Check config](https://github.com/skdw/home-assistant-config/actions/workflows/ci.yml/badge.svg)

My [Home Assistant](http://home-assistant.io) configuration. The system is running live on Raspberry Pi 4 with Home Assistant OS.

Dashboards are optimized for desktop browser, mobile app and wall panel display.

## Integrations

- [Matter](https://www.home-assistant.io/integrations/matter)
  - IKEA Dirigera Hub
    - Zigbee lights (IKEA, Philips)
    - Temperature, humidity sensors
    - Door sensors
  - Apple Home ([multi fabric](https://www.home-assistant.io/integrations/matter#multi-fabric-join-to-multiple-controllers) provides an independent Dirigera <-> iOS connection)
- [HomeKit Device](https://www.home-assistant.io/integrations/homekit_controller)
  - IKEA Dirigera Hub (not yet fully Matter enabled)
    - Motion sensors
    - Water leakage sensors
  - [Aqara FP2](https://www.aqara.com/eu/product/presence-sensor-fp2/)
    - Human presence sensor
    - Light level sensor
- [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
  - Wall light switches
  - Remote light switches, audio knobs
  - [Aqara C3](https://www.aqara.com/en/product/curtain-controller-c3/) curtains
  - [Bseed](https://www.bseed.com/products/bseed-zigbee-eu-wall-sockets-power-outlets-with-energy-monitoring-kids-protection) Energy monitoring power outlets
- [SmartThings](https://www.home-assistant.io/integrations/smartthings/) - home appliances
  - Air conditioner
  - Oven
  - Cooktop
- [Onkyo](https://www.home-assistant.io/integrations/onkyo/) - Pioneer home cinema (5.1 + Zone 2 + Zone 3)
- [Spotify](https://www.home-assistant.io/integrations/spotify/)
- [Android TV](https://www.home-assistant.io/integrations/androidtv/)
- [System Bridge](https://www.home-assistant.io/integrations/system_bridge/) - Windows PC
- [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) - HASS entities exposed to Apple Home (complements the Matter service)
  - Pioneer home cinema, as Apple media player accessory
  - Curtains
  - Air quality
- [IPP](https://www.home-assistant.io/integrations/ipp/) - Printer
- [OpenAI Conversation](https://www.home-assistant.io/integrations/openai_conversation/)
- [Strava](https://github.com/craibo/ha_strava) - exercises tracking
- [Electricity Maps](https://www.home-assistant.io/integrations/co2signal/) - CO2 intensity of home energy
- [GIOŚ](https://www.home-assistant.io/integrations/gios/) - air quality index
- [RESTful sensor](https://www.home-assistant.io/integrations/sensor.rest/) - Warsaw public transport live tracking
- [InfluxDB](https://www.home-assistant.io/integrations/influxdb/) - history logging
- [Cloudflared](https://github.com/brenner-tobias/addon-cloudflared) - DNS tunnel for remote access
- [ESPHome](https://www.home-assistant.io/integrations/esphome/) - PWM-controlled fans

## Household guide

### Quick actions

Quick actions offer a simple way to execute routines at home. They are displayed as a card with buttons, available in both the full desktop home view and the compact mobile wall panel.

The card is illustrated in the image: ![screenshot_card_scenes](image/screenshot_card_scenes.png)

#### Entering and leaving home

Actions are designed to be triggered manually by the user upon entering or leaving the home as part of their daily routine. The system detects whether the user intends to enter or exit the apartment, consolidating both actions into a single button for convenience.

- **Welcome Home**
  - *Condition: no home switches\* are active (indicating the user is outside home)*
  - Sets the lighting scene based on the time of day
    - Between 9 PM and 5 AM, activates the **Lights evening** scene
    - If the sun's elevation is below 5°, activates the **Lights dinner** scene
    - Otherwise, skips the lighting adjustment (daytime)
  - Transfers media playback to the home media player
- **Leave Home**
  - *Condition: one or more home switches\* are active (indicating the user is at home)*
  - Turns all the home lights off
  - Transfers media playback to the mobile device, allowing the continuation of the track outside the home
  - Turns the media player off

\* Enabled switches counter tracks states of the entities listed in [entities/home_presence.yaml](entities/home_presence.yaml). The list includes selected light switches and media players. If at least one entity is active, we infer home presence. Hall lights are intentionally excluded from the list as they are on both upon entering and leaving the home.

#### Lights scenes

The middle section of the card lists the available home lighting scenes, arranged from the brightest to the dimmest. These scenes can also be activated by **triple-clicking** the corresponding control on the physical six-button switch in the living room, ordered from left to right.

- **Lights on**
  - Turns all the home lights on
  - Maintains the recent brightness and temperature properties
- **Lights focus**
  - Turns the living room lights on brightly
  - Sets cold temperature of 4500 K
- **Lights cooking**
  - Sets lights in a way that is comfortable for cooking
  - Sets kitchen and table lights to bright, 3000 K
  - Dims sofa and desk lights, 2000 K
- **Lights dinner**
  - Sets lights that are comfortable for having a dinner
  - Sets the bright table light, with warm temperature 2500 K
  - Dims kitchen, sofa and desk lights
  - Dims balcony bamboo and bedroom lights
- **Lights evening**
  - Sets dimmed lights suited for late evening relaxation
  - Dims kitchen spot, desk light and bedroom spots to 1% with the warmest 2000 K
  - Turns hall lights, kitchen countertop, table and all ceiling lights off
- **Lights off**
  - Turns all the lights off

#### Lighting automation

The final part of the interface provides controls for lighting automation in rooms without natural light, such as the bathroom and walk-in closet. This feature is available exclusively on the full desktop panel.

- **Lights dim**
  - Dims lights at night, between 10 PM and 6:30 AM
- **Lights motion**
  - Activates lights on motion detection

## Setup

### Overwrite core integrations
Perform `home-assistant-core` repo sparse checkout (instead of full submodule init)
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
