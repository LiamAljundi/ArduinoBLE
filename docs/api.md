# ArduinoBLE library

## BLE class

Used to enable the BLE module.

### `begin()`

Initializes the BLE device.

#### Syntax

```
BLE.begin()

```

#### Parameters

None

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }
…

```

### `end()`

Stops the BLE device.

#### Syntax

```
BLE.end()

```

#### Parameters

None

Returns
Nothing

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ....

  BLE.end();
…

```

### `poll()`

Poll for BLE radio events and handle them.

#### Syntax

```
BLE.poll() BLE.poll(timeout)

```

#### Parameters

**timeout**: optional timeout in ms, to wait for event. If not specified defaults to 0 ms.

Returns
Nothing

#### Example

```Arduino
…
  // assign event handlers for connected, disconnected to peripheral
  BLE.setEventHandler(BLEConnected, blePeripheralConnectHandler);
  BLE.setEventHandler(BLEDisconnected, blePeripheralDisconnectHandler);

  // …

  BLE.poll();
…

```

### `setEventHandler()`

Set the event handler (callback) function that will be called when the specified event occurs.

#### Syntax

```
BLE.setEventHandler(eventType, callback)

```

#### Parameters

**eventType**: event type (BLEConnected, BLEDisconnected)
**callback**: function to call when event occurs
Returns
Nothing.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  // assign event handlers for connected, disconnected to peripheral
  BLE.setEventHandler(BLEConnected, blePeripheralConnectHandler);
  BLE.setEventHandler(BLEDisconnected, blePeripheralDisconnectHandler);

  // …


void blePeripheralConnectHandler(BLEDevice central) {
  // central connected event handler
  Serial.print("Connected event, central: ");
  Serial.println(central.address());
}

void blePeripheralDisconnectHandler(BLEDevice central) {
  // central disconnected event handler
  Serial.print("Disconnected event, central: ");
  Serial.println(central.address());
}
…

```

### `connected()`

Query if another BLE device is connected

#### Syntax

```
BLE.connected()

```

#### Parameters

None

Returns
**true** if another BLE device is connected, otherwise **false**.

#### Example

```Arduino
…
    // while the central is still connected to peripheral:
    while (BLE.connected()) {

       // ...
    }
…

```

### `disconnect()`

Disconnect any BLE devices that are connected

#### Syntax

```
BLE.disconnect()

```

#### Parameters

None

Returns
**true** if any BLE device that was previously connected was disconnected, otherwise **false**.

#### Example

```Arduino
…
  if (BLE.connected()) {
    // …

    BLE.disconnect();
  }
…

```

### `address()`

Query the Bluetooth address of the BLE device.

#### Syntax

```
BLE.address()

```

#### Parameters

None

Returns
The **Bluetooth address** of the BLE device (as a String).

#### Example

```Arduino
…
  **String** address = BLE.address();

  Serial.print(“Local address is: “);
  Serial.println(address);
…

```

### `rssi()`

Query the RSSI (Received signal strength indication) of the connected BLE device.

#### Syntax

```
BLE.rssi()

```

#### Parameters

None

Returns
The **RSSI** of the connected BLE device, 127 if no BLE device is connected.

#### Example

```Arduino
…
  if (BLE.connected()) {
    // …

   Serial.print(“RSSI = “);
    Serial.println(BLE.rssi());
  }
…

```

### `setAdvertisedServiceUuid()`

Set the advertised service UUID used when advertising.

#### Syntax

```
BLE.setAdvertisedServiceUuid(uuid)

```

#### Parameters

**uuid:** 16-bit or 128-bit BLE UUID in **String** format

Returns
Nothing

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  BLE.setAdvertisedServiceUuid(“19B10000-E8F2-537E-4F6C-D104768A1214");

  // ...  

  // start advertising
  BLE.advertise();
…

```

### `setAdvertisedService()`

Set the advertised service UUID used when advertising to the value of the BLEService provided.

#### Syntax

```
BLE.setAdvertisedService(bleService)

```

#### Parameters

**bleService:** BLEService to use UUID from

Returns
Nothing

#### Example

```Arduino
…
BLEService ledService("19B10000-E8F2-537E-4F6C-D104768A1214"); // BLE LED Service

// ...

  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  BLE.setAdvertisedService(ledService);

  // ...  

  // start advertising
  BLE.advertise();
…

```

### `setManufacturerData()`

Set the manufacturer data value used when advertising.

#### Syntax

```
BLE.setManufacturerData(data, length)

```

#### Parameters

**data:** byte array containing manufacturer data
**length:** length of manufacturer data array

Returns
Nothing

#### Example

```Arduino
…
 // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  byte data[5] = { 0x01, 0x02, 0x03, 0x04, 0x05};

  BLE.setManufacturerData(data, 5);

  // ...  

  // start advertising
  BLE.advertise();

…

```

### `setLocalName()`

Set the local value used when advertising.

#### Syntax

```
BLE.setLocalName(name)

```

#### Parameters

**name:** local name value to use when advertising

Returns
Nothing

#### Example

```Arduino
…
 // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  BLE.setLocalName("LED");

  // ...  

  // start advertising
  BLE.advertise();

…

```

### `setDeviceName()`

Set the device name in the built in device name characteristic. If not set, the value defaults “Arduino”.

#### Syntax

```
BLE.setDeviceName(name)

```

#### Parameters

**name:** device name value

Returns
Nothing

#### Example

```Arduino
…
 // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  BLE.setDeviceName("LED");

  // ...  

  // start advertising
  BLE.advertise();

…

```

### `setAppearance()`

Set the appearance in the built in appearance characteristic. If not set, the value defaults 0x0000.

