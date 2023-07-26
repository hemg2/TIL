
URL 주소 불러오기
```swift
let url = "http://~~~"
let components = URL(string: url)! 
```
이런식으로 사용이 가능하다.


하지만 이제 json 주소는 비슷하면서 재사용할 수있게 진행 하고자 나누면 좋다는 생각에
기존 url를 가지고 있으며 네트워킹을 해야하는 부분에서 추가?변경?되는부분만을 item으로  하여 나눠 쓸수있게 진행 할 수있다.!!
```swift
var components = URLComponents(string: url)
 
 components?.queryItems = [
 URLQueryItem(name: "key", value: apiKey),
 URLQueryItem(name: "targetDt", value: targetDate)
 ]
let url = components.url
```



/*
 let url = "http://kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=asdsadadsad&targetDt=20230101"
 guard let components = URL(string: url) else { return }
 
 
 
 let url = "http://kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json"
 let apiKey = "asdasdsad"
 let targetDate = "20230722"
 
 var components = URLComponents(string: url)
 
 components?.queryItems = [
 URLQueryItem(name: "key", value: apiKey),
 URLQueryItem(name: "targetDt", value: targetDate)
 ]
 
 guard let url = components?.url else {
 return
 }
 */
