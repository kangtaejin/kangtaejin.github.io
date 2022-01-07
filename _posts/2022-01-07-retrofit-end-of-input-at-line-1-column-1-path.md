---
title: "Retrofit java.io.EOFException: End of input at line 1 column 1 path"
categories: 
  - android
toc: true
---

## Retrofit java.io.EOFException: End of input at line 1 column 1 path
  
Retrofit을 이용해 개발중인데  
리스폰스를 받지 않는 상황에서 아래와 같은 에러가 났다  
  
```
java.io.EOFException: End of input at line 1 column 1 path  
```
  
Retrofit 빌더를 이용해 만들어 줄때 addConverterFactory에 아래와 같이 설정해주면 된다.  
  
```kotlin
  addConverterFactory(nullOnEmptyConverterFactory)
```
  
nullOnEmptyConverterFactory는 아래와 같다.  
  
```kotlin
  private val nullOnEmptyConverterFactory = object : Converter.Factory() {
      fun converterFactory() = this
      override fun responseBodyConverter(type: Type, annotations: Array<out Annotation>, retrofit: Retrofit) = object : Converter<ResponseBody, Any?> {
          val nextResponseBodyConverter = retrofit.nextResponseBodyConverter<Any?>(converterFactory(), type, annotations)
          override fun convert(value: ResponseBody) = if (value.contentLength() != 0L) nextResponseBodyConverter.convert(value) else null
      }
  }
```
