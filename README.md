# RICOH THETA Plug-in Library

Copied from the 
[RICOH THETA Plug-in SDK](https://github.com/ricohapi/theta-plugin-sdk) with no
modifications to the library. 
Intended for developers that want to create a new Android
SDK and import the module.

The plug-in library implements the following functions:

    * Get button operation event
    * Plug-in termination processing
    * LED control
    * Control of speaker

By inheriting `PluginActivity` you will be able to use library methods.

        ```java
        public class MainActivity extends PluginActivity {
            @Override
            protected void onCreate (Bundle savedInstanceState) {
                super.onCreate (savedInstanceState);
                setContentView (R.layout.activity_main);
        ```

Please refer to the [Plug-in Development Guide](http://theta360.guide/plugin/) 
for usage information.

1. Import "pluginlibrary" in the SDK by selecting "File"-"New"-"Import Module..."
2. Add "include ':app', ':pluginlibrary'" in "settings.gradle" file
3. You may need to add `implementation project(':pluginlibrary')` in build.gradle
4. Sync by selecting "File"-"Sync Project with Gradle Files"

## Start New Project

![Start Project](doc/img/new-project-1.png) 

![Create Project](doc/img/new-project-2.png) 

## Select API 25

![API 25](doc/img/api.png) 

## Basic Activity

I'm using Basic Activity. You can use any template and work from there.

![basic activity](doc/img/basic-activity-1.png) 

![configure activity](doc/img/basic-activity-2.png) 

![project structure](doc/img/basic-activity-3.png) 

## Import module

![import module](doc/img/import-module-1.png) 

![project structure](doc/img/import-module-2.png) 

## Edit Gradle Configuration Files

In build.gradle

![build.gradle](doc/img/gradle-config-1.png) 

![implementation project](doc/img/gradle-config-2.png) 

In settings.gradle

![settings.gradle](doc/img/gradle-config-3.png) 

![plugin library](doc/img/gradle-config-4.png) 

![gradle sync project](doc/img/gradle-config-5.png) 

## import pluginlibrary into MainActivity.java

![import pluginlibrary](doc/img/import-pluginlibrary.png) 

## Build apk

![build apk](doc/img/build-apk-1.png) 

Success.

![build success](doc/img/build-apk-2.png) 


## Test in Camera

To verify that your application is controlling the camera, write a simple test will light up two LEDs on the camera when it is placed into plug-in mode.

### Code Listing of Import Test

    package guide.theta360.libraryimporttest;

    import android.os.Bundle;
    import android.view.KeyEvent;

    import com.theta360.pluginlibrary.activity.PluginActivity;
    import com.theta360.pluginlibrary.callback.KeyCallback;
    import com.theta360.pluginlibrary.receiver.KeyReceiver;
    import com.theta360.pluginlibrary.values.LedColor;
    import com.theta360.pluginlibrary.values.LedTarget;

    public class MainActivity extends PluginActivity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            setKeyCallback(new KeyCallback() {
                @Override
                public void onKeyDown(int keyCode, KeyEvent event) {
                    if (keyCode == KeyReceiver.KEYCODE_CAMERA) {
                        System.out.println("theta debug: pressed camera mode button down");
                    }
                }

                @Override
                public void onKeyUp(int keyCode, KeyEvent event) {
                    notificationLedShow(LedTarget.LED6);
                    notificationLed3Show(LedColor.MAGENTA);
                    System.out.println("theta debug: camera now in plug-in mode  :-)");
                }

                @Override
                public void onKeyLongPress(int keyCode, KeyEvent event) {

                }
            });
        }
    }

### Install apk into camera

![locate apk](doc/img/install-camera-1.png) 

![install apk](doc/img/install-camera-2.png) 

### Set Library Import Test as Active Plug-in

Use the THETA Desktop application.

![active plugin](doc/img/active-plugin.png) 


### Test Plug-in On Camera

Reboot camera. Press mode button for two seconds.

Verify that app is lighting the correct LEDs with the correct color.

![successful camera test](doc/img/test-camera.jpg) 

![Analytics](https://ga-beacon.appspot.com/UA-73311422-5/pluginlibrary)
