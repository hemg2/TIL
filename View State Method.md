# 아래의 코드는 UIViewController의 view 관련 메서드(viewDidLoad, viewWillAppear, viewDidAppear, viewWillDisappear, viewDidDisappear) 중 어느 메서드 내부에 위치하는 것이 좋을지 생각해봅시다.
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

---

- 그럼 loadView의 역할은 뭘까요?
바로 컨트롤러가 관리하는 뷰를 '만드는' 역할을 합니다. 
그럼 loadView가 뷰를 만들고, 메모리에 올린 후에!
viewDidLoad가 호출된다고 할 수 있겠네요.

- viewDidLoad - 뷰가 로드 되었다
뷰가 초기 화면을 띄어준다???
뷰의 컨트롤러가 메모리에 로드되고 난 후에 호출됩니다.

이 viewDidLoad 메소드는 뷰의 로딩이 완료 되었을 때 
시스템에 의해 자동으로 호출되기 때문에 
일반적으로 리소스를 초기화하거나 
초기 화면을 구성하는 용도로 주로 사용합니다.
화면이 처음 만들어질 때 한 번만 실행되므로, 
처음 한 번만 실행해야 하는 초기화 코드가 있을 경우 
이 메소드 내부에 작성하면 됩니다. 

- viewWillAppear - 뷰가 곧 나타날 것이다
-처음 뷰디드 로드에서 화면을 생성한후에 화면에 변화가 있을떄?
뷰윌어페어를 사용해서 화면은 업데이트하는방법용도??

뷰가 이제 나타날 거라는 신호를 컨트롤러에게 알리는 역활을 합니다.
즉 뷰가 나타나기 직전에 호출된다고 볼 수있따.

뷰디드로드랑 똑같은거아니야?? -> 다른점을 찾아보자
처음 화면을 실행 시킨다면
뷰디드로드 -> 뷰윌어페어가 실행된다.
그리고 2번째 화면으로 넘어가면
2번째 화면에서도 뷰디드로드가 실행된후 뷰윌어페어가 실행됩니다.
그후에 다시 첫번째 화면으로 가게 된다면 뷰디드로드가 호출되는것이 아니라
뷰 윌어페어가 실행 된다. (뷰디드 로드는 초기화면만 지정한다.)

- 다른뷰에서 갔다가 다시 돌아오는 상황에
- 해주고 싶은 처리가 있겠죠?
- 이때는 viewWillAppear에서 해주면 된답니다.


- viewDidAppear - 뷰가 나타났다.
이 부분을 써본적은 없다. 뷰윌어페어가 있으니깐 뷰윌 어페는 써도 이부분은 안쓴거 같다.

viewDidAppear는 뷰가 나타났다는 것을 컨트롤러에게 알리는 역할을 합니다. 또한 화면에 적용될 애니메이션을 그려줘요.
이 viewDidAppear는 뷰가 화면에 나타난 직후에 실행됩니다. 

이 것을 제외하고 viewDidAppear와 viewWillAppear는 거의 같아요.

- viewWillDisappear - 뷰가 사라질 것이다
아직까지는 써볼 환경은 되어본적이 없다.

뷰가 사라지기 직전에 호출되는 함수인데요,
뷰가 삭제 되려고하고있는 것을 뷰 콘트롤러에 통지합니다.

- viewDidDisappear - 뷰가 사라졌다

마지막인 viewDidDisAppear까지 왔네요!
(생명주기는 순환되기 때문에 마지막?은 아닐 수도 있겠지만..)
역시 위와 같아요
viewDidDisAppear가 호출되면,
뷰 컨트롤러가 뷰가 제거되었음을 알려준답니다. 

1VC -> 2VC
1.ViewDidLoad      -> 뷰가 로드 된다
1.ViewWillAppear    -> 뷰가 곧 나타난다.
1.ViewDidAppear     -> 뷰가 나타났다.
---------------- 2번화면 등장
1.ViewWillDisappear     -> 뷰가 사라질 것이다.
2.ViewDidLoad          -> 뷰가 로드 된다  
2.ViewWillAppear     -> 뷰가 곧 나타난다.
1.ViewDidDisappear     -> 뷰가 사라졌다.
2.ViewDidAppear       -> 뷰가 나타났다.

뷰가 나타났다 2번 쨰 화면으로 이동 한다면
첫번째화면의 뷰는 곧 사라질 예정이며  2번재 뷰가 로드되고 2번째 뷰가 나타나기 직전에 1번째 화면 의 뷰가 사라지고 난후에 2번째화면이 나타난다.
