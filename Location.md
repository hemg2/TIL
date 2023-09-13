Info List에서 
Information Property List 에서 + 추가후 
Privacy - Location When In Use Usage Description - 위치 허용 하시겠습니까?
위치 허용 알럿 띄우는 메시지 입니다.

```swift
 func fetchLocation() {
        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyBest 거리 정확도
        locationManager.requestWhenInUseAuthorization() 위치 사용 허용 알림
        locationManager.requestLocation()
    }
    
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
          위치 사용을 허용하면 현재 위치 정보를 가져옴
        if let location = locations.first {
            print("위치 업데이트!")
            print("위도 : \(location.coordinate.latitude)")
            print("경도 : \(location.coordinate.longitude)")
        }
    }
    
    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        print("위치 에러")
    }
```

어어 근데 왜 에러 뜨지? 하하하
휴대폰으로 직접했다면 그에 맞는 위치 로케이션이 나타나겠지만
지금 맥 시뮬레이터로 진행하고있기에 나타나지 않고 에러가 뜰것입니다.
시뮬레이터 Location 옵션에서 none 에서 custom으로 변경하면 그에 맞는 좌표가 나타날것이며 그렇게 변경될꺼니 이상없이 진행될것입니다.

이렇게 하지 않았다면... 경고창이 계속 나타날것이며 문제가 발생되어 위치 정보를 받아 올 수없습니다.
