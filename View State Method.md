# 아래의 코드는 UIViewController의 view 관련 메서드(viewDidLoad, viewWillAppear, viewDidAppear, viewWillDisappear, viewDidDisappear) 중 어느 메서드 내부에 위치하는 것이 좋을지 생각해봅시다. (40분)
- 사용자 환영 애니메이션을 보여주는 코드
- 뷰에 보여질 데이터를 불러올 코드
- 배경음악을 재생할 코드
- 배경음악을 중지할 코드
- 노티피케이션 수신을 위한 옵저버 등록 코드
- 노티피케이션 수신 중단을 위한 구독 중단 코드
- 스토리보드로 구성한 뷰 요소의 초기값을 설정하는 


## viewDidLoad - 뷰가 메모리
- 사용자 환영 애니메이션을 보여주는 코드
- 노티피케이션 수신을 위한 옵저버 등록 코드
- 스토리보드로 구성한 뷰 요소의 초기값을 설정하는 코드

viewWillAppear - 뷰가 곧 나타날 것이다
- 뷰에 보여질 데이터를 불러올 코드

## viewDidAppear - 뷰가 나타났다.
- 배경음악을 재생할 코드(자동재생이다. ex)네이버웹툰)

## viewWillDisappear - 뷰가 사라질 것이다
- 노티피케이션 수신 중단을 위한 구독 중단 코드

## viewDidDisappear - 뷰가 사라졌다
- 배경음악을 중지할 코드
