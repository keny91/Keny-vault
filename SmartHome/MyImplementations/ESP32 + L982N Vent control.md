#ESP32 #L982N #SmartHome


![[Pasted image 20260507163323.png]]



![[Pasted image 20260507163347.png]]


![[Pasted image 20260507163527.png]]



If Docker hosted HomeAssistant. A ESP HOME container to the compose:

```
#sample ha
services:
  homeassistant:
    image: ghcr.io/home-assistant/home-assistant:${HA_VERSION:-stable}
    container_name: ${HA_CONTAINER_NAME:-homeassistant}
    restart: unless-stopped
    networks:
      - core_net
    ports:
      - "${HA_PORT:-8123}:8123"
    volumes:
      - ${HA_CONFIG_PATH:-./volumes/homeassistant}:/config
      - /etc/localtime:/etc/localtime:ro
    privileged: true

  esphome:
    image: ghcr.io/esphome/esphome:latest
    container_name: esphome
    restart: unless-stopped
    network_mode: host
    privileged: true
    devices:
      - /dev/ttyUSB0:/dev/ttyUSB0
    volumes:
      - ./esphome/config:/config
      - /etc/localtime:/etc/localtime:ro
```


Navigate to:

http://{{IP-of-machine-running-container}}:6052/

Detect new ESP32 and here is a .yml to control multiple engines:

```

esphome:

  name: esp-rejilla-1

  friendly_name: ESP Rejilla 1

  

esp32:

  board: esp32dev

  framework:

    type: esp-idf

  

logger:

  

api:

  encryption:

    key: "pZP1LkurIRClbnFSzIUrBoZuCi3stUVa0aMvCrmJ1Z0="

  

ota:

  - platform: esphome

    password: "12345678"

  

wifi:

  ssid: !secret wifi_ssid

  password: !secret wifi_password

  

  ap:

    ssid: "Esp-Rejilla-1 Fallback Hotspot"

    password: "12345678"

  

captive_portal:

  

output:

  # Motor 1 - Canal A

  - platform: gpio

    pin: GPIO18

    id: motor1_in1

  

  - platform: gpio

    pin: GPIO19

    id: motor1_in2

  

  - platform: ledc

    pin: GPIO25

    id: motor1_enable

    frequency: 1000 Hz

  

  # Motor 2 - Canal B

  - platform: gpio

    pin: GPIO21

    id: motor2_in1

  

  - platform: gpio

    pin: GPIO22

    id: motor2_in2

  

  - platform: ledc

    pin: GPIO26

    id: motor2_enable

    frequency: 1000 Hz

  

cover:

  - platform: time_based

    name: "Compuerta 1"

    id: compuerta_1

    assumed_state: true

  

    open_action:

      - output.turn_on: motor1_in1

      - output.turn_off: motor1_in2

      - output.set_level:

          id: motor1_enable

          level: 100%

  

    close_action:

      - output.turn_off: motor1_in1

      - output.turn_on: motor1_in2

      - output.set_level:

          id: motor1_enable

          level: 100%

  

    stop_action:

      - output.set_level:

          id: motor1_enable

          level: 0%

      - output.turn_off: motor1_in1

      - output.turn_off: motor1_in2

  

    open_duration: 10s

    close_duration: 10s

  

  - platform: time_based

    name: "Compuerta 2"

    id: compuerta_2

    assumed_state: true

  

    open_action:

      - output.turn_on: motor2_in1

      - output.turn_off: motor2_in2

      - output.set_level:

          id: motor2_enable

          level: 100%

  

    close_action:

      - output.turn_off: motor2_in1

      - output.turn_on: motor2_in2

      - output.set_level:

          id: motor2_enable

          level: 100%

  

    stop_action:

      - output.set_level:

          id: motor2_enable

          level: 0%

      - output.turn_off: motor2_in1

      - output.turn_off: motor2_in2

  

    open_duration: 10s

    close_duration: 10s

```