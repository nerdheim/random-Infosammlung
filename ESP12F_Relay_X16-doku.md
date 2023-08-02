Packige!!!  
ESP8266/ESP-12E/ ESP-12F 16 channel Relays board arrived.  
So what do we have?  
- Power input 24V 
- 16x 10A Songle relays 
- ESP-12E 
- Pinrow to cut & solder yourself 
- a jumper 


| Relay | Pin |
| ----- | --- |
| 1     | 0   |
| 2     | 1   |
| 3     | 2   |
| 4     | 3   |
| 5     | 4   |
| 6     | 5   |
| 7     | 6   |
| 8     | 7   |
| 9     | 8   |
| 10    | 9   |
| 11    | 10  |
| 12    | 11  |
| 13    | 12  |
| 14    | 13  |
| 15    | 14  |
| 16    | 15  |



```
esphome:
  name: system-relay16-1
  friendly_name: system-relay16-1

esp8266:
  board: esp12e

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "XXXXXXXXXXXXXX="

ota:
  password: XXXXXXXXXXXXXX

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "System-Srv-Relay8-1"
    password: "XXXXXXXXXXXXXX"

captive_portal:
    
# Webserver
web_server:
  port: 80
  version: 2

sn74hc595:
  - id: 'sn74hc595_hub'
    data_pin: GPIO14
    clock_pin: GPIO13
    latch_pin: GPIO12
    oe_pin: GPIO05
    sr_count: 2

switch:
  - platform: gpio
    id: relay01
    name: "frei01"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 0
      inverted: False
  - platform: gpio
    id: relay02
    name: "frei02"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 1
      inverted: False
  - platform: gpio
    id: relay03
    name: "frei03"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 2
      inverted: False
  - platform: gpio
    id: relay04
    name: "frei04"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 3
      inverted: False
  - platform: gpio
    id: relay05
    name: "frei05"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 4
      inverted: False
  - platform: gpio
    id: relay06
    name: "frei06"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 5
      inverted: False
  - platform: gpio
    id: relay07
    name: "frei07"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 6
      inverted: False
  - platform: gpio
    id: relay08
    name: "frei08"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 7
      inverted: False
  - platform: gpio
    id: relay09
    name: "frei09"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 8
      inverted: False
  - platform: gpio
    id: relay10
    name: "frei10"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 9
      inverted: False
  - platform: gpio
    id: relay11
    name: "frei11"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 10
      inverted: False
  - platform: gpio
    id: relay12
    name: "frei12"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 11
      inverted: False
  - platform: gpio
    id: relay13
    name: "frei13"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 12
      inverted: False
  - platform: gpio
    id: relay14
    name: "frei14"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 13
      inverted: False
  - platform: gpio
    id: relay15
    name: "frei15"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 14
      inverted: False
  - platform: gpio
    id: relay16
    name: "frei16"
    pin: 
      sn74hc595: sn74hc595_hub
      number: 15
      inverted: False


```
