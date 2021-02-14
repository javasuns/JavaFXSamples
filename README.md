# JavaFX Services (Gradle)

This software leverages the [Gluon Client plugin for Gradle](https://github.com/gluonhq/client-gradle-plugin) which is able to compile the application into native code along with its required dependencies, so it can directly be executed as a native application on the target platform. Cross-platform feature compatibility is achieved through [Gluon Attach](https://gluonhq.com/products/mobile/attach). The software utilizes some of its pre-built services (Browser, Device, Push Notifications and Share) 

[![BSD-3 license](https://img.shields.io/badge/license-BSD--3-%230778B9.svg)](https://opensource.org/licenses/BSD-3-Clause)


## Getting started

To use the plugin, apply the following steps:

### 1. Apply the plugin

Using the `plugins` DSL, add:


    plugins {
        id 'com.gluonhq.client-gradle-plugin' version '0.1.36'
    }
    
This requires adding the plugin repository to the `settings.gradle` file:

    pluginManagement {
        repositories {
            maven {
                url "https://nexus.gluonhq.com/nexus/content/repositories/releases"
            }
            
            gradlePluginPortal()
        }
    }
    rootProject.name = ...

    

### 2. Tasks

You can run the regular tasks to build and run your project as a regular VM project:

    ./gradlew clean build
    ./gradlew run
    
Once the project is ready, the plugin has these three main tasks:    

#### `Compiling for Desktop`

This tasks does the AOT compilation. It is a very intensive and lengthy task (several minutes, depending on your project and CPU).

Run:

    gradlew nativeBuild
    
#### `Compiling for Mobile (iOS)`

Make sure that you have completed the list in build.info with the necessary information before compiling to iOS. 
This task can be run only on MacOS (Read more at .....)

Run:

    gradlew nativeBuild -ptarget=ios

#### `nativeLink`

When the object is created, this task will generate the native executable for the target platform.

Run:

    ./gradlew nativeLink
    
The results will be available at `$buildDir/client/$hostPlatform/$AppName`.
    
#### `nativeBuild`

This task simply combines `nativeCompile` and `nativeLink`.

#### `nativeRun`

Runs the executable in the target platform

Run:

    ./gradlew nativeRun
    
Or run the three tasks combined:

    ./gradlew build nativeBuild nativeRun
    
Or run directly the application from command line:

    build/client/$hostPlatform/$AppName/$AppName    
    
It will create a distributable native application.

#### `nativePackage`

On mobile only, create a package of the executable in the target platform

Run:

	./gradlew nativePackage

On iOS, this can be used to create an IPA, on Android it will create an APK.


#### `nativeInstall`

On mobile only, installs the generated package that was created after `nativePackage`.

Run:

	./gradlew nativeInstall
    
### Requirements

Check the requirements for the [target platform](https://docs.gluonhq.com/#_platforms) before you get started.

## Issues and Contributions ##

Issues can be reported to the [Issue tracker](https://github.com/gluonhq/client-gradle-plugin/issues)

Contributions can be submitted via [Pull requests](https://github.com/gluonhq/client-gradle-plugin/pulls), 
providing you have signed the [Gluon Individual Contributor License Agreement (CLA)](https://docs.google.com/forms/d/16aoFTmzs8lZTfiyrEm8YgMqMYaGQl0J8wA0VJE2LCCY).
