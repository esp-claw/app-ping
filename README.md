# app-ping

esp-claw WASM app: ping a host from the device (ICMP) and return sent/received/RTT as JSON.

Provides the tool `ping_host(host, count)`. It needs the `ping` permission; the firmware sends 1-10 ICMP probes to one host per call.

## Build

```sh
git clone --recursive https://github.com/esp-claw/app-ping.git
cd app-ping && ./sdk/build-app.sh .
```

This needs clang with the wasm32 target and wasm-ld (on Debian/Ubuntu: `apt install clang lld`). The output is `build/app.wasm` and `build/manifest.json`. CI builds every push and attaches both files to releases.

## Install

Copy both files to `/apps/ping/` on the device, for example over WebDAV (`dav://<device>/dav/apps/ping/`). Then send `/apps reload ping` in Telegram, or restart the device.

**Status:** works with runtime v1 in [esp-claw/esp-claw](https://github.com/esp-claw/esp-claw). Packages are not signed yet; signing arrives with the installer.

Part of [esp-claw (community)](https://github.com/esp-claw), an unofficial community fork of espressif/esp-claw that is not affiliated with Espressif.

## License

Apache-2.0
