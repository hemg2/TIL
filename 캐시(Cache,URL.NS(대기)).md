Cache 
* 캐시란 무엇이고 어떤 역할일까?
    * 캐시(CACHE) -> 데이터나 값을 미리 복사해서 놓아두는 임시 저장소이다.
    * 기존 데이터에 접근하는 시간이 오래 걸리는 경우나 값을 다시 계산하는 시간을 절약하고 싶은경우 사용한다.
    * 캐시에 데이터를 미리 복사해 놓으면 계산이나 접근 시간없이 더 빠른 속도로 데이터에 접근할 수 있다.
    * 필요할때 마다 서버에서 다운받는것이 아니라 임시저장소(캐시)에 다운 받은 이미지를 넣어두고 불러오면 효율적으로 된다.


* 몇 가지 기준으로 캐시를 구분해볼까?
    * 캐시는 클라이언트 서버 구분이 있나?
        * 클라이언트는 클라이언트만의 로컬에 저장할 수 있는 캐시가 있으며, 서버는 여러 클라이언트의 요청에 대해 저장할 수 있는 캐시가있다.
    * 캐시는 어디어디에 저장할 수 있을까?
        * 메모리, 앱디스크내부, 앱디스크외부

- iOS에서의 Cache
    -  메모리 캐시와 디스크 캐시
    - 메모리, 디스크 차이는 램에 저장하냐 하드디스크에 저장하냐

- 메모리 캐시(Memory Cache)
    - iOS에서 자체적으로 제공해주는 캐시
    - App을 끄면 캐시에 저장된 내용이 사라짐
    - NSCache를 통해서 사용 가능
    - 처리속도가 빠르지만 저장 공간이 작다

- 디스크 캐시(Disk Cache)
    - 캐시에 저장할 데이터를 기기 내부에 아카이빙 하는 방식 App을 껐다가 켜도 데이터가 사라지지 않고 남아있다.
    - FileManager를 통해 사용 가능
    - App을 삭제할 떄 캐시에 저장된 데이터를 삭제하게 만들수도 있고, 그렇지 않고 계속 남아있게 만들수도 있다.
        - UserDefault를 사용해 간단하게 저장하면, App이 삭제되어도 캐시가 남아있게 됨
        - 파일 경로에 이미지를 저장하면, App이 삭제되어도 캐시가 남아있게 됨(보통 파일 경로에 이미지 저장)
        - 저장공간은 비교적 크지만, 파일 입출력으로 인해 처리속도가 `메모리 캐시` 보다 느림

* 캐시를 구현할 때 고려해야 하는 캐시 운용 정책에는 어떤것들이 있을까?
    * 보안성(캐시 접근 관련)
    * 캐시 교체
        * 데이터 사용시간에 따른 교체
    * 저장하는 시점에 따른 정책
        * Write Through: 쓰기 요청 시 즉시 저장
        * WriteBack: 쓰기 요청 시 캐시에서만 이뤄지고 바로 저장되지 않고 추후 캐시에서 해당 사항이 끝날때 최종으로 한번에 변경사항 저장


* NSCache의 용도는?
- 메모리에 저장한다
- 킹피셔는 디스크에서 저장한다 NSCache로 ? 사기인가?
- 



https://developer.apple.com/documentation/foundation/nscache
https://developer.apple.com/documentation/foundation/url_loading_system/accessing_cached_data
https://developer.apple.com/documentation/foundation/urlcache/storagepolicy

```swift
- 이미지 크기 줄이기?
func resizeImage(image: UIImage, newWidth: CGFloat) -> UIImage {
    let scale = newWidth / image.size.width // 새 이미지 확대/축소 비율
    let newHeight = image.size.height * scale
    UIGraphicsBeginImageContext(CGSizeMake(newWidth, newHeight))
    image.drawInRect(CGRectMake(0, 0, newWidth, newHeight))
    let newImage = UIGraphicsGetImageFromCurrentImageContext()
    UIGraphicsEndImageContext()
    return newImage
}
```

- 날씨 에서 썼던거
```swift
class ImageDownload {
    static var shared: ImageDownload = ImageDownload()
    var cache: [URL: Data]?
    
    func download(url: URL) -> Data {
        if let cache = cache?[url] {
            return cache
        }
        let data = try! Data(contentsOf: url)
        cache?[url] = data
        return data
    }
}
guard let icon = model.icon, let url = URL(string: "https://openweathermap.org/img/wn/\(icon)@2x.png") else { return }
        weatherIconImage.image = UIImage(data: ImageDownload.shared.download(url: url))
```




## URLCache
```swift
 let imageCacheURL = URLCache.shared
    @IBOutlet weak var firstImageView: UIImageView!
    @IBOutlet weak var secondImageView: UIImageView!
    @IBOutlet weak var firstImageButton: UIButton!
    @IBOutlet weak var secondImageButton: UIButton!
    @IBOutlet weak var imageResetButton: UIButton!
    @IBOutlet weak var cacheDelete: UIButton!
    
@IBAction func firstImageView(_ sender: Any) {
        loadImage(url: "https://wallpaperaccess.com/download/europe-4k-1369012", imageView: firstImageView)
    }
    @IBAction func secondImageView(_ sender: Any) {
        loadImage(url: "https://wallpaperaccess.com/download/europe-4k-1318341", imageView: secondImageView)
    }
    @IBAction func resetImageButton(_ sender: Any) {
        firstImageView.image = nil
        secondImageView.image = UIImageView() 이렇게 진행해도된다.
        print("이미지 초기화!")
    }
    @IBAction func clearCacheButton(_ sender: Any) {
        imageCacheURL.removeAllCachedResponses()
        print("캐시 비우기")
    }

private func loadImage(url: String, imageView: UIImageView) {
  let urlSession: URLSession = {
            let config = URLSessionConfiguration.default
            config.requestCachePolicy = .returnCacheDataElseLoad
            config.urlCache = imageCacheURL
            return URLSession(configuration: config)
        }()
        
        guard let url = URL(string: url) else {
            print("url없어")
            return
        }
    if let cachedResponse = imageCacheURL.cachedResponse(for: URLRequest(url: url)) {
            if let image = UIImage(data: cachedResponse.data) {
                imageView.image = image
                print("이미지 캐시 사용")
                return
            }
        }
        
        let task = urlSession.dataTask(with: url) { data, response, error in
            guard let data = data, let image = UIImage(data: data) else {
                print("이미지 실패")
                return
            }
 DispatchQueue.main.async {
                imageView.image = image
                let cachedData = CachedURLResponse(response: response!, data: data)
                self.imageCacheURL.storeCachedResponse(cachedData, for: URLRequest(url: url))
                print("이미지 다운")
            }
        }
        task.resume()
    }
}
```
