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

## react-native v0.61.4 -> v0.63.2
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.61.4&to=0.63.2
* compare -> https://github.com/watanabeyu/rn-update-repo/compare/v0.61.4...v0.63.2
* react-native-unimodules v0.10.1
* react-native v0.63.2

## react-native v0.60.4 -> v0.61.4
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.60.4&to=0.61.4
* compare -> https://github.com/watanabeyu/rn-update-repo/compare/v0.60.4...v0.61.4
* react-native-unimodules v0.7.0-rc.4
* react-native v0.61.4

## react-native v0.59.8 -> v0.60.4
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.59.8&to=0.60.4
* react-native-unimodules v0.5.2
* react-native v0.60.4

#### other

##### Invariant Violation: "main" has not been registered. or Invariant Violation: "RNUpdateRepo" has not been registered.
* if use `import { registerRootComponent } from 'expo'`, error happend on android.
* if use `AppRegistry.registerComponent`, error happend on ios.
* So decided to take it all out.

##### Could not find or use auto-linked library 'swiftObjectiveC' any other
img
* check Project > Build Settings > Library Search Paths
* if blank here, add below params

```
"$(TOOLCHAIN_DIR)/usr/lib/swift/$(PLATFORM_NAME)"
"$(TOOLCHAIN_DIR)/usr/lib/swift-5.0/$(PLATFORM_NAME)"
"$(inherited)"
```

##### Undefined symbol: _swift_getFunctionReplacement
img
* check Project > Build Settings > Preprocessor Macros
* add `FB_SONARKIT_ENABLED=1` DEBUG value

img
* check TARGETS > Build Settings > Dead Code Stripping
* Dead Code Stripping = `YES`

##### This copy of libswiftCore.dylib requires an OS version prior to 12.2.0.
* Add New file Swift File
* Would you like to show configure an Objective-C bridging header? -> `Create Bridging Header`
* check Project > Build Settings > Always Embed Swift Standard Libraries
* set `YES`

##### Could not connect to development server after update
* https://github.com/facebook/react-native/issues/23380#issuecomment-473871592
* add `android:usesCleartextTraffic="true"` to `app/src/AndroidManifest.xml`
```
<application
       ....
       android:usesCleartextTraffic="true"
       android:theme="@style/AppTheme">
```

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