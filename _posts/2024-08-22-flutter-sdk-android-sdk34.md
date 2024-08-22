---
title: "Flutter SDK 3.24.0 Android SDK34"
categories: 
  - flutter
toc: true
---
  
## Flutter SDK 3.24.0 Android SDK34
  
매년 찾아오는 Android Target SDK 버전 올리는 작업을 했다.  
이번에는 Android SDK 34로 올리고 Flutter SDK버전도 3.13.7 버전에서 3.24.0 버전으로 올렸다.  
3.24.0버전으로 올리니 다트 버전도 올리게되었고 기존 업데이트를 많이 안했던 플러터 프로젝트의 경우는 다트 버전 범위도 더 높여야했다.  
다트 버전이 기존에 많이 낮았으면 옵셔널체크하는 내용이 많이 바뀌어 소스 수정하는데 고생을 좀 하게 된다.  
다트 버전에 크게 문제가 없던 가장 최근에 만든 앱이 LabRec 이란 앱의 수정된 내용은 아래와 같다.  
  
setting.gradle  
```gradle
pluginManagement {
    def flutterSdkPath = {
        def properties = new Properties()
        file("local.properties").withInputStream { properties.load(it) }
        def flutterSdkPath = properties.getProperty("flutter.sdk")
        assert flutterSdkPath != null, "flutter.sdk not set in local.properties"
        return flutterSdkPath
    }()

    includeBuild("$flutterSdkPath/packages/flutter_tools/gradle")

    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}

plugins {
    id "dev.flutter.flutter-plugin-loader" version "1.0.0"
    id "com.android.application" version "8.1.1" apply false
    id "org.jetbrains.kotlin.android" version "1.8.10" apply false
}

include ":app"
```

build.gradle(project)  
```gradle
allprojects {
    repositories {
        google()
        mavenCentral()
    }
}

rootProject.buildDir = '../build'
subprojects {
    project.buildDir = "${rootProject.buildDir}/${project.name}"
}
subprojects {
    project.evaluationDependsOn(':app')
}

tasks.register("clean", Delete) {
    delete rootProject.buildDir
}
```

build.gradle(app)  
```gradle
plugins {
    id "com.android.application"
    id "kotlin-android"
    id "dev.flutter.flutter-gradle-plugin"
}

def localProperties = new Properties()
def localPropertiesFile = rootProject.file('local.properties')
if (localPropertiesFile.exists()) {
    localPropertiesFile.withReader('UTF-8') { reader ->
        localProperties.load(reader)
    }
}

def flutterVersionCode = localProperties.getProperty('flutter.versionCode')
if (flutterVersionCode == null) {
    flutterVersionCode = '1'
}

def flutterVersionName = localProperties.getProperty('flutter.versionName')
if (flutterVersionName == null) {
    flutterVersionName = '1.0'
}

def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('키스토어 위치')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android {
    namespace 'com.chemkaaa.laboratory'
    compileSdkVersion 34

    ndkVersion flutter.ndkVersion

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_17
        targetCompatibility JavaVersion.VERSION_17
    }

    kotlinOptions {
        jvmTarget = '17'
    }

    sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }

    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.chemkaaa.laboratory"
        // You can update the following values to match your application needs.
        // For more information, see: https://docs.flutter.dev/deployment/android#reviewing-the-gradle-build-configuration.
        minSdkVersion flutter.minSdkVersion
        targetSdkVersion 34
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        multiDexEnabled true
    }

    // start of signingConfigs
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
        }
    }

    buildTypes {
        release {
            // TODO: Add your own signing config for the release build.
            // Signing with the debug keys for now, so `flutter run --release` works.
            signingConfig signingConfigs.release
        }
    }
}

flutter {
    source '../..'
}
```

gradle-wrapper.properties  
```
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-8.0-all.zip
```

안드로이드 프로젝트 경우 수정한 내용은 위와 같고 플러터 프로젝트의 pub으로 사용하는 외부라이브러리 경우 최신버전으로 바꿔줬다.  
외부라이브러리 경우 유지보수가 계속 되지 않은 버전 경우 네임스페이스 문제가 생겨 유지보수되지 않는 라이브러리는 다른 유지보수되는 라이브러리로 교체해줬다.  

위젯 디자인이 기존과 다르게 바뀌는 경우가 있어 빌드 후 확인을 다시해봐야 한다.  
큰 문제없이 안드로이드 버전과 플러터 버전을 올려 업데이트 했다.  