#### Syntax

```
BLE.setAppearance(appearance)

```

#### Parameters

**appearance:** appearance value

Returns
Nothing

#### Example

```Arduino
…
 // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  BLE.setAppearance(0x8000);

  // ...  

  // start advertising
  BLE.advertise();

…

```

### `addService()`

Add a BLEService to the set of services the BLE device provides

#### Syntax

```
BLE.addService(service)

```

#### Parameters

**service:** BLEService to add

Returns
Nothing

#### Example

```Arduino
…
BLEService ledService("19B10000-E8F2-537E-4F6C-D104768A1214"); // BLE LED Service

// …

 // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.addService(ledService);

  // ...  
…

```

### `advertise()`

Start advertising.

#### Syntax

```
BLE.advertise()

```

#### Parameters

None

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.advertise();

  // ...  
…

```

### `stopAdvertise()`

Stop advertising.

#### Syntax

```
BLE.stopAdvertise()

```

#### Parameters

None

Returns
Nothing

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.advertise();

  // ...  

  BLE.stopAdvertise();
…

```

### `central()`

Query the central BLE device connected.

#### Syntax

```
BLE.central()

```

#### Parameters

None

Returns
**BLEDevice** representing the central.

#### Example

```Arduino
…
  // listen for BLE peripherals to connect:
  BLEDevice central = BLE.central();

  // if a central is connected to peripheral:
  if (central) {
    Serial.print("Connected to central: ");
    // print the central's MAC address:
    Serial.println(central.address());

    // …
  }
…

```

### `setAdvertisingInterval()`

Set the advertising interval in units of 0.625 ms. Defaults to 100ms (160 * 0.625 ms) if not provided.

#### Syntax

```
BLE.setAdvertisingInterval(advertisingInterval)

```

#### Parameters

**advertisingInterval:** advertising interval in units of 0.625 ms

Returns
Nothing.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.setAdvertisingInterval(320); // 200 * 0.625 ms

  BLE.advertise();
…

```

### `setConnectionInterval()`

Set the minimum and maximum desired connection intervals in units of 1.25 ms.

#### Syntax

```
BLE.setConnectionInterval(minimum, maximum)

```

#### Parameters

**minimum:** minimum desired connection interval in units of 1.25 ms
**maximum:** maximum desired connection interval in units of 1.25 ms

Returns
Nothing.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.setConnectionInterval(0x0006, 0x0c80); // 7.5 ms minimum, 4 s maximum

…

```

### `setConnectable()`

Set if the device is connectable after advertising, defaults to **true**.

#### Syntax

```
BLE.setConnectable(connectable)

```

#### Parameters

**true**: the device will be connectable when advertising
**false**: the device will NOT be connectable when advertising

Returns
Nothing.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  // ...

  BLE.setConnectable(false); // make the device unconnectable when advertising

…

```

### `scan()`

Start scanning for BLE devices that are advertising.

#### Syntax

```
BLE.scan()
BLE.scan(withDuplicates)

```

#### Parameters

**withDuplicates:** optional, defaults to **false**. If **true**, advertisements received more than once will not be filtered

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
     // ...
  }
…

```

### `scanForName()`

Start scanning for BLE devices that are advertising with a particular (local) name.

#### Syntax

```
BLE.scanForName(name)
BLE.scanForName(name, withDuplicates)

```

#### Parameters

**name:** (local) name of device (as a **String**) to filter for
**withDuplicates:** optional, defaults to **false**. If **true**, advertisements received more than once will not be filtered.

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scanForName("LED");

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
     // ...
  }
…

```

### `scanForAddress()`

Start scanning for BLE devices that are advertising with a particular (Bluetooth) address.

#### Syntax

```
BLE.scanForAddress(address)
BLE.scanForAddress(address, withDuplicates)

```

#### Parameters

**address:** (Bluetooth) address (as a String) to filter for
**withDuplicates:** optional, defaults to **false**. If **true**, advertisements received more than once will not be filtered

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scanForAddress("aa:bb:cc:ee:dd:ff");

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
     // ...
  }
…

```

### `scanForUuid()`

Start scanning for BLE devices that are advertising with a particular (service) UUID.

#### Syntax

```
BLE.scanForUuid(uuid)
BLE.scanForUuid(uuid, withDuplicates)

```

#### Parameters

**uuid:** (service) UUID (as a **String**) to filter for
**withDuplicates:** optional, defaults to **false**. If **true**, advertisements received more than once will not be filtered.

Returns
1 on success, 0 on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scanForUuid("aa10");

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
     // ...
  }
…

```

### `stopScan()`

Stop scanning for BLE devices that are advertising.

#### Syntax

```
BLE.stopScan()

```

#### Parameters

None

Returns
Nothing

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …
  BLE.stopScan();
…

```

### `available()`

Query for a discovered BLE device that was found during scanning.

#### Syntax

```
BLE.available()

```

#### Parameters

Nothing

Returns
**BLEDevice** representing the discovered device.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
     // ...
  }
…

```

## BLEDevice Class

Used to get information about the devices connected or discovered while scanning

### `poll()`

Poll for BLE radio events for the specified BLE device and handle them.

#### Syntax

```
bleDevice.poll()
bleDevice.poll(timeout)

```

#### Parameters

**timeout**: optional timeout in ms, to wait for event. If not specified defaults to 0 ms.

Returns
Nothing

#### Example

```Arduino
…
  // listen for BLE centrals to connect:
  BLEDevice central = BLE.central();

  // if a central is connected to peripheral:
  if (central) {
    // …

   central.poll();

    // ...
  }
…

```

### `connected()`

Query if a BLE device is connected

#### Syntax

```
bleDevice.connected()

```

#### Parameters

None

Returns
**true** if the BLE device is connected, otherwise **false**.

#### Example

```Arduino
…
  // listen for BLE centrals to connect:
  BLEDevice central = BLE.central();

    // while the central is still connected
    while (central.connected()) {

       // ...
    }
…

```

### `disconnect()`

Disconnect the BLE device, if connected

#### Syntax

```
bleDevice.disconnect()

```

#### Parameters

None

Returns
**true** if the BLE device was disconnected, otherwise **false**.

#### Example

```Arduino
…
 // listen for BLE centrals to connect:
  BLEDevice central = BLE.central();

  // …

  central.disconnect();
…

```

### `address()`

Query the Bluetooth address of the BLE device.

#### Syntax

```
bleDevice.address()

```

#### Parameters

None

Returns
The **Bluetooth address** of the BLE device (as a String).

#### Example

```Arduino
…
  // listen for BLE peripherals to connect:
  BLEDevice central = BLE.central();

  // if a central is connected to peripheral:
  if (central) {
    Serial.print("Connected to central: ");
    // print the central's MAC address:
    Serial.println(central.address());

    // ….
  }
…

```

### `rssi()`

Query the RSSI (Received signal strength indication) of the BLE device.

#### Syntax

```
bleDevice.rssi()

```

#### Parameters

None

Returns
The **RSSI** of the connected BLE device, 127 if the BLE device is not connected.

#### Example

```Arduino
…
  if (bleDevice.connected()) {
    // …

    Serial.print(“RSSI = “);
    Serial.println(bleDevice.rssi());
  }
…

```

### `characteristic()`

Get a BLECharacteristic representing a BLE characteristic the device provides.

#### Syntax

```
bleDevice.characteristic(index)
bleDevice.characteristic(uuid)
bleDevice.characteristic(uuid, index)

```

#### Parameters

**index**: index of characteristic
**uuid**: uuid (as a **String**)

Returns
**BLECharacteristic** for provided parameters

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    BLECharacteristic batteryLevelCharacterisic = peripheral.characteristic("2a19");

    if (batteryLevelCharacterisic) {
      // use the characteristic
    } else {
      Serial.println("Peripheral does NOT have battery level characteristic");
    }

    // ...
  }
…

```

### `discoverAttributes()`

Discover all of the attributes of BLE device.

#### Syntax

```
bleDevice.discoverAttributes()

```

#### Parameters

None

Returns
**true**, if successful, **false** on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    // ...
  }
…

```

### `discoverService()`

Discover the attributes of a particular service on the BLE device.

#### Syntax

```
bleDevice.discoverService(serviceUuid)

```

#### Parameters

**serviceUuid:** service UUID to discover (as a **String**)

Returns
**true**, if successful, **false** on failure.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover service attributes
    Serial.println("Discovering service attributes ...");
    if (peripheral.serviceUuid("fffe")) {
      Serial.println("Service attributes discovered");
    } else {
      Serial.println("Service attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    // ...
  }
…

```

### `deviceName()`

Query the device name (BLE characteristic UUID 0x2a00) of a BLE device.

#### Syntax

```
bleDevice.deviceName()

```

#### Parameters

None

Returns
**Device name** (as a String).

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    // read and print device name of peripheral
    Serial.println();
    Serial.print("Device name: ");
    Serial.println(peripheral.deviceName());
    Serial.print("Appearance: 0x");
    Serial.println(peripheral.appearance(), HEX);
    Serial.println();

    // ...
  }
…

```

### `appearance()`

Query the appearance (BLE characteristic UUID 0x2a01) of a BLE device.

#### Syntax

```
bleDevice.appearance()

```

#### Parameters

None

Returns
**Appearance value** (as a number).

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    // read and print device name of peripheral
    Serial.println();
    Serial.print("Device name: ");
    Serial.println(peripheral.deviceName());
    Serial.print("Appearance: 0x");
    Serial.println(peripheral.appearance(), HEX);
    Serial.println();

    // ...
  }
…

```

### `serviceCount()`

Query the number of services discovered for the BLE device.

#### Syntax

```
bleDevice.serviceCount()

```

#### Parameters

None

Returns
The number of **services discovered** for the BLE device.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    int serviceCount = peripheral.serviceCount();

    Serial.print(serviceCount);
    Serial.println(" services discovered");

    // ...
  }
…

```

### `hasService()`

Query if the BLE device has a particular service.

#### Syntax

```
bleDevice.hasService(uuid)
bleDevice.hasService(uuid, index)

```

#### Parameters

**uuid**: uuid to check (as a **String**)
**index**: optional, index of service to check if the device provides more than on. Defaults to 0, if not provided.

Returns
**true**, if the device provides the service, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    if (peripheral.hasService("180f")) {
      Serial.println("Peripheral has battery service");
    }

    // ...
  }
…

```

### `service()`

Get a BLEService representing a BLE service the device provides.

#### Syntax

```
bleDevice.service(index)
bleDevice.service(uuid)
bleDevice.service(uuid, index)

```

#### Parameters

**index**: index of service
**uuid**: uuid (as a **String**)

Returns
**BLEService** for provided parameters

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    BLEService batteryService = peripheral.service("180f");

    if (batteryService) {
      // use the service
    } else {
      Serial.println("Peripheral does NOT have battery service");
    }

    // ...
  }
…

```

### `characteristicCount()`

Query the number of characteristics discovered for the BLE device.

#### Syntax

```
bleDevice.characteristicCount()

