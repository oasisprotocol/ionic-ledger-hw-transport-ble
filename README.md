# ionic-ledger-hw-transport-ble

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![CI test status][github-ci-tests-badge]][github-ci-tests-link]

<!-- markdownlint-disable line-length -->
[github-ci-tests-badge]: https://github.com/oasisprotocol/ionic-ledger-hw-transport-ble/workflows/ci-test/badge.svg
[github-ci-tests-link]: https://github.com/oasisprotocol/ionic-ledger-hw-transport-ble/actions?query=workflow:ci-test+branch:master
<!-- markdownlint-enable line-length -->

**Ledger Hardware Wallet Bluetooth BLE transport for Ionic.**

```shell
yarn add @oasisprotocol/ionic-ledger-hw-transport-ble
```

### Pre-requisite

-   [**Install and link library `@capacitor-community/bluetooth-le` + configure your app for Bluetooth permissions**](https://github.com/capacitor-community/bluetooth-le) (Open the link for documentation)
-   **global.Buffer** available. Typically `global.Buffer = require("buffer").Buffer;` that can be placed in a `polyfill.js` and imported with `import "./polyfill";` at first line of the main JavaScript entry file.

## Minimal getting started

`@oasisprotocol/ionic-ledger-hw-transport-ble` works like any of `@ledgerhq/hw-transport` libraries.

The difference here is that the list() is costy and you likely don't want to always scan for devices, you would better save a selected device as "known" to suggest it to user later.

> Important: you will also have to deal with specifics of Bluetooth BLE, for instance, you need to request the LOCATION permission on Android!

Here is a gist of the most important parts required.

### Check for Bluetooth state

```ts
import BleTransport from "@ledgerhq/react-native-hw-transport-ble";

// Check if @capacitor-community/bluetooth-le is setup
BleTransport.isSupported()

// Check for bluetooth status
BleTransport.isEnabled()
```

### Scan for devices

```ts
const scannedDevices = TransportBLE.list()
```

### Connect to device

```ts
const [scannedDevice] = scannedDevices
const transport = await TransportBLE.open(scannedDevice)
```

**and now we can just use the transport like any other Ledger transport!**
