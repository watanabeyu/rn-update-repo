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
# fix node_modules/@unimodules/react-native-adapter/android/build.gradle#L69-L71
$ npm run android
```

## react-native v0.59.8 -> v0.60.4
* diff -> https://react-native-community.github.io/upgrade-helper/?from=0.59.8&to=0.60.4

### common
```
$ react-native unlink react-native-reanimated
$ react-native unlink react-native-gesture-handler
```
* react-native v0.60 auto link

### iOS
* [`iOS-v0.60.4`](https://github.com/watanabeyu/rn-update-repo/tree/ios-v0.60.4)

### Android
* [`Android-v0.60.4`](https://github.com/watanabeyu/rn-update-repo/tree/android-v0.60.4)

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

##### unimodules-react-native-adapter
```
* What went wrong:
Could not determine the dependencies of task ':unimodules-react-native-adapter:compileDebugAidl'.
> Could not resolve all task dependencies for configuration ':unimodules-react-native-adapter:debugCompileClasspath'.
  ...

   > Could not resolve androidx.vectordrawable:vectordrawable:{strictly 1.0.0}.
     ...

   > Could not resolve androidx.core:core:1.0.0.
     ...

   > Could not resolve androidx.vectordrawable:vectordrawable:1.0.0.
     ...

   > Could not resolve androidx.core:core:1.0.1.
     ...

   > Could not resolve androidx.vectordrawable:vectordrawable:1.0.1.
     ...
```
* this related to unimodules react-native-adapter [link](https://github.com/unimodules/react-native-unimodules/issues/52#issuecomment-503495466)
* `react-native` only, use `jetifier`, but `jetifier` can't fix `node_modules/@unimodules/react-native-adapter/android/build.gradle`.
* so you fix `node_modules/@unimodules/react-native-adapter/android/build.gradle#L69-L71`
```
-  compileOnly('com.facebook.react:react-native:+') {
-    exclude group: 'com.android.support'
-  }
+  implementation 'com.facebook.react:react-native:+'
```

##### debug.keystore not found for signing config 'debug'.
```
* What went wrong:
Execution failed for task ':app:validateSigningDebug'.
> Keystore file '/path/to/app/android/app/debug.keystore' not found for signing config 'debug'.
```
* remove signingConfigs from `/path/to/app/android/app/build.gradle`