```

#### Parameters

None

Returns
The **number of characteristics** discovered for the BLE device.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    int characteristicCount = peripheral.characteristicCount();

    Serial.print(characteristicCount);
    Serial.println(" characteristis discovered");

    // ...
  }
…

```

### `hasCharacteristic()`

Query if the BLE device has a particular characteristic.

#### Syntax

```
bleDevice.hasCharacteristic(uuid)
bleDevice.hasCharacteristic(uuid, index)

```

#### Parameters

**uuid**: uuid to check (as a **String**)
**index**: optional, index of characteristic to check if the device provides more than on. Defaults to 0, if not provided.

Returns
**true**, if the device provides the characteristic, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    if (peripheral.hasCharacteristic("2a19")) {
      Serial.println("Peripheral has battery level characteristic");
    }

    // ...
  }
…

```

### `hasLocalName()`

Query if a discovered BLE device is advertising a local name.

#### Syntax

```
bleDevice.hasLocalName()

```

#### Parameters

Nothing

Returns
**true**, if the device is advertising a local name, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    // print the local name, if present
    if (peripheral.hasLocalName()) {
      Serial.print("Local Name: ");
      Serial.println(peripheral.localName());
    }

    // ...
  }
…

```

### `hasAdvertisedServiceUuid()`

Query if a discovered BLE device is advertising a service UUID.

#### Syntax

```
bleDevice.hasAdvertisedServiceUuid()
bleDevice.hasAdvertisedServiceUuid(index)

```

#### Parameters

**index**: optional, defaults to 0, the index of the service UUID, if the device is advertising more than one.

Returns
**true**, if the device is advertising a service UUID, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    // print the advertised service UUIDs, if present
    if (peripheral.hasAdvertisedServiceUuid()) {
      Serial.print("Service UUIDs: ");
      for (int i = 0; i < peripheral.advertisedServiceUuidCount(); i++) {
        Serial.print(peripheral.advertisedServiceUuid(i));
        Serial.print(" ");
      }
      Serial.println();
    }

    // ...
  }
…

```

### `advertisedServiceUuidCount()`

Query the number of advertised services a discovered BLE device is advertising.

#### Syntax

```
bleDevice.advertisedServiceUuidCount()

```

#### Parameters

None

Returns
The **number of advertised services** a discovered BLE device is advertising.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    // print the advertised service UUIDs, if present
    if (peripheral.hasAdvertisedServiceUuid()) {
      Serial.print("Service UUIDs: ");
      for (int i = 0; i < peripheral.advertisedServiceUuidCount(); i++) {
        Serial.print(peripheral.advertisedServiceUuid(i));
        Serial.print(" ");
      }
      Serial.println();
    }

    // ...
  }
…

```

### `localName()`

Query the local name a discovered BLE device is advertising with.

#### Syntax

```
bleDevice.localName()

```

#### Parameters

Nothing

Returns
**Advertised local name** (as a String).

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    // print the local name, if present
    if (peripheral.hasLocalName()) {
      Serial.print("Local Name: ");
      Serial.println(peripheral.localName());
    }

    // ...
  }
…

```

### `advertisedServiceUuid()`

Query an advertised service UUID discovered BLE device is advertising.

#### Syntax

```
bleDevice.advertisedServiceUuid()
bleDevice.advertisedServiceUuid(index)

```

#### Parameters

**index**: optional, defaults to 0, the index of the **service UUID**, if the device is advertising more than one.

Returns
Advertised service **UUID** (as a String).

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    // print the advertised service UUIDs, if present
    if (peripheral.hasAdvertisedServiceUuid()) {
      Serial.print("Service UUIDs: ");
      for (int i = 0; i < peripheral.advertisedServiceUuidCount(); i++) {
        Serial.print(peripheral.advertisedServiceUuid(i));
        Serial.print(" ");
      }
      Serial.println();
    }

    // ...
  }
…

```

### `connect()`

Connect to a BLE device.

#### Syntax

```
bleDevice.connect()

```

#### Parameters

None

Returns
**true**, if the connection was successful, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // ...
  }
…

```

## BLEService Class

Used to enable the services board provides or interact with services a remote board provides.

### `BLEService()`

Create a new BLE service.

#### Syntax

```
BLEService(uuid)

```

#### Parameters

**uuid**: 16-bit or 128-bit UUID in **String** format

Returns
New **BLEService** with the specified **UUID**

#### Example

```Arduino
…
BLEService ledService("19B10000-E8F2-537E-4F6C-D104768A1214"); // BLE LED Service
…

```

### `uuid()`

Query the UUID of the specified BLEService.

#### Syntax

```
bleService.uuid()

```

#### Parameters

None

Returns
UUID of the BLE service as a **String**.

#### Example

```Arduino
…
BLEService ledService("19B10000-E8F2-537E-4F6C-D104768A1214"); // BLE LED Service

// …
Serial.print(“LED service UUID = “);
Serial.println(ledService.uuid());

…

```

### `addCharacteristic()`

Add a BLECharateristic to the BLE service.

#### Syntax

```
bleService.addCharacteristic(bleCharacteristic)

```

#### Parameters

None

Returns
Nothing

#### Example

```Arduino
…
BLEService ledService("19B10000-E8F2-537E-4F6C-D104768A1214"); // BLE LED Service

// BLE LED Switch Characteristic - custom 128-bit UUID, readable and writable by central
BLECharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite, 1);


// …

// add the characteristic to the service
ledService.addCharacteristic(switchCharacteristic);

…

```

### `characteristicCount()`

Query the number of characteristics discovered for the BLE service.

#### Syntax

```
bleService.characteristicCount()

