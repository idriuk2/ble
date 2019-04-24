# Bluetooth Low Energy (BLE) with react-native 


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
