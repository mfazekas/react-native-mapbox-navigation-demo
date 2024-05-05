### Create project

```
npx react-native@0.71.4 init rnmbxnavigation_rn71demo --version 0.71.4
```


### 1. Add react-native-mapbox-navigation


```
yarn add mfazekas/react-native-mapbox-navigation#ndk23plus
```

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/1e05069df7f155d178a5c9038da7a090c5184af3)

### 2. Configure the project for iOS

Make sure your `.netrc` has your mapbox token set up [follow instructions](https://docs.mapbox.com/ios/maps/guides/install/#configure-your-secret-token). Otherwise you'll get 404 error during `pod install`.


```sh
cd ios
NO_FLIPPER=1 pod install
cd ..
yarn ios # or build rnmbxnavigation_rn71demo.xcworkspace
```

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/9a768360c4e14ac26a3b97ecb02e17986e0cae57)


Add audio and location background modes to Info.plist:
```xml
  <key>UIBackgroundModes</key>
  <array>
    <string>audio</string>
    <string>location</string>
  </array>
```

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/2668e8a36392726c59c496c47b8712cdd9827229)


### 3. Configure the project for Android

Make sure your `~/.gradle/gradle.properties` has your mapbox download token. [follow instructions](https://docs.mapbox.com/android/maps/guides/install/#configure-your-secret-token).
Add the following to your root build.gradle `android/build.gradle`.

```gradle
allprojects {
    repositories {
        maven {
            url 'https://api.mapbox.com/downloads/v2/releases/maven'
            authentication {
                basic(BasicAuthentication)
            }
            credentials {
                username = "mapbox"
                password = project.properties['MAPBOX_DOWNLOADS_TOKEN'] ?: ""
            }
        }
        maven {
            url 'https://api.mapbox.com/downloads/v2/snapshots/maven'
            authentication {
                basic(BasicAuthentication)
            }
            credentials {
                username = "mapbox"
                password = project.properties['MAPBOX_DOWNLOADS_TOKEN'] ?: ""
            }
        }
    }
}
```

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/9a768360c4e14ac26a3b97ecb02e17986e0cae57)

Add location permission to manifest `android/app/src/main/AndroidManifest.xml`
see [Mapbox instructions](https://docs.mapbox.com/android/navigation/v2/guides/get-started/install/#configure-permissions)
```xml
<manifest ... >
  <!-- Always include this permission -->
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

  <!-- Include only if your app benefits from precise location access. -->
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
</manifest>
```

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/b53adb8e3588109f336da7fff60f3ff54d4a1bf0)


### 4. Add mapbox tokens to `android/app/src/main/AndroidManifest.xml` and `ios/rnmbxnavigation_rn71demo/Info.plist`:

Add `MAPBOX_ACCESS_TOKEN` to your `android/app/src/main/AndroidManifest.xml` and `MBXAccessToken` to your `ios/rnmbxnavigation_rn71demo/Info.plist`.
For more information please check [andorid](https://docs.mapbox.com/android/navigation/v2/guides/get-started/install/#configure-your-public-token) and [ios](https://docs.mapbox.com/ios/navigation/guides/get-started/install/#configure-your-public-token) instructions.




[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/a0827b856dfd6365910e9acdc3b5ec46c60dcec9)

### 5. Add a component that uses navigation to your app

[diff](https://github.com/mfazekas/react-native-mapbox-navigation-demo/commit/fae4f43f5d3c7d6134ec0175b54ee4835b49f1d0)



