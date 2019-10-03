### Ionic-3
- Push Notifications
  - `ionic start OnboardApp blank`
- Publishing your App (Android)

---

### Android Studio Setup
- Install Android Studio
- [Gradle](https://gradle.org/next-steps/?version=4.10.3&format=all) 
- To add new Environment variables:
  - Right click on `Computer/This PC`
  - Open `Properties` and select `Advanced System Settings`
  - Open `Environment Variables`

+++

- Add the following to file path (your path may vary):
  - ANDROID_SDK: C:\Users\<windows-user>\AppData\Local\Android\sdk
  - PATH: 
    - %ANDROID_HOME%\tools
    - %ANDROID_HOME%\tools\bin
    - %ANDROID_HOME%\platform-tools;
    - %ANDROID_HOME%\build-tools\<your-version>
    - <your-gradle-location>\bin


+++

### You may need the following:
- ```bash
  npm install -g native-run
  scoop install ojdkbuild8
  npm install -g cordova-res
  ```

---

### Push Notifications
- In essence, a message/alert sent by an app installed on your phone
- Similar to text messages, yet different
- Common Examples (Grab, Uber)

+++

### About Push notifications
- A way to engage/interact your users
- Redirects to the app sending push notifications (Call To Actoins)
- Can be muted by users

---

### Setting up your app with Push Notifications enabled
- In your `config.xml`
  ```
    <widget id="write-your-own-package-name"></widget>
  ``` 
- e.g `com.push.testapp`
- `ionic cordova plugin add cordova-plugin-fcm-with-dependecy-updated`
- `npm install @ionic-native/fcm`

+++

```javascript
// app.module.ts
import {FCM} from '@ionic-native/fcm/ngx'

@NgModule({
  declarations: [AppComponent],
  entryComponents: [],
  imports: [BrowserModule, IonicModule.forRoot(), AppRoutingModule],
  providers: [
    StatusBar,
    SplashScreen,
    FCM,
    { provide: RouteReuseStrategy, useClass: IonicRouteStrategy }
  ],
  bootstrap: [AppComponent]
})
```

+++

### Running your app
- `ionic cordova platform add android`
- If you have an emulator setup:
  - `ionic cordova run android`
- If you are using your mobile:
  - `ionic cordova build android --release`


---

### Setting up Push Notifications(Firebase)
- Sign up to [Firebase](https://console.firebase.google.com)
- Create a project with a name and enter the project
- On your project, setup an android app, and provide a package name
  - do not leave it as `com.example`
  - download the `google-service.json` and put in the `root` of your app.
- Send a push notification through Cloud Messaging on Firebase Dashboard
  - You may also send using a POST request

---

### Different handling of Push Notifications
- Foreground (silent notification)
- Background (standrad notification)
- Closed (standrad notification)

---

### Publishing Your App
```bash
# Build the apk file 
# You can find it in: platforms/android/app/build/outputs/release
ionic cordova build android --release
```

+++

### App Signing (Self signing)
- To publish your app, you will need to provide a signed certificate
- This is used to validate yourself as the author of this app
- You will need the Android SDK to use these functions

+++

```bash
# Generate a keystore
# You will be prompted to provide password
keytool -genkey -v -keystore <name-of-keystore>.keystore -alias <alias_name> -keyalg RSA -keysize 2048 -validity 10000

# Sign your application
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <name-of-keystore>.keystore .\platforms\android\app\build\outputs\apk\release\app-release-unsigned.apk <alias_name>

# Optimize the apk file
zipalign -v 4 .\platforms\android\app\build\outputs\apk\release\app-release-unsigned.apk <final-apk-filename>.apk
```

--- 

### Publishing an App (Android)
- [Google Play Store Console](https://play.google.com/apps/publish/) 
- Create an application
- You will need to provide:
  - Listing details
  - Content Details and Rating
  - Price and Distribution Details
  - APK file
- You can publish to internal testers, or as production

--- 

### Exercise: Onboard
- Start a new ionic app
- Allow it to receive a welcome push notifications
  - `Welcome <app-name>, Thank you for installing our app`
- Display different on foreground, background, closed
- Show a Toast in when receiving the message


---

### Project Requirements
- Create a mobile app
- Enable push notifications
- Create a backend to store/process data from mobile app
- Optional:
  - Find and use a native mobile functionality within your app
- A good rule of thumb is to consider what problems/incoveniences the company has

+++

### Proejct Suggestions
- Budget App
- Visitor Registration (QR code)
- Food Advisor
- Event/MeetUps (Mark Available timeslots)