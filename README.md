# Bluetooth Low Energy (BLE) with react-native 

**Bluetooth Low Energy (BLE)**. Also called *Bluetooth smart*, this technology allows peripherals to communicate by consuming much less energy than regular Bluetooth. Another major advantage is that the *user does not need to manually pair with the device* using the system settings.

Library for BLE [react-native-ble-manager](https://github.com/innoveit/react-native-ble-manager)

[Short ios doc for BLE](https://codeburst.io/getting-started-with-bluetooth-low-energy-on-ios-ada3090fc9cc)

## Terminology
### devices types
- **_central_** (*client*): phone (search and initiates the connection to the peripheral)
- **_peripheral_** (*server*): heart rate monitor (exposes fields that the central can read, write or be notified)
### communication modes
- **_advertising_**: the peripheral sends information to be available to all the centrals around (GAP broadcasting)
- **_connected_**: allows a central to exchange data with a peripheral (GATT protocol, one-to-one mode)
### communication in connected mode
- The peripheral *exposes fields* that the *central can read, write or be notified of*. Each of these fields is called a **_characteristic_**. A characteristic is also accompanied by a *descriptor* which explains it.
- Characteristics are grouped into a **_service_**
- Each characteristic and service is defined by a *unique identifier* called **UUID**. There are predefined UUIDs for many services and characteristics. You can find a list here: [services](https://www.bluetooth.com/specifications/gatt/services) and [characteristics](https://www.bluetooth.com/specifications/gatt/characteristics). 

## run ios example on simulator

```
git clone https://github.com/innoveit/react-native-ble-manager
cd react-native-ble-manager
cd example
npm install
react-native link
react-native run-ios
```

## run android example on emulator
- open `example/android` in android studio
- pressed OK in Gradle Sync modal to recreate Gradle properties
- Downgrade Gradle to version 3.5. Edit `distributionUrl=https\://services.gradle.org/distributions/gradle-3.5-all.zip` in `gradle-wrapper.properties`.
- open metro bundler `react-native run-android` (ignore error)
- run project from android studio on simulator
- app throws warnins about bluetooth
  ```
  ‘No bluetooth support’ (Promise rejection id: 1)
  ‘PermissionsAndroid.requestPermission’ is deprecated. Use ‘PermissionsAndroid.request’ 
  after press “Scan Bluetooth” or “Retrieve connected peripherals” - new Possible Unhandled Promise Rejection (id: 11)
  ```

## run android example on device in develpment
- delete app from apk
- enable bluetooth on android phone
- run from terminal
  ```
  cd example
  adb devices
  adb -s ES2BA81020000658 reverse tcp:8081 tcp:8081
  react-native run-android
  ```

## build android apk

[react-native docs for signed apk android](https://facebook.github.io/react-native/docs/signed-apk-android)

- add `my-release-key.keystore` to `android/app`
- add to `android/gradle.properties`
  ```
  MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
  MYAPP_RELEASE_KEY_ALIAS=my-key-alias
  MYAPP_RELEASE_STORE_PASSWORD=111111
  MYAPP_RELEASE_KEY_PASSWORD=111111
  ```

- edit `android/app/build.gradle`

  [signingConfigs](https://github.com/idriuk2/rntest/blob/google_maps_android/android/app/build.gradle#L112)

  [release](https://github.com/idriuk2/rntest/blob/google_maps_android/android/app/build.gradle#L135)
  
- assembleRelease
  ``` 
  cd android
  sudo chmod 755 ./gradlew
  ./gradlew assembleRelease
  ```
  [docs about chmod](http://osxh.ru/content/chmod)

  [example release apk](https://github.com/idriuk2/ble/blob/master/ble-manager-example-app-release.apk)

## simulate a peripheral with the mac
  ```
  clone https://github.com/noble/bleno
  cd bleno
  npm install
  npm install git://github.com/taoyuan/node-xpc-connection.git
  cd examples/echo
  node main.js
  ```
  [issue with node.js](https://github.com/sandeepmistry/node-xpc-connection/issues/24#issuecomment-451629018)

## test connection
- [run android example on device in develpment](https://github.com/idriuk2/ble#run-android-example-on-device-in-develpment)
- 
  ```
  cd bleno/examples/pizza
  node peripheral
  ```
- shake device and open dev tools
- scan bluetooth 
- select PizzaSquat [android example screen](https://github.com/idriuk2/ble/blob/master/android_ble_screen.png)
- check console in dev tools [dev tools and peripheral console screen](https://github.com/idriuk2/ble/blob/master/connect_with_peripheral_simulator_screen.png)

## issues
- no robust way to test react-native BLE app with ios simulator or android emulator
- no robust way to connect android with apple peripherals (android phone with apple watch)
- no robust way to setup reliable build and development environments for ios and android (settings, IDEs modules and plugins versions, permissions, packages, etc.)

## interest ble-manager issues
- `#492` iOS cant connect device after remember device (maintainer can’t help)
- `#456` Bluetooth Devices not listing in android (maintainer answer, about android 8 issues with bluetooth)
- `#441` IOS | how to read data more than 512 bytes using BLE react native. now we can read only 512 bytes of data (maintainer answer to try notifications)

## other react-native libraries for BLE
- https://github.com/Polidea/react-native-ble-plx - maybe hidden marketing of Polidea (hard to setup, use polidea's native rx libraries inside, have link to their landing page)

## native ios libraries for BLE
- [BlueCap](https://github.com/troystribling/BlueCap), [interest article about BLE with example](https://codeburst.io/getting-started-with-bluetooth-low-energy-on-ios-ada3090fc9cc)
- Core Bluetooth (BLE framework developed by apple and included in the iOS SDK since iOS5)