```

#### Parameters

None

Returns
The **number of characteristics** discovered for the BLE service.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    BLEService batteryService = peripheral.service("180f");

    if (batteryService) {
      // use the service
      int characteristicCount = batteryService.characteristicCount();

      Serial.print(characteristicCount);
      Serial.println(" characteristics discovered in battery service");
    } else {
      Serial.println("Peripheral does NOT have battery service");
    }

    // ...
  }
…

```

### `hasCharacteristic()`

Query if the BLE service has a particular characteristic.

#### Syntax

```
bleService.hasCharacteristic(uuid)
bleService.hasCharacteristic(uuid, index)

```

#### Parameters

**uuid**: uuid to check (as a **String**)
**index**: optional, index of characteristic to check if the device provides more than on. Defaults to 0, if not provided.

Returns
**true**, if the service provides the characteristic, **false** otherwise.

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …
  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    BLEService batteryService = peripheral.service("180f");

    if (batteryService) {
      // use the service
      if (batteryService.hasCharacteristic("2a19")) {
        Serial.println("Battery service has battery level characteristic");
      }
    } else {
      Serial.println("Peripheral does NOT have battery service");
    }

    // ...
  }
…

```

### `characteristic()`

Get a BLECharacteristic representing a BLE characteristic the service provides.

#### Syntax

```
bleService.characteristic(index)
bleService.characteristic(uuid)
bleService.characteristic(uuid, index)

```

#### Parameters

**index**: index of characteristic
**uuid**: uuid (as a **String**)

Returns
**BLECharacteristic** for provided parameters

#### Example

```Arduino
…
  // begin initialization
  if (!BLE.begin()) {
    Serial.println("starting BLE failed!");

    while (1);
  }

  Serial.println("BLE Central scan");

  // start scanning for peripheral
  BLE.scan();

  // …

  BLEDevice peripheral = BLE.available();

  if (peripheral) {
    // ...

    Serial.println("Connecting ...");

    if (peripheral.connect()) {
      Serial.println("Connected");
    } else {
      Serial.println("Failed to connect!");
      return;
    }

    // discover peripheral attributes
    Serial.println("Discovering attributes ...");
    if (peripheral.discoverAttributes()) {
      Serial.println("Attributes discovered");
    } else {
      Serial.println("Attribute discovery failed!");
      peripheral.disconnect();
      return;
    }

    BLEService batteryService = peripheral.service("180f");

    if (batteryService) {
      // use the service
      BLECharacteristic batteryLevelCharacterisic = peripheral.characteristic("2a19");

      if (batteryLevelCharacterisic) {
        // use the characteristic
      } else {
        Serial.println("Peripheral does NOT have battery level characteristic");
      }
    } else {
      Serial.println("Peripheral does NOT have battery service");
    }

    // ...
  }
…

```

## BLECharacteristic Class

Used to enable the characteristics board offers in a service or interact with characteristics a remote board provides.

### `BLECharacteristic()`

Create a new BLE characteristic.

#### Syntax

```
BLECharacteristic(uuid, properties, value, valueSize)
BLECharacteristic(uuid, properties, stringValue)

BLEBoolCharacteristic(uuid, properties)
BLEBooleanCharacteristic(uuid, properties)
BLECharCharacteristic(uuid, properties)
BLEUnsignedCharCharacteristic(uuid, properties)
BLEByteCharacteristic(uuid, properties)
BLEShortCharacteristic(uuid, properties)
BLEUnsignedShortCharacteristic(uuid, properties)
BLEWordCharacteristic(uuid, properties)
BLEIntCharacteristic(uuid, properties)
BLEUnsignedIntCharacteristic(uuid, properties)
BLELongCharacteristic(uuid, properties)
BLEUnsignedLongCharacteristic(uuid, properties)
BLEFloatCharacteristic(uuid, properties)
BLEDoubleCharacteristic(uuid, properties)
```

#### Parameters

**uuid**: 16-bit or 128-bit UUID in **String** format
**properties**: mask of the properties (BLEBroadcast, BLERead, BLEWriteWithoutResponse, BLEWrite, BLENotify, BLEIndicate)
**valueSize**: (maximum) size of characteristic value
**stringValue**: value as a string

Returns
New **BLECharacteristic** with the specified **UUID** and value

#### Example

```Arduino
…
// BLE Battery Level Characteristic
BLEUnsignedCharCharacteristic batteryLevelChar("2A19",  // standard 16-bit characteristic UUID
    BLERead | BLENotify); // remote clients will be able to get notifications if this characteristic changes

…

```

### `uuid()`

Query the UUID of the specified BLECharacteristic.

#### Syntax

```
bleCharacteristic.uuid()

```

#### Parameters

None

Returns
**UUID** of the BLE service as a **String**.

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);

// …
Serial.print(“Switch characteristic UUID = “);
Serial.println(switchCharacteristic.uuid());

…

```

### `properties()`

Query the property mask of the specified BLECharacteristic.

#### Syntax

```
bleCharacteristic.properties()

```

#### Parameters

None

Returns
**Properties of the characteristic masked** (BLEBroadcast, BLERead, BLEWriteWithoutResponse, BLEWrite, BLENotify, BLEIndicate)

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);

// …
byte properties = switchCharacteristic.properties();

if (properties & BLERead) {
  // characteristic is readable ...
}

if (properties & (BLEWrite | BLEWriteWithoutResponse)) {
  // characteristic is writable ...
}
…

```

### `valueSize()`

Query the maximum value size of the specified BLECharacteristic.

#### Syntax

```
bleCharacteristic.valueSize()

```

#### Parameters

None

Returns
The **maximum value** size of the characteristic (in bytes)

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);

// …

Serial.print(“value size = “);
Serial.println(switchCharacteristic.valueSize());
…

```

