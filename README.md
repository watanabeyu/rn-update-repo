# install and run
```
# iOS
$ cd ios
$ pod install
$ cd ../
$ npm run ios

# Android
# open android directory by android studio for create local.properties
$ npm run start
$ npm run android
```

## react-native v0.60.4 -> v0.61.4
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.60.4&to=0.61.4

## react-native v0.59.8 -> v0.60.4
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.59.8&to=0.60.4

### common
```
$ react-native unlink react-native-reanimated
$ react-native unlink react-native-gesture-handler
```
* react-native >= v0.60 auto link

### iOS
* [`iOS-v0.61.4`](https://github.com/watanabeyu/rn-update-repo/tree/iOS-v0.61.4)
* [`iOS-v0.60.4`](https://github.com/watanabeyu/rn-update-repo/tree/iOS-v0.60.4)

### Android
* [`Android-v0.61.4`](https://github.com/watanabeyu/rn-update-repo/tree/Android-v0.61.4)
  * API 28 necessary [this](https://github.com/facebook/react-native/issues/23380#issuecomment-473871592)
* [`Android-v0.60.4`](https://github.com/watanabeyu/rn-update-repo/tree/Android-v0.60.4)

#### other

##### task wrapper(type: Wrapper) -> wrapper
* `wrapper` error in `build.gradle`.
```
- task wrapper(type: Wrapper) {
+ wrapper {
```

##### local.properties error
```
* What went wrong:
A problem occurred configuring project ':app'.
> SDK location not found. Define location with an ANDROID_SDK_ROOT environment variable or by setting the sdk.dir path in your project's local properties file at '/path/to/app/android/local.properties'.
```
* fix -> open android studio

##### debug.keystore not found for signing config 'debug'.
```
* What went wrong:
Execution failed for task ':app:validateSigningDebug'.
> Keystore file '/path/to/app/android/app/debug.keystore' not found for signing config 'debug'.
```
* remove signingConfigs from `/path/to/app/android/app/build.gradle`