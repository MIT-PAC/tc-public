# Instrumenting an Android Application

## APK

(Delete `sootDebug/` directory in current working directory if it exists.)

1. `$ instr <app-name>.apk`

Aligned and (debug) signed apk is written to `sootOutput/<app-name>-instr-aligned.apk`.

## Ant Project

The easiest method is provide an option to the Ant build:

1. `$ ant debug -Dtc.inst=dex`

## Android Studio

1. Open the root Gradle file (`build.gradle`) for your project and
replace the `buildscript` block with the following:

    repositories {
        maven { url '/home/cleardroid/Android/studio-master-dev/out/repo' }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.4.0-beta4'
    }
    
1. Open application (Module for application) Gradle file, in `Android`
block add or edit `dexOptions` block to include `instrument = dex`.
For example:

    android {
    	    ...
    	    dexOptions {
	        ...
                instrument = "dex"
		...
    	    }
    	    ...
     }

1. Sync and build application as normal.

## Eclipse

Not supported.