### `value()`

Query the current value of the specified BLECharacteristic.

#### Syntax

```
bleCharacteristic.value()

```

#### Parameters

None

Returns
The **current value** of the characteristic, value type depends on the constructor used

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);

// …

      if (switchCharacteristic.value()) {   // any value other than 0
          Serial.println("LED on");
          digitalWrite(ledPin, HIGH);         // will turn the LED on
        } else {                              // a 0 value
          Serial.println(F("LED off"));
          digitalWrite(ledPin, LOW);          // will turn the LED off
        }

…

```

### `valueLength()`

Query the current value size of the specified BLECharacteristic.

#### Syntax

```
bleCharacteristic.valueLength()

```

#### Parameters

None

Returns
The **current value** size of the characteristic (in bytes)

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);

// …

Serial.print(“value length = “);
Serial.println(switchCharacteristic.valueLength());
…

```

### `readValue()`

Read the current value of the characteristic. If the characteristic is on a remote device, a read request will be sent.

#### Syntax

```
bleCharacteristic.readValue(buffer, length)
bleCharacteristic.readValue(value)

```

#### Parameters

**buffer:** byte array to read value into length: size of buffer argument in bytes 
**value**: variable to read value into (by reference)

Returns
Number of bytes read

#### Example

```Arduino
…
  while (peripheral.connected()) {
    // while the peripheral is connected

    // check if the value of the simple key characteristic has been updated
    if (simpleKeyCharacteristic.valueUpdated()) {
      // yes, get the value, characteristic is 1 byte so use byte value
      byte value = 0;

      simpleKeyCharacteristic.readValue(value);

      if (value & 0x01) {
        // first bit corresponds to the right button
        Serial.println("Right button pressed");
      }

      if (value & 0x02) {
        // second bit corresponds to the left button
        Serial.println("Left button pressed");
      }
    }
  }
…

```

### `writeValue()`

Write the value of the characteristic. If the characteristic is on a remote device, a write request or command will be sent.

#### Syntax

```
bleCharacteristic.writeValue(buffer, length)
bleCharacteristic.writeValue(value)

```

#### Parameters

**buffer**: byte array to write value with
**length**: number of bytes of the buffer argument to write
**value**: value to write

Returns
1 on success, 0 on failure

#### Example

```Arduino
…
    // read the button pin
    int buttonState = digitalRead(buttonPin);

    if (oldButtonState != buttonState) {
      // button changed
      oldButtonState = buttonState;

      if (buttonState) {
        Serial.println("button pressed");

        // button is pressed, write 0x01 to turn the LED on
        ledCharacteristic.writeValue((byte)0x01);
      } else {
        Serial.println("button released");

        // button is released, write 0x00 to turn the LED off
        ledCharacteristic.writeValue((byte)0x00);
      }
    }
…

```

### `setEventHandler()`

Set the event handler (callback) function that will be called when the specified event occurs.

#### Syntax

```
bleCharacteristic.setEventHandler(eventType, callback)

```

#### Parameters

**eventType**: event type (BLESubscribed, BLEUnsubscribed, BLERead, BLEWritten) 
**callback**: function to call when the event occurs

Returns
Nothing

#### Example

```Arduino
…
// create switch characteristic and allow remote device to read and write
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);


// …

  // assign event handlers for characteristic
  switchCharacteristic.setEventHandler(BLEWritten, switchCharacteristicWritten);

// …

void switchCharacteristicWritten(BLEDevice central, BLECharacteristic characteristic) {
  // central wrote new value to characteristic, update LED
  Serial.print("Characteristic event, written: ");

  if (switchCharacteristic.value()) {
    Serial.println("LED on");
    digitalWrite(ledPin, HIGH);
  } else {
    Serial.println("LED off");
    digitalWrite(ledPin, LOW);
  }
}

  …

```

### `broadcast()`

Broadcast the characteristics value as service data when advertising.

#### Syntax

```
bleCharacteristic.broadcast()

```

#### Parameters

None

Returns
1 on success, 0 on failure

#### Example

```Arduino
…
// create button characteristic and allow remote device to get notifications
BLEByteCharacteristic buttonCharacteristic("19B10012-E8F2-537E-4F6C-D104768A1214", BLERead | BLENotify | BLEBroadcast);

// …

buttonCharacteristic.broadcast();

…

```

### `written()`

Query if the characteristic value has been written by another BLE device.

#### Syntax

```
bleCharacteristic.written()

```

#### Parameters

None

Returns
**true** if the characteristic value has been written by another BLE device, **false** otherwise

#### Example

```Arduino
…
// BLE LED Switch Characteristic - custom 128-bit UUID, read and writable by central
BLEByteCharacteristic switchCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLEWrite);


// …

 // listen for BLE peripherals to connect:
  BLEDevice central = BLE.central();

  // if a central is connected to peripheral:
  if (central) {
    Serial.print("Connected to central: ");
    // print the central's MAC address:
    Serial.println(central.address());

    // while the central is still connected to peripheral:
    while (central.connected()) {
      // if the remote device wrote to the characteristic,
      // use the value to control the LED:
      if (switchCharacteristic.written()) {
        if (switchCharacteristic.value()) {   // any value other than 0
          Serial.println("LED on");
          digitalWrite(ledPin, HIGH);         // will turn the LED on
        } else {                              // a 0 value
          Serial.println(F("LED off"));
          digitalWrite(ledPin, LOW);          // will turn the LED off
        }
      }
    }

    // when the central disconnects, print it out:
    Serial.print(F("Disconnected from central: "));
    Serial.println(central.address());
  }


…

```

### `subscribed()`

