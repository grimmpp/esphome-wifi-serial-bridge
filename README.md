Serial to Wifi Bridge for ESPHome
=========================

Custom component for ESPHome to expose a UART stream over WiFi or Ethernet. Can be used as a serial-to-wifi bridge as
known from ESPLink or ser2net by using ESPHome.

This component creates a TCP server listening on port 6638 (by default), and relays all data between the connected
clients and the serial port. It doesn't support any control sequences, telnet options or RFC 2217, just raw data.

This is original component from https://github.com/oxan/esphome-stream-server extend by ayufan to define a set of additional options
to better handle for high baud rate UART modes and define a way how clients are handled.

Usage
-----

Requires ESPHome v1.10.0 or higher.

```yaml
external_components:
  - source: github://grimmpp/esphome-wifi-serial-bridge

stream_server:
   # default 6638
   port: 2323

   # 0: unlimited
   # positive: keep only N latest connected clients
   # negative: reject over N clients
   max_clients: 4
```

You can set the UART ID and port to be used under the `stream_server` component.

```yaml
uart:
   id: uart_bus
   # add further configuration for the UART here

stream_server:
   uart_id: uart_bus
   port: 1234
```


How to build and push code locally
======

Create virtual python environment
`python -m venv .venv`

Install esphome
`pip install esphome`

Install libraries
`?`

Create secrets.yaml in project folder file:
```
wifi_ssid: "**********"
wifi_password: "**********"
api_password: "**********"
ota_password: "**********"
```

Compile und upload via USB
`esphome run project.yaml`