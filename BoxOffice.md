## 이번 프로젝트를 진행하면서 얻은 걷들을 하니씩 추가 하기


```swift
func fetchImageDataToURL(_ url: String, completion: @escaping (Result<Data, APIError>) -> Void) {
        let path = ""
        let queryItem: [String: Any] = ["": ""]
        let header: [String: Any] = ["": ""]
        sessionProvider.requestData(url, path, queryItem, header) { result in
            switch result {
            case .success(let data):
                print(data)
            case .failure(let error):
                print(error)
            }
        }
    }
```

queryItem, header의 키값이 ""으로 빈값을 설정하였다고 볼수있지만 해당 값에 대해서 실행을하게 되면 "" 의 빈값에 대한 키를 찾아 벨류값을 만들어 내게 된다.



```swift
(lldb) po header
▿ 1 element
  ▿ 0 : 2 elements
    - key : ""
    - value : ""

(lldb) po queryItem
▿ 1 element
  ▿ 0 : 2 elements
    - key : ""
    - value : ""
```
빈값이 나타나는걸 알수있다.  하지만  urlComponents 값에 query 의 값에 모르는 값이 추가되는것을 알 수 있었다.

```swift
 private func setUpRequestURL(_ baseURL: String,_ path: String, _ queryItems: [String: Any]) -> URLRequest? {
        guard var urlComponents = URLComponents(string: baseURL) else { return nil }
        
        urlComponents.path += path
        urlComponents.queryItems = queryItems.map { URLQueryItem(name: $0.key, value: "\($0.value)") }
        
        guard let url = urlComponents.url else { return nil }
        let urlRequest = URLRequest(url: url)
        
        return urlRequest
    }

(lldb) po urlComponents
▿ https://dapi.kakao.com/v2/search/image?query=%EC%BD%98%ED%81%AC%EB%A6%AC%ED%8A%B8%20%EC%9C%A0%ED%86%A0%ED%94%BC%EC%95%84%20%EC%98%81%ED%99%94%20%ED%8F%AC%EC%8A%A4%ED%84%B0
```


```swift
let queryItem: [String: Any] = ["": ""]
let header: [String: Any] = ["": ""]

let queryItem: [String: Any] = [:]
let header: [String: Any] = [:]
```

"" 이렇게 빈값을 넣었다고 할수있지만 이것또한 이에 맞는 키에 벨류 값이 나올수있기때문에 확인하여 진행하기!
