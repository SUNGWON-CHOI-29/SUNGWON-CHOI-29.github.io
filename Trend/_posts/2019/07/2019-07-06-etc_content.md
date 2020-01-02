---
layout: post
title: Medium - Network Library (iOS/Android)
description: >
  <a href="https://medium.com/better-programming/learn-ios-android-networking-e19808f554a7">원문 링크 - Elye</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - iOS와 Android에서 쓰이는 네트워크 라이브러리

![500x400](https://cdn-images-1.medium.com/max/1600/1*4jgiBwrgISGWWETRj49aaA.gif)

네트워킹은 모바일 앱 개발에서 매우 중요한 컴포넌트이다. Android와 iOS에서 이러한

네트워킹을 위해 사용하는 라이브러리의 기초에 대해 알아보자.

## 각 운영체제별 사용되는 라이브러리

### iOS :

- Alamofire - 데이터를 해석하기 위한 네트워크 라이브러리

- SwiftyJSON - JSON데이터를 파싱하기 위한 라이브러리


#### request 형식

~~~Swift
let url = "https://en.wikipedia.org/w/api.php"
let parameters: Parameters = [
      "action": "query",
      "format": "json",
      "list": "search",
      "srsearch": searchText
    ]
~~~

#### fetch 수행부

~~~Swift
request = Alamofire.SessionManager.default.request(
    url, method: .get, parameters: parameters)
      .responseData { (resData) -> Void in
      // Handle the result data i.e. resData
      // ...
}
~~~

#### result

~~~Swift
switch (resData.result) {
    case let .success(data):
       // Handle success case with provided data
       // i.e. use SwiftyJSON to convert data to needed format             
    case let .failure(error):
       // Handle failre case with provided error
       // use the error.localizedDescription to get the message
}
~~~

에러 발생 시 아래와 같이 문구를 확인할 수 있다.

- 네트워크가 없는 경우 : The Internet connection appears to be offline.

- 호스트가 잘못된 경우 : A server with the specified hostname could not be found.

#### Parsing JSON

~~~Swift
let swiftyJsonVar = JSON(data)
let countObj = swiftyJsonVar["query"]["searchinfo"]["totalhits"]

guard let count = countObj.int else {
   self.showResult(data: “No data found”)
   return
}
self.showResult(data: “Count is \(count)”)
~~~

### Android :

- OkHttp - 데이터를 해석하기 위한 네트워크 라이브러리

- Gson - JSON 데이터를 파싱하기 위한 라이브러리

#### request 형식

~~~Java
private val httpUrlBuilder = HttpUrl.Builder()
    .scheme("https")
    .host("en.wikipedia.org")
    .addPathSegment("w")
    .addPathSegment("api.php")
    .addQueryParameter("action", "query")
    .addQueryParameter("format", "json")
    .addQueryParameter("list", "search")
~~~

#### fetch 수행부

~~~Java
val httpUrl = httpUrlBuilder
    .addQueryParameter("srsearch", searchText).build()
val request = Request.Builder().get().url(httpUrl).build()
val response = httpClient.newCall(request).execute()
// Use the result data i.e. response
// ...
~~~

#### result

~~~Java
if (response.isSuccessful) {
    val raw = response.body()?.string()
    // Use the raw data to be process by gson
} else {
    // Process the response.message()
}
~~~

#### JSON 파싱

~~~Java
val raw = response.body()?.string()
try {
    val result = Gson().fromJson(raw, Model.Result::class.java)
    result.query.searchinfo.totalhits.toString()
} catch (exception: JsonSyntaxException) {
    "No data found "
}
object Model {
    data class Result(val query: Query)
    data class Query(val searchinfo: SearchInfo)
    data class SearchInfo(val totalhits: Int)
}}
~~~

## Summary
* Alamofire와 OkHttp모두 JSON payload를 다루기 위한 써드파티 툴이다.
* 두 라이브러리 모두 fetch를 수행하고 성공과 실패를 결과값으로 얻을 수 있다.
* Alamofire가 OkHttp에 비해 커버하는 특징이 더욱 많다.
* 물론 이러한 것은 가벼운 비교이고 두 라이브러리 중 어느 것이 더 나음을 강조하는 것이 아니다.
