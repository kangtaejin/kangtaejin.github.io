---
title: "Android 기기 고유값"
categories: 
  - android
toc: true
---

## Android 기기 고유값
  
안드로이드를 개발하다보면 각 앱마다 기기 고유값이 필요한 경우가 많다.  
  
일명 UUID  
  
하지만 안드로이드 버전이 올라갈수록 개인정보에 해당하는 값을 얻기가 힘들어졌다.  
  
- Build  
getSerial()  
  
- TelephonyManager  
getImei()  
getDeviceId()  
getMeid()  
getSimSerialNumber()  
getSubscriberId()  
  
특히 위의 경우는 사용하면 안된다.
또한 광고ID의 경우는 광고에만 사용하도록 명시하고 있다.

경우에 따라 다르지만 앱을 삭제하고 재설치했을 경우에도 같은 값이 필요한 경우가 있는데
안드로이드 진영에서는 SSAID를 사용하라고 권장하는듯하다. 
READ_PHONE_STATE 권한이 필요한 불편한 점이 있기는 하나 프로요 이상부터는 별문제 없다고하니
사용하기 좋아보인다.

사용법은 간단하다

```kotlin

  private fun getSSAID(): String{

      return Settings.Secure.getString(
          applicationContext.contentResolver, Settings.Secure.ANDROID_ID
      )
      
  }

```
  
Widevine 이용도 추천하는데 사용법은 아래와 같다. 
  
```kotlin

  private fun getWidevineID(): String? {
        
      return try {

          val wvDrm = MediaDrm(UUID(-0x121074568629b532L, -0x5c37d8232ae2de13L))

          val widevineId = wvDrm.getPropertyByteArray(MediaDrm.PROPERTY_DEVICE_UNIQUE_ID)

          if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
              Base64.getEncoder().encodeToString(widevineId).trim()
          } else {
              android.util.Base64.encodeToString(widevineId, android.util.Base64.DEFAULT).trim()
          }

      } catch (e: UnsupportedSchemeException) {
          null
      }

  }

```
  
좀 느린게 단점이라고 한다.  
Splash 같은 곳에서 저장했다가 사용하면 될 것 같다.  