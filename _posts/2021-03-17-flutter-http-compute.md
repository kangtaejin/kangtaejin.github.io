---
title: "flutter Invalid argument(s): Illegal argument in isolate message : (object is a closure - Function 'parsePhotos':.)"
categories: 
  - flutter
toc: true
---

## flutter compute. Illegal argument in isolate message : (object is a closure - Function 'parsePhotos':.)

flutter http 와 json파싱하는 예제를 공부중이었다.
(https://flutter.dev/docs/cookbook/networking/background-parsing)

예제를 똑같이 따라하지는 않았지만 같게 만들었다고 생각했는데

Illegal argument in isolate message : (object is a closure - Function 'parsePhotos':.)

이런 에러 메시지를 보여주고 파싱이 제대로 되지 않았다.

구글링해보니 compuse는 top level에 둬야 한다고 써있었다.

문제의 코드

```flutter

Future<List<Photo>> fetchPhotos(http.Client client) async {
  final response = await client
      .get(Uri.parse('https://jsonplaceholder.typicode.com/photos'));

  // Use the compute function to run parsePhotos in a separate isolate.
  return compute(parsePhotos, response.body);
}

// A function that converts a response body into a List<Photo>.
List<Photo> parsePhotos(String responseBody) {
  final parsed = jsonDecode(responseBody).cast<Map<String, dynamic>>();

  return parsed.map<Photo>((json) => Photo.fromJson(json)).toList();
}

```

난 위젯 클래스 안에 함수로 parsePhotos을 사용하고 있었는데 그것이 문제가 되었나보다.

예제 코드를 보니 위젯 클래스안에 함수로 둔게 아닌 top level에 둔 형태였다.

역시나 따라서 밖에 빼두니 별 문제 없이 동작했다.
