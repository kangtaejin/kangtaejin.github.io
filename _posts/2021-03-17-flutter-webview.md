---
title: "flutter android webview backbutton"
categories: 
  - flutter
toc: true
---

## flutter android webview backbutton

안드로이드 개발을 하다보면 뒤로 가기 처리를 하는 경우가 있다. (안드로이드는 하단 소프트키가 있다)  
아래는 뒤로 가기 했을때 히스토리가 있을때 뒤로 가는 처리를 추가한 웹뷰이다.  

```dart
import 'dart:async';
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

class WebWidget extends StatefulWidget {

  @override
  WebState createState() => WebState();

}

class WebState extends State<WebWidget>{

  WebViewController _controller;

  final Completer<WebViewController> _completerController = Completer<WebViewController>();

  @override
  void initState() {
    super.initState();
    if (Platform.isAndroid) WebView.platform = SurfaceAndroidWebView();
  }

  @override
  Widget build(BuildContext context){
    return Container(
      child: SafeArea(
        child:WillPopScope(
          onWillPop: () => _goBack(context),
          child: WebView(
            onWebViewCreated: (WebViewController webViewController) {
              _completerController.future.then((value) => _controller = value);
              _completerController.complete(webViewController);
            },
            initialUrl: "https://kangtaejin.github.io",
            javascriptMode: JavascriptMode.unrestricted,
          ),
        )
      )
    );
  }

  Future<bool> _goBack(BuildContext context) async{
    if(await _controller.canGoBack()){
      _controller.goBack();
      return Future.value(false);
    }else{
      return Future.value(true);
    }
  }

}
```
  
뒤로 가기 처리를 위해서는 WillPopScope로 감싸줘야하며 onWillPop에서 처리를 해주면 된다.  
  
if (Platform.isAndroid) WebView.platform = SurfaceAndroidWebView();  
이부분을 안해주면 웹뷰 퍼포먼스가 떨어진다.  
