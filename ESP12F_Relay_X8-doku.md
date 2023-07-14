Packige!!!  
ESP8266/ESP-12E/ ESP-12F 8 channel Relays board arrived.  
So what do we have?  
- Power input 5V / 7-28V 
- 8x 10A Songle relays 
- ESP-12E 
- Pinrow to solder yourself 
- a jumper 

Ok, first try -> just give it some power via a CP2102 USB TTL Konverter.  
- it opened an AP, but no captive portal has been running on it
- guess from my wife, it might me just a function check firmware
Let’s see…
- connect RX to TX
- TX to RX
- tell esphome that it’s dealing with an 
```
esp8266:
  board: esp12e
```
- ok, flash
- nop… no serial connection established :/  
- only a reset button, but no programming
“may you need to short out GND & IO0”  
*checking…*  
Maybe this is what the Jumper is for  
*connects jumper*  
flash works  
  
No doku what relay is on what gpio… then try and error it is.  
After like… 30min, I now have all Pins.  
| Relay   | GPIO Pin |
| ------- | -------- |
| Relay 1 | GPIO16   |
| Relay 2 | GPIO14   |
| Relay 3 | GPIO12   |
| Relay 4 | GPIO13   |
| Relay 5 | GPIO15   |
| Relay 6 | GPIO0    |
| Relay 7 | GPIO4    |
| Relay 8 | GPIO5    |

Oh wow… GPIO1 & GPIO3 are not in use? O.O  
So yay, I2C Ports, where I can connect an AHT10 ^^  
I guess GPIO2 is empty and I maybe could use it for dallas/onewire sensors or as a dum binery sensor for a switch or so.  

Finally I now have a 8c relay board, that also has 3 custom Pins for free use for 17,50€ (AWS price, Ali is more like 9,50€)  

```
esphome:
  name: system-srv-relay8-1
  friendly_name: system-srv-relay8-1

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
    
# i2c Ports
i2c:
  sda: GPIO1
  scl: GPIO3
  scan: true
  id: bus_a

sensor:
  - platform: uptime
    name: Uptime Sensor
    filters:
      - lambda: return x / 3600;
    unit_of_measurement: "h"
  - platform: aht10
    temperature:
      name: "Temperature Keller"
      id: air_temperature
    humidity:
      name: "Humidity Keller"
      id: relative_humidity
    update_interval: 20s
  - platform: absolute_humidity
    name: Absolute Humidity
    temperature: air_temperature
    humidity: relative_humidity

switch:
  - platform: gpio
    id: relay6
    name: "frei6"
    pin: 
      number: GPIO0
      inverted: False
  - platform: gpio
    id: relay7
    name: "frei7"
    pin: 
      number: GPIO4
      inverted: False
  - platform: gpio
    id: relay8
    name: "frei8"
    pin: 
      number: GPIO5
      inverted: False
  - platform: gpio
    id: relay3
    name: "frei3"
    pin: 
      number: GPIO12
      inverted: False
  - platform: gpio
    id: relay4
    name: "frei4"
    pin: 
      number: GPIO13
      inverted: False
  - platform: gpio
    id: relay2
    name: "frei2"
    pin: 
      number: GPIO14
      inverted: False
  - platform: gpio
    id: relay5
    name: "frei5"
    pin: 
      number: GPIO15
      inverted: False
  - platform: gpio
    id: relay1
    name: "frei1"
    pin: 
      number: GPIO16
      inverted: False

# Webserver
web_server:
  port: 80
  version: 2
```
