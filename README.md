# app-ping

esp-claw WASM app: ping a host from the device (ICMP) and return sent/received/RTT as JSON.

Provides the tool `ping_host(host, count)`. It needs the `ping` permission; the firmware sends 1-10 ICMP probes to one host per call.

## Build

```sh
git clone --recursive https://github.com/esp-claw/app-ping.git
cd app-ping && ./sdk/build-app.sh .
```

This needs clang with the wasm32 target and wasm-ld (on Debian/Ubuntu: `apt install clang lld`). The output is `build/app.wasm` and `build/manifest.json`. CI builds every push, checks the manifest and the module with the SDK's `manifest_check.py` and `wasm_check.py`, and attaches both files to releases.

**Status:** works with runtime v1 in [esp-claw/esp-claw](https://github.com/esp-claw/esp-claw).

## Install

Install a signed release in Telegram (see [Releases](#releases)):

```
/app install https://github.com/esp-claw/app-ping/releases/download/v1.0.0/ping-1.0.0.ecapp
```

The device must trust the esp-claw key: `app_trusted_keys` must contain `XHQYDdKaRZ6pNzXYcrGAB8bTyPa3D22NU+lVzAt2Acw=` (see [trusted keys](https://github.com/esp-claw/app-sdk#trusted-keys)). The device asks for confirmation before installing. To update, send `/app update ping <url of the newer .ecapp>`. `/app remove ping` deletes the app and its data.

To test a local build, use a development device with `app_allow_unsigned` set to `true`. Copy `build/manifest.json` and `build/app.wasm` to `/apps/ping/`, for example over WebDAV (`dav://<device>/dav/apps/ping/`). Then send `/apps reload ping` in Telegram.

## Releases

Each release `v<version>` carries the signed package `ping-<version>.ecapp`, signed with the esp-claw key (key_id `7087d6a8`). It also carries the CI build it was made from (`app.wasm`, `manifest.json`). Install a release with:

```
/app install https://github.com/esp-claw/app-ping/releases/download/v<version>/ping-<version>.ecapp
```

Maintainers: bump `version` in `manifest.json` and publish a release tagged `v<version>`. CI attaches the build. Then sign it locally and upload the `.ecapp`, as described in the [app-sdk release steps](https://github.com/esp-claw/app-sdk#releasing-an-app).

Part of [esp-claw (community)](https://github.com/esp-claw), an unofficial community fork of espressif/esp-claw that is not affiliated with Espressif.

## License

Apache-2.0
