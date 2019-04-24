# Bluetooth Low Energy (BLE) with react-native 

Library for BLE [react-native-ble-manager](https://github.com/innoveit/react-native-ble-manager)

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

  [android example screen](https://github.com/idriuk2/ble/blob/master/android_ble_screen.png)

## issues
- no robust way to test bluetooth without real devices
- setup correct build and development environments for ios and android (settings; versions of each library, package, module, etc.)

## interest ble-manager issues
- `#492` iOS cant connect device after remember device (author can’t help)
- `#456` Bluetooth Devices not listing in android (author answer, about android 8 issues with bluetooth)
- `#441` IOS | how to read data more than 512 bytes using BLE react native. now we can read only 512 bytes of data (author answer to try notifications)

## other react-native libraries for BLE
- https://github.com/Polidea/react-native-ble-plx - maybe hidden marketing of Polidea (hard to setup, use polidea's native rx libraries inside, have link to their landing page)
