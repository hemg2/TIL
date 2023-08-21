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






# 코디네이터 적용을 위한 공부 진행

```swift
final class ViewController: UIViewController {
    private var coordinator: CoordinatorPush
    
    private lazy var pushButton: UIButton = {
        let button = UIButton()
        
        button.translatesAutoresizingMaskIntoConstraints = false
        button.setTitle("다음화면", for: .normal)
        button.setTitleColor(.black, for: .normal)
        
        let nextButton = UIAction { [weak self] _ in
            guard let self else { return }
            self.nextButton()
        }
        
        button.addAction(nextButton, for: .touchUpInside)
        return button
    }()
    
    init(coordinator: Coordinator) {
        self.coordinator = coordinator
        super.init(nibName: nil, bundle: nil)
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .systemBackground
        setUpButtonLayout()
    }
    
    private func setUpButtonLayout() {
        view.addSubview(pushButton)
        
        NSLayoutConstraint.activate([
            pushButton.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            pushButton.centerYAnchor.constraint(equalTo: view.centerYAnchor)
        ])
    }
        코디네이터 객체를 알고 그것을 가져와서 쓴다. 굳이 프로토콜을 채택하지 않아도 된다.
    private func nextButton() {
        coordinator.navigateToSecondVC()
    }
}
```


```swift
protocol CoordinatorPush {
    func navigateToSecondVC()
}

final class Coordinator: CoordinatorPush {
    private var navigationController: UINavigationController
    
    init(navigationController: UINavigationController) {
        self.navigationController = navigationController
    }
    
    func start() {
        let firstVC = ViewController(coordinator: self)
        navigationController.pushViewController(firstVC, animated: true)
    }
    
    func navigateToSecondVC() {
        let secondVC = SecondViewController(coordinator: self)
        navigationController.pushViewController(secondVC, animated: true)
    }
}
```


```swift
final class SecondViewController: UIViewController {
    
    private var coordinator: Coordinator?
    
    init(coordinator: Coordinator) {
        self.coordinator = coordinator
        super.init(nibName: nil, bundle: nil)
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .blue
    }
}
```