Query if the characteristic has been subscribed to by another BLE device.

#### Syntax

```
bleCharacteristic.subscribed()

```

#### Parameters

None

Returns
**true** if the characteristic value has been subscribed to by another BLE device, **false** otherwise

#### Example

```Arduino
…
// BLE Battery Level Characteristic
BLEUnsignedCharCharacteristic batteryLevelChar("2A19",  // standard 16-bit characteristic UUID
    BLERead | BLENotify); // remote clients will be able to get notifications if this characteristic changes



// …

  if (batteryLevelChar.subscribed()) {
     // set a new value , that well be pushed to subscribed BLE devices
    batteryLevelChar.writeValue(0xab);
  }
…

```

### `addDescriptor()`

Add a BLEDescriptor to the characteristic.

#### Syntax

```
bleCharacteristic.addDescriptor(bleDescriptor)

```

#### Parameters

**bleDescriptor**: descriptor to add to the characteristic

Returns
Nothing

#### Example

```Arduino
…
// BLE Battery Level Characteristic
BLEUnsignedCharCharacteristic batteryLevelChar("2A19",  // standard 16-bit characteristic UUID
    BLERead | BLENotify); // remote clients will be able to get notifications if this characteristic changes

BLEDescriptor batteryLevelDescriptor("2901", "millis");



// …

  batteryLevelChar.addDescriptor(batteryLevelDescriptor);
…

```

### `descriptorCount`

Query the number of BLE descriptors discovered for the characteristic.

#### Syntax

```
bleCharacteristic.descriptorCount()

```

#### Parameters

None

Returns
The **number of BLE descriptors** discovered for the characteristic

#### Example

```Arduino
…
 // loop the descriptors of the characteristic and explore each
  for (int i = 0; i < characteristic.descriptorCount(); i++) {
    BLEDescriptor descriptor = characteristic.descriptor(i);

    // ...
  }
…

```

### `hasDescriptor`

Check if a characteristic has a particular descriptor.

#### Syntax

```
bleCharacteristic.hasDescriptor(uuid)
bleCharacteristic.hasDescriptor(uuid, index)

```

#### Parameters

**index**: index of descriptor
**uuid**: uuid (as a **String**)

Returns
**true**, if the characteristic has a matching descriptor, otherwise **false**.

#### Example

```Arduino
…
  if (characteristic.hasDescriptor("2901")) {
    Serial.println("characteristic has description descriptor");
  }
…

```

### `descriptor()`

Get a BLEDescriptor that represents a characteristics BLE descriptor.

#### Syntax

```
bleCharacteristic.descriptor(index)
bleCharacteristic.descriptor(uuid)
bleCharacteristic.descriptor(uuid, index)

```

#### Parameters

**index**: index of descriptor
**uuid**: uuid (as a **String**)

Returns
BLEDescriptor that represents a characteristics BLE descriptor

#### Example

```Arduino
…
  if (characteristic.hasDescriptor("2901")) {
    Serial.println("characteristic has description descriptor");
  }
…

```

### `canRead()`

Query if a BLE characteristic is readable.

#### Syntax

```
bleCharacteristic.canRead()

```

#### Parameters

None

Returns
**true**, if characteristic is readable, **false** otherwise

#### Example

```Arduino
…
  if (characteristic.canRead("2901")) {
    Serial.println("characteristic is readable");
  }
…

```

read

Perform a read request for the characteristic.

#### Syntax

```
bleCharacteristic.read()

```

#### Parameters

None

Returns
**true**, if successful, **false** on failure

#### Example

```Arduino
…
  if (characteristic.read()) {
    Serial.println("characteristic value read");

    // ...
  } else {
    Serial.println("error reading characteristic value");
  }
…

```

### `canWrite()`

Query if a BLE characteristic is writable.

#### Syntax

```
bleCharacteristic.canWrite()

```

#### Parameters

None

Returns
**true**, if characteristic is writable, **false** otherwise

#### Example

```Arduino
…
  if (characteristic.canWrite()) {
    Serial.println("characteristic is writable");
  }
…

```

### `canSubscribe()`

Query if a BLE characteristic is subscribable.

#### Syntax

```
bleCharacteristic.canSubscribe()

```

#### Parameters

None

Returns
**true**, if characteristic is subscribable, **false** otherwise

#### Example

```Arduino
…
  if (characteristic.canSubscribe()) {
    Serial.println("characteristic is subscribable");
  }
…

```

### `subscribe()`

Subscribe to a BLE characteristics notification or indications.

#### Syntax

```
bleCharacteristic.subscribe()

```

#### Parameters

None

Returns
**true**, on success, **false** on failure

#### Example

```Arduino
…
  // ...

  // retrieve the simple key characteristic
  BLECharacteristic simpleKeyCharacteristic = peripheral.characteristic("ffe1");

  // subscribe to the simple key characteristic
  Serial.println("Subscribing to simple key characteristic ...");
  if (!simpleKeyCharacteristic) {
    Serial.println("no simple key characteristic found!");
    peripheral.disconnect();
    return;
  } else if (!simpleKeyCharacteristic.canSubscribe()) {
    Serial.println("simple key characteristic is not subscribable!");
    peripheral.disconnect();
    return;
  } else if (!simpleKeyCharacteristic.subscribe()) {
    Serial.println("subscription failed!");
    peripheral.disconnect();
    return;
  }

  // ...
…

```

### `canUnsubscribe()`

Query if a BLE characteristic is unsubscribable.

#### Syntax

```
bleCharacteristic.canUnsubscribe()

```

#### Parameters

None

Returns
**true**, if characteristic is unsubscribable, **false** otherwise

#### Example

