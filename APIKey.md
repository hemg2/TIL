Property List 추가
plist 생성이 되면
key -> 어떤 API키임?
value -> APIKey값 입력하기(내꺼)


```swift
enum APIKey {
    static var boxOffice: String =  {
        var boxOfficeAPIKey = ""
        
        if let path = Bundle.main.path(forResource: "Keys", ofType: "plist") {
            let networkKeys = NSDictionary(contentsOfFile: path)
            
            if let networkKeys = networkKeys {
                boxOfficeAPIKey = (networkKeys["BoxOfficeAPIKey"] as? String) ?? ""
            }
        }
            
        return boxOfficeAPIKey
    }()
}

```


```swift
 func fetchMovieDetailInformation() {
        let queryItems: [String: Any] = [
            "key": APIKey.boxOffice,
            "movieCd": "20218541"
        ]
        
        let requestURL = setUpRequestURL(BaseURL.boxOffice, BoxOfficeURLPath.movieDetail, queryItems)
        
        sessionProvider.requestData(requestURL) { (result: Result<MovieDetailResult, APIError>) in
            switch result {
            case .success(let result):
                self.delegate?.completeFetchMovieDetailInformation(result)
            case .failure(let error):
                self.delegate?.failFetchMovieDetailInformation(error.errorDescription)
            }
        }
    }
```


이렇게 쓸쑤있다.

또다른 예시
```swift
extension Bundle {
    
    var apiKey: String {
        // forResource에다 plist 파일 이름을 입력해주세요.
        guard let filePath = Bundle.main.path(forResource: "생성한Plist제목", ofType: "plist"),
              let plistDict = NSDictionary(contentsOfFile: filePath) else {
            fatalError("Couldn't find file 'SecureAPIKeys.plist'.")
        }
        
        // plist 안쪽에 사용할 Key값을 입력해주세요.
        guard let value = plistDict.object(forKey: "내가 생성한 키값") as? String else {
            fatalError("Couldn't find key 'API_Key' in 'SecureAPIKeys.plist'.")
        }
        return value
    }
}
```


- gitignore 들어가서
- 파일제목.plist 추가해서 막기!
