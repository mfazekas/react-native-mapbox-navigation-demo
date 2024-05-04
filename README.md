### Create project

```
npx react-native@0.71.4 init rnmbxnavigation_rn71demo --version 0.71.4
```

### Add react-native-mapbox-navigation


```
yarn add mfazekas/react-native-mapbox-navigation#ndk23plus
```

### Configure the project for iOS

Make sure your `.netrc` has your mapbox token set up (follow instructions)[https://docs.mapbox.com/ios/maps/guides/install/#configure-your-secret-token]. Otherwise you'll get 404 error during `pod install`.


```sh
cd ios
NO_FLIPPER=1 pod install
cd ..
yarn ios # or build rnmbxnavigation_rn71demo.xcworkspace
```

Add audio and location background modes to Info.plist:
```xml
  <key>UIBackgroundModes</key>
  <array>
    <string>audio</string>
    <string>location</string>
  </array>
```

### Configure the project for Android

Make sure your `~/.gradle/gradle.properties` has your mapbox download token. (follow instructions)[https://docs.mapbox.com/android/maps/guides/install/#configure-your-secret-token].
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


Add location permission to manifest `android/app/src/main/AndroidManifest.xml`
see (Mapbox instructions)[https://docs.mapbox.com/android/navigation/v2/guides/get-started/install/#configure-permissions] 
```xml
<manifest ... >
  <!-- Always include this permission -->
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

  <!-- Include only if your app benefits from precise location access. -->
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
</manifest>
```


### Add mapbox tokens to `android/app/src/main/AndroidManifest.xml` and `ios/rnmbxnavigation_rn71demo/Info.plist`:




