# app-ping

esp-claw WASM app: ping a host from the device (ICMP) and return sent/received/RTT as JSON.

Provides the tool `ping_host(host, count)`. It needs the `ping` permission; the firmware sends 1-10 ICMP probes to one host per call.

**Status:** in development. The code will be published here once the esp-claw WASM app runtime has been tested on hardware.

Part of [esp-claw (community)](https://github.com/esp-claw), an unofficial community fork of espressif/esp-claw that is not affiliated with Espressif.

## License

Apache-2.0
