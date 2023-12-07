---
title: "Android Webview Javascript Window open url null"
categories: 
  - android
toc: true
---
  
## Android Webview Javascript Window open url null
  
기존 url이 null로 들어오는 경우가 있는 경우

```kotlin
override fun onCreateWindow(view: WebView?, isDialog: Boolean, isUserGesture: Boolean, resultMsg: Message?): Boolean {
    kotlin.runCatching {
      val newWebView = WebView(view!!.context)
      val settings = newWebView.settings
      settings.javaScriptEnabled = true

      newWebView.webViewClient = object : WebViewClient() {
          override fun shouldOverrideUrlLoading(
              view: WebView?,
              request: WebResourceRequest?
          ): Boolean {
              val url = request?.url.toString()
              if(url.contains("http")){
                  val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
                  startActivity(intent)
              }
              return true
          }
      }

      val container = view?.parent as? ViewGroup
      container?.addView(newWebView)

      val transport = resultMsg?.obj as? WebView.WebViewTransport
      transport?.webView = newWebView
      resultMsg?.sendToTarget()
      return true
    }
    return true
}

```
  
수정은 webview를 새로 로드해 url을 얻어오는 방법이다.  
  
```kotlin
override fun onCreateWindow(view: WebView?, isDialog: Boolean, isUserGesture: Boolean, resultMsg: Message?): Boolean {
    kotlin.runCatching {
        val newWebView = WebView(view!!.context)
        val settings = newWebView.settings
        settings.javaScriptEnabled = true

        newWebView.webViewClient = object : WebViewClient() {
            override fun shouldOverrideUrlLoading(
                view: WebView?,
                request: WebResourceRequest?
            ): Boolean {
                val url = request?.url.toString()
                if(url.contains("http")){
                    val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
                    startActivity(intent)
                }
                return true
            }
        }

        val container = view?.parent as? ViewGroup
        container?.addView(newWebView)

        val transport = resultMsg?.obj as? WebView.WebViewTransport
        transport?.webView = newWebView
        resultMsg?.sendToTarget()
        return true
    }
    return true
}
```

수정은 되었으나 코드가 지저분해졌다...