```Arduino
…
  if (characteristic.canUnsubscribe()) {
    Serial.println("characteristic is unsubscribable");
  }
…

```

### `unsubscribe()`

Unsubscribe to a BLE characteristics notifications or indications.

#### Syntax

```
bleCharacteristic.unsubscribe()

```

#### Parameters

None

Returns
**true**, on success, **false** on failure

#### Example

```Arduino
…
  // ...

  // retrieve the simple key characteristic
  BLECharacteristic simpleKeyCharacteristic = peripheral.characteristic("ffe1");

  // subscribe to the simple key characteristic
  Serial.println("Subscribing to simple key characteristic ...");
  if (!simpleKeyCharacteristic) {
    Serial.println("no simple key characteristic found!");
    peripheral.disconnect();
    return;
  } else if (!simpleKeyCharacteristic.canSubscribe()) {
    Serial.println("simple key characteristic is not subscribable!");
    peripheral.disconnect();
    return;
  } else if (!simpleKeyCharacteristic.subscribe()) {
    Serial.println("subscription failed!");
    peripheral.disconnect();
    return;
  }

  // ...

  simpleKeyCharacteristic.unsubscribe();
…

```

### `valueUpdated()`

Has the characteristics value been updated via a notification or indication.

#### Syntax

```
bleCharacteristic.valueUpdated()

```

#### Parameters

None

Returns
**true**, if the characteristics value been updated via a notification or indication

#### Example

```Arduino
…
  while (peripheral.connected()) {
    // while the peripheral is connected

    // check if the value of the simple key characteristic has been updated
    if (simpleKeyCharacteristic.valueUpdated()) {
      // yes, get the value, characteristic is 1 byte so use byte value
      byte value = 0;

      simpleKeyCharacteristic.readValue(value);

      if (value & 0x01) {
        // first bit corresponds to the right button
        Serial.println("Right button pressed");
      }

      if (value & 0x02) {
        // second bit corresponds to the left button
        Serial.println("Left button pressed");
      }
    }
  }
…

```

## BLEDescriptor Class

Used to describe a characteristic the board offers

### `BLEDescriptor()`

Create a new BLE descriptor.

#### Syntax

```
BLEDescriptor(uuid, value, valueSize)
BLEDescriptor(uuid, stringValue)

```

#### Parameters

**uuid**: 16-bit or 128-bit UUID in string format
**value**: byte array value
**valueSize**: size of byte array value
**stringValue**: value as a string

Returns
New **BLEDescriptor** with the specified **UUID** and value

#### Example

```Arduino
…
BLEDescriptor millisLabelDescriptor("2901", "millis");
…

```

### `uuid()`

Query the UUID of the specified BLEDescriptor.

#### Syntax

```
bleDescriptor.uuid()

```

#### Parameters

None

Returns
**UUID** of the BLE descriptor (as a String).

#### Example

```Arduino
…
BLEDescriptor millisLabelDescriptor("2901", "millis");

// …
Serial.print(“millis label descriptor UUID = “);
Serial.println(millisLabelDescriptor.uuid());

…

```

### `valueSize()`

Query the value size of the specified BLEDescriptor.

#### Syntax

```
bleDescriptor.valueSize()

```

#### Parameters

None

Returns
**Value size** (in bytes) of the BLE descriptor.

#### Example

```Arduino
…
BLEDescriptor millisLabelDescriptor("2901", "millis");

// …
Serial.print(“millis label descriptor value size = “);
Serial.println(millisLabelDescriptor.valueSize());

…

```

### `valueLength()`

Query the length, in bytes, of the descriptor current value.

#### Syntax

```
bleDescriptor.valueLength()

```

#### Parameters

None

Returns
**Length of descriptor** value in bytes.

#### Example

```Arduino
…
  // read the descriptor value
  descriptor.read();

  // print out the value of the descriptor
  Serial.print(", value 0x");
  printData(descriptor.value(), descriptor.valueLength());

  // ...

  void printData(const unsigned char data[], int length) {
    for (int i = 0; i < length; i++) {
      unsigned char b = data[i];

      if (b < 16) {
        Serial.print("0");
      }

      Serial.print(b, HEX);
    }
  }
…

```

### `value()`

Query the value of the specified BLEDescriptor.

#### Syntax

```
bleDescriptor.value()

```

#### Parameters

None

Returns
Value byte array of the **BLE descriptor**.

#### Example

```Arduino
…
BLEDescriptor millisLabelDescriptor("2901", "millis");

// …

  int descriptorValueSize = millisLabelDescriptor.valueSize();
  byte descriptorValue[descriptorValueSize];

  for (int i = 0; i < descriptorValueSize; i++) {
    descriptorValue[i] = millisLabelDescriptor.value()[i];
  }

…

```

### `readValue()`

Read the current value of the descriptor. If the descriptor is on a remote device, a read request will be sent.

#### Syntax

```
bleDescriptor.readValue(buffer, length)
bleDescriptor.readValue(value)

```

#### Parameters

**buffer**: byte array to read value into
**length**: size of buffer argument in bytes
**value**: variable to read value into (by reference)

Returns
**Number of bytes** read

#### Example

```Arduino
…
  byte value = 0;

  /get the value, descriptor is 1 byte so use byte value    
  descriptor.readValue(value);
…

```

### `read()`

Perform a read request for the descriptor.

#### Syntax

```
bleDescriptor.read()

```

#### Parameters

None

Returns
**true**, if successful, **false** on failure

#### Example

```Arduino
…
  if (descriptor.read()) {
    Serial.println("descriptor value read");

    // ...
  } else {
    Serial.println("error reading descriptor value");
  }
…
```
