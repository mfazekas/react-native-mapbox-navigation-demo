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

